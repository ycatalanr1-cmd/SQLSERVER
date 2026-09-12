# Introducción

Este manual explica, paso a paso, cómo utilizar **SQL Server Agent**, la herramienta de SQL Server que permite automatizar tareas administrativas dentro del motor de base de datos.

El contenido está organizado en dos grandes bloques:

* **Conceptos**: qué es SQL Server Agent, para qué sirve y qué significan los términos que vas a encontrar durante la práctica (Job, Job Step, Schedule, Alertas, Operadores, Proxies).
* **Procedimiento práctico**: el trabajo realizado por el Grupo 4, documentado con capturas de pantalla reales, desde iniciar el Agente hasta crear un Job completo con su programación, sus alertas, su operador y su proxy.

Al final se incluye una sección de **solución de problemas**, una guía rápida de **administración básica de Jobs**, **buenas prácticas** y las **referencias bibliográficas** utilizadas para fundamentar los conceptos.

Este manual está pensado para una persona que **nunca ha usado SQL Server Agent**. Por eso, cada término técnico se explica la primera vez que aparece, antes de utilizarlo en los pasos prácticos.

> **Entorno de referencia utilizado en este manual**
>
> * SQL Server 2025 (versión de motor 17.x), edición Developer.
> * SQL Server Management Studio (SSMS) 22.
> * SQL Server Agent, ejecutándose sobre el servidor local (`localhost`).
>
> Las capturas de pantalla del procedimiento muestran la conexión como `localhost` (instancia predeterminada). Si tu instalación usa una instancia con nombre (por ejemplo `localhost\SQLAGENT`), el procedimiento es idéntico: solo cambia el nombre que escribes al conectarte en SSMS.
