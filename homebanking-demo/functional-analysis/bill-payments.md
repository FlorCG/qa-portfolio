
# Análisis Funcional — Pago de servicios

**Módulo:** Pago de servicios
**Prioridad:** Alta

> Este análisis está basado en la exploración de la aplicación. No existe documentación oficial de requisitos — los comportamientos esperados fueron inferidos a partir del comportamiento observado.

---

## Objetivo

Permitir al usuario realizar el pago de un servicio seleccionándolo de un listado disponible, ingresando el monto a pagar y seleccionando una cuenta bancaria desde la cual se debitará el importe.
El sistema debe validar que los datos requeridos sean válidos y que la cuenta seleccionada disponga de saldo suficiente antes de procesar el pago.

---

## Elementos de la interfaz

| Elemento               | Tipo           | Descripción                                                                 |
| ---------------------- | -------------- | --------------------------------------------------------------------------- |
| Selecciona el Servicio | Dropdown       | Permite seleccionar el servicio que el usuario desea pagar                  |
| Monto a Pagar          | Input numérico | Permite ingresar el importe correspondiente al servicio seleccionado        |
| Cuenta a Debitar       | Dropdown       | Permite seleccionar la cuenta bancaria desde la cual se realizará el débito |
| Pagar Servicio         | Botón          | Procesa el pago del servicio con los datos ingresados                       |

La interfaz observada presenta estos cuatro elementos principales dentro del módulo de Pago de Servicios.

---

## Reglas de negocio

* Es obligatorio seleccionar un servicio antes de realizar el pago.
* Es obligatorio ingresar un monto a pagar.
* El monto debe ser un valor numérico válido y mayor a cero.
* Es obligatorio seleccionar una cuenta a debitar.
* La cuenta seleccionada debe ser una cuenta apta para realizar débitos.
* La cuenta seleccionada debe disponer de saldo suficiente para cubrir el importe del servicio.
* El monto debitado debe coincidir con el monto ingresado por el usuario.
* Una vez confirmado correctamente el pago, el sistema debe registrar la operación como realizada.
* El pago debería reflejarse posteriormente en los movimientos de la cuenta utilizada.
* La Tarjeta de Crédito debería quedar excluida de las cuentas disponibles para débito directo, dado que el pago se realiza desde una cuenta bancaria *(a confirmar mediante exploración)*.

---

## Flujo principal — Pagar un Servicio

1. Usuario accede al módulo **Pago de Servicios**.
2. Usuario abre el dropdown **Selecciona el Servicio**.
3. Usuario selecciona un servicio disponible.
4. Usuario ingresa el **Monto a Pagar**.
5. Usuario selecciona una **Cuenta a Debitar**.
6. Usuario hace click en **Pagar Servicio**.
7. El sistema valida los datos ingresados.
8. El sistema verifica que la cuenta seleccionada tenga saldo suficiente.
9. El sistema procesa el débito.
10. El sistema informa al usuario que el pago fue realizado exitosamente.
11. El movimiento debería quedar registrado en la cuenta correspondiente.

---

## Flujos alternativos / excepciones

### No seleccionar un servicio

* Usuario intenta realizar el pago sin seleccionar un servicio.
* El sistema debería impedir el procesamiento.
* Se espera un mensaje de validación indicando que debe seleccionar un servicio *(mensaje exacto a confirmar)*.

### Monto vacío

* Usuario deja vacío el campo **Monto a Pagar**.
* Usuario hace click en **Pagar Servicio**.
* El sistema debería impedir el procesamiento.
* Se espera un mensaje de validación indicando que el monto es obligatorio *(mensaje exacto a confirmar)*.

### Monto igual a cero

* Usuario ingresa `$0`.
* El sistema debería rechazar la operación.
* Se espera un mensaje indicando que el monto debe ser mayor a cero *(mensaje exacto a confirmar)*.

### Monto negativo

* Usuario intenta ingresar un importe negativo.
* El sistema debería impedir el procesamiento o mostrar una validación.
* Se espera un mensaje de error específico *(a confirmar)*.

### Monto con formato inválido

* Usuario ingresa caracteres no numéricos.
* El sistema debería impedir el ingreso o rechazar el pago.
* Se espera una validación indicando que el monto debe ser numérico *(a confirmar)*.

### Cuenta a debitar no seleccionada

* Usuario completa servicio y monto, pero no selecciona una cuenta.
* Hace click en **Pagar Servicio**.
* El sistema debería impedir el procesamiento.
* Se espera un mensaje indicando que debe seleccionar una cuenta *(mensaje exacto a confirmar)*.

### Saldo insuficiente

* Usuario selecciona una cuenta cuyo saldo disponible es menor al monto del servicio.
* Usuario intenta realizar el pago.
* El sistema debería rechazar la operación.
* No debería realizarse ningún débito.
* Se espera un mensaje indicando que la cuenta no posee saldo suficiente *(mensaje exacto a confirmar)*.

### Cuenta con saldo exacto

* El saldo disponible de la cuenta es exactamente igual al monto a pagar.
* El sistema debería permitir la operación.
* El saldo de la cuenta debería quedar en `$0`.

### Cancelación de la operación

* Si durante el proceso existe un modal de confirmación, el botón **Cancelar** debería cerrar el modal sin ejecutar el pago.
* No debería producirse ningún débito.
* El comportamiento exacto debe confirmarse mediante exploración.

---

## Flujo de validación de saldo

1. Usuario selecciona un servicio.
2. Ingresa el monto.
3. Selecciona una cuenta a debitar.
4. El sistema verifica el saldo disponible.
5. Si el saldo es suficiente, permite continuar con el pago.
6. Si el saldo es insuficiente, rechaza la operación.
7. El saldo de la cuenta no debe modificarse cuando el pago es rechazado.

---

## Reglas sobre cuentas

Se identifican tres productos/cuentas en el Home Banking:

* Cuenta Corriente
* Caja de Ahorro
* Tarjeta de Crédito

La pantalla principal muestra Cuenta Corriente y Caja de Ahorro como cuentas con **saldo disponible**, mientras que Tarjeta de Crédito muestra **disponible**, por lo que debería verificarse cuáles de ellas aparecen realmente en el dropdown **Cuenta a Debitar**.

### Regla esperada

* Cuenta Corriente: potencialmente válida para débito.
* Caja de Ahorro: potencialmente válida para débito.
* Tarjeta de Crédito: potencialmente no válida para débito directo.

> La composición exacta del dropdown debe confirmarse durante la exploración funcional.

---

## Comportamiento esperado después de un pago exitoso

Luego de realizar correctamente un pago:

* El sistema debería mostrar un mensaje de éxito.
* El importe debería descontarse del saldo de la cuenta seleccionada.
* La operación debería registrarse en los movimientos de la cuenta.
* El servicio y el monto deberían corresponder con los datos ingresados.
* No debería producirse un segundo débito ante una única confirmación.

---

## Riesgos detectados

* **Alto:** No está documentado qué servicios están disponibles ni si el listado es fijo o dinámico.
* **Alto:** No está definido si el sistema valida saldo suficiente antes de habilitar el pago o únicamente al momento de procesarlo.
* **Alto:** No está definido si el monto ingresado por el usuario corresponde a un importe libre o si determinados servicios tienen importes predefinidos.
* **Medio:** No está documentado el monto mínimo o máximo permitido para pagar un servicio.
* **Medio:** No está documentado si se permiten valores decimales.
* **Medio:** No está documentado qué cuentas pueden utilizarse como cuenta de débito.
* **Medio:** No está documentado el mensaje de éxito luego de realizar el pago.
* **Medio:** No está documentado si existe un modal de confirmación antes de ejecutar el débito.
* **Medio:** No está documentado cómo se registra el pago dentro de los movimientos de la cuenta.

---

## Dudas / puntos a verificar

| #  | Duda                                                                     | Impacto                                              |
| -- | ------------------------------------------------------------------------ | ---------------------------------------------------- |
| 1  | ¿Qué servicios aparecen disponibles en el dropdown?                      | Define las opciones válidas para los casos de prueba |
| 2  | ¿El monto es libre o cada servicio tiene un importe determinado?         | Define las reglas de validación del monto            |
| 3  | ¿Cuál es el monto mínimo permitido?                                      | Necesario para definir límites y casos negativos     |
| 4  | ¿Existe un monto máximo permitido?                                       | Necesario para definir límites y casos negativos     |
| 5  | ¿Se permiten valores decimales?                                          | Define el formato válido del importe                 |
| 6  | ¿Qué cuentas aparecen en "Cuenta a Debitar"?                             | Define las cuentas válidas para el pago              |
| 7  | ¿La Tarjeta de Crédito está excluida como cuenta de débito?              | Define una regla funcional importante                |
| 8  | ¿Qué sucede cuando la cuenta no tiene saldo suficiente?                  | Define el flujo de excepción                         |
| 9  | ¿Existe un modal de confirmación antes de realizar el pago?              | Define el flujo de confirmación/cancelación          |
| 10 | ¿Cuál es el mensaje exacto de éxito?                                     | Necesario para los casos de prueba                   |
| 11 | ¿Cuál es el mensaje exacto ante saldo insuficiente?                      | Necesario para los casos de prueba                   |
| 12 | ¿El pago aparece inmediatamente en "Últimos Movimientos"?                | Permite validar la persistencia de la operación      |
| 13 | ¿Se puede realizar más de un pago consecutivo del mismo servicio?        | Define restricciones de repetición                   |
| 14 | ¿Qué sucede si se hace doble click en "Pagar Servicio"?                  | Riesgo de doble débito                               |
| 15 | ¿Qué ocurre si el usuario cambia la cuenta después de ingresar el monto? | Define el comportamiento del formulario              |

---

## Casos de prueba relacionados

### Happy Path

* Pago exitoso seleccionando un servicio, monto válido y cuenta con saldo suficiente.
* Pago utilizando Cuenta Corriente.
* Pago utilizando Caja de Ahorro.
* Pago por un importe exactamente igual al saldo disponible.

### Validaciones

* Servicio no seleccionado.
* Monto vacío.
* Monto igual a cero.
* Monto negativo.
* Monto con caracteres no numéricos.
* Monto decimal.
* Monto mínimo permitido.
* Monto máximo permitido.
* Cuenta no seleccionada.
* Cuenta sin saldo suficiente.

### Cuentas

* Verificar cuentas disponibles en el dropdown.
* Verificar que Tarjeta de Crédito no pueda utilizarse como cuenta de débito, si corresponde.
* Verificar que una cuenta con saldo suficiente pueda utilizarse.
* Verificar que una cuenta sin saldo suficiente no permita procesar el pago.

### Persistencia

* Verificar descuento del importe sobre el saldo de la cuenta.
* Verificar registro del pago en movimientos.
* Verificar que el importe registrado coincida con el importe pagado.
* Verificar que un pago rechazado no modifique el saldo.

### Seguridad / integridad

* Verificar que no se produzca doble débito ante doble click.
* Verificar que no se procese un pago sin completar los campos obligatorios.
* Verificar que modificar los datos del formulario antes de confirmar no genere información inconsistente.

---

## Bugs encontrados

*Se completará después de la ejecución.*

