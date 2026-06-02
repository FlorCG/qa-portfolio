# Home Banking Demo - Testing Manual

## Aplicación bajo prueba

| Campo | Detalle |
|---|---|
| **Nombre** | Home Banking Demo |
| **URL** | https://homebanking-demo-tests.netlify.app/ |
| **Tipo** | Aplicación simulada de home banking en español |
| **Datos** | Entorno de prueba con datos ficticios |

---

## Objetivo del Proyecto
El objetivo de este proyecto es aplicar el ciclo completo de testing manual sobre una aplicación de homebanking, abarcando desde el análisis funcional hasta la ejecución de pruebas y reporte de bugs.

## Módulos testeados

| Módulo | Descripción |
|---|---|
| **Login** | Autenticación con credenciales válidas e inválidas |
| **Dashboard** | Resumen de cuentas (Cuenta Corriente, Caja de Ahorro, Tarjeta de Crédito) y últimos movimientos |
| **Transferencias** | Transferencias entre cuentas propias y a terceros |
| **Plazos Fijos** | Consulta, creación y cancelación de plazos fijos |
| **Préstamos** | Consulta, solicitud y cancelación de préstamos |
| **Pago de Servicios** | Alta y pago de servicios (luz, gas, internet, etc.) |
| **Tarjetas Virtuales** | Generación y consulta de tarjetas virtuales |
| **Mis Datos** | Visualización de información personal, cuentas y tarjetas |

---

## Tipos de pruebas realizadas

| Tipo | Descripción |
|---|---|
| **Exploratory Testing** | Exploración libre de la app para entender el sistema y detectar comportamientos inesperados |
| **Smoke Testing** | Pruebas básicas de estabilidad para verificar que los flujos principales funcionan |
| **Functional Testing** | Verificación de la funcionalidad principal de cada módulo |
| **Negative Testing** | Pruebas con datos inválidos, campos vacíos y flujos incorrectos |
| **Boundary Value Analysis** | Pruebas en valores límite y casos borde |
| **UI / Usability Testing** | Validación de mensajes de error, claridad visual y experiencia de usuario |

---

## Herramientas utilizadas

| Herramienta | Uso |
|---|---|
| **Jira** | Gestión y seguimiento de bugs en entorno laboral |
| **Chrome DevTools** | Inspección de elementos, consola, red |
| **GitHub** | Control de versiones y publicación del portfolio |
| **Markdown** | Documentación de artefactos en el repositorio |

> Los bug reports de este proyecto están documentados en formato Markdown directamente en el repositorio, para facilitar su lectura en GitHub. En entornos laborales utilizo Jira para la gestión de defectos.

---

## Estructura del proyecto

```
homebanking-demo/
├── README.md                        → Este archivo
├── test-plan.md                     → Alcance, estrategia y criterios de prueba
├── functional-analysis/             → Análisis funcional por módulo
│   ├── login.md
│   ├── dashboard.md
│   ├── transferencias.md
│   ├── plazos-fijos.md
│   ├── prestamos.md
│   ├── pago-servicios.md
│   ├── tarjetas-virtuales.md
│   └── mis-datos.md
├── test-cases/                      → Casos de prueba por módulo
│   ├── TC-LOGIN.md
│   ├── TC-DASHBOARD.md
│   ├── TC-TRANSFERENCIAS.md
│   ├── TC-PLAZOS-FIJOS.md
│   ├── TC-PRESTAMOS.md
│   ├── TC-PAGO-SERVICIOS.md
│   ├── TC-TARJETAS-VIRTUALES.md
│   └── TC-MIS-DATOS.md
├── bug-reports/                     → Reporte de defectos encontrados
│   ├── BUG-001.md
│   └── ...
└── test-execution-report.md         → Resumen de ejecución y resultados
```

## Resultados

> ⏳ Sección en progreso — se completará al finalizar la ejecución de pruebas.

| Métrica | Resultado |
|---|---|
| Total de casos de prueba | — |
| Casos ejecutados | — |
| ✅ Pass | — |
| ❌ Fail | — |
| ⚠️ Blocked | — |
| 🐛 Bugs reportados | — |

---

*Portfolio QA · [Flor CG](https://www.linkedin.com/in/florcg/) · [Repositorio](https://github.com/FlorCG/qa-portfolio/tree/main/homebanking-demo)*
