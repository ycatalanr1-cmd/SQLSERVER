# Administración básica de Jobs

Una vez que un Job existe, hay operaciones básicas de mantenimiento que se van a necesitar con frecuencia. Todas se pueden realizar desde el mismo lugar: Agente SQL Server → Trabajos (o desde el Job Activity Monitor).

## Ejecutar manualmente

**Cómo:** Clic derecho sobre el Job → **Iniciar trabajo en el paso...** Esto ya se usó en este manual para probar `Demo_SQL_Agent` sin esperar a su programación.[^1]

## Detener un Job en ejecución

**Cómo:** Clic derecho sobre el Job → **Detener trabajo**. También se puede hacer desde el Job Activity Monitor, seleccionando uno o varios Jobs a la vez.

**Nota importante:** Si el paso en ejecución es de tipo Sistema operativo (CmdExec) o PowerShell, detener el Job fuerza el cierre del proceso externo de forma abrupta, lo que puede dejar archivos en uso o resultados incompletos. Esta acción debe usarse con cuidado, especialmente en pasos que no son de tipo T-SQL.[^2]

## Modificar un Job

**Cómo:** Doble clic sobre el Job (o clic derecho → **Propiedades**) para abrir el mismo cuadro que se usó al crearlo, con acceso a sus páginas General, Pasos, Programaciones, Alertas, Notificaciones y Destinos. Un Job solo puede ser modificado por su propietario o por un miembro del rol `sysadmin`.[^3]

## Habilitar o deshabilitar un Job

**Cómo:** Clic derecho sobre el Job → **Deshabilitar** (o **Habilitar** si ya está deshabilitado). Deshabilitar un Job no lo elimina: simplemente evita que se ejecute automáticamente según su programación, aunque se le puede seguir dejando iniciar manualmente en algunos casos. Es útil, por ejemplo, para pausar temporalmente una tarea sin perder su configuración.[^4]

## Eliminar un Job

**Cómo:** Clic derecho sobre el Job → **Eliminar**, y confirmar en el cuadro de diálogo. A menos que el usuario sea miembro de `sysadmin`, solo puede eliminar los Jobs de los que es propietario.[^5]

> Eliminar un Job es una acción permanente: se pierde tanto la definición del Job como su historial de ejecuciones asociado. Si solo se quiere pausar la automatización de forma temporal, es preferible deshabilitar el Job en lugar de eliminarlo.

## Consultar el historial

**Cómo:** Clic derecho sobre el Job → **Ver historial**. Se abre el visor de registros con el detalle de cada ejecución, incluyendo el resultado de cada paso por separado.[^6]

[^1]: Microsoft. *Start a SQL Server Agent job*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/start-a-job
[^2]: Microsoft. *Stop a Job*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/stop-a-job
[^3]: Microsoft. *Create Jobs*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-jobs
[^4]: Microsoft. *Disable or Enable a Job*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/disable-or-enable-a-job
[^5]: Microsoft. *Delete One or More Jobs*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/delete-one-or-more-jobs
[^6]: Microsoft. *View the Job History*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/view-the-job-history
