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
- Entorno de prueba configurado.

## 7. Criterios de salida
- Al menos el 90% de los casos de prueba críticos ejecutados.
- Todos los bugs críticos y altos debidamente reportados y clasificados.
- Evidencias (capturas) almacenadas.
- Reporte de ejecución (`Test_Execution_Report.md`) completado.

## 8. Riesgos
- Uso de datos dummy que pueden no reflejar comportamientos reales
- Posibles limitaciones en la lógica del sistema al tratarse de una aplicación demo
- Funcionalidades incompletas o no implementadas




