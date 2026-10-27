# Plan completo (extraído de mi Google Calendar el 26 oct 2026)

Horario: bloques de laboratorio los martes/lunes 19:00-22:00 y jueves/sábado 19:30-21:30 (varía). Domingos 19:00-20:30: AZ-900. Bootcamp: lun, mié y vie 19:30-22:30. Mi calendario es la fuente de verdad de las fechas; si hay conflicto, manda el calendario.

Regla general de cada bloque: yo escribo primero, Claude revisa; en cada bloque hay un fallo provocado por Claude, que yo diagnostico y documento (síntoma, causa, solución, prevención); al cerrar, README con diagrama y limpieza de recursos.

## Bloque 1: GitHub Actions y registry
| Fecha | Tema | Entregable |
|---|---|---|
| Lun 26 oct | Presupuesto, resource group y repo con 3 servicios | Repo creado y presupuesto activo |
| Mar 27 oct | ACR (Basic) + primer workflow build/push | Workflow funcionando |
| Jue 29 oct | Fallo provocado (login al registry) | Caso documentado |
| Sáb 31 oct | Workflow reutilizable + composite action | Llamado desde los 3 servicios |
| Mar 3 nov | README comparativo Azure Pipelines vs Actions y cierre | README, diagrama |

## Bloque 2: Entornos, ramas y OIDC
| Fecha | Tema | Entregable |
|---|---|---|
| Jue 5 nov | Environments dev/qa/preprod con aprobación manual | Workflow con 3 environments y caso |
| Sáb 7 nov | Reglas de rama, PR obligatorio y CODEOWNERS | Reglas configuradas |
| Mar 10 nov | OIDC hacia Azure sin claves | Login sin client secret |
| Jue 12 nov | Matrix y caché | Tabla de tiempos antes/después |
| Sáb 14 nov | Fallo provocado de OIDC | Caso documentado |
| Mar 17 nov | Cierre del bloque | README y diagrama |

## Bloque 3: Seguridad en el pipeline
| Fecha | Tema | Entregable |
|---|---|---|
| Jue 19 nov | CodeQL, secret scanning y SonarCloud | Workflow, un hallazgo y registro de decisión |
| Sáb 21 nov | Dependabot y revisión de dependencias | dependabot.yml y un PR revisado |
| Mar 24 nov | Trivy sobre la imagen | Pipeline que corta si no pasa |
| Jue 26 nov | Permisos mínimos del token y acciones por SHA | Workflows endurecidos y nota |
| Sáb 28 nov | Fallo provocado de seguridad | Caso documentado |
| Mar 1 dic | Cierre del bloque | README y diagrama |

## Bloque 4: Plataforma con Terraform y AKS
| Fecha | Tema | Entregable |
|---|---|---|
| Jue 3 dic | Terraform base desde Actions (state remoto) | init y plan en workflow |
| Sáb 5 dic | Plan en PR y apply con aprobación | PR con plan y apply |
| Mar 8 dic | AKS con Terraform | Clúster creado y destruido |
| Jue 10 dic | Despliegue a AKS desde Actions | rollout status en el pipeline |
| Sáb 12 dic | Self-hosted runner en VM de Azure | Workflow en mi runner |
| Mar 15 dic | Fallo provocado (drift o runner) y cierre | Caso, README |

## Bloque 5: Migración y estándares
| Fecha | Tema | Entregable |
|---|---|---|
| Jue 17 dic | Auditoría con Actions Importer (pipeline de práctica) | Informe |
| Sáb 19 dic | Migración de un pipeline completa | Equivalencias Azure Pipelines → Actions |
| Dom 20 dic | Observabilidad: Prometheus, Grafana, alerta probada | Panel y registro de decisión |
| Mar 22 dic | Plantillas reutilizables y repo central | Repo de plantillas y guía |
| Sáb 26 dic | Docs as Code | Sitio publicado desde el pipeline |
| Mar 29 dic | Métricas del pipeline, simulacro de entrevista y cierre | Tabla de métricas |

## Certificaciones
- AZ-900: domingos 1, 8, 15 y 22 de nov (19:00-20:30). Valorar fijar fecha de examen tras el 22 de nov, verificando el temario vigente en la página oficial.
- AZ-104: enero-febrero de 2027.
