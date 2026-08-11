# Test Cases – Transferencias

## Información general

- **Elementos de la interfaz:**
- Selector de tipo (Entre mis cuentas / A terceros)
- Cuenta origen
- Cuenta destino
- Alias/CBU destino
- Monto
- Descripción (opcional)
- Botón Transferir
- Modal de confirmación (Confirmar / Cancelar)  
- **Reglas de negocio consideradas:**
  - Monto mínimo: $1 — Monto máximo: $50.000 por transferencia
  - Límite diario: $100.000 (persiste entre sesiones)
  - No se puede transferir de una cuenta a sí misma
  - Alias debe cumplir formato específico (ej. `DEMO.HOLA.COSO`)
  - CBU debe ser un número de 22 dígitos *(comportamiento inconsistente detectado)*
  - Descripción es un campo opcional
  - Modal de confirmación muestra resumen antes de ejecutar la transferencia

---

# Casos Funcionales — Entre mis cuentas

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TRANS-01 | Transferencia exitosa entre cuentas propias | Usuario logueado, cuenta origen con saldo suficiente | 1. Seleccionar "Entre mis cuentas".<br>2. Elegir cuenta origen y destino distintas.<br>3. Ingresar monto válido (ej. $500).<br>4. Click en "Transferir".<br>5. Confirmar en el modal. | Se muestra "Transferencia realizada exitosamente". | Alta |
| TRANS-02 | Disminución del saldo en cuenta origen | Transferencia entre cuentas propias procesada | 1. Registrar saldo de cuenta origen antes de transferir.<br>2. Realizar transferencia válida.<br>3. Verificar saldo de cuenta origen luego de confirmar. | El saldo de origen disminuye exactamente en el monto transferido. | Alta |
| TRANS-03 | Aumento del saldo en cuenta destino | Transferencia entre cuentas propias procesada | 1. Registrar saldo de cuenta destino antes de transferir.<br>2. Realizar transferencia válida.<br>3. Verificar saldo de cuenta destino luego de confirmar. | El saldo de destino aumenta exactamente en el monto transferido. | Alta |
| TRANS-04 | Modal de confirmación muestra datos correctos | Formulario de transferencia completo con datos válidos | 1. Completar cuenta origen, destino y monto.<br>2. Click en "Transferir". | El modal muestra cuenta origen, cuenta destino y monto exactamente como fueron ingresados, antes de confirmar. | Alta |

---

# Casos Funcionales — A terceros

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TRANS-05 | Transferencia exitosa a tercero con Alias válido | Alias de tercero existente y con formato válido (ej. DEMO.HOLA.COSO) | 1. Seleccionar "A terceros".<br>2. Ingresar Alias válido.<br>3. Ingresar monto válido.<br>4. Confirmar. | Se procesa la transferencia y muestra mensaje de éxito. | Alta |
| TRANS-06 | Transferencia exitosa a tercero con CBU válido | CBU de 22 dígitos válido | 1. Seleccionar "A terceros".<br>2. Ingresar CBU de 22 dígitos.<br>3. Ingresar monto válido.<br>4. Confirmar. | Se procesa la transferencia y muestra mensaje de éxito. | Alta |

---

# Casos de Validación de Monto

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TRANS-07 | Rechazo con monto vacío | Formulario abierto | 1. Dejar campo Monto vacío.<br>2. Click en "Transferir". | Muestra: "El valor debe ser superior o igual a 0.01". No permite avanzar. | Alta |
| TRANS-08 | Rechazo con monto igual a cero | Formulario abierto | 1. Ingresar $0 en Monto.<br>2. Click en "Transferir". | Muestra el mismo mensaje de validación que monto vacío. No permite avanzar. | Alta |
| TRANS-09 | Monto de $0.01 pasa validación inicial pero falla en confirmación *(bug conocido)* | Formulario abierto | 1. Ingresar $0.01 en Monto.<br>2. Click en "Transferir" (avanza al modal).<br>3. Click en "Confirmar". | **Comportamiento actual:** el modal se abre igual, pero al confirmar muestra "El monto mínimo para transferir es $1" y no procesa. Documentar como inconsistencia UX: la validación debería bloquear antes del modal, no después. | Alta |
| TRANS-10 | Rechazo con monto mayor al máximo permitido | Formulario abierto | 1. Ingresar un monto mayor a $50.000 (ej. $50.001).<br>2. Click en "Transferir". | Muestra: "El monto máximo por transferencia es $50.000". No permite avanzar al modal. | Alta |
| TRANS-11 | Monto en el límite mínimo exacto ($1) | Formulario abierto, saldo suficiente | 1. Ingresar exactamente $1.<br>2. Click en "Transferir".<br>3. Confirmar. | El sistema acepta el monto y procesa la transferencia sin error. | Media |
| TRANS-12 | Monto en el límite máximo exacto ($50.000) | Formulario abierto, saldo suficiente | 1. Ingresar exactamente $50.000.<br>2. Click en "Transferir".<br>3. Confirmar. | El sistema acepta el monto y procesa la transferencia sin error. | Media |
| TRANS-13 | Monto con decimales no válidos | Formulario abierto | 1. Ingresar $50.001 o un valor con más de 2 decimales.<br>2. Click en "Transferir". | Muestra: "Introduce un valor válido. Los dos valores válidos más aproximados son 50 y 50.01". No permite avanzar. | Media |
| TRANS-14 | Monto negativo | Formulario abierto | 1. Intentar ingresar un valor negativo (ej. -100) en Monto.<br>2. Click en "Transferir". | El campo rechaza el valor o muestra validación equivalente a monto inválido. No permite avanzar. | Media |
| TRANS-15 | Monto superior al saldo disponible *(pendiente de confirmación)* | Cuenta origen con saldo menor a $50.000 (ej. saldo de $200) | 1. Ingresar un monto mayor al saldo disponible pero dentro del límite de $50.000 (ej. $300).<br>2. Click en "Transferir".<br>3. Confirmar. | **No verificado en la exploración.** Se espera un mensaje de "saldo insuficiente" — a confirmar comportamiento real y documentar como bug si el sistema no lo valida. | Alta |

---

# Casos de Validación de Cuentas y Destino

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TRANS-16 | Rechazo al transferir a la misma cuenta | Formulario en modo "Entre mis cuentas" | 1. Seleccionar la misma cuenta como origen y destino.<br>2. Completar monto válido.<br>3. Click en "Transferir". | Muestra: "La cuenta origen y destino no pueden ser la misma". No permite avanzar. | Alta |
| TRANS-17 | Rechazo de Alias con formato inválido | Formulario en modo "A terceros" | 1. Ingresar un alias sin el formato esperado (ej. "pepe").<br>2. Completar monto válido.<br>3. Click en "Transferir". | Muestra: "CBU o Alias de destino no válido". No permite avanzar. | Alta |
| TRANS-18 | Rechazo de CBU con menos de 22 dígitos | Formulario en modo "A terceros" | 1. Ingresar un CBU con menos de 22 dígitos (ej. 15 dígitos).<br>2. Completar monto válido.<br>3. Click en "Transferir". | Se espera: "CBU o Alias de destino no válido". No permite avanzar. | Alta |
| TRANS-19 | CBU incompleto aceptado inconsistentemente *(bug conocido)* | Formulario en modo "A terceros" | 1. Ingresar un CBU de 19 dígitos (variante detectada en exploración).<br>2. Completar monto válido.<br>3. Click en "Transferir". | **Comportamiento actual:** el sistema acepta el CBU incompleto en ciertos casos, sin mostrar error de formato. Documentar como bug — validación de longitud de CBU inconsistente. | Alta |
| TRANS-20 | CBU con caracteres no numéricos | Formulario en modo "A terceros" | 1. Ingresar un CBU con letras o símbolos (ej. "12345ABC...").<br>2. Completar monto válido.<br>3. Click en "Transferir". | Muestra validación de formato inválido. No permite avanzar. | Media |

---

# Casos de Límite Diario

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TRANS-21 | Bloqueo al superar el límite diario | Usuario sin transferencias previas en el día | 1. Realizar transferencias válidas que en conjunto superen $100.000 (ej. dos de $50.000).<br>2. Intentar una transferencia adicional, aunque sea de bajo monto. | Muestra: "Has excedido el límite diario de transferencias ($100.000)". No permite procesar. | Alta |
| TRANS-22 | Transferencia justo en el límite diario ($100.000 exactos) | Usuario sin transferencias previas en el día | 1. Realizar transferencias válidas que sumen exactamente $100.000. | El sistema permite la última transferencia que completa el límite, sin bloquear antes de tiempo. | Media |
| TRANS-23 | Persistencia del límite diario tras logout/login | Usuario alcanzó el límite diario | 1. Alcanzar el límite diario de $100.000.<br>2. Cerrar sesión.<br>3. Iniciar sesión nuevamente.<br>4. Intentar una nueva transferencia. | El sistema sigue bloqueando transferencias, el límite no se resetea por cerrar sesión. | Alta |
| TRANS-24 | Reseteo del límite diario *(pendiente de confirmación)* | Usuario alcanzó el límite diario el día anterior | 1. Alcanzar el límite diario.<br>2. Esperar a que pase la medianoche o 24hs desde la primera transferencia (según se defina).<br>3. Intentar una nueva transferencia. | **Comportamiento no confirmado.** Documentar como asunción de diseño una vez definido si el reseteo es a medianoche o 24hs rotativas. | Media |

---

# Casos de Modal de Confirmación

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TRANS-25 | Cancelar transferencia desde el modal | Formulario completo con datos válidos, modal abierto | 1. Completar formulario con datos válidos.<br>2. Click en "Transferir" (abre modal).<br>3. Click en "Cancelar". | El modal se cierra sin procesar. No se modifican saldos ni el contador del límite diario. Vuelve al formulario. | Alta |

---

# Casos de UI / UX

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TRANS-26 | Estado del dropdown tras transferencia a terceros *(bug conocido)* | Ninguna | 1. Realizar una transferencia exitosa "A terceros".<br>2. Observar el estado del dropdown "Tipo de transferencia" al volver al formulario. | **Comportamiento actual:** el dropdown vuelve a "Entre mis cuentas" en lugar de mantener "A terceros". Documentar como bug de UX — puede confundir al usuario en transferencias sucesivas al mismo tercero. | Media |
| TRANS-27 | Límite de caracteres en Descripción *(pendiente de confirmación)* | Formulario abierto | 1. Ingresar un texto muy largo en el campo Descripción (ej. 500 caracteres).<br>2. Completar el resto del formulario.<br>3. Click en "Transferir". | **No definido.** A confirmar si el campo trunca, rechaza o acepta sin límite — documentar como asunción de diseño una vez decidido. | Baja |
| TRANS-28 | Transferencia sin completar Descripción (campo opcional) | Formulario abierto | 1. Completar todos los campos obligatorios.<br>2. Dejar Descripción vacía.<br>3. Click en "Transferir".<br>4. Confirmar. | La transferencia se procesa correctamente sin exigir la Descripción. | Baja |

---

# Casos Generales / No Funcionales

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TRANS-29 | Falla de conexión durante transferencia confirmada *(pendiente — caso de error de red)* | Transferencia lista para confirmar en el modal | 1. Simular corte de conexión justo después de hacer click en "Confirmar".<br>2. Restablecer conexión y verificar estado de la cuenta. | **No verificado.** Se espera que el sistema no duplique la transferencia ni descuente saldo sin confirmar el resultado — a definir comportamiento esperado con el equipo de desarrollo. | Alta |

---

**Total de Test Cases: 29**
