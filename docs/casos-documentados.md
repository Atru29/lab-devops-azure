# Casos documentados

Formato: síntoma, causa, solución, prevención. Si la causa no está confirmada, se dice.

## Caso 1: no se puede crear el presupuesto (26 oct 2026)
- **Síntoma:** notificación "No se puede crear el presupuesto, vuelva a intentarlo más tarde", sin código de error. Ninguna entrada de presupuesto en el Registro de actividad del grupo.
- **Causa:** **no confirmada.** Funcionó al reintentar sin cambiar nada; lo más probable es un fallo transitorio del servicio.
- **Solución:** reintentar la creación.
- **Prevención:** tras crear un recurso, comprobar que aparezca en su lista y no fiarse solo de la notificación. Aquí la de éxito y la de error convivían en la campana.

## Caso 2: alertas sin destinatario válido (26 oct 2026)
- **Síntoma:** mensajes en rojo "Es necesario especificar el grupo de acciones o como mínimo una dirección de correo" en cada umbral, y "Es necesaria una dirección de correo electrónico única" en los destinatarios.
- **Causa:** la lista de destinatarios es única para todas las alertas y no admite el mismo correo repetido. Al repetirlo cuatro veces, la validación falló.
- **Solución:** dejar el correo una sola vez.
- **Prevención:** una alerta sin destinatario válido es un fallo silencioso: el presupuesto existe pero nadie se entera. Comprobarlo antes de crear.

## Caso 3: el filtro por grupo de recursos no se completa (26 oct 2026)
- **Síntoma:** chip "ResourceGroupName : 0 seleccionados" y el gráfico seguía mostrando el gasto de toda la suscripción.
- **Causa:** **no confirmada.** Hipótesis: el grupo estaba vacío y recién creado, y la lista de valores se arma con grupos que ya tienen gasto.
- **Solución:** crear el presupuesto desde el propio grupo (Administración de costos > Presupuestos), donde el ámbito ya viene fijado.
- **Prevención:** para un ámbito por grupo, crearlo desde el grupo.
