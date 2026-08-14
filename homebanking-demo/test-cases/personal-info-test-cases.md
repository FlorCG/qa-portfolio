# Test Cases – Mis Datos

## Información general

- **Elementos de la interfaz:** Sección "Información Personal" (nombre, DNI, email, teléfono, dirección), sección "Mis Cuentas" (Cuenta Corriente, Caja de Ahorro, Tarjeta de Crédito — número, CBU, monto), sección de Tarjetas (Visa Débito, Mastercard Débito, Visa Crédito — número, monto)
- **Reglas de negocio consideradas:**
  - Todos los datos son de solo lectura (no editables ni eliminables)
- **Hallazgo relevante:** se detectó una inconsistencia entre los números de cuenta mostrados acá y los mostrados en el Dashboard — ver `BUG-DATOS-01` en el análisis funcional

---

# Casos Funcionales — Información Personal

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-01 | Visualización correcta de la información personal | Usuario logueado | 1. Ingresar al módulo "Mis Datos".<br>2. Observar la sección "Información Personal". | Se muestran correctamente: nombre completo, DNI, email, teléfono y dirección del usuario. | Alta |

---

# Casos Funcionales — Mis Cuentas

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-02 | Visualización de los datos de las 3 cuentas | Usuario logueado | 1. Observar la sección "Mis Cuentas". | Se muestran las 3 cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito), cada una con número, CBU y monto. | Alta |
| DATOS-03 | Consistencia del número de Cuenta Corriente entre Mis Datos y Dashboard *(bug detectado)* | Usuario logueado, con acceso a ambas pantallas | 1. Anotar el número de Cuenta Corriente mostrado en el Dashboard.<br>2. Ir a "Mis Datos" y comparar el número de Cuenta Corriente mostrado allí. | **Comportamiento actual:** los números no coinciden. Se espera que ambos módulos muestren el mismo número de cuenta — documentar como bug de inconsistencia de datos. | Alta |
| DATOS-04 | Consistencia del número de Caja de Ahorro entre Mis Datos y Dashboard *(bug detectado)* | Usuario logueado, con acceso a ambas pantallas | 1. Anotar el número de Caja de Ahorro mostrado en el Dashboard.<br>2. Ir a "Mis Datos" y comparar el número de Caja de Ahorro mostrado allí. | **Comportamiento actual:** los números no coinciden. Documentar como bug de inconsistencia de datos, igual que DATOS-03. | Alta |
| DATOS-05 | El CBU mostrado corresponde a cada cuenta correctamente | Usuario logueado | 1. Observar el CBU listado junto a cada cuenta en "Mis Cuentas". | Cada cuenta muestra un CBU asociado, con formato numérico consistente (22 dígitos, según la regla vista en Transferencias). | Media |

---

# Casos Funcionales — Tarjetas

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-06 | Visualización de las 3 tarjetas listadas | Usuario logueado | 1. Observar la sección de Tarjetas en "Mis Datos". | Se listan 3 tarjetas: Visa Débito, Mastercard Débito y Visa Crédito. | Media |
| DATOS-07 | "Visa Crédito" coincide con la Tarjeta de Crédito del Dashboard | Usuario logueado | 1. Anotar el número y monto de "Tarjeta de Crédito" en el Dashboard.<br>2. Comparar con "Visa Crédito" en Mis Datos. | Los datos de "Visa Crédito" coinciden con los de la Tarjeta de Crédito mostrada en el Dashboard. | Media |
| DATOS-08 | Relación de "Visa Débito" y "Mastercard Débito" con productos reales *(pendiente de confirmación)* | Usuario logueado | 1. Observar "Visa Débito" y "Mastercard Débito" en la sección de Tarjetas.<br>2. Buscar si existe algún producto relacionado en Dashboard, Mis Cuentas o Tarjetas Virtuales. | **No confirmado a qué producto real corresponden estas dos tarjetas**, dado que no tienen monto asociado y sus números no coinciden con ningún otro dato visible. Documentar como hallazgo a definir con el equipo de desarrollo. | Media |
| DATOS-09 | "Visa Débito" y "Mastercard Débito" no muestran monto | Usuario logueado | 1. Observar las cards de "Visa Débito" y "Mastercard Débito". | Ambas tarjetas se muestran sin un monto asociado, a diferencia de "Visa Crédito" que sí lo tiene. | Baja |

---

# Casos de Solo Lectura

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-10 | No es posible modificar la información personal | Usuario logueado, en "Mis Datos" | 1. Intentar hacer click o interactuar con los campos de "Información Personal" para editarlos. | Ningún campo permite edición; no existen botones de "Editar" ni "Guardar" visibles. | Media |
| DATOS-11 | No es posible eliminar cuentas ni tarjetas desde este módulo | Usuario logueado, en "Mis Datos" | 1. Buscar alguna opción de eliminación en las cards de cuentas o tarjetas. | No existe ninguna acción de eliminación disponible en esta pantalla. | Baja |

---

**Total de Test Cases: 11**



