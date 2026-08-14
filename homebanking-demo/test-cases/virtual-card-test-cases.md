# Test Cases – Tarjetas Virtuales

## Información general

- **Elementos de la interfaz:** Dropdown de cuenta (Cuenta Corriente / Caja de Ahorro), botón "Generar nueva tarjeta", placeholder de estado vacío, card de tarjeta generada (número, vencimiento, CVV, titular, tipo), opciones "Copiar" y "Eliminar" al hover, modal de baja, estado "Activa" en sidebar
- **Reglas de negocio consideradas:**
  - Límite: 1 tarjeta virtual activa por cuenta (máximo 2 en total: Corriente y Caja de Ahorro)
  - Mensaje de éxito al generar: "✅ Tarjeta virtual generada exitosamente"
  - Mensaje de error al intentar duplicar: "❌ Esta cuenta ya posee una tarjeta virtual activa"
  - Modal de confirmación al eliminar: "Baja de tarjeta virtual"
  - Mensaje de éxito al eliminar: "Tarjeta virtual eliminada exitosamente"

---

# Casos Funcionales — Generación

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TARJ-01 | Generación exitosa de tarjeta para Cuenta Corriente | Cuenta Corriente sin tarjeta virtual activa | 1. Seleccionar "Cuenta Corriente" en el dropdown.<br>2. Click en "Generar nueva tarjeta". | Se muestra "✅ Tarjeta virtual generada exitosamente" y se despliega la tarjeta con sus datos. | Alta |
| TARJ-02 | Generación exitosa de tarjeta para Caja de Ahorro | Caja de Ahorro sin tarjeta virtual activa | 1. Seleccionar "Caja de Ahorro" en el dropdown.<br>2. Click en "Generar nueva tarjeta". | Se muestra "✅ Tarjeta virtual generada exitosamente" y se despliega la tarjeta con sus datos. | Alta |
| TARJ-03 | Visualización completa de los datos de la tarjeta generada | Tarjeta virtual generada exitosamente | 1. Observar la card de la tarjeta generada. | Se muestran correctamente: número de tarjeta, vencimiento, CVV, titular, y tipo "Visa Débito". | Alta |
| TARJ-04 | Mensaje de estado vacío antes de generar cualquier tarjeta | Ninguna tarjeta virtual generada aún | 1. Ingresar al módulo de Tarjetas Virtuales sin tarjetas activas. | Se muestra: "No tienes una tarjeta virtual activa. Genera tu tarjeta virtual para compras seguras en internet." | Media |

---

# Casos de Límite por Cuenta

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TARJ-05 | Rechazo al generar una segunda tarjeta para la misma cuenta | Cuenta ya posee una tarjeta virtual activa | 1. Seleccionar la misma cuenta que ya tiene tarjeta activa.<br>2. Click en "Generar nueva tarjeta" (si el botón está habilitado). | Se muestra: "❌ Esta cuenta ya posee una tarjeta virtual activa". No se genera una segunda tarjeta. | Alta |
| TARJ-06 | Botón "Generar nueva tarjeta" se deshabilita cuando ambas cuentas tienen tarjeta activa | Cuenta Corriente y Caja de Ahorro ya poseen su tarjeta virtual activa | 1. Generar tarjeta para ambas cuentas.<br>2. Observar el estado del botón "Generar nueva tarjeta". | El botón queda deshabilitado, sin posibilidad de generar una tercera tarjeta. | Media |
| TARJ-07 | Se puede generar tarjeta para la segunda cuenta si la primera ya tiene una | Cuenta Corriente con tarjeta activa, Caja de Ahorro sin tarjeta | 1. Seleccionar "Caja de Ahorro" en el dropdown.<br>2. Click en "Generar nueva tarjeta". | El sistema permite la generación, dado que el límite es por cuenta y no global. | Media |

---

# Casos de Acciones sobre la Tarjeta (Copiar / Eliminar)

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TARJ-08 | Opciones "Copiar" y "Eliminar" aparecen al hacer hover | Tarjeta virtual generada | 1. Posicionar el cursor sobre la card de la tarjeta (hover). | Aparecen las opciones "Copiar" y "Eliminar" sobre la tarjeta. | Baja |
| TARJ-09 | Copiar el número de tarjeta al portapapeles | Tarjeta virtual generada | 1. Hacer hover sobre la tarjeta.<br>2. Click en "Copiar". | El número de tarjeta se copia correctamente al portapapeles (verificar pegando en otro campo). | Media |

---

# Casos de Eliminación

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TARJ-10 | Eliminación exitosa de una tarjeta virtual | Tarjeta virtual activa existente | 1. Hacer hover sobre la tarjeta.<br>2. Click en "Eliminar".<br>3. Click en "Confirmar" en el modal. | Se muestra "Tarjeta virtual eliminada exitosamente" y la tarjeta desaparece de la pantalla. | Alta |
| TARJ-11 | Modal de eliminación muestra el texto de confirmación correcto | Tarjeta virtual activa existente | 1. Hacer hover sobre la tarjeta.<br>2. Click en "Eliminar". | El modal muestra: "Baja de tarjeta virtual — ¿Estás seguro que deseas eliminar esta tarjeta virtual? Se dará de baja inmediatamente." | Media |
| TARJ-12 | Cancelar la eliminación desde el modal no ejecuta la baja | Modal de eliminación abierto | 1. Click en "Eliminar" sobre una tarjeta (abre el modal).<br>2. Click en el botón "Cancelar" del modal (no en "Confirmar"). | El modal se cierra sin eliminar la tarjeta. La tarjeta sigue activa. | Media |
| TARJ-13 | Se puede generar una nueva tarjeta luego de eliminar la existente de esa cuenta | Cuenta con tarjeta eliminada recientemente | 1. Eliminar la tarjeta virtual de una cuenta.<br>2. Seleccionar la misma cuenta en el dropdown.<br>3. Click en "Generar nueva tarjeta". | El sistema permite generar una nueva tarjeta para esa cuenta sin restricciones. | Media |
| TARJ-14 | Vuelve el estado vacío tras eliminar la única tarjeta activa | Una sola tarjeta virtual activa en total | 1. Eliminar la única tarjeta virtual existente. | Se vuelve a mostrar el placeholder: "No tienes una tarjeta virtual activa. Genera tu tarjeta virtual para compras seguras en internet." | Baja |

---

# Casos de Estado en el Sidebar

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| TARJ-15 | Estado "Activa" se muestra en el sidebar tras generar una tarjeta | Ninguna tarjeta virtual generada previamente | 1. Generar una tarjeta virtual.<br>2. Observar el menú lateral, debajo de "Tarjeta Virtual". | El sidebar muestra el estado "Activa". | Media |
| TARJ-16 | Estado del sidebar tras eliminar todas las tarjetas activas *(pendiente de confirmación)* | Todas las tarjetas virtuales eliminadas | 1. Eliminar todas las tarjetas virtuales activas.<br>2. Observar el estado en el sidebar. | **No confirmado si vuelve a un estado "Inactiva" o similar.** Documentar comportamiento real como asunción de diseño. | Baja |

---

**Total de Test Cases: 16**

