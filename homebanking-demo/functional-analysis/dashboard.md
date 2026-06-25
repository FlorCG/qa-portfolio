# Análisis Funcional — Dashboard

**Módulo:** Dashboard / Panel Principal  
**Prioridad:** Alta  

---

## Objetivo

Mostrar un resumen de la situación financiera del usuario luego de autenticarse. Centraliza el acceso a todas las funcionalidades de la app y permite visualizar rápidamente el estado de las cuentas y movimientos recientes.

---

## Elementos de la interfaz

| Elemento | Tipo | Descripción |
|---|---|---|
| Navbar | Barra fija superior | Contiene nombre de usuario y botón "Salir" |
| Sidebar | Panel lateral izquierdo | Menú de navegación con links a módulos |
| Panel Principal | Sección principal | Título y resumen de saldos |
| Botón "Restablecer saldos" | Botón de acción | Reinicia los valores de las cuentas |
| Tarjeta Cuenta Corriente | Card | Muestra título, número, saldo, botón ocultar |
| Tarjeta Caja de Ahorro | Card | Muestra título, número, saldo, botón ocultar |
| Tarjeta Tarjeta de Crédito | Card | Muestra título, número, saldo, botón ocultar |
| Últimos Movimientos | Tabla/Lista | Detalle de transacciones recientes |

---

## Reglas de negocio

- El Dashboard es la página principal tras el login exitoso
- El usuario solo ve información de sus propias cuentas
- Las tres cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito) deben estar siempre visibles en el Dashboard
- El botón "Ocultar" en cada cuenta permite ocultar el número y saldo, manteniendo el título visible
- Los últimos movimientos muestran las transacciones más recientes primero
- El saldo debe ser consistente con las operaciones realizadas (transferencias, pagos, etc.)
- El botón "Restablecer saldos" reinicia los valores a un estado inicial conocido (debido a que es un entorno demo)

---

## Flujo principal

1. Usuario inicia sesión con credenciales válidas
2. Sistema redirige al Dashboard
3. Dashboard carga y muestra:
   - Nombre de usuario en la navbar
   - Resumen de las tres cuentas con saldos actuales
   - Últimos movimientos registrados
4. El usuario puede navegar a otros módulos desde el sidebar o cerrar sesión desde la navbar

---

## Flujos alternativos / excepciones

**Ocultar información de cuenta**
- Usuario hace click en el botón "Ocultar" de una cuenta
- El número de cuenta y saldo se ocultan
- El título de la cuenta permanece visible
- El estado se mantiene al navegar entre módulos *(a verificar)*

**Restablecer saldos**
- Usuario hace click en "Restablecer saldos"
- Los saldos de todas las cuentas vuelven a un valor inicial
- Los últimos movimientos se resetean *(a confirmar)*

---

## Riesgos detectados

- Es la puerta de entrada a toda la funcionalidad — si falla, el usuario queda bloqueado
- Muestra información sensible (saldos, números de cuenta) — debe tener restricciones de acceso adecuadas
- El estado de ocultar/mostrar información de cuentas podría no persistir consistentemente
- Los saldos deben coincidir con las operaciones realizadas en otros módulos — si hay inconsistencia, afecta la confianza del usuario

---

## Dudas / puntos a verificar

| # | Duda | Impacto |
|---|---|---|
| 1 | ¿El estado de "ocultar" en una cuenta persiste al cambiar de módulo y volver? | Define si hay caso de persistencia |
| 2 | ¿El botón "Restablecer saldos" también resetea los últimos movimientos? | Comprensión de la funcionalidad |
| 3 | ¿Los saldos mostrados se actualizan en tiempo real si se realiza una transferencia en otro módulo? | Comportamiento de actualización |
| 4 | ¿Hay un orden específico en los últimos movimientos (más reciente primero)? | Validación de orden |
| 5 | ¿Qué sucede si no hay movimientos recientes? ¿Se muestra un mensaje o una tabla vacía? | Comportamiento de error |

---

## Casos de prueba relacionados

*Se completará después de escribir los test cases*

---

## Bugs encontrados

*Se completará después de la ejecución*


