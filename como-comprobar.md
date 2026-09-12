# ¿Cómo comprobar que el Job funcionó?

Este manual utilizó tres formas distintas de comprobar que el Job `Demo_SQL_Agent` funcionó correctamente. Se resumen aquí para tenerlas como referencia rápida.

## 1. El cuadro de resultado al ejecutar manualmente

Al iniciar el Job manualmente (**Iniciar trabajo en el paso...**), SSMS muestra de inmediato un cuadro con el resultado de la ejecución. Un ícono verde y la palabra **Correcto** confirman que todos los pasos se ejecutaron sin error. Ver [Ejecutar el Job manualmente y verificar el resultado](procedimiento/05-ejecutar-y-verificar.md).

## 2. Consultar la tabla de bitácora

La forma más directa de comprobar el efecto real del Job es consultar la tabla que el paso modifica:

```sql
SELECT *
FROM dbo.AgentDemoLog;
```

Si aparece una fila nueva cada vez que el Job se ejecuta, el paso T-SQL está funcionando como se espera.

## 3. Job Activity Monitor

El **Monitor de actividad de trabajo** permite ver, sin ejecutar ninguna consulta, el estado general del Job: si está habilitado, cuál fue el resultado de su última ejecución y cuándo volverá a ejecutarse. Ver [Consultar el estado del Job con el Job Activity Monitor](procedimiento/06-monitor-actividad.md).

## 4. Historial del Job

Adicional a lo documentado con capturas en este manual, SQL Server Agent guarda un historial detallado de cada ejecución. Para consultarlo: clic derecho sobre el Job → **Ver historial**. Ahí se puede expandir el Job para ver el resultado de cada paso por separado, junto con cualquier mensaje de error, en caso de haberlo.[^1]

[^1]: Microsoft. *View the Job History*. Microsoft Learn. https://learn.microsoft.com/en-us/ssms/agent/view-the-job-history
