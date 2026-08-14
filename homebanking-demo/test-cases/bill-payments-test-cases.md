# Test Cases – Pago de Servicios

## Información general

- **Elementos de la interfaz:** Dropdown "Selecciona el Servicio" (Electricidad, Gas Natural, AySA, Internet, Telefonía), campo "Monto a Pagar" (precargado con sugerencia editable), dropdown "Cuenta a Debitar" (3 cuentas disponibles), botón "Pagar Servicio"
- **Reglas de negocio consideradas:**
  - Monto mínimo: $0.01 — sin monto máximo definido (solo limita el saldo disponible)
  - Las 3 cuentas del usuario están disponibles para débito, incluyendo Tarjeta de Crédito
  - No existe modal de confirmación — el pago se ejecuta directo al hacer click
  - Mensaje de éxito: "¡Pago Finalizado con éxito!" con botón de descarga de comprobante PDF
  - El formulario se resetea automáticamente tras unos segundos post-pago
  - Los pagos se reflejan en Últimos Movimientos del Dashboard

---

# Casos Funcionales

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| SERV-01 | Pago exitoso de un servicio con el monto sugerido | Usuario logueado, cuenta con saldo suficiente | 1. Seleccionar un servicio (ej. Electricidad).<br>2. Dejar el monto sugerido sin modificar.<br>3. Seleccionar una cuenta a debitar.<br>4. Click en "Pagar Servicio". | Se muestra "¡Pago Finalizado con éxito!" junto con el botón de descarga de comprobante en PDF. | Alta |
| SERV-02 | Cada servicio muestra un monto sugerido distinto | Ninguna | 1. Seleccionar "Electricidad" y anotar el monto sugerido.<br>2. Cambiar a "Gas Natural" y anotar el monto sugerido.<br>3. Repetir con el resto de los servicios. | Los montos sugeridos difieren entre servicios (o se documenta el patrón si alguno coincide). | Media |
| SERV-03 | Edición del monto sugerido antes de pagar | Servicio seleccionado, monto sugerido visible | 1. Seleccionar un servicio.<br>2. Modificar el monto sugerido por otro valor válido.<br>3. Seleccionar cuenta.<br>4. Click en "Pagar Servicio". | El sistema procesa el pago con el monto editado, no con el sugerido original. | Alta |
| SERV-04 | Cambio de servicio después de editar el monto | Servicio seleccionado, monto sugerido editado manualmente | 1. Seleccionar un servicio y editar el monto.<br>2. Cambiar la selección a otro servicio. | Se verifica si el monto vuelve al sugerido del nuevo servicio o conserva el valor editado — documentar el comportamiento real. | Baja |

---

# Casos de Cuenta a Debitar

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| SERV-05 | Las 3 cuentas están disponibles como cuenta a debitar | Servicio y monto seleccionados | 1. Abrir el dropdown "Cuenta a Debitar". | Se listan las 3 cuentas: Cuenta Corriente, Caja de Ahorro y Tarjeta de Crédito. | Media |
| SERV-06 | Pago exitoso debitando desde Cuenta Corriente | Cuenta Corriente con saldo suficiente | 1. Completar servicio y monto.<br>2. Seleccionar Cuenta Corriente.<br>3. Click en "Pagar Servicio". | El pago se procesa exitosamente y el saldo de Cuenta Corriente disminuye según el monto pagado. | Media |
| SERV-07 | Pago exitoso debitando desde Caja de Ahorro | Caja de Ahorro con saldo suficiente | 1. Completar servicio y monto.<br>2. Seleccionar Caja de Ahorro.<br>3. Click en "Pagar Servicio". | El pago se procesa exitosamente y el saldo de Caja de Ahorro disminuye según el monto pagado. | Media |
| SERV-08 | Pago exitoso debitando desde Tarjeta de Crédito | Tarjeta de Crédito con saldo/límite suficiente | 1. Completar servicio y monto.<br>2. Seleccionar Tarjeta de Crédito.<br>3. Click en "Pagar Servicio". | El pago se procesa exitosamente, a diferencia de Préstamos donde esta cuenta queda excluida como destino. | Media |

---

# Casos de Validación de Monto

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| SERV-09 | Rechazo con monto igual a cero | Servicio seleccionado | 1. Modificar el monto a $0.<br>2. Click en "Pagar Servicio". | Muestra: "El valor debe ser superior o igual a 0.01". No se procesa el pago. | Alta |
| SERV-10 | Monto en el límite mínimo exacto ($0.01) | Servicio seleccionado, cuenta con saldo suficiente | 1. Ingresar $0.01 como monto.<br>2. Seleccionar cuenta.<br>3. Click en "Pagar Servicio". | El sistema acepta el monto y procesa el pago sin error. | Baja |
| SERV-11 | Rechazo por saldo insuficiente en la cuenta seleccionada | Cuenta con saldo menor al monto a pagar | 1. Ingresar un monto mayor al saldo disponible de la cuenta elegida.<br>2. Click en "Pagar Servicio". | Muestra: "Saldo insuficiente". No se procesa el pago ni se modifica el saldo. | Alta |
| SERV-12 | Pago con un monto alto sin tope máximo definido | Cuenta con saldo suficiente para cubrir un monto elevado | 1. Ingresar un monto considerablemente alto (ej. $200.000), dentro del saldo disponible.<br>2. Click en "Pagar Servicio". | El sistema procesa el pago sin rechazarlo por exceder un límite — el único freno posible es el saldo disponible. | Media |
| SERV-13 | Monto negativo | Servicio seleccionado | 1. Intentar ingresar un valor negativo en el campo Monto. | El campo rechaza el valor o se comporta como monto inválido. No permite procesar el pago. | Baja |

---

# Casos de Confirmación y Post-Pago

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| SERV-14 | Ausencia de modal de confirmación | Formulario completo con datos válidos | 1. Completar servicio, monto y cuenta.<br>2. Click en "Pagar Servicio". | El pago se ejecuta inmediatamente, sin mostrar un paso intermedio de confirmación antes de procesar. | Media |
| SERV-15 | Botón de descarga de comprobante en PDF disponible tras el pago | Pago exitoso realizado | 1. Completar un pago exitoso.<br>2. Verificar la presencia del botón de descarga del comprobante. | El botón para descargar el comprobante en PDF está disponible junto al mensaje de éxito. | Media |
| SERV-16 | Reseteo automático del formulario tras el pago | Pago exitoso realizado, mensaje de éxito visible | 1. Completar un pago exitoso.<br>2. Esperar unos segundos sin interactuar. | La pantalla vuelve automáticamente a su estado inicial, mostrando solo el dropdown de selección de servicio. | Baja |
| SERV-17 | El pago se refleja en Últimos Movimientos del Dashboard | Pago de servicio exitoso realizado | 1. Realizar un pago exitoso.<br>2. Navegar al Dashboard.<br>3. Revisar la sección "Últimos Movimientos". | El pago aparece reflejado con el monto, servicio y fecha correspondientes. | Alta |
| SERV-18 | Comportamiento ante doble click en "Pagar Servicio" *(pendiente de confirmación)* | Formulario completo con datos válidos | 1. Completar el formulario.<br>2. Hacer doble click rápido sobre "Pagar Servicio". | **No confirmado.** Se espera que el sistema procese un único pago y no genere doble débito — documentar el comportamiento real y, si se detecta doble débito, reportar como bug. | Alta |
| SERV-19 | Monto con caracteres no numéricos *(pendiente de confirmación)* | Servicio seleccionado | 1. Intentar ingresar caracteres no numéricos en el campo Monto (ej. "abc"). | **No confirmado.** Se espera que el campo rechace el ingreso o muestre validación de formato — documentar el comportamiento real. | Baja |
| SERV-20 | Monto con decimales no estándar *(pendiente de confirmación)* | Servicio seleccionado, cuenta con saldo suficiente | 1. Ingresar un monto con más de 2 decimales (ej. $100.999).<br>2. Click en "Pagar Servicio". | **No confirmado.** Se espera que el sistema redondee, trunque o rechace el valor — documentar el comportamiento real. | Baja |

---

**Total de Test Cases: 18**




