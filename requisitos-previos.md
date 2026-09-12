# Requisitos previos

Para seguir este manual necesitas contar con lo siguiente:

* **SQL Server 2025** (edición Developer), instalado y en ejecución.
* **SQL Server Management Studio (SSMS) 22**, instalado en el equipo.
* El servicio de **SQL Server Agent** disponible en tu instalación (viene incluido con SQL Server, pero puede estar detenido; en la sección de procedimiento se explica cómo iniciarlo).
* Una conexión a tu instancia local de SQL Server (en este manual, `localhost`) con una cuenta que tenga permisos suficientes para administrar SQL Server Agent. En las capturas de este manual se usó el inicio de sesión `sa`.

> **¿Por qué se necesitan permisos especiales?**
>
> Para administrar SQL Server Agent (crear Jobs, Alertas, Operadores o Proxies) el usuario debe ser miembro del rol de servidor `sysadmin`, o bien pertenecer a uno de los roles de base de datos específicos de SQL Server Agent dentro de `msdb` (`SQLAgentUserRole`, `SQLAgentReaderRole` o `SQLAgentOperatorRole`).[^1] Si el nodo **Agente SQL Server** no aparece en el Explorador de objetos, normalmente es por esta razón.

No es necesario tener conocimientos avanzados de T-SQL: el único código que se utiliza en este manual es una instrucción `INSERT` sencilla y una consulta `SELECT` para verificar el resultado, ambas explicadas paso a paso.

[^1]: Microsoft. *Implement SQL Server Agent Security*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/implement-sql-server-agent-security
