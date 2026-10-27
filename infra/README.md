# infra/

- `resource-group.arm.json`: plantilla ARM exportada del portal el 26/10/2026 al crear `rg-lab-devops` a mano. Se despliega a nivel de suscripción.
- Valores usados: `rgName=rg-lab-devops`, `rgLocation=eastus2`, `tags={proyecto: pedidos, entorno: lab, dueno: arturo}`.
- En el bloque de plataforma (diciembre) esto se reescribe en Terraform. Evidencia de pasar de portal a código.
