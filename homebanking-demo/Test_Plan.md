# Test Plan — Home Banking Demo

## 1. Introducción
Este documento tiene como objetivo definir el enfoque, alcance y estrategia de pruebas para la validación de las funcionalidades de la aplicación Home Banking Demo.

## 2. Objetivo
- Realizar un ciclo completo de testing manual simulando el rol de QA en un banco digital.
- Diseñar y ejecutar casos de prueba para los módulos críticos de la aplicación.
- Identificar y documentar defectos con sus respectivos pasos de reproducción.

## 3. Alcance
**In Scope:**
- Módulos principales de la aplicación:
-   Login
-   Dashboard
-   Transferencias
-   Plazos fijos
-   Préstamos
-   Pago de servicios
-   Tarjetas virtuales
-   Mis datos

**Out of Scope:**
- Integraciones con sistemas reales
- Pruebas de performance


## 4. Estrategia
Se aplicarán los siguientes enfoques:
- Exploratory Testing
- Smoke Testing
- Functional Testing
- Negative Testing
- Boundary Value Analysis
- Pruebas de Usabilidad / UI

## 5. Entorno de prueba
URL: https://homebanking-demo-tests.netlify.app/ 
Sistema Operativo: Windows 11
Navegador: Chrome Versión
Herramientas: GitHub, Chrome DevTools, Notion

## 6. Criterios de entrada
- La aplicación responde sin errores críticos (sin errores 404/500)
- Credenciales de prueba disponibles y validadas.
- Casos de prueba documentados.
- Las funcionalidades principales están implementadas.
- Entorno de prueba configurado.

## 7. Criterios de salida
- Al menos el 90% de los casos de prueba críticos ejecutados.
- Todos los bugs críticos y altos debidamente reportados y clasificados.
- Evidencias (capturas) almacenadas.
- No existen defectos críticos abiertos que impidan el uso básico del sistema.
- Reporte de ejecución (`Test_Execution_Report.md`) completado.

## 8. Riesgos
- Uso de datos dummy que pueden no reflejar comportamientos reales
- Posibles limitaciones en la lógica del sistema al tratarse de una aplicación demo
- Funcionalidades incompletas o con comportamiento no definido.
- Dependencia de un único entorno (no se prueban distintos dispositivos o navegadores).


| # | Riesgo | Probabilidad | Impacto | Mitigación |
|---|--------|--------------|---------|------------|
| 1 | **Datos dummy no reflejan comportamiento real** | ALTA | MEDIO | - Documentar limitaciones en el reporte final<br>- Aclarar que es ambiente de prueba<br>- No asumir que bugs encontrados existen en producción |
| 2 | **Funcionalidades incompletas o no implementadas** | MEDIA | ALTO | - Explorar app antes de escribir test cases<br>- Documentar features "Out of Scope"<br>- Ajustar test cases solo a features existentes |
| 3 | **App demo puede caerse o estar offline** | BAJA | CRÍTICO | - Hacer capturas de pantalla durante exploración<br>- Guardar copia local del HTML (si es posible)<br>- Documentar estado de la app en cada sesión |
| 4 | **Cambios en la app sin notificación** | MEDIA | MEDIO | - Versionar test cases con fecha<br>- Documentar versión de la app testeada<br>- Re-ejecutar smoke tests si detectás cambios |
| 5 | **Falta de documentación oficial** | ALTA | MEDIO | - Basarse en la sección "Documentación Funcional" de la app<br>- Documentar asunciones propias<br>- Validar asunciones con exploración |



