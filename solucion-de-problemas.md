# Solución de problemas

Esta sección reúne los problemas más comunes que puede encontrar una persona que recién empieza a usar SQL Server Agent, junto con su causa probable, cómo comprobarlo y la solución, siguiendo la documentación oficial de Microsoft. Los pasos prácticos de este manual no presentaron estos errores; se incluyen como guía preventiva.

## El nodo "Agente SQL Server" no aparece en el Explorador de objetos

**Causa probable:** El usuario conectado no tiene permisos suficientes para administrar SQL Server Agent.

**Cómo comprobarlo:** Verificar si el inicio de sesión usado es miembro del rol de servidor `sysadmin`, o de alguno de los roles `SQLAgentUserRole`, `SQLAgentReaderRole` o `SQLAgentOperatorRole` dentro de la base `msdb`.[^1]

**Solución:** Conectarse con un inicio de sesión que sí tenga esos permisos, o solicitar a un administrador que agregue al usuario al rol correspondiente.

## SQL Server Agent aparece detenido

**Causa probable:** El servicio no se inició, ya sea porque no está configurado para iniciar automáticamente, o porque se detuvo manualmente.

**Cómo comprobarlo:** El ícono del nodo Agente SQL Server en el Explorador de objetos muestra una marca distinta cuando el servicio no está en ejecución.

**Solución:** Clic derecho sobre **Agente SQL Server** → **Iniciar**. Ver [Iniciar SQL Server Agent](procedimiento/01-iniciar-agente.md).[^2]

## El Job no se ejecuta a la hora programada

**Causa probable:** El servicio de SQL Server Agent está detenido, la programación está deshabilitada, o el Job mismo está deshabilitado.

**Cómo comprobarlo:** Revisar en el Job Activity Monitor si el Job aparece como **Habilitado**, y revisar en las propiedades del Job, página Programaciones, si la programación asociada está marcada como habilitada.

**Solución:** Habilitar el Job y/o la programación según corresponda. Recordar que, si el Job ya se está ejecutando, SQL Server Agent no permitirá una segunda ejecución simultánea del mismo Job.[^3]

## El Job termina con resultado "Failed" (con error)

**Causa probable:** El paso que falló contiene un error de sintaxis en el comando, hace referencia a un objeto que no existe (por ejemplo, una tabla eliminada), o el usuario que ejecuta el paso no tiene permisos suficientes sobre la base de datos.

**Cómo comprobarlo:** Clic derecho sobre el Job → **Ver historial**. Expandir el paso que falló para leer el mensaje de error específico que SQL Server Agent registró.[^4]

**Solución:** Corregir el comando del paso según el mensaje de error (por ejemplo, revisar el nombre exacto de la tabla o columna), o verificar y ajustar los permisos del usuario o proxy usado por el paso.

## Error en un Job Step de tipo T-SQL

**Causa probable:** El script tiene un error de sintaxis, o hace referencia a un objeto de una base de datos distinta a la seleccionada en el paso.

**Cómo comprobarlo:** Antes de guardar el paso, usar el botón **Analizar** en el cuadro de propiedades del paso para validar la sintaxis. Si el error ocurre después de guardado, consultar el historial del Job para ver el mensaje exacto devuelto por el motor.[^5]

**Solución:** Corregir el script según el mensaje de análisis o de error, confirmando que la base de datos seleccionada en el campo **Base de datos** del paso es la correcta.

## Un Job queda ejecutándose sin terminar

**Causa probable:** Un paso está tardando más de lo esperado (por ejemplo, una consulta larga o un proceso externo que no responde).

**Cómo comprobarlo:** Revisar el estado del Job en el Job Activity Monitor; si aparece como "Ejecutando" durante un tiempo anormalmente largo, puede ser necesario detenerlo.

**Solución:** Detener el Job manualmente: clic derecho sobre el Job → **Detener trabajo**. Ten en cuenta que, si el paso en ejecución es de tipo CmdExec o PowerShell, detener el Job puede forzar el cierre abrupto del proceso externo, lo que puede dejar archivos abiertos o resultados incompletos.[^6]

## No llegan las notificaciones al operador

**Causa probable:** Database Mail no está configurado en la instancia, o el operador no tiene un correo válido asignado.

**Cómo comprobarlo:** Revisar la configuración de Database Mail y las propiedades del operador (página **Notificaciones**) para confirmar que el correo está bien escrito y que la notificación por correo está habilitada para las alertas o Jobs deseados.

**Solución:** Configurar Database Mail si aún no está configurado, y verificar que el operador tenga marcada la casilla de notificación por correo.[^7]

[^1]: Microsoft. *Implement SQL Server Agent Security*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/implement-sql-server-agent-security
[^2]: Microsoft. *Start, Stop, or Pause the SQL Server Agent Service*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/start-stop-or-pause-the-sql-server-agent-service
[^3]: Microsoft. *Create and Attach Schedules to Jobs*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-and-attach-schedules-to-jobs
[^4]: Microsoft. *View the Job History*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/view-the-job-history
[^5]: Microsoft. *Create a Transact-SQL Job Step*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-a-transact-sql-job-step
[^6]: Microsoft. *Stop a Job*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/stop-a-job
[^7]: Microsoft. *SQL Server Agent alerts*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/alerts
