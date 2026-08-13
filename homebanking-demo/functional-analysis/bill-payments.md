
# Análisis Funcional — Pago de Servicios

**Módulo:** Pago de Servicios
**Prioridad:** Alta

> Este análisis está basado en la exploración de la aplicación. No existe documentación oficial de requisitos — los comportamientos esperados fueron inferidos a partir del comportamiento observado.

---

## Objetivo

Permitir al usuario pagar un servicio seleccionándolo de un listado fijo, con un monto sugerido editable, debitando el importe de una cuenta a elección entre las disponibles.

---

## Elementos de la interfaz

| Elemento | Tipo | Descripción |
|---|---|---|
| Selecciona el Servicio | Dropdown | Lista fija: Electricidad, Gas Natural, AySA, Internet, Telefonía |
| Monto a Pagar | Input numérico | Aparece tras seleccionar un servicio, precargado con un monto sugerido (ej. $8.500), editable. El monto sugerido varía según el servicio elegido |
| Cuenta a Debitar | Dropdown | Muestra las 3 cuentas del usuario: Cuenta Corriente, Caja de Ahorro y Tarjeta de Crédito |
| Pagar Servicio | Botón | Ejecuta el pago directamente, sin modal de confirmación previo |
| Mensaje de éxito | Texto/Modal | "¡Pago Finalizado con éxito!" + botón para descargar comprobante en PDF |

---

## Reglas de negocio

- El listado de servicios es fijo: Electricidad, Gas Natural, AySA, Internet, Telefonía
- Al seleccionar un servicio, se precarga un monto sugerido que varía según el servicio (ej. $8.500 para uno de ellos)
- El monto sugerido es editable por el usuario
- **Monto mínimo:** $0.01 (por debajo, o en $0, muestra: *"El valor debe ser superior o igual a 0.01"*)
- **No hay monto máximo definido** — el único límite real es el saldo disponible en la cuenta seleccionada
- Las 3 cuentas del usuario están disponibles como cuenta a debitar (a diferencia de Préstamos, acá **no se excluye la Tarjeta de Crédito**)
- **No existe modal de confirmación** — el botón "Pagar Servicio" ejecuta el pago directamente
- Si el saldo de la cuenta seleccionada es insuficiente, muestra: *"Saldo insuficiente"*
- Tras un pago exitoso, se muestra "¡Pago Finalizado con éxito!" con opción de descargar comprobante en PDF
- Luego de unos segundos, la pantalla vuelve automáticamente a su estado inicial (solo el dropdown de servicio visible)
- Los pagos realizados se reflejan correctamente en "Últimos Movimientos" del Dashboard

---

## Flujo principal — Pagar un Servicio

1. Usuario abre el dropdown "Selecciona el Servicio" y elige uno (ej. Electricidad)
2. El sistema muestra el campo "Monto a Pagar" precargado con un monto sugerido, y el dropdown "Cuenta a Debitar"
3. Usuario puede modificar el monto sugerido, o dejarlo como está
4. Usuario selecciona una cuenta a debitar
5. Usuario hace click en "Pagar Servicio"
6. El sistema valida los datos y el saldo disponible
7. Si es válido, procesa el pago y muestra "¡Pago Finalizado con éxito!" con botón de descarga de comprobante PDF
8. Tras unos segundos, la pantalla vuelve al estado inicial
9. El pago queda reflejado en "Últimos Movimientos" del Dashboard

---

## Flujos alternativos / excepciones

**Monto igual a cero (o menor a $0.01)**
- Muestra: "El valor debe ser superior o igual a 0.01"
- No permite procesar el pago

**Saldo insuficiente en la cuenta seleccionada**
- Muestra: "Saldo insuficiente"
- No se procesa el débito

**Sin monto máximo**
- El sistema no rechaza montos altos por sí mismos; solo se bloquea si superan el saldo disponible de la cuenta

**Ausencia de modal de confirmación**
- El pago se ejecuta inmediatamente al hacer click en "Pagar Servicio" — no hay paso intermedio de revisión antes de confirmar, a diferencia de Transferencias, Plazos Fijos y Préstamos

---

## Riesgos detectados

- **Alto:** Al no existir modal de confirmación, un click accidental en "Pagar Servicio" ejecuta el pago de inmediato — sin posibilidad de revisar o cancelar antes de procesar. Este es un comportamiento de UX distinto (y potencialmente más riesgoso) que el resto de los módulos transaccionales
- **Medio:** No se verificó el comportamiento ante doble click rápido en "Pagar Servicio" — riesgo de doble débito, similar a lo que se probó en Login (UI-03) y Transferencias
- **Bajo:** No hay validación de tope máximo de monto — comportamiento distinto a Transferencias ($50.000) y Préstamos ($500.000), pero consistente y simple: el saldo disponible actúa como único techo

---

## Dudas / puntos a verificar

| # | Duda | Impacto |
|---|---|---|
| 1 | ¿Qué sucede ante doble click rápido en "Pagar Servicio"? ¿Se genera un doble débito? | Riesgo de bug crítico, no verificado aún |
| 2 | ¿El monto sugerido es siempre el mismo por servicio, o varía (ej. simula una factura real)? | Define si es un valor fijo o dinámico para los test cases |
| 3 | ¿Se puede pagar el mismo servicio más de una vez en el mismo período? | Define si hay restricción de repetición |
| 4 | ¿El comprobante PDF descargado contiene los datos correctos del pago? | Válido como caso de prueba de contenido, no solo de existencia del botón |
| 5 | ¿Qué pasa si se cambia de servicio después de haber editado el monto? ¿Se resetea el monto al del nuevo servicio sugerido? | Define comportamiento del formulario ante cambios |

---

## Casos de prueba relacionados

*Ver `test-cases-pago-servicios.md`*

---

## Bugs encontrados

*Se completará después de la ejecución*




