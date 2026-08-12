
# Test Cases – Pago de Servicios

## Información general

**Elementos de la interfaz:**

- Formulario de Pago de Servicios (servicio, monto a pagar, cuenta a debitar, botón "Pagar Servicio")
- Dropdown de selección de servicio
- Dropdown de cuenta a debitar
- Campo de monto a pagar
- Mensajes de validación y confirmación

**Reglas de negocio consideradas:**

- Requiere seleccionar un servicio.
- Requiere ingresar un monto a pagar.
- Requiere seleccionar una cuenta a debitar.
- La cuenta seleccionada debe disponer de saldo suficiente para realizar el pago.
- El importe debitado debe corresponder al monto ingresado.
- Un pago exitoso debe registrarse como movimiento en la cuenta utilizada.
- La Tarjeta de Crédito no debería utilizarse como cuenta de débito directo *(pendiente de confirmación)*.
- No se encuentran documentados actualmente un monto mínimo ni un monto máximo para el pago.
- No se encuentra confirmado si el sistema requiere un modal de confirmación antes de ejecutar el pago.

---

# Casos Funcionales - Pago de servicio

| ID       | Título                                      | Precondición                                         | Pasos                                                                                                                                                       | Resultado Esperado                                                                                                  | Prioridad |
|----------|----------------------------------------------|------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|-----------|
| SERV-01  | Pago exitoso de un servicio con datos válidos | Usuario logueado, cuenta con saldo suficiente        | 1. Seleccionar un servicio.<br>2. Ingresar un monto válido.<br>3. Seleccionar una cuenta con saldo suficiente.<br>4. Click en "Pagar Servicio".          | El pago se procesa correctamente y se muestra un mensaje de confirmación/éxito.                                   | Alta      |
| SERV-02  | Pago de servicio utilizando Cuenta Corriente  | Cuenta Corriente disponible y con saldo suficiente   | 1. Seleccionar un servicio.<br>2. Ingresar un monto válido.<br>3. Seleccionar Cuenta Corriente.<br>4. Click en "Pagar Servicio".                         | El pago se procesa correctamente y el importe se debita de la Cuenta Corriente.                                   | Alta      |
| SERV-03  | Pago de servicio utilizando Caja de Ahorro    | Caja de Ahorro disponible y con saldo suficiente     | 1. Seleccionar un servicio.<br>2. Ingresar un monto válido.<br>3. Seleccionar Caja de Ahorro.<br>4. Click en "Pagar Servicio".                           | El pago se procesa correctamente y el importe se debita de la Caja de Ahorro.                                     | Alta      |

---

# Casos de Selección de Servicio

| ID       | Título                                      | Precondición        | Pasos                                                                                   | Resultado Esperado                                                                                  | Prioridad |
|----------|----------------------------------------------|---------------------|-----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|-----------|
| SERV-04  | Visualización de servicios disponibles       | Formulario abierto  | 1. Abrir el dropdown "Selecciona el Servicio".                                         | Se muestran los servicios disponibles para realizar el pago.                                      | Alta      |
| SERV-05  | Selección de un servicio                     | Servicios disponibles | 1. Abrir el dropdown.<br>2. Seleccionar un servicio.                                   | El servicio seleccionado queda correctamente reflejado en el campo.                              | Alta      |
| SERV-06  | Intentar pagar sin seleccionar un servicio  | Formulario abierto  | 1. No seleccionar ningún servicio.<br>2. Ingresar un monto válido.<br>3. Seleccionar cuenta.<br>4. Click en "Pagar Servicio". | El sistema no procesa el pago y muestra una validación indicando que debe seleccionarse un servicio. | Alta      |

---

# Casos de Validación de Monto

| ID       | Título                              | Precondición        | Pasos                                                                                         | Resultado Esperado                                                                                     | Prioridad |
|----------|--------------------------------------|---------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|-----------|
| SERV-07  | Monto vacío                          | Formulario abierto  | 1. Seleccionar un servicio.<br>2. Dejar vacío "Monto a Pagar".<br>3. Seleccionar cuenta.<br>4. Intentar pagar. | El sistema no permite procesar el pago y muestra una validación de campo obligatorio.                 | Alta      |
| SERV-08  | Monto igual a cero                   | Formulario abierto  | 1. Seleccionar un servicio.<br>2. Ingresar $0.<br>3. Seleccionar cuenta.<br>4. Intentar pagar. | El sistema rechaza el pago y muestra una validación indicando que el monto no es válido.               | Alta      |
| SERV-09  | Monto negativo                        | Formulario abierto  | 1. Seleccionar un servicio.<br>2. Intentar ingresar un monto negativo.                       | El campo rechaza el valor o el sistema impide procesar el pago.                                        | Media     |
| SERV-10  | Monto con caracteres no numéricos    | Formulario abierto  | 1. Seleccionar un servicio.<br>2. Intentar ingresar letras o caracteres no numéricos.        | El sistema impide ingresar valores no numéricos o rechaza el pago.                                     | Media     |
| SERV-11  | Monto con decimales *(pendiente)*   | Formulario abierto  | 1. Seleccionar un servicio.<br>2. Ingresar un monto decimal.<br>3. Seleccionar cuenta.<br>4. Intentar pagar. | **No confirmado.** Documentar comportamiento real: acepta, rechaza o redondea el valor.                | Media     |
| SERV-12  | Monto mínimo permitido *(pendiente)* | Formulario abierto  | 1. Ingresar el menor importe permitido.<br>2. Intentar realizar el pago.                    | **No confirmado.** No se encuentra documentado actualmente un monto mínimo para Pago de Servicios.     | Media     |
| SERV-13  | Monto máximo permitido *(pendiente)* | Formulario abierto  | 1. Ingresar el mayor importe permitido.<br>2. Intentar realizar el pago.                    | **No confirmado.** No se encuentra documentado actualmente un monto máximo para Pago de Servicios.     | Media     |

---

# Casos de Cuenta a Debitar

| ID       | Título                                             | Precondición                              | Pasos                                                                                               | Resultado Esperado                                                                                              | Prioridad |
|----------|-----------------------------------------------------|-------------------------------------------|-----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|-----------|
| SERV-14  | Visualización de cuentas disponibles para débito    | Formulario abierto                       | 1. Abrir el dropdown "Cuenta a Debitar".                                                           | Se muestran las cuentas habilitadas para realizar pagos.                                                        | Alta      |
| SERV-15  | Intentar pagar sin seleccionar una cuenta           | Servicio y monto válidos                  | 1. Seleccionar servicio.<br>2. Ingresar monto.<br>3. No seleccionar cuenta.<br>4. Click en "Pagar Servicio". | El sistema no procesa el pago y muestra una validación indicando que debe seleccionarse una cuenta.           | Alta      |
| SERV-16  | Verificar disponibilidad de Cuenta Corriente       | Cuenta Corriente existente                 | 1. Abrir "Cuenta a Debitar".                                                                         | Cuenta Corriente aparece como opción si está habilitada para realizar débitos.                                | Media     |
| SERV-17  | Verificar disponibilidad de Caja de Ahorro         | Caja de Ahorro existente                   | 1. Abrir "Cuenta a Debitar".                                                                         | Caja de Ahorro aparece como opción si está habilitada para realizar débitos.                                  | Media     |
| SERV-18  | Verificar disponibilidad de Tarjeta de Crédito *(pendiente)* | Tarjeta de Crédito existente       | 1. Abrir "Cuenta a Debitar".                                                                         | **No confirmado.** Verificar si Tarjeta de Crédito aparece como opción y documentar el comportamiento real.   | Media     |

---

# Casos de Saldo

| ID       | Título                                         | Precondición                                      | Pasos                                                                                                                  | Resultado Esperado                                                                                               | Prioridad |
|----------|-------------------------------------------------|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|-----------|
| SERV-19  | Pago con saldo insuficiente                     | Cuenta con saldo inferior al monto a pagar        | 1. Seleccionar servicio.<br>2. Ingresar monto superior al saldo.<br>3. Seleccionar cuenta.<br>4. Intentar pagar.      | El sistema rechaza el pago, muestra un mensaje de saldo insuficiente y no realiza ningún débito.              | Alta      |
| SERV-20  | Pago utilizando exactamente el saldo disponible | Cuenta con saldo igual al monto a pagar            | 1. Registrar saldo disponible.<br>2. Ingresar exactamente dicho monto.<br>3. Seleccionar cuenta.<br>4. Pagar.        | El pago se procesa correctamente y el saldo de la cuenta queda en $0.                                           | Alta      |
| SERV-21  | Pago con saldo superior al monto a pagar         | Cuenta con saldo superior al monto                 | 1. Seleccionar servicio.<br>2. Ingresar monto inferior al saldo.<br>3. Seleccionar cuenta.<br>4. Pagar.                | El pago se procesa correctamente y el saldo queda reducido exactamente por el importe pagado.                | Alta      |

---

# Casos de Confirmación / Cancelación

| ID       | Título                                           | Precondición                                      | Pasos                                                                                                                                              | Resultado Esperado                                                                                                     | Prioridad |
|----------|---------------------------------------------------|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|-----------|
| SERV-22  | Mostrar modal de confirmación antes del pago *(pendiente)* | Datos válidos completos                 | 1. Seleccionar servicio.<br>2. Ingresar monto.<br>3. Seleccionar cuenta.<br>4. Click en "Pagar Servicio".                                         | **No confirmado.** Verificar si se muestra un modal antes de ejecutar el pago y qué información contiene.            | Media     |
| SERV-23  | Cancelar pago desde el modal *(pendiente)*        | Modal de confirmación abierto                    | 1. Completar formulario.<br>2. Click en "Pagar Servicio".<br>3. Click en "Cancelar" en el modal.                                                    | **No confirmado.** Se espera que el modal se cierre sin realizar el débito ni registrar el pago.                     | Media     |
| SERV-24  | Confirmar pago desde el modal *(pendiente)*       | Modal de confirmación abierto                    | 1. Completar formulario.<br>2. Click en "Pagar Servicio".<br>3. Click en "Confirmar".                                                                | **No confirmado.** Se espera que el pago sea procesado y se muestre el mensaje de éxito correspondiente.             | Alta      |

---

# Casos de Actualización de Saldo

| ID       | Título                                      | Precondición                        | Pasos                                                                                                                          | Resultado Esperado                                                                                      | Prioridad |
|----------|----------------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|-----------|
| SERV-25  | Actualización del saldo después del pago     | Pago realizado exitosamente         | 1. Registrar saldo inicial.<br>2. Realizar un pago exitoso.<br>3. Consultar el saldo de la cuenta.                            | El saldo final corresponde al saldo inicial menos el monto pagado.                                      | Alta      |
| SERV-26  | El pago rechazado no modifica el saldo       | Cuenta con saldo insuficiente       | 1. Registrar saldo inicial.<br>2. Intentar realizar un pago superior al saldo.<br>3. Consultar nuevamente el saldo.          | El saldo permanece sin cambios porque la operación fue rechazada.                                       | Alta      |

---

# Casos de Registro de Movimientos

| ID       | Título                                      | Precondición                     | Pasos                                                                                                                       | Resultado Esperado                                                                                       | Prioridad |
|----------|----------------------------------------------|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|-----------|
| SERV-27  | Registro del pago en los movimientos         | Pago realizado exitosamente      | 1. Registrar servicio y monto.<br>2. Realizar el pago.<br>3. Acceder a los movimientos de la cuenta utilizada.             | El pago aparece registrado como movimiento con el importe correspondiente.                               | Alta      |
| SERV-28  | Importe registrado coincide con importe pagado | Pago realizado exitosamente    | 1. Realizar un pago por un importe determinado.<br>2. Consultar el movimiento generado.                                    | El importe registrado coincide exactamente con el importe pagado.                                       | Alta      |
| SERV-29  | Pago rechazado no genera movimiento           | Pago rechazado por saldo insuficiente | 1. Intentar realizar un pago con saldo insuficiente.<br>2. Consultar los movimientos de la cuenta.                      | No se genera ningún movimiento correspondiente al pago rechazado.                                       | Alta      |


---

# Casos Generales

| ID       | Título                                      | Precondición                         | Pasos                                                                                                     | Resultado Esperado                                                                                         | Prioridad |
|----------|----------------------------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|-----------|
| SERV-30  | Evitar doble procesamiento del pago           | Datos válidos y saldo suficiente     | 1. Completar el formulario.<br>2. Realizar doble click rápidamente sobre "Pagar Servicio".              | Se procesa una única operación y no se generan dos débitos ni dos movimientos.                             | Alta      |
| SERV-31  | Cambio de cuenta antes de realizar el pago    | Formulario parcialmente completado   | 1. Seleccionar servicio y monto.<br>2. Seleccionar una cuenta.<br>3. Cambiar la cuenta seleccionada.<br>4. Realizar el pago. | El débito se realiza únicamente sobre la cuenta finalmente seleccionada.                                   | Media     |
| SERV-32  | Cambio de monto antes de realizar el pago     | Formulario parcialmente completado   | 1. Seleccionar servicio y cuenta.<br>2. Ingresar un monto.<br>3. Modificar el monto.<br>4. Realizar el pago. | El importe debitado coincide con el último monto ingresado y no con el valor anterior.                     | Media     |

---

**Total de Test Cases: 32**





