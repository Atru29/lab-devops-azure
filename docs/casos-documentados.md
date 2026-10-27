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

## Caso 4: no carga el formulario para crear el ACR (27 oct 2026)
- **Síntoma:** al pulsar "+ Crear" en Container registries, el portal mostró "Error al mostrar el contenido" con motivo `ErrorLoadingExtensionAndDefinition` y el detalle "Failed to retrieve the blade definition for 'CreateBladeV2'". Sin código de error. No se creó ningún recurso.
- **Causa:** **no confirmada.** El fallo fue del portal al cargar sus propios módulos, no de la suscripción ni del servicio. Lo más probable es un problema transitorio de caché del navegador o del despliegue del portal.
- **Solución:** recargar la página. El formulario cargó a la primera.
- **Prevención:** si el portal falla, reintentar con recarga forzada o ventana de incógnito, y si persiste, crear el recurso con la CLI (`az acr create`). Guardar el Id. de sesión del error por si hay que abrir un ticket con Microsoft.

## Caso 5: identidad huérfana tras un create-for-rbac fallido (27 oct 2026)
- **Síntoma:** `az ad sp create-for-rbac --name ___ --role ___` terminó con "Role assignment creation failed. Role '___' doesn't exist." Parecía que no se había creado nada.
- **Causa:** el comando hace tres pasos: crear la aplicación en Entra ID, generarle un secreto y asignarle el rol. Los dos primeros se completaron y solo falló el tercero, porque el rol no existía (se ejecutó con los marcadores `___` sin reemplazar). Quedó una aplicación `___` con un secreto válido y sin permisos.
- **Solución:** localizarla con `az ad app list --display-name "___"` y borrarla con `az ad app delete --id <appId>`. Borrar la aplicación elimina también su service principal y su secreto. Después se creó la correcta (`sp-github-lab-devops`, rol `AcrPush` sobre el ACR).
- **Prevención:** tras un comando que falla, comprobar qué quedó creado y no fiarse solo del mensaje de error. Revisar el comando antes de ejecutarlo, sin marcadores pendientes. Las identidades huérfanas con secretos activos son un hallazgo típico de auditoría.
