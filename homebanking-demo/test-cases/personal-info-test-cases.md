# Test Cases – Mis Datos

## Información general

- **Elementos de la interfaz:** Sección de Información Personal (Nombre, DNI, Email, Teléfono, Dirección), sección de Mis Cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito con número, CBU y saldo), sección de Tarjetas (Visa Débito, Mastercard Débito, Visa Crédito con número y monto).
- **Reglas de negocio consideradas:**
  - Todos los datos mostrados son estrictamente de **solo lectura**.
  - No existen funcionalidades de modificación, actualización o eliminación en este módulo.
  - Coherencia estricta de datos financieros con el resto de la aplicación (Dashboard).

---

# Casos Funcionales — Visualización y Restricciones

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-01 | Visualización completa de los datos de Información Personal | Sesión activa en la homebanking demo | 1. Navegar al módulo "Mis Datos" desde el menú lateral.<br>2. Observar la sección de Información Personal. | Se visualizan correctamente y sin errores de formato: Nombre completo, DNI, Email, Teléfono y Dirección. | Alta |
| DATOS-02 | Verificación de que los campos personales no son editables | Sesión activa en el módulo "Mis Datos" | 1. Intentar hacer clic o editar los campos de email, teléfono o dirección.<br>2. Buscar botones de "Editar" o "Guardar". | Los campos son de solo lectura, no permiten edición de texto y no existen botones de modificación en la interfaz. | Alta |
| DATOS-03 | Visualización de la sección "Mis cuentas" | Sesión activa en el módulo "Mis Datos" | 1. Desplazarse a la sección "Mis cuentas".<br>2. Revisar los registros de Cuenta Corriente, Caja de Ahorro y Tarjeta de Crédito. | Se muestran los números de cuenta, el CBU correspondiente y el monto/saldo actual de cada una. | Alta |
| DATOS-04 | Validación de consistencia de cuentas con el Dashboard *(Bug/Inconsistencia)* | Sesión activa | 1. Registrar los números de cuenta mostrados en el Dashboard principal.<br>2. Navegar al módulo "Mis Datos" y comparar los números de cuenta listados. | **(Defecto esperado en demo):** Los números de cuenta en "Mis Datos" deben coincidir exactamente con los del Dashboard. Si difieren, se registra un bug de inconsistencia de datos. | Media |
| DATOS-05 | Visualización de la sección "Tarjetas" asociadas | Sesión activa en el módulo "Mis Datos" | 1. Desplazarse a la sección de tarjetas (Visa Débito, Mastercard Débito, Visa Crédito).<br>2. Inspeccionar los números y montos mostrados. | Se visualizan las tarjetas detalladas. *(Nota: Verificar si la ausencia de montos en débitos y la disparidad de números responde a un comportamiento mock no deseado).* | Media |
| DATOS-06 | Ausencia de controles de modificación o eliminación de tarjetas | Sesión activa en el módulo "Mis Datos" | 1. Inspeccionar visualmente las cards de cuentas y tarjetas.<br>2. Posicionar el cursor sobre las tarjetas (hover) o buscar iconos de acción. | No aparecen opciones de copiar, eliminar, editar o dar de baja ningún elemento dentro de este módulo. | Media |

---

**Total de Test Cases: 6**
