# ¿Para qué sirve SQL Server Agent?

SQL Server Agent permite automatizar tareas administrativas repetitivas para que no dependan de que una persona las ejecute manualmente cada vez. Según la documentación oficial, puede ejecutar un Job "según una programación, en respuesta a un evento específico o bajo demanda".[^1]

Un ejemplo típico que utiliza la propia documentación de Microsoft: si se necesita respaldar (hacer *backup*) de todos los servidores de la empresa cada día después de las 22:00, en lugar de que alguien lo haga manualmente todas las noches, se programa esa tarea una sola vez y SQL Server Agent se encarga de ejecutarla automáticamente. Si el respaldo tiene un problema, SQL Server Agent puede registrar el evento y notificar a la persona responsable.[^1]

En términos generales, con SQL Server Agent se pueden automatizar tareas como:

* Ejecutar scripts T-SQL de mantenimiento o de negocio en un horario definido.
* Respaldar bases de datos de forma periódica.
* Ejecutar comandos del sistema operativo o scripts de PowerShell.
* Notificar a un responsable cuando ocurre un error específico en el servidor (por medio de Alertas y Operadores).

Este manual documenta, precisamente, un caso práctico simplificado de este tipo de automatización: un Job que registra una ejecución en una tabla de bitácora todos los días, más una Alerta que puede notificar y ejecutar un Job en respuesta a un evento del servidor.

[^1]: Microsoft. *SQL Server Agent*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/sql-server-agent
