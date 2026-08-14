# Test Cases – Mis Datos

## Información general

- **Elementos de la interfaz:** Sección de Información Personal (Nombre, DNI, Email, Teléfono, Dirección), sección de Mis Cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito con número, CBU y saldo), sección de Tarjetas (Visa Débito, Mastercard Débito, Visa Crédito con número y monto).
- **Reglas de negocio consideradas:**
  - Todos los datos mostrados son estrictamente de **solo lectura**.
  - No existen funcionalidades de modificación, actualización o eliminación en este módulo.
  - Coherencia estricta de datos financieros con el resto de la aplicación (Dashboard).

---

# Casos Funcionales

## ESC-01 — Información Personal

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-01 | Visualización completa de Información Personal | Sesión activa en la homebanking demo | 1. Navegar al módulo "Mis Datos".<br>2. Observar la sección "Información Personal". | Se visualizan correctamente Nombre completo, DNI, Email, Teléfono y Dirección, sin valores vacíos inesperados y con formato válido. | Alta |
| DATOS-02 | Verificación de que los datos personales no son editables | Sesión activa en el módulo "Mis Datos" | 1. Intentar interactuar con los campos de Información Personal.<br>2. Buscar botones o iconos de edición. | Los datos son de solo lectura y no existe ninguna opción para modificarlos o eliminarlos. | Alta |

---

## ESC-02 — Mis Cuentas

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-03 | Visualización y formato de las cuentas del usuario | Sesión activa en el módulo "Mis Datos" | 1. Navegar a "Mis Cuentas".<br>2. Observar Cuenta Corriente, Caja de Ahorro y Tarjeta de Crédito.<br>3. Verificar números, CBU y montos. | Se muestran correctamente las tres cuentas con sus datos correspondientes. Los CBU poseen 22 dígitos numéricos y los montos presentan formato de moneda válido. | Alta |
| DATOS-04 | Consistencia de cuentas entre Dashboard y Mis Datos | Sesión activa | 1. Registrar los números de cuenta mostrados en el Dashboard.<br>2. Navegar a "Mis Datos".<br>3. Comparar los números de Cuenta Corriente, Caja de Ahorro y Tarjeta de Crédito. | Los datos deberían coincidir entre ambos módulos. **Resultado observado:** Se detectan diferencias en los números de cuenta. Registrar como posible defecto de consistencia de datos. | Alta |
| DATOS-05 | Verificación de que las cuentas no son editables ni eliminables | Sesión activa en "Mis Datos" | 1. Intentar interactuar con los datos de las cuentas.<br>2. Buscar controles de edición o eliminación. | Los datos son de solo lectura y no existen acciones para modificar o eliminar las cuentas. | Media |

---

## ESC-03 — Mis Tarjetas

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-06 | Visualización de tarjetas asociadas | Sesión activa en el módulo "Mis Datos" | 1. Navegar a la sección "Mis Tarjetas".<br>2. Observar Visa Débito, Mastercard Débito y Visa Crédito.<br>3. Verificar números y montos mostrados. | Las tres tarjetas se visualizan correctamente con sus datos correspondientes y números en formato válido. | Alta |
| DATOS-07 | Verificación de ausencia de monto en tarjetas de débito | Sesión activa en el módulo "Mis Datos" | 1. Observar las cards de Visa Débito y Mastercard Débito.<br>2. Comparar con la información mostrada para Visa Crédito. | **Hallazgo:** Las tarjetas de débito no muestran monto. Se debe confirmar con Producto/Negocio si se trata del comportamiento esperado o de un defecto. | Media |
| DATOS-08 | Consistencia de Visa Crédito entre Dashboard y Mis Datos | Sesión activa | 1. Registrar número y monto de Visa Crédito en el Dashboard.<br>2. Navegar a "Mis Datos".<br>3. Comparar con los datos de Visa Crédito. | Los datos de Visa Crédito deberían coincidir entre ambos módulos. **Resultado observado:** Los datos coinciden correctamente. | Alta |

---

## ESC-04 — Navegación y UI

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-09 | Acceso al módulo "Mis Datos" desde el menú principal | Usuario autenticado | 1. Ingresar al homebanking.<br>2. Seleccionar "Mis Datos" desde el menú lateral. | Se accede correctamente al módulo y se cargan sus diferentes secciones sin errores visibles. | Alta |
| DATOS-10 | Verificación de navegación y persistencia de datos | Sesión activa en "Mis Datos" | 1. Navegar desde "Mis Datos" hacia otra sección.<br>2. Regresar a "Mis Datos".<br>3. Comparar la información visualizada antes y después de navegar. | El módulo vuelve a cargar correctamente y los datos se mantienen consistentes. | Media |
| DATOS-11 | Visualización responsive del módulo | Sesión activa en "Mis Datos" | 1. Visualizar el módulo en resolución desktop.<br>2. Repetir utilizando un viewport mobile.<br>3. Recorrer todas las secciones. | La interfaz se adapta correctamente a ambas resoluciones, sin elementos superpuestos, textos cortados ni overflow horizontal. | Media |

---

**Total de Test Cases: 11**


