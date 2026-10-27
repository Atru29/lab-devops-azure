# Plan de la semana 1: GitHub Actions y registry

Inicio real: lunes 26 de octubre de 2026 (el plan se corrió desde el 22).

| Fecha | Bloque | Entregable |
|---|---|---|
| Lun 26 oct, 15:00-17:00 | S1 D1: presupuesto, resource group y repo | Repo creado, presupuesto activo |
| Mar 27 oct, 08:00-11:00 | ACR (SKU Basic) y primer workflow build/push | Workflow funcionando |
| Jue 29 oct, 19:30-21:30 | Fallo provocado y caso documentado | Caso con síntoma, causa, solución, prevención |
| Sáb 31 oct, 19:30-21:30 | Workflow reutilizable (`workflow_call`) y composite action | Llamado desde los 3 servicios |
| Mar 3 nov, 19:00-22:00 | README comparativo (Azure Pipelines vs GitHub Actions) y cierre | README, diagrama, limpieza de recursos |

Domingos de AZ-900: 1, 8, 15 y 22 de noviembre. El bootcamp ocupa lunes, miércoles y viernes de 19:30 a 22:30.

## Pendiente del día 1
- [x] Nota de LAB-1 (ver `ticket-LAB-1.md`)
- [x] Repositorio público `lab-devops-azure` en GitHub
- [x] Tres servicios mínimos con `/health` y su Dockerfile (Spring Boot 21, multi-stage, usuario no root)

## Detalle del martes 27 (08:00-11:00)
1. Crear Azure Container Registry, SKU Basic, en `rg-lab-devops`, East US 2, con las tres etiquetas.
2. Escribir yo el workflow: build de las 3 imágenes y push con etiqueta por commit. Secrets en el repositorio.
3. Pedir revisión (permisos del token, buenas prácticas).
4. Sin los Dockerfiles de hoy, mañana no hay nada que construir.

## Reglas de limpieza
Al final de cada sesión, revisar el grupo en Análisis de costos y borrar lo que no se use. Borrar el grupo borra todo su contenido.
