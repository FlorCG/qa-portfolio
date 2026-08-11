
# Análisis Funcional — Plazos Fijos

**Módulo:** Plazos Fijos
**Prioridad:** Alta

> Este análisis está basado en la exploración de la aplicación. No existe documentación oficial de requisitos — los comportamientos esperados fueron inferidos a partir del comportamiento observado.

---

## Objetivo

Permitir al usuario invertir dinero a un plazo determinado con una tasa de interés fija (TNA), y visualizar/gestionar sus plazos fijos activos, incluyendo la posibilidad de cancelarlos antes del vencimiento.

---

## Elementos de la interfaz

| Elemento | Tipo | Descripción |
|---|---|---|
| Panel izquierdo — Plazos Fijos activos | Lista de cards | Muestra monto, TNA, plazo en días, interés estimado, fecha de inicio, fecha de vencimiento, total al vencimiento, botón "Cancelar" |
| Modal de cancelación | Modal | Pregunta de confirmación, monto a reintegrar, botones Cancelar / Confirmar |
| Panel derecho — Crear nuevo Plazo Fijo | Formulario | Dropdown de cuenta origen, Monto a invertir, Plazo (dropdown), y una vez completado: interés estimado, total al vencimiento, fecha de vencimiento (calculados), botón "Crear Plazo Fijo" |
| Modal de creación | Modal | Resumen: cuenta origen, monto, plazo, TNA, interés estimado, total al vencimiento, fecha de vencimiento, botones Cancelar / Confirmar |
| Toast de éxito (creación) | Notificación | "Plazo fijo creado exitosamente" |
| Toast de éxito (cancelación) | Notificación | "Plazo fijo cancelado exitosamente. El dinero se acreditó en tu cuenta" |

---

## Reglas de negocio

- **Monto mínimo:** $1.000. Por debajo, muestra: *"El valor debe ser superior o igual a 1000"*
- **Plazos disponibles:** 30, 60, 90, 180 y 360 días (opciones fijas, no texto libre)
- Los campos de interés estimado, total al vencimiento y fecha de vencimiento se calculan dinámicamente al completar monto y plazo, antes de crear
- Requiere modal de confirmación tanto para crear como para cancelar un plazo fijo
- Al confirmar la creación, el nuevo plazo fijo se agrega al final de la lista de activos (orden: más antiguo primero, más nuevo al final)
- Al confirmar la cancelación, el plazo fijo se elimina de la lista y el monto se acredita a la cuenta de origen
- **Validación de saldo:** si el monto a invertir supera el saldo disponible de la cuenta origen, muestra: *"Saldo insuficiente en la cuenta origen"* y no permite crear

---

## Flujo principal — Crear Plazo Fijo

1. Usuario selecciona cuenta de origen
2. Ingresa monto a invertir (≥ $1.000, dentro del saldo disponible)
3. Selecciona plazo (30/60/90/180/360 días)
4. El sistema calcula y muestra interés estimado, total al vencimiento y fecha de vencimiento
5. Usuario hace click en "Crear Plazo Fijo"
6. Se abre el modal con el resumen completo
7. Usuario hace click en "Confirmar"
8. El sistema procesa la operación, muestra el toast de éxito, y el nuevo plazo fijo aparece al final de la lista de activos

---

## Flujo principal — Cancelar Plazo Fijo

1. Usuario hace click en "Cancelar" sobre un plazo fijo activo
2. Se abre el modal: "¿Estás seguro que deseas cancelar este plazo fijo?" + monto a reintegrar
3. Usuario hace click en "Confirmar"
4. El sistema procesa la cancelación, muestra el toast de éxito, acredita el dinero en la cuenta, y elimina el plazo fijo de la lista

---

## Flujos alternativos / excepciones

**Monto menor al mínimo**
- Muestra: "El valor debe ser superior o igual a 1000"
- No permite avanzar

**Saldo insuficiente**
- Muestra: "Saldo insuficiente en la cuenta origen"
- No permite crear

**Cancelación desde el modal (botón "Cancelar" del modal, no del plazo fijo)**
- Cierra el modal sin ejecutar la cancelación *(a confirmar comportamiento exacto — se asume por patrón de Transferencias)*

**Creación desde el modal (botón "Cancelar" del modal de creación)**
- Cierra el modal sin crear el plazo fijo *(a confirmar)*

---

## Riesgos detectados

- **Alto:** No se especifica si el monto a reintegrar al cancelar incluye el interés generado hasta la fecha, o solo el capital invertido — puede haber inconsistencia si el usuario espera cobrar intereses proporcionales
- **Medio:** No hay validación de monto máximo mencionada — a diferencia de Transferencias, que sí tiene tope de $50.000
- **Medio:** No se sabe si existen validaciones de decimales en el monto (como el caso de $50.001 en Transferencias)

---

## Dudas / puntos a verificar

| # | Duda | Impacto |
|---|---|---|
| 1 | ¿El monto a reintegrar al cancelar incluye interés generado o solo el capital? | Define expectativa del usuario — riesgo de bug de negocio si no es claro |
| 2 | ¿Existe un monto máximo para invertir en un Plazo Fijo? | Define caso límite |
| 3 | ¿La TNA es fija para todos los plazos o varía según el plazo elegido (ej. a 360 días rinde más que a 30)? | Afecta cálculo esperado de interés en los test cases |
| 4 | ¿Se puede crear más de un Plazo Fijo simultáneo desde la misma cuenta? | Define si hay límite de cantidad activa |
| 5 | ¿Qué pasa si se ingresan decimales en el monto (ej. $1000.50)? | Validación de formato |
| 6 | ¿El botón "Cancelar" del modal (tanto de creación como de cancelación) cierra sin ejecutar la acción? | A confirmar, se asume por patrón de Transferencias |

---

## Casos de prueba relacionados

*Ver `fixed-term-test-cases.md`*

---

## Bugs encontrados

*Se completará después de la ejecución*
