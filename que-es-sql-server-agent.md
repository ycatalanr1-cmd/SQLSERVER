# ¿Qué es SQL Server Agent?

**SQL Server Agent** es un servicio de Windows incluido con SQL Server cuya función es ejecutar tareas administrativas de manera automática, según una programación (horario), en respuesta a un evento, o bien cuando el usuario lo solicita manualmente.[^1][^2]

Dicho de forma sencilla: es el componente que se encarga de que ciertas tareas en la base de datos "se ejecuten solas", sin que una persona tenga que hacerlo manualmente cada vez.

Algunos puntos importantes que debes conocer antes de continuar:

* SQL Server Agent es un **servicio independiente** del motor de base de datos. Esto significa que puede estar detenido aunque SQL Server esté funcionando con normalidad, y en ese caso ninguna tarea automática se ejecutará.
* Por defecto, el servicio de SQL Server Agent **viene deshabilitado** cuando se instala SQL Server, a menos que se configure para iniciar automáticamente.[^2]
* SQL Server Agent utiliza la propia base de datos de SQL Server (una base de datos interna llamada `msdb`) para guardar la información de todas las tareas que administra.[^1][^3]

## ¿Dónde se encuentra en SSMS?

Dentro de SQL Server Management Studio (SSMS), en el **Explorador de objetos**, el nodo **Agente SQL Server** aparece al mismo nivel que "Bases de datos" o "Seguridad". Si ese nodo no aparece, generalmente significa que el usuario conectado no tiene permisos para administrarlo.[^2]

<figure><img src="assets/01-arbol-agente-sql-server.png" alt="Árbol de SQL Server Agent en el Explorador de objetos, mostrando Trabajos, Monitor de actividad de trabajo, Alertas, Operadores, Servidores proxy y Registros de errores"><figcaption>Vista del nodo Agente SQL Server en el Explorador de objetos de SSMS, con sus componentes principales.</figcaption></figure>

Como se observa en la captura, dentro de **Agente SQL Server** se encuentran los elementos que se usarán a lo largo de este manual: **Trabajos**, **Monitor de actividad de trabajo**, **Alertas**, **Operadores** y **Servidores proxy**.

[^1]: Microsoft. *SQL Server Agent*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/sql-server-agent
[^2]: Microsoft. *Configure SQL Server Agent*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/configure-sql-server-agent
[^3]: Microsoft. *The msdb Database*. Microsoft Learn. https://learn.microsoft.com/en-us/sql/relational-databases/databases/msdb-database
