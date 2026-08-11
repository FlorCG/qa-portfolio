
# Análisis Funcional — Préstamos

**Módulo:** Préstamos
**Prioridad:** Alta

> Este análisis está basado en la exploración de la aplicación. No existe documentación oficial de requisitos — los comportamientos esperados fueron inferidos a partir del comportamiento observado.

---

## Objetivo

Permitir al usuario solicitar un préstamo dentro de límites definidos de monto y cuotas, visualizar sus préstamos activos, y contar con dos mecanismos de finalización anticipada: pago total del saldo restante, o desistimiento dentro del plazo legal de revocación.

---

## Elementos de la interfaz

| Elemento | Tipo | Descripción |
|---|---|---|
| Panel izquierdo — Préstamos activos | Lista de cards | Muestra monto, cuotas, fecha (días), total a pagar, botón "Pagar Total", y botón "Desistir" (solo dentro del plazo de revocación) |
| Modal de "Pagar Total" | Modal | Pregunta "¿Deseas cancelar totalmente este préstamo?", monto total, dropdown de cuenta de pago, botones Cancelar / Confirmar |
| Modal de "Desistir" | Modal | Texto legal sobre plazo de revocación (10 días), monto a devolver, dropdown de cuenta a debitar, botones Cancelar / Confirmar |
| Panel derecho — Solicitar nuevo préstamo | Formulario | Dropdown de cuenta destino, Monto a solicitar, Cuotas (dropdown), texto informativo "Info: 3 total, 2 válidas", botón "Solicitar Préstamo" |

---

## Reglas de negocio

- **Monto mínimo:** $1.000
- **Monto máximo:** $500.000
- **Cuotas disponibles:** 6, 12, 18 y 24 cuotas (opciones fijas)
- **Plazo de revocación (derecho de desistimiento):** 10 días desde la creación del préstamo. Dentro de ese plazo, aparece el botón "Desistir" además de "Pagar Total"
- **Desistir:** devuelve el monto original recibido (sin intereses), y el préstamo queda marcado como pagado y desaparece del panel
- **Pagar Total:** cancela el préstamo pagando el monto total (a confirmar si incluye intereses de cuotas restantes)
- **Validación de saldo en "Pagar Total":** si ninguna cuenta tiene saldo suficiente, muestra: *"No tienes cuentas con saldo suficiente para cancelar este préstamo"*
- **Filtrado de cuenta de pago en "Pagar Total":** el dropdown solo muestra las cuentas con saldo suficiente para cubrir el monto total a pagar. Las cuentas sin saldo suficiente no aparecen como opción
- Mensaje "Info: 3 total, 2 válidas" debajo del dropdown de cuenta destino — se interpreta como: de las 3 cuentas del usuario (Corriente, Caja de Ahorro, Tarjeta de Crédito), solo 2 son válidas como cuenta destino de un préstamo (probablemente excluyendo Tarjeta de Crédito, ya que no es una cuenta apta para recibir depósitos) *(a confirmar el detalle exacto de qué cuenta queda excluida y por qué)*

---

## Flujo principal — Solicitar Préstamo

1. Usuario selecciona cuenta destino (dropdown)
2. Ingresa monto a solicitar (entre $1.000 y $500.000)
3. Selecciona cantidad de cuotas (6/12/18/24)
4. Hace click en "Solicitar Préstamo"
5. El sistema muestra mensaje de éxito ("se ha creado exitosamente")
6. El nuevo préstamo aparece en el panel izquierdo de préstamos activos

---

## Flujo principal — Pagar Total (cancelación anticipada, fuera o dentro del plazo de revocación)

1. Usuario hace click en "Pagar Total" sobre un préstamo activo
2. Se abre el modal: "¿Deseas cancelar totalmente este préstamo?", con el monto total y un dropdown de cuenta de pago
3. Usuario selecciona cuenta (o el sistema la preselecciona automáticamente — comportamiento a confirmar) y hace click en "Confirmar"
4. El sistema procesa el pago y el préstamo se da por cancelado

---

## Flujo principal — Desistir (dentro del plazo de revocación de 10 días)

1. Usuario hace click en "Desistir" sobre un préstamo activo (solo visible dentro de los 10 días desde la creación)
2. Se abre el modal con el texto: "Estás dentro del plazo de revocación (10 días). Puedes cancelar el préstamo devolviendo el monto original recibido", el monto a devolver, y un dropdown de cuenta a debitar
3. Usuario selecciona cuenta y hace click en "Confirmar"
4. El préstamo queda marcado como pagado y desaparece del panel de préstamos activos

---

## Flujos alternativos / excepciones

**Monto fuera de rango**
- Menor a $1.000 o mayor a $500.000: se espera un mensaje de validación específico *(mensaje exacto a confirmar en la exploración)*
- No permite avanzar

**Saldo insuficiente para "Pagar Total"**
- Ninguna cuenta tiene saldo suficiente
- Muestra: "No tienes cuentas con saldo suficiente para cancelar este préstamo"
- No permite procesar el pago

**Dropdown de cuenta de pago en "Pagar Total" filtra por saldo suficiente**
- Solo se muestran las cuentas que pueden cubrir el monto total del préstamo
- Comportamiento esperado, no es un bug

**Cancelar desde los modales (botón "Cancelar", no "Confirmar")**
- Se espera que cierre el modal sin ejecutar la acción, siguiendo el mismo patrón que Transferencias y Plazos Fijos *(a confirmar)*

**Botón "Desistir" fuera del plazo de 10 días**
- Se espera que el botón deje de estar visible o se deshabilite pasado ese plazo *(a confirmar en la exploración, ya que requiere esperar 10 días o simular fecha)*

---

## Riesgos detectados

- **Alto:** No está claro si "Pagar Total" incluye intereses de las cuotas restantes o solo el capital adeudado — puede generar una discrepancia entre lo que el usuario espera pagar y lo que el sistema cobra
- **Medio:** No se verificó el comportamiento exacto de las validaciones de monto mínimo/máximo (mensajes de error específicos)
- **Medio:** Si "Tarjeta de Crédito" queda excluida como cuenta destino válida, conviene validar que el sistema comunique claramente por qué esa cuenta no aparece como opción, en lugar de solo mostrar "2 válidas" sin contexto

---

## Dudas / puntos a verificar

| # | Duda | Impacto |
|---|---|---|
| 1 | ¿Cuál de las 3 cuentas queda excluida como destino válido de un préstamo, y por qué? | Confirmar si es Tarjeta de Crédito y documentar la regla exacta |
| 2 | ¿"Pagar Total" incluye los intereses de las cuotas restantes, o solo el capital? | Afecta el cálculo esperado en los test cases |
| 3 | ¿Cuáles son los mensajes exactos de error para monto menor a $1.000 y mayor a $500.000? | Necesario para definir el resultado esperado en los test cases |
| 4 | ¿El botón "Desistir" desaparece automáticamente pasado el día 10, o sigue visible pero deshabilitado? | Define el caso de prueba de límite de tiempo |
| 5 | ¿Se puede solicitar más de un préstamo activo simultáneamente? | Define si hay límite de cantidad |
| 6 | ¿Qué pasa si se cancela un modal ("Pagar Total" o "Desistir") con el botón Cancelar? | A confirmar, se asume por patrón de otros módulos |

---

## Casos de prueba relacionados



---

## Bugs encontrados

*Se completará después de la ejecución*
