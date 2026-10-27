# Ticket LAB-1: Preparar el entorno base del producto "Pedidos" con control de costos

## Contexto
El equipo de producto empezará a desplegar tres microservicios (catálogo, pedidos y pagos) en Azure la próxima semana. Hubo un gasto inesperado por recursos olvidados y finanzas pidió que ningún entorno nuevo se cree sin control de costos.

## Requerimiento
1. Crear el grupo de recursos `rg-lab-devops` en una sola región, con etiquetas de proyecto, entorno y dueño.
2. Crear un presupuesto mensual **solo para ese grupo**, con alertas al 50 %, 80 % y 100 % del gasto real.
3. Documentar el monto elegido y por qué.

## Criterios de aceptación
| Criterio | Estado |
|---|---|
| El grupo existe y tiene las tres etiquetas | Cumplido |
| El presupuesto tiene como ámbito ese grupo | Cumplido |
| Las tres alertas llegan a un correo que se revisa a diario | Creadas. Filtro de Gmail descartado; llegada de alertas sin comprobar hasta el primer umbral |
| Existe una nota de una página con monto y justificación | Cumplido |

## Fuera de alcance
Red, permisos de la pipeline y despliegues (tickets posteriores).

## Nota

### 1. ¿Por qué 30 US$ y qué cabe dentro?
Elegí 30 US$ al mes porque cubre los recursos del laboratorio, que existen pocas horas o pocos días, y además deja margen para un olvido. Estimación en East US 2, pago por uso (precios web del 26 oct 2026, pendiente confirmar en la calculadora de Azure):
- **ACR Basic:** ~0,167 US$/día, unos 5 US$/mes si está activo todo el mes.
- **AKS de nivel gratuito con 1 nodo Standard_B2s (Linux):** ~0,042 US$/h. Cinco días seguidos son unos 5 US$, más el disco y el balanceador o la IP pública (2-3 US$).
- **Una VM pequeña (B1s/B2s)** unas horas para pruebas: menos de 2 US$.

El total ronda 15 US$. La otra mitad es el margen para detectar un recurso olvidado antes de que el gasto se dispare. Si dejara un B2s encendido todo el mes, solo ese recurso costaría ~30 US$, y el presupuesto me lo avisaría a tiempo.

### 2. ¿Qué hago al 50 %, al 80 % y al 100 %?
- **50 % (15 US$): mirar.** Abro *Análisis de costos* del grupo, agrupado por recurso, y compruebo que el gasto encaja con lo que tengo desplegado esa semana.
- **80 % (24 US$): revisar y reducir.** Busco en el *Registro de actividad* quién creó cada recurso caro y cuándo. Apago o escalo a cero lo que no esté en uso: detengo el AKS y desasigno las VM.
- **100 % (30 US$): parar.** Borro todo lo que no sea imprescindible, aunque implique recrearlo después con IaC. Documento la causa del desvío como caso.

### 3. ¿Quién recibe el aviso y cada cuánto lo reviso?
El aviso llega a mi correo personal, que es el único destinatario porque soy el dueño del entorno (`dueno=arturo`). Reviso ese correo a diario. Como los costos llegan a Azure con 8 a 24 horas de retraso, al final de cada sesión miro además *Análisis de costos* y no espero solo a la alerta.

### 4. ¿Qué no hace este presupuesto?
Solo avisa: no apaga, no bloquea ni borra ningún recurso al llegar al 100 %. Además, su ámbito es solo `rg-lab-devops`. Los nodos, discos y balanceador de un AKS se crean en un grupo aparte (`MC_rg-lab-devops_<cluster>_eastus2`) y este presupuesto no los ve. Antes de crear el AKS hay que cubrir ese grupo con otro presupuesto o con uno a nivel de suscripción.

## Notas técnicas del ticket
- El presupuesto se creó desde el propio grupo de recursos (Administración de costos > Presupuestos). Desde la suscripción, el filtro por grupo mostraba "0 seleccionados" porque el grupo estaba vacío.
- Evaluación del presupuesto: empieza "en unas horas". Los costos llegan con desfase de 8 a 24 horas.
- Lista de destinatarios: una por presupuesto, cada correo una sola vez.
