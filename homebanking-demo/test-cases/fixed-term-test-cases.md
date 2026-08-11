# Test Cases – Plazos Fijos

## Información general

- **Elementos de la interfaz:** Panel de Plazos Fijos activos (monto, TNA, plazo, interés estimado, fecha inicio/vencimiento, total al vencimiento, botón Cancelar), formulario de creación (cuenta origen, monto, plazo, botón Crear Plazo Fijo), modales de confirmación (creación y cancelación)
- **Reglas de negocio consideradas:**
  - Monto mínimo: $1.000
  - Plazos disponibles: 30, 60, 90, 180 y 360 días
  - Requiere modal de confirmación tanto para crear como para cancelar
  - Al crear, el nuevo Plazo Fijo se agrega al final de la lista de activos
  - Al cancelar, se elimina el Plazo Fijo y se acredita el monto a la cuenta origen
  - Si el monto supera el saldo disponible, se rechaza con "Saldo insuficiente en la cuenta origen"

---

# Casos Funcionales — Creación

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PF-01 | Creación exitosa de un Plazo Fijo con datos válidos | Usuario logueado, cuenta origen con saldo suficiente | 1. Seleccionar cuenta origen.<br>2. Ingresar monto válido (ej. $5.000).<br>3. Seleccionar plazo (ej. 90 días).<br>4. Click en "Crear Plazo Fijo".<br>5. Confirmar en el modal. | Se muestra el toast "Plazo fijo creado exitosamente" y el nuevo plazo aparece en el panel de activos. | Alta |
| PF-02 | Cálculo correcto de interés estimado, total al vencimiento y fecha de vencimiento | Formulario con monto y plazo completos | 1. Ingresar monto válido.<br>2. Seleccionar un plazo.<br>3. Observar los campos calculados (interés estimado, total al vencimiento, fecha de vencimiento) antes de crear. | Los valores calculados son matemáticamente correctos según la TNA aplicada y coherentes con el plazo elegido. | Alta |
| PF-03 | Modal de confirmación muestra datos correctos antes de crear | Formulario completo con datos válidos | 1. Completar cuenta origen, monto y plazo.<br>2. Click en "Crear Plazo Fijo". | El modal muestra cuenta origen, monto, plazo, TNA, interés estimado, total al vencimiento y fecha de vencimiento, coincidiendo exactamente con lo ingresado/calculado en el formulario. | Alta |

---

# Casos de Validación de Monto

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PF-04 | Rechazo con monto menor al mínimo | Formulario abierto | 1. Ingresar un monto menor a $1.000 (ej. $999).<br>2. Intentar continuar. | Muestra: "El valor debe ser superior o igual a 1000". No permite avanzar. | Alta |
| PF-05 | Monto en el límite mínimo exacto ($1.000) | Formulario abierto, saldo suficiente | 1. Ingresar exactamente $1.000.<br>2. Seleccionar un plazo.<br>3. Click en "Crear Plazo Fijo".<br>4. Confirmar. | El sistema acepta el monto y crea el Plazo Fijo sin error. | Media |
| PF-06 | Rechazo por saldo insuficiente en la cuenta origen | Cuenta origen con saldo menor al monto ingresado | 1. Ingresar un monto mayor al saldo disponible de la cuenta seleccionada.<br>2. Intentar continuar. | Muestra: "Saldo insuficiente en la cuenta origen". No permite crear. | Alta |
| PF-07 | Monto con decimales *(pendiente de confirmación)* | Formulario abierto | 1. Ingresar un monto con decimales (ej. $1000.50).<br>2. Intentar continuar. | **No confirmado.** Documentar comportamiento real (acepta, rechaza o redondea) como asunción de diseño. | Media |
| PF-08 | Monto vacío | Formulario abierto | 1. Dejar el campo Monto vacío.<br>2. Intentar continuar. | El sistema no permite avanzar; se espera validación de campo obligatorio o el mismo mensaje de monto mínimo. | Media |
| PF-09 | Monto negativo | Formulario abierto | 1. Intentar ingresar un valor negativo en Monto. | El campo rechaza el valor o se comporta como monto inválido. No permite avanzar. | Baja |

---

# Casos de Plazo

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PF-10 | Dropdown de plazo muestra únicamente las opciones definidas | Formulario abierto | 1. Abrir el dropdown de Plazo. | Se listan únicamente las opciones 30, 60, 90, 180 y 360 días — sin valores adicionales ni campo de texto libre. | Media |
| PF-11 | Creación de Plazo Fijo a 30 días | Monto válido ingresado | 1. Seleccionar plazo de 30 días.<br>2. Completar el resto del formulario.<br>3. Crear y confirmar. | El Plazo Fijo se crea con fecha de vencimiento a 30 días desde la fecha de inicio, y el interés/total corresponden a ese plazo. | Media |
| PF-12 | Creación de Plazo Fijo a 360 días | Monto válido ingresado | 1. Seleccionar plazo de 360 días.<br>2. Completar el resto del formulario.<br>3. Crear y confirmar. | El Plazo Fijo se crea con fecha de vencimiento a 360 días desde la fecha de inicio, y el interés/total corresponden a ese plazo. | Media |
| PF-13 | Variación de TNA/interés según el plazo elegido *(pendiente de confirmación)* | Mismo monto, distintos plazos | 1. Ingresar el mismo monto con plazo de 30 días y anotar la TNA/interés mostrados.<br>2. Repetir con plazo de 360 días. | **No confirmado si la TNA es fija o variable según plazo.** Documentar el comportamiento real como asunción de diseño. | Media |

---

# Casos de Visualización de Plazos Fijos Activos

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PF-14 | Visualización completa de los datos de un Plazo Fijo activo | Al menos un Plazo Fijo activo existente | 1. Observar el panel de Plazos Fijos activos. | Se muestran correctamente: monto, TNA, plazo en días, interés estimado, fecha de inicio, fecha de vencimiento y total al vencimiento. | Alta |
| PF-15 | Orden de aparición de nuevos Plazos Fijos | Ya existe al menos un Plazo Fijo activo | 1. Crear un nuevo Plazo Fijo.<br>2. Observar su posición en la lista. | El nuevo Plazo Fijo aparece al final de la lista, debajo de los ya existentes. | Baja |

---

# Casos de Cancelación

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PF-16 | Cancelación exitosa de un Plazo Fijo activo | Al menos un Plazo Fijo activo existente | 1. Click en "Cancelar" sobre un Plazo Fijo.<br>2. Confirmar en el modal. | Se muestra el toast "Plazo fijo cancelado exitosamente. El dinero se acreditó en tu cuenta". | Alta |
| PF-17 | Monto a reintegrar al cancelar *(pendiente de confirmación)* | Plazo Fijo activo con tiempo transcurrido desde su creación | 1. Cancelar un Plazo Fijo antes de su vencimiento.<br>2. Verificar el monto acreditado en la cuenta. | **No confirmado si incluye interés proporcional generado o solo el capital invertido.** Documentar como asunción de diseño una vez definido. | Alta |
| PF-18 | El Plazo Fijo se elimina de la lista tras cancelación | Plazo Fijo activo cancelado exitosamente | 1. Cancelar un Plazo Fijo.<br>2. Verificar el panel de Plazos Fijos activos. | El Plazo Fijo cancelado ya no aparece en la lista. | Alta |
| PF-19 | El dinero cancelado se acredita en la cuenta origen | Plazo Fijo activo cancelado exitosamente | 1. Registrar el saldo de la cuenta origen antes de cancelar.<br>2. Cancelar el Plazo Fijo.<br>3. Verificar el saldo luego de la cancelación. | El saldo de la cuenta aumenta según el monto a reintegrar mostrado en el modal. | Alta |
| PF-20 | Cancelar desde el modal de cancelación no ejecuta la acción | Modal de cancelación abierto | 1. Click en "Cancelar" sobre un Plazo Fijo (abre el modal).<br>2. Click en el botón "Cancelar" del modal (no en "Confirmar"). | El modal se cierra sin cancelar el Plazo Fijo. El plazo sigue activo en la lista. | Media |

---

# Casos del Modal de Creación

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PF-21 | Cancelar la creación desde el modal no genera el Plazo Fijo | Formulario completo, modal de creación abierto | 1. Completar el formulario con datos válidos.<br>2. Click en "Crear Plazo Fijo" (abre el modal).<br>3. Click en el botón "Cancelar" del modal (no en "Confirmar"). | El modal se cierra sin crear el Plazo Fijo. No se agrega ningún elemento nuevo al panel de activos. | Media |

---

# Casos Generales

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PF-22 | Límite de Plazos Fijos simultáneos por cuenta *(pendiente de confirmación)* | Cuenta con varios Plazos Fijos ya creados | 1. Crear múltiples Plazos Fijos consecutivos desde la misma cuenta. | **No confirmado si existe un límite de cantidad.** Documentar comportamiento real como asunción de diseño. | Baja |
| PF-23 | Toast de éxito se muestra al crear un Plazo Fijo | Formulario válido completo | 1. Crear un Plazo Fijo válido y confirmar. | El toast "Plazo fijo creado exitosamente" se muestra correctamente y desaparece tras unos segundos. | Baja |
| PF-24 | Toast de éxito se muestra al cancelar un Plazo Fijo | Plazo Fijo activo existente | 1. Cancelar un Plazo Fijo y confirmar. | El toast "Plazo fijo cancelado exitosamente. El dinero se acreditó en tu cuenta" se muestra correctamente y desaparece tras unos segundos. | Baja |

---

**Total de Test Cases: 24**
