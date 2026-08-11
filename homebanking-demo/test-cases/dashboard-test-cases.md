# Test Cases – Dashboard / Panel Principal

## Información general

- **Elementos de la interfaz:** Navbar (usuario + botón "Salir"), Sidebar (menú de navegación), Panel Principal (resumen de saldos), botón "Restablecer saldos", Tarjetas de cuenta (Corriente, Caja de Ahorro, Tarjeta de Crédito) con botón "Ocultar", Últimos Movimientos
- **Reglas de negocio consideradas:**
  - El Dashboard es la página principal tras el login exitoso
  - Las tres cuentas deben estar siempre visibles
  - El botón "Ocultar" oculta número y saldo, manteniendo el título visible
  - Los últimos movimientos muestran las transacciones más recientes primero
  - El botón "Restablecer saldos" reinicia los valores a un estado inicial conocido (entorno demo)

---

# Casos Funcionales

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DASH-01 | Visualización del resumen de cuentas | Usuario logueado con cuentas activas | 1. Ingresar al Dashboard tras login exitoso. | Se muestran las 3 cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito), cada una con título, número y saldo. | Alta |
| DASH-02 | Nombre de usuario visible en la navbar | Usuario logueado | 1. Ingresar al Dashboard.<br>2. Observar la navbar. | Se muestra el nombre del usuario autenticado en la navbar. | Baja |
| DASH-03 | Visualización de Últimos Movimientos | Usuario logueado, con movimientos registrados | 1. Ingresar al Dashboard.<br>2. Ubicar la sección "Últimos Movimientos". | Se muestra un listado de movimientos, ordenados del más reciente al más antiguo. | Media |
| DASH-04 | Últimos Movimientos sin datos | Usuario logueado, sin movimientos registrados | 1. Ingresar al Dashboard con una cuenta sin historial. | Se muestra un mensaje indicando ausencia de movimientos, o una tabla vacía con estado claro (no un error). | Media |
| DASH-05 | Actualización de saldo tras transferencia *(pendiente de confirmación)* | Usuario logueado | 1. Registrar saldo de una cuenta en el Dashboard.<br>2. Realizar una transferencia desde/hacia esa cuenta.<br>3. Volver al Dashboard. | **No confirmado si se actualiza en tiempo real o requiere refresco manual.** Documentar comportamiento real como asunción de diseño. | Alta |

---

# Casos de "Ocultar" cuenta

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DASH-06 | Ocultar número y saldo de una cuenta | Usuario logueado, Dashboard visible | 1. Click en "Ocultar" en la tarjeta de una cuenta (ej. Caja de Ahorro). | El número de cuenta y el saldo se ocultan; el título de la cuenta permanece visible. | Media |
| DASH-07 | Mostrar nuevamente una cuenta oculta | Cuenta previamente oculta | 1. Click en el botón para revertir "Ocultar" (mostrar) en la tarjeta oculta. | El número de cuenta y saldo vuelven a mostrarse correctamente. | Media |
| DASH-08 | Persistencia del estado "Ocultar" al cambiar de módulo *(pendiente de confirmación)* | Una cuenta oculta en el Dashboard | 1. Ocultar una cuenta.<br>2. Navegar a otro módulo (ej. Transferencias).<br>3. Volver al Dashboard. | **No confirmado si el estado persiste.** Documentar comportamiento real como asunción de diseño. | Baja |

---

# Casos de "Restablecer saldos"

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DASH-09 | Restablecer saldos desde el botón correspondiente | Usuario logueado, con saldos modificados por operaciones previas | 1. Click en "Restablecer saldos". | Los saldos de las tres cuentas vuelven a su valor inicial de demo. | Media |
| DASH-10 | Restablecer saldos y su efecto en Últimos Movimientos *(pendiente de confirmación)* | Usuario con movimientos registrados | 1. Click en "Restablecer saldos".<br>2. Verificar la sección "Últimos Movimientos". | **No confirmado si los movimientos también se resetean.** Documentar comportamiento real como asunción de diseño. | Baja |

---

# Casos de Navegación y Sesión

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DASH-11 | Navegación a otros módulos desde el sidebar | Usuario logueado | 1. Click en cada uno de los links del sidebar (Transferencias, Plazos Fijos, Préstamos, etc.). | El sistema navega correctamente al módulo correspondiente en cada caso. | Alta |
| DASH-12 | Cierre de sesión desde la navbar | Usuario logueado | 1. Click en el botón "Salir" de la navbar. | El sistema cierra la sesión y redirige a la pantalla de Login. | Alta |

---

**Total de Test Cases: 12**

