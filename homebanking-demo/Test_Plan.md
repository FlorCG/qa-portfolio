# Test Plan — Home Banking Demo  

**Proyecto:** Home Banking Demo   
**URL:** https://homebanking-demo-tests.netlify.app/   

---

## 1. Objetivo
Este documento tiene como objetivo verificar que los módulos principales de la aplicación Home Banking Demo funcionan correctamente según el comportamiento esperado, identificando defectos funcionales, de validación y de experiencia de usuario mediante técnicas de testing manual.  

---

## 2. Alcance  

### Dentro del alcance  

| Módulo | Prioridad | Cobertura |
|---|---|---|
| Login | Alta | Completa — casos positivos, negativos, límites y edge cases |
| Dashboard | Alta | Completa — visualización de datos, consistencia y navegación |
| Transferencias | Alta | Completa — flujos válidos, validaciones y casos borde |
| Pago de Servicios | Alta | Completa — alta, pago y validaciones |
| Tarjetas Virtuales | Alta | Completa — generación y visualización |
| Plazos Fijos | Media | Parcial — flujos principales y casos básicos |
| Préstamos | Media | Parcial — flujos principales y casos básicos |
| Mis Datos | Baja | Mínima — verificación de visualización de datos |

### Fuera del alcance

- Testing de performance o carga
- Testing de seguridad (penetration testing)
- Testing en dispositivos móviles nativos
- Testing en browsers distintos a Google Chrome — el cross-browser testing se abordará en la fase de automatización, que permite ejecutar los mismos tests en Chromium, Firefox y WebKit
- Integración con sistemas externos (la app usa datos simulados)

> **Nota:** Los módulos de Plazos Fijos y Préstamos, aunque de prioridad media, se incluyen en el alcance porque manejan operaciones financieras. Un defecto en estos módulos, aunque poco frecuentes, tiene impacto significativo.

---

## 3. Tipos de prueba  

| Tipo | Aplicación en este proyecto |
|---|---|
| **Exploratory Testing** | Realizado al inicio del proyecto para entender el sistema, identificar comportamientos inesperados y definir el alcance |
| **Smoke Testing** | Verificación básica de que los flujos principales de cada módulo funcionan antes de profundizar en las pruebas |
| **Functional Testing** | Validación de la funcionalidad principal de cada módulo según el comportamiento esperado |
| **Negative Testing** | Pruebas con datos inválidos, campos vacíos, formatos incorrectos y flujos no esperados — especialmente relevante en formularios de transferencias y pagos |
| **Boundary Value Analysis** | Pruebas en valores límite en campos numéricos como montos, cuotas y fechas — crítico en módulos financieros |
| **UI / Usability Testing** | Validación de mensajes de error, feedback visual al usuario, claridad de la interfaz y consistencia de datos entre módulos |

---

## 4. Criterios de entrada

Condiciones que deben cumplirse para **comenzar** la ejecución de pruebas:

- La aplicación está accesible en su URL
- Los datos de prueba están disponibles (credenciales, cuentas simuladas)
- El entorno de pruebas está configurado (browser, resolución)
- Los casos de prueba están diseñados y revisados
- El repositorio está configurado para documentar los resultados

---

## 5. Criterios de salida

Condiciones que determinan que el ciclo de pruebas está **completo**:

- El 100% de los casos de prueba fue ejecutado
- Todos los defectos encontrados están documentados en bug reports
- Los bugs de severidad crítica y alta están reportados con evidencia
- El Test Execution Report está completo con métricas finales
- El README fue actualizado con los resultados

---

## 6. Riesgos

| Riesgo | Impacto | Mitigación |
|---|---|---|
| La app es un demo con datos simulados — algunos comportamientos pueden no reflejar un sistema real | Medio | Documentar las limitaciones encontradas en los bug reports |
| Los datos se resetean entre sesiones | Bajo | Recrear las precondiciones necesarias antes de cada caso |
| No hay documentación oficial de requisitos | Medio | Basar el comportamiento esperado en el análisis funcional propio y en estándares de usabilidad |
| Testing realizado en un solo browser | Bajo | Aclarado en el alcance — fuera de scope para este proyecto |

---

## 7. Entorno de pruebas

| Componente | Detalle |
|---|---|
| **Browser** | Google Chrome (última versión estable) |
| **Sistema operativo** | Windows 11 |
| **Resolución** | 1920x1080 |
| **Herramientas** | Chrome DevTools, Jira, GitHub, Markdown |
| **Tipo de conexión** | Conexión a internet estable |

---

## 8. Estrategia de reporte de bugs

- Cada defecto encontrado se documenta en un archivo individual dentro de `bug-reports/`
- El formato incluye: ID, título, módulo, severidad, prioridad, pasos para reproducir, resultado actual, resultado esperado y evidencia visual
- Los bugs se gestionan además en **Jira** para simular un flujo de trabajo real
- La severidad sigue esta escala:

| Severidad | Criterio |
|---|---|
| **Crítica** | Bloquea el uso de la app o causa pérdida de datos |
| **Alta** | Funcionalidad principal no funciona correctamente |
| **Media** | Funcionalidad secundaria con comportamiento incorrecto |
| **Baja** | Problemas de UI, textos o inconsistencias menores |

---


# Asunciones de Diseño — Módulo Login

> **Nota:** Dado que esta es una aplicación demo sin documentación funcional completa por parte de un Product Owner, se establecieron las siguientes asunciones para poder ejecutar los casos de prueba. Estas decisiones fueron tomadas por el equipo de QA y deberían ser validadas por negocio en un contexto real.

| Regla ambigua | Asunción adoptada | Casos afectados |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|----------------|
| Checkbox **"Recordarme"** | Al tildarse, mantiene la sesión activa por **7 días**, aunque se cierre el navegador. Si no se tilda, la sesión expira al cerrar el navegador. | LOG-12, LOG-13 |
| Longitud mínima de Usuario | **4 caracteres**. | LOG-15 |
| Longitud máxima de Usuario | **20 caracteres**. | LOG-16, LOG-17 |
| Longitud mínima de Contraseña | **6 caracteres**. | LOG-18, LOG-19 |
| Longitud máxima de Contraseña | **20 caracteres**. | LOG-20 |
| Case-sensitivity de Usuario | El campo Usuario **no distingue entre mayúsculas y minúsculas** (*case-insensitive*). | LOG-23 |
| Case-sensitivity de Contraseña | La Contraseña **sí distingue entre mayúsculas y minúsculas** (*case-sensitive*), siguiendo una regla estándar de seguridad. | LOG-24 |
| Caracteres especiales permitidos en Usuario | Se permiten únicamente **punto (`.`)** y **guion bajo (`_`)**. Cualquier otro carácter especial se considera inválido. | LOG-25, LOG-26 |








