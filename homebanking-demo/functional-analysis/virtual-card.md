# Análisis Funcional — Tarjetas Virtuales

**Módulo:** Tarjetas Virtuales
**Prioridad:** Media

> Este análisis está basado en la exploración de la aplicación. No existe documentación oficial de requisitos — los comportamientos esperados fueron inferidos a partir del comportamiento observado.

---

## Objetivo

Permitir al usuario generar tarjetas de débito virtuales asociadas a sus cuentas (Cuenta Corriente o Caja de Ahorro), para uso en compras online, con un límite de 1 tarjeta activa por cuenta.

---

## Elementos de la interfaz

| Elemento | Tipo | Descripción |
|---|---|---|
| Subtítulo | Texto | "Genera tarjetas de débito virtuales para compras online" |
| Dropdown de cuenta | Dropdown | Permite elegir la cuenta (Cuenta Corriente / Caja de Ahorro) a la que se sincronizará la nueva tarjeta |
| Aclaración de límite | Texto | "Límite: 1 tarjeta virtual activa por cuenta (Caja de Ahorro / Cta Cte)" |
| Botón "Generar nueva tarjeta" | Botón | Genera la tarjeta virtual para la cuenta seleccionada |
| Placeholder de estado vacío | Texto | "No tienes una tarjeta virtual activa. Genera tu tarjeta virtual para compras seguras en internet." |
| Tarjeta generada | Card | Muestra número de tarjeta, vencimiento, CVV, titular, tipo (Visa Débito) |
| Opciones al hover | Iconos/botones | "Copiar" (copia el número de tarjeta) y "Eliminar" |
| Modal de eliminación | Modal | "Baja de tarjeta virtual", pregunta de confirmación, botones Cancelar / Confirmar |
| Estado en sidebar | Texto/indicador | Debajo de "Tarjeta Virtual" en el menú lateral, muestra "Activa" cuando hay al menos una tarjeta generada |

---

## Reglas de negocio

- Límite: 1 tarjeta virtual activa por cuenta (es decir, hasta 2 tarjetas en total: una por Cuenta Corriente y una por Caja de Ahorro)
- Al generar una tarjeta, se muestra: "✅ Tarjeta virtual generada exitosamente"
- La tarjeta generada muestra: número de tarjeta, fecha de vencimiento, CVV, titular, y tipo (Visa Débito)
- Si se intenta generar una segunda tarjeta para una cuenta que ya tiene una activa, se muestra: "❌ Esta cuenta ya posee una tarjeta virtual activa"
- El botón "Generar nueva tarjeta" se deshabilita cuando ambas cuentas ya tienen su tarjeta virtual activa
- Al hacer hover sobre una tarjeta, aparecen dos opciones: "Copiar" (copia el número de tarjeta al portapapeles) y "Eliminar"
- Al eliminar, se abre un modal de confirmación: "Baja de tarjeta virtual — ¿Estás seguro que deseas eliminar esta tarjeta virtual? Se dará de baja inmediatamente."
- Al confirmar la eliminación, se muestra: "Tarjeta virtual eliminada exitosamente" y la tarjeta desaparece de la pantalla
- El menú lateral (sidebar) muestra el estado "Activa" debajo de "Tarjeta Virtual" cuando existe al menos una tarjeta generada

---

## Flujo principal — Generar Tarjeta Virtual

1. Usuario selecciona una cuenta (Cuenta Corriente o Caja de Ahorro) en el dropdown
2. Usuario hace click en "Generar nueva tarjeta"
3. El sistema genera la tarjeta y muestra: "✅ Tarjeta virtual generada exitosamente"
4. La tarjeta se muestra con sus datos completos (número, vencimiento, CVV, titular, tipo)
5. El sidebar actualiza el estado de "Tarjeta Virtual" a "Activa"

---

## Flujo principal — Eliminar Tarjeta Virtual

1. Usuario hace hover sobre una tarjeta generada
2. Aparecen las opciones "Copiar" y "Eliminar"
3. Usuario hace click en "Eliminar"
4. Se abre el modal: "Baja de tarjeta virtual — ¿Estás seguro que deseas eliminar esta tarjeta virtual? Se dará de baja inmediatamente."
5. Usuario hace click en "Confirmar"
6. Se muestra: "Tarjeta virtual eliminada exitosamente" y la tarjeta desaparece de la pantalla

---

## Flujos alternativos / excepciones

**Intento de generar una segunda tarjeta para una cuenta que ya tiene una activa**
- Muestra: "❌ Esta cuenta ya posee una tarjeta virtual activa"
- No se genera la tarjeta

**Ambas cuentas ya poseen tarjeta activa**
- El botón "Generar nueva tarjeta" queda deshabilitado
- No se puede iniciar una nueva generación hasta eliminar alguna existente

**Cancelar eliminación desde el modal**
- Se espera que el botón "Cancelar" cierre el modal sin ejecutar la baja *(comportamiento asumido por patrón de otros módulos, a confirmar)*

**Estado vacío inicial**
- Antes de generar cualquier tarjeta, se muestra el placeholder: "No tienes una tarjeta virtual activa. Genera tu tarjeta virtual para compras seguras en internet."

---

## Riesgos detectados

- **Medio:** No se verificó si el estado "Activa" del sidebar distingue entre "una tarjeta activa" y "dos tarjetas activas", o si vuelve a un estado distinto cuando se eliminan todas las tarjetas
- **Bajo:** No se verificó si el número de tarjeta y CVV se muestran completos siempre, o si existe alguna opción de ocultar (como el botón "Ocultar" visto en Dashboard) — no se detectó tal opción en la exploración
- **Bajo:** No se verificó el comportamiento exacto del botón "Cancelar" del modal de eliminación

---

## Dudas / puntos a verificar

| # | Duda | Impacto |
|---|---|---|
| 1 | ¿El botón "Cancelar" del modal de eliminación cierra sin ejecutar la baja? | A confirmar, se asume por patrón de otros módulos |
| 2 | ¿Qué muestra el sidebar cuando se eliminan todas las tarjetas activas (vuelve a un estado "Inactiva" o similar)? | Define comportamiento de sincronización de estado |
| 3 | ¿El número de tarjeta y CVV se muestran siempre visibles, sin opción de ocultar? | Confirmar ausencia de esa funcionalidad, dado que si en Dashboard existe "Ocultar" para cuentas, podría esperarse algo similar acá |
| 4 | ¿La fecha de vencimiento de la tarjeta se calcula de alguna forma (ej. +5 años desde la generación), o es un valor fijo de la demo? | Relevante si se quiere validar el dato mostrado |

---

## Casos de prueba relacionados

*Ver `test-cases-tarjetas-virtuales.md`*

---

## Bugs encontrados

*Se completará después de la ejecución*

