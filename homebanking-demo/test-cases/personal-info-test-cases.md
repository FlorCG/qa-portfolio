# Test Cases – Mis Datos

## Información general

- **Elementos de la interfaz:** Sección de Información Personal (Nombre, DNI, Email, Teléfono, Dirección), sección de Mis Cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito con número, CBU y saldo), sección de Tarjetas (Visa Débito, Mastercard Débito, Visa Crédito con número y monto).
- **Reglas de negocio consideradas:**
  - Todos los datos mostrados son estrictamente de **solo lectura**.
  - No existen funcionalidades de modificación, actualización o eliminación en este módulo.
  - Coherencia estricta de datos financieros con el resto de la aplicación (Dashboard).

---

# Casos Funcionales — Visualización y Restricciones

# 3. Test Cases

## ESC-01 — Información Personal

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-01 | Visualización completa de los datos de Información Personal | Sesión activa en la homebanking demo | 1. Navegar al módulo "Mis Datos" desde el menú lateral.<br>2. Observar la sección "Información Personal". | Se visualizan correctamente y sin errores de formato: Nombre completo, DNI, Email, Teléfono y Dirección. Los campos no presentan valores vacíos inesperados. | Alta |
| DATOS-02 | Verificación de que los campos personales no son editables | Sesión activa en el módulo "Mis Datos" | 1. Intentar hacer clic o editar los campos de Nombre, DNI, Email, Teléfono y Dirección.<br>2. Buscar botones, iconos o controles de "Editar" o "Guardar". | Los campos son de solo lectura, no permiten edición de texto y no existen controles de modificación en la interfaz. | Alta |
| DATOS-03 | Verificación de ausencia de opción para eliminar datos personales | Sesión activa en el módulo "Mis Datos" | 1. Inspeccionar la sección "Información Personal".<br>2. Buscar botones, iconos o menús contextuales asociados a los datos personales. | No existe ninguna opción disponible para eliminar los datos personales. | Media |

---

## ESC-02 — Mis Cuentas

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-04 | Visualización de Cuenta Corriente | Sesión activa en el módulo "Mis Datos" | 1. Navegar a la sección "Mis Cuentas".<br>2. Observar la card de "Cuenta Corriente". | Se muestra correctamente el número de cuenta, CBU y monto/saldo, con valores no vacíos y formato válido. El CBU posee 22 dígitos numéricos. | Alta |
| DATOS-05 | Visualización de Caja de Ahorro | Sesión activa en el módulo "Mis Datos" | 1. Navegar a la sección "Mis Cuentas".<br>2. Observar la card de "Caja de Ahorro". | Se muestra correctamente el número de cuenta, CBU y monto/saldo, con valores no vacíos y formato válido. | Alta |
| DATOS-06 | Visualización de Tarjeta de Crédito en la sección "Mis Cuentas" | Sesión activa en el módulo "Mis Datos" | 1. Navegar a la sección "Mis Cuentas".<br>2. Observar la card de "Tarjeta de Crédito". | Se muestran correctamente el número, CBU y monto/saldo asociados. | Alta |
| DATOS-07 | Validación del formato de CBU en las tres cuentas | Sesión activa en el módulo "Mis Datos" | 1. Registrar el CBU de Cuenta Corriente.<br>2. Registrar el CBU de Caja de Ahorro.<br>3. Registrar el CBU de Tarjeta de Crédito.<br>4. Comparar los tres valores. | Cada CBU posee 22 dígitos numéricos y los valores son únicos entre las cuentas. | Media |
| DATOS-08 | Validación del formato de monto en las tres cuentas | Sesión activa en el módulo "Mis Datos" | 1. Observar el monto de cada cuenta.<br>2. Verificar símbolo de moneda, separadores y valor mostrado. | Los montos utilizan un formato de moneda válido, sin caracteres inválidos ni valores negativos inesperados. | Media |
| DATOS-09 | Verificación de que los datos de las cuentas no son editables ni eliminables | Sesión activa en el módulo "Mis Datos" | 1. Intentar interactuar con el número de cuenta, CBU y monto de cada cuenta.<br>2. Buscar controles de edición o eliminación. | Los datos son de solo lectura y no existen opciones para modificarlos o eliminarlos. | Alta |

---

## ESC-03 — Mis Tarjetas

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-10 | Visualización de Visa Débito | Sesión activa en el módulo "Mis Datos" | 1. Navegar a la sección "Mis Tarjetas".<br>2. Observar la card "Visa Débito". | Se muestra el número de tarjeta con formato válido. *(A confirmar con Negocio si corresponde mostrar también un monto/saldo).* | Alta |
| DATOS-11 | Visualización de Mastercard Débito | Sesión activa en el módulo "Mis Datos" | 1. Navegar a la sección "Mis Tarjetas".<br>2. Observar la card "Mastercard Débito". | Se muestra el número de tarjeta con formato válido. *(A confirmar con Negocio si corresponde mostrar también un monto/saldo).* | Alta |
| DATOS-12 | Visualización de Visa Crédito | Sesión activa en el módulo "Mis Datos" | 1. Navegar a la sección "Mis Tarjetas".<br>2. Observar la card "Visa Crédito". | Se muestran el número de tarjeta y el monto/saldo, ambos con valores no vacíos y formato válido. | Alta |
| DATOS-13 | Validación del formato de los números de tarjeta | Sesión activa en el módulo "Mis Datos" | 1. Registrar los números de Visa Débito, Mastercard Débito y Visa Crédito.<br>2. Verificar el formato de cada número.<br>3. Comparar los tres valores. | Cada número respeta el formato esperado de tarjeta (16 dígitos, agrupados de a 4) y los números son diferentes entre sí. | Media |
| DATOS-14 | Verificación de ausencia de monto en tarjetas de débito | Sesión activa en el módulo "Mis Datos" | 1. Observar las cards de Visa Débito y Mastercard Débito.<br>2. Verificar si muestran monto o saldo. | **A confirmar:** Actualmente no se observa monto en las tarjetas de débito. Registrar el hallazgo para validar con Producto si corresponde al comportamiento esperado o constituye un defecto. | Alta |
| DATOS-15 | Verificación de que los datos de tarjetas no son editables ni eliminables | Sesión activa en el módulo "Mis Datos" | 1. Intentar interactuar con el número y monto de cada tarjeta.<br>2. Buscar botones, iconos o acciones de edición/eliminación. | No se habilita ninguna opción de edición, modificación, eliminación o baja de las tarjetas. | Alta |

---

## ESC-04 — Inmutabilidad General

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-16 | Verificación de ausencia de botones de edición o eliminación en toda la pantalla | Sesión activa en el módulo "Mis Datos" | 1. Recorrer visualmente las secciones "Información Personal", "Mis Cuentas" y "Mis Tarjetas".<br>2. Buscar botones, iconos, enlaces o controles de edición y eliminación. | No existe ningún control que permita editar, eliminar o modificar información dentro del módulo "Mis Datos". | Alta |
| DATOS-17 | Verificación de comportamiento ante acceso directo a una supuesta ruta de edición | Sesión activa en el módulo "Mis Datos" | 1. Intentar acceder mediante URL directa a una posible ruta de edición, por ejemplo `/mis-datos/editar`, si existe un patrón conocido.<br>2. Observar el comportamiento de la aplicación. | La aplicación no expone una funcionalidad de edición no soportada por la interfaz. Debe redirigir, mostrar un error controlado o impedir el acceso. | Baja |

---

## ESC-05 — Consistencia de Datos entre Módulos

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-18 | Comparación del número de Cuenta Corriente entre Dashboard y Mis Datos | Sesión activa y acceso a Dashboard y "Mis Datos" | 1. Ingresar al Dashboard y registrar el número de Cuenta Corriente.<br>2. Ingresar a "Mis Datos" y registrar el número de Cuenta Corriente.<br>3. Comparar ambos valores. | Los números deberían coincidir al representar la misma cuenta del usuario. **Resultado observado:** No coinciden (ver O1). | Alta |
| DATOS-19 | Comparación del número de Caja de Ahorro entre Dashboard y Mis Datos | Sesión activa y acceso a Dashboard y "Mis Datos" | 1. Ingresar al Dashboard y registrar el número de Caja de Ahorro.<br>2. Ingresar a "Mis Datos" y registrar el número de Caja de Ahorro.<br>3. Comparar ambos valores. | Los números deberían coincidir al representar la misma cuenta del usuario. **Resultado observado:** No coinciden (ver O1). | Alta |
| DATOS-20 | Comparación del número de Tarjeta de Crédito entre Dashboard y Mis Datos | Sesión activa y acceso a Dashboard y "Mis Datos" | 1. Registrar el número de Tarjeta de Crédito mostrado en el Dashboard.<br>2. Registrar el número mostrado en "Mis Datos" dentro de "Mis Cuentas".<br>3. Comparar ambos valores. | Los números deberían coincidir al representar la misma tarjeta/cuenta del usuario. **Resultado observado:** No coinciden (ver O1). | Alta |
| DATOS-21 | Comparación de Visa Crédito entre Dashboard y Mis Tarjetas | Sesión activa y acceso a Dashboard y "Mis Datos" | 1. Registrar número y monto de la tarjeta de crédito en el Dashboard.<br>2. Registrar número y monto de "Visa Crédito" en "Mis Tarjetas".<br>3. Comparar ambos valores. | Los datos deberían coincidir entre ambas pantallas. **Resultado observado:** Los datos coinciden. | Alta |
| DATOS-22 | Determinación de relación entre tarjetas de débito y cuentas del Dashboard | Sesión activa y acceso a Dashboard y "Mis Datos" | 1. Registrar los números de Visa Débito y Mastercard Débito en "Mis Datos".<br>2. Compararlos con los números visibles en el Dashboard (Cuenta Corriente, Caja de Ahorro y Tarjeta de Crédito). | Debería poder identificarse una relación clara entre las tarjetas de débito y las cuentas correspondientes. **Resultado observado:** No se identifica una relación clara (ver O2). | Alta |
| DATOS-23 | Verificación de unicidad de CBU entre las cuentas | Sesión activa en el módulo "Mis Datos" | 1. Registrar los tres CBU mostrados en "Mis Cuentas".<br>2. Comparar los valores entre sí. | Los tres CBU son diferentes entre sí y no existen duplicados. | Media |

---

## ESC-06 — Navegación y Acceso

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-24 | Acceso al módulo "Mis Datos" desde el menú principal | Usuario autenticado en la aplicación | 1. Ingresar al homebanking.<br>2. Hacer clic en la opción "Mis Datos" del menú lateral. | Se accede correctamente al módulo y se cargan todas sus secciones sin pantalla en blanco ni errores visibles. | Alta |
| DATOS-25 | Verificación del tiempo de carga del módulo "Mis Datos" | Usuario autenticado con acceso al módulo | 1. Ingresar a "Mis Datos".<br>2. Medir el tiempo hasta que se muestran todos los datos. | La información se carga en un tiempo razonable (ej. menor a 3 segundos), sin secciones vacías inesperadamente ni estados de carga infinitos. | Media |
| DATOS-26 | Verificación de navegación de salida y reingreso al módulo | Sesión activa en "Mis Datos" | 1. Navegar desde "Mis Datos" hacia otra sección, por ejemplo Dashboard.<br>2. Volver a ingresar a "Mis Datos".<br>3. Comparar la información mostrada. | La navegación funciona correctamente y los datos se mantienen o recargan de forma consistente. | Media |

---

## ESC-07 — Responsividad y UI

| ID | Título | Precondición | Pasos | Resultado Esperado | Prioridad |
|---|---|---|---|---|---|
| DATOS-27 | Verificación de visualización en resolución de escritorio | Sesión activa en "Mis Datos" | 1. Acceder al módulo desde un navegador de escritorio con resolución aproximada de 1920x1080.<br>2. Recorrer todas las secciones. | Todas las secciones se visualizan correctamente, sin solapamientos, elementos cortados ni problemas de alineación. | Media |
| DATOS-28 | Verificación de visualización en resolución mobile | Sesión activa en "Mis Datos" | 1. Acceder al módulo utilizando un viewport mobile, por ejemplo 375x667.<br>2. Recorrer todas las secciones. | Las secciones se adaptan correctamente al viewport, utilizando distribución vertical cuando corresponda, sin overflow horizontal ni textos cortados. | Media |
| DATOS-29 | Verificación de legibilidad y truncamiento de textos largos | Sesión activa en "Mis Datos" | 1. Observar campos que pueden contener información extensa, como Dirección, Email y Nombre completo.<br>2. Verificar su comportamiento ante textos largos. | El contenido se muestra completo o se trunca correctamente con "..." sin romper el layout ni superponerse con otros elementos. | Baja |

---

**Total de Test Cases: 6**
