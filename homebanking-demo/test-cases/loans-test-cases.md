
# Test Cases – Préstamos

## Información general

**Elementos de la interfaz:**
- Panel de préstamos activos (monto, cuotas, fecha, total a pagar, botones "Pagar Total" y "Desistir")
- Formulario de solicitud (cuenta destino, monto, cuotas, botón Solicitar Préstamo)
- Modales de confirmación (Pagar Total y Desistir)

**Reglas de negocio consideradas:**
  - Monto mínimo: $1.000 — Monto máximo: $500.000
  - Cuotas disponibles: 6, 12, 18 y 24
  - Plazo de revocación (desistimiento): 10 días desde la creación, devuelve el monto original sin intereses
  - "Pagar Total" cancela el préstamo pagando el total; el dropdown de cuenta filtra por saldo suficiente
  - De las 3 cuentas del usuario, solo 2 son válidas como destino de un préstamo

---

# Casos Funcionales — Solicitud de Préstamo

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PREST-01 | Solicitud exitosa de un préstamo con datos válidos | Usuario logueado, cuenta destino válida | 1. Seleccionar cuenta destino.<br>2. Ingresar monto válido (ej. $50.000).<br>3. Seleccionar cantidad de cuotas (ej. 12).<br>4. Click en "Solicitar Préstamo". | Se muestra el mensaje de éxito y el préstamo aparece en el panel de préstamos activos. | Alta |
| PREST-02 | Dropdown de cuenta destino excluye la cuenta no válida | Formulario abierto | 1. Abrir el dropdown de "Cuenta destino".<br>2. Observar las opciones listadas. | Solo se muestran 2 de las 3 cuentas del usuario como destino válido; se confirma cuál queda excluida (ej. Tarjeta de Crédito). | Media |
| PREST-03 | Texto informativo "Info: X total, Y válidas" es consistente con las cuentas del usuario | Usuario con 3 cuentas asociadas | 1. Abrir el formulario de solicitud.<br>2. Observar el texto informativo debajo del dropdown. | El texto refleja correctamente la cantidad total de cuentas y cuántas son válidas como destino. | Baja |
| PREST-04 | Dropdown de cuotas muestra únicamente las opciones definidas | Formulario abierto | 1. Abrir el dropdown de "Cuotas". | Se listan únicamente 6, 12, 18 y 24 cuotas — sin valores adicionales ni campo libre. | Media |

---

# Casos de Validación de Monto

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PREST-05 | Rechazo con monto menor al mínimo | Formulario abierto | 1. Ingresar un monto menor a $1.000 (ej. $999).<br>2. Intentar continuar. | Se muestra validación de monto mínimo. No permite avanzar. | Alta |
| PREST-06 | Monto en el límite mínimo exacto ($1.000) | Formulario abierto | 1. Ingresar exactamente $1.000.<br>2. Completar el resto del formulario.<br>3. Solicitar el préstamo. | El sistema acepta el monto y crea el préstamo sin error. | Media |
| PREST-07 | Rechazo con monto mayor al máximo permitido | Formulario abierto | 1. Ingresar un monto mayor a $500.000 (ej. $500.001).<br>2. Intentar continuar. | Se muestra validación de monto máximo. No permite avanzar. | Alta |
| PREST-08 | Monto en el límite máximo exacto ($500.000) | Formulario abierto | 1. Ingresar exactamente $500.000.<br>2. Completar el resto del formulario.<br>3. Solicitar el préstamo. | El sistema acepta el monto y crea el préstamo sin error. | Media |
| PREST-09 | Monto vacío | Formulario abierto | 1. Dejar el campo Monto vacío.<br>2. Intentar continuar. | El sistema no permite avanzar; se espera validación de campo obligatorio. | Media |

---

# Casos de Visualización de Préstamos Activos

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PREST-10 | Visualización completa de los datos de un préstamo activo | Al menos un préstamo activo existente | 1. Observar el panel de préstamos activos. | Se muestran correctamente: monto, cuotas, fecha (días), y total a pagar. | Alta |

---

# Casos de "Pagar Total"

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PREST-11 | Cancelación exitosa de un préstamo mediante "Pagar Total" | Préstamo activo, al menos una cuenta con saldo suficiente | 1. Click en "Pagar Total" sobre un préstamo.<br>2. Seleccionar cuenta de pago en el dropdown.<br>3. Click en "Confirmar". | El préstamo se cancela exitosamente y desaparece (o se marca como pagado) del panel de préstamos activos. | Alta |
| PREST-12 | Dropdown de cuenta de pago solo muestra cuentas con saldo suficiente | Usuario con varias cuentas, solo una con saldo suficiente para el monto total | 1. Click en "Pagar Total" sobre un préstamo.<br>2. Abrir el dropdown de cuenta de pago. | Solo aparecen listadas las cuentas cuyo saldo cubre el monto total a pagar. | Media |
| PREST-13 | Rechazo cuando ninguna cuenta tiene saldo suficiente | Ninguna cuenta del usuario tiene saldo suficiente para cubrir el préstamo | 1. Click en "Pagar Total" sobre un préstamo.<br>2. Observar el modal / intentar confirmar. | Se muestra: "No tienes cuentas con saldo suficiente para cancelar este préstamo". No permite procesar el pago. | Alta |
| PREST-14 | Monto total a pagar coincide con el mostrado en el panel | Préstamo activo con cuotas restantes | 1. Registrar el "total a pagar" mostrado en la card del préstamo.<br>2. Click en "Pagar Total".<br>3. Comparar con el monto mostrado en el modal. | El monto del modal coincide exactamente con el total a pagar mostrado en el panel. | Media |
| PREST-15 | El monto de "Pagar Total" incluye o no intereses restantes *(pendiente de confirmación)* | Préstamo activo con varias cuotas restantes | 1. Calcular manualmente el capital adeudado restante.<br>2. Comparar con el monto mostrado al hacer "Pagar Total". | **No confirmado si el monto incluye intereses de cuotas futuras.** Documentar el comportamiento real como asunción de diseño. | Alta |
| PREST-16 | Cancelar desde el modal de "Pagar Total" no ejecuta la acción | Modal de "Pagar Total" abierto | 1. Click en "Pagar Total" (abre el modal).<br>2. Click en el botón "Cancelar" del modal (no en "Confirmar"). | El modal se cierra sin procesar el pago. El préstamo sigue activo. | Media |

---

# Casos de "Desistir" (Plazo de Revocación)

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PREST-17 | Botón "Desistir" visible dentro del plazo de 10 días | Préstamo creado hace menos de 10 días | 1. Observar la card del préstamo activo. | El botón "Desistir" está visible junto a "Pagar Total". | Alta |
| PREST-18 | Desistimiento exitoso dentro del plazo | Préstamo dentro del plazo de revocación, cuenta con saldo suficiente | 1. Click en "Desistir".<br>2. Verificar el texto legal y el monto a devolver en el modal.<br>3. Seleccionar cuenta a debitar.<br>4. Click en "Confirmar". | El préstamo queda marcado como pagado y desaparece del panel de préstamos activos. | Alta |
| PREST-19 | Monto a devolver en "Desistir" es igual al monto original recibido | Préstamo dentro del plazo de revocación | 1. Click en "Desistir".<br>2. Comparar el monto a devolver mostrado en el modal con el monto original solicitado. | El monto a devolver coincide exactamente con el monto original del préstamo, sin intereses. | Alta |
| PREST-20 | Comportamiento del botón "Desistir" pasado el plazo de 10 días *(pendiente de confirmación)* | Préstamo creado hace más de 10 días | 1. Observar la card de un préstamo fuera del plazo de revocación. | **No confirmado si el botón desaparece o se deshabilita.** Documentar el comportamiento real como asunción de diseño. | Media |
| PREST-21 | Cancelar desde el modal de "Desistir" no ejecuta la acción | Modal de "Desistir" abierto | 1. Click en "Desistir" (abre el modal).<br>2. Click en el botón "Cancelar" del modal (no en "Confirmar"). | El modal se cierra sin procesar el desistimiento. El préstamo sigue activo. | Media |

---

# Casos Generales

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| PREST-22 | Límite de préstamos activos simultáneos *(pendiente de confirmación)* | Usuario con al menos un préstamo activo | 1. Solicitar un segundo préstamo mientras el primero sigue activo. | **No confirmado si existe un límite de cantidad.** Documentar comportamiento real como asunción de diseño. | Baja |

---

**Total de Test Cases: 22**
