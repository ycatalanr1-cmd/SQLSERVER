# Buenas prácticas

Recomendaciones útiles para alguien que empieza a trabajar con SQL Server Agent, basadas en la documentación oficial:

* **Usar nombres descriptivos** para Jobs, pasos, programaciones, alertas, operadores y proxies (como se hizo en este manual con el prefijo `Demo_`), de forma que cualquier persona que administre el servidor pueda identificar rápidamente qué hace cada objeto.

* **No usar la cuenta `sa` como práctica permanente.** En este manual se usó `sa` por ser un entorno de práctica; en un entorno real es recomendable que cada Job tenga un propietario identificable y que los permisos se otorguen mediante los roles de SQL Server Agent (`SQLAgentUserRole`, `SQLAgentReaderRole`, `SQLAgentOperatorRole`) en lugar de dar acceso `sysadmin` a todo el mundo.[^1]

* **Usar proxies en lugar de ejecutar todo con la cuenta del servicio de Agent.** Cuando un paso necesita ejecutar algo fuera de T-SQL (PowerShell, comandos del sistema operativo, etc.), es más seguro crear un proxy con permisos limitados a lo que ese paso realmente necesita, en lugar de otorgar permisos amplios a la cuenta del servicio de SQL Server Agent.[^2]

* **Revisar el historial de Jobs periódicamente**, no solo cuando algo falla. Esto ayuda a detectar Jobs que empiezan a tardar más de lo normal, lo cual puede ser señal de un problema antes de que se convierta en una falla completa.[^3]

* **Hacer respaldo de la base `msdb` con regularidad**, sobre todo después de crear, modificar o eliminar Jobs, alertas o proxies, ya que toda esa configuración se almacena ahí.[^4]

* **Preferir deshabilitar antes que eliminar** cuando se necesita pausar temporalmente un Job, para no perder su configuración ni su historial.

* **Documentar el propósito de cada Job** (por ejemplo, en el campo Descripción del Job) para que, si alguien más administra el servidor en el futuro, pueda entender qué automatiza cada uno sin tener que abrir y revisar el código paso por paso.

[^1]: Microsoft. *Implement SQL Server Agent Security*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/implement-sql-server-agent-security
[^2]: Microsoft. *Create a SQL Server Agent Proxy*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/create-a-sql-server-agent-proxy
[^3]: Microsoft. *View the Job History*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/view-the-job-history
[^4]: Microsoft. *The msdb Database*. Microsoft Learn. https://learn.microsoft.com/en-us/sql/relational-databases/databases/msdb-database
