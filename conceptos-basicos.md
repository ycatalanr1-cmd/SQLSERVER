# Conceptos básicos

Antes de entrar al procedimiento práctico, es necesario comprender algunos términos que se usan constantemente al trabajar con SQL Server Agent. Cada uno se explica de forma sencilla y se relaciona con el ejemplo práctico que se construye en este manual (el Job `Demo_SQL_Agent`).

## Job (trabajo)

Un **Job** es una serie de operaciones que SQL Server Agent ejecuta en un orden específico, una tarea completa que se automatiza.[^1] Un Job puede tener uno o varios pasos, y puede programarse para que se ejecute automáticamente o iniciarse de forma manual.

En este manual, el Job creado se llama **`Demo_SQL_Agent`**.

## Job Step (paso de trabajo)

Un Job casi nunca es una sola acción: está compuesto por uno o más **Job Steps** (pasos), que se ejecutan de manera secuencial. Cada paso tiene un **tipo** (por ejemplo, Script Transact-SQL, Sistema operativo (CmdExec), PowerShell, entre otros) que determina qué clase de comando ejecuta y en qué contexto de seguridad lo hace.[^1][^2]

En este manual, el Job `Demo_SQL_Agent` tiene un solo paso llamado **`Registrar ejecución`**, de tipo **Script Transact-SQL (T-SQL)**, que inserta un registro en una tabla de bitácora.

## Schedule (programación)

Una **Schedule** (programación) define **cuándo** debe ejecutarse un Job de forma automática: puede ser al iniciar el servicio de SQL Server Agent, cuando el procesador está inactivo, una sola vez en una fecha específica, o de forma recurrente (por ejemplo, todos los días a cierta hora).[^3] Una misma programación puede asociarse a más de un Job.

En este manual, la programación se llama **`Demo_Diario`** y está configurada para ejecutarse una vez al día.

## Historial del Job (Job History)

Cada vez que un Job se ejecuta, SQL Server Agent guarda un registro del resultado (correcto o con error), la duración y los mensajes generados por cada paso. A esto se le llama **historial del Job**, y se puede consultar haciendo clic derecho sobre el Job y seleccionando **Ver historial**.[^4]

## Job Activity Monitor (Monitor de actividad de trabajo)

El **Job Activity Monitor** es una pantalla dentro de SSMS que muestra, en tiempo real, el estado de todos los Jobs definidos en el servidor: si están habilitados, si se están ejecutando, cuál fue el resultado de su última ejecución y cuándo se ejecutarán de nuevo.[^5] Desde ahí también se pueden iniciar, detener, habilitar o deshabilitar Jobs sin tener que buscarlos uno por uno en la carpeta de Trabajos.

## Alertas (Alerts)

Una **Alerta** es una respuesta automática que SQL Server Agent activa cuando ocurre un evento específico: por ejemplo, un error de SQL Server de cierto número o de cierta gravedad ("severity"). Una alerta puede responder notificando a un operador, ejecutando un Job, o ambas cosas.[^6]

En este manual se crea la alerta **`Alerta_Demo_SQL_Agent`**, configurada sobre la gravedad *001 - Información diversa del sistema*.

## Operadores (Operators)

Un **Operador** es, en esencia, un alias para una persona (o un correo) a la que SQL Server Agent puede notificar cuando un Job falla o tiene éxito, o cuando se dispara una alerta.[^7]

En este manual se crea el operador **`Operador_Demo_SQL_Agent`**.

## Proxies y credenciales

Por default, un paso de tipo T-SQL se ejecuta con los permisos del propietario del Job. Pero cuando un paso necesita ejecutar otro tipo de comando (por ejemplo PowerShell o comandos del sistema operativo), puede requerir permisos distintos a los del usuario que creó el Job. Para eso existen los **Proxies**: un proxy define un contexto de seguridad —basado en una **credencial** ya creada— que un paso de trabajo puede usar para ejecutarse con permisos específicos, sin necesidad de dar esos permisos directamente al usuario.[^8]

En este manual se crea la credencial **`Cred_Demo_Proxy`** y, sobre ella, el proxy **`Proxy_Demo_SQL_Agent`**, habilitado para el subsistema **PowerShell**.

## msdb

Todos los objetos anteriores (Jobs, Job Steps, Schedules, Alertas, Operadores, Proxies e historial) se almacenan internamente en una base de datos del sistema llamada **`msdb`**, que SQL Server crea automáticamente y que es usada por SQL Server Agent para todo su funcionamiento.[^9]

[^1]: Microsoft. *Create Jobs*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-jobs
[^2]: Microsoft. *Create a Transact-SQL Job Step*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-a-transact-sql-job-step
[^3]: Microsoft. *Create and Attach Schedules to Jobs*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-and-attach-schedules-to-jobs
[^4]: Microsoft. *View the Job History*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/view-the-job-history
[^5]: Microsoft. *Job Activity Monitor*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/job-activity-monitor
[^6]: Microsoft. *Monitor and Respond to Events*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/monitor-and-respond-to-events
[^7]: Microsoft. *Create an Operator*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-an-operator
[^8]: Microsoft. *Create a SQL Server Agent Proxy*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-a-sql-server-agent-proxy
[^9]: Microsoft. *The msdb Database*. Microsoft Learn. https://learn.microsoft.com/en-us/sql/relational-databases/databases/msdb-database
