# Análisis Funcional — Mis Datos

**Módulo:** Mis Datos  
**Prioridad:** Media / Alta (Módulo crítico de visualización de PII e información financiera)

> Este análisis está basado en la exploración de la aplicación demo. Al tratarse de un entorno de pruebas, se evalúan tanto los comportamientos esperados de diseño como las inconsistencias detectadas en los datos expuestos.

---

## Objetivo

Permitir al usuario visualizar de manera centralizada su información personal de contacto, sus cuentas bancarias asociadas con sus respectivos saldos y CBU, y las tarjetas vinculadas a su perfil, garantizando la seguridad mediante la restricción de modificación o eliminación directa desde esta vista.

---

## Elementos de la interfaz

| Elemento | Tipo | Descripción |
|---|---|---|
| Subtítulo / Encabezado | Texto | "Información personal y cuentas" (o similar según diseño de la vista) |
| Sección 1: Información personal | Bloque de texto/campos | Muestra Nombre completo, DNI, Email, Teléfono y Dirección |
| Sección 2: Mis cuentas | Bloque de cards/listado | Muestra Cuenta Corriente, Caja de Ahorro y Tarjeta de Crédito, incluyendo número de cuenta, CBU y monto/saldo |
| Sección 3: Tarjetas | Bloque de cards/listado | Muestra Visa Débito, Mastercard Débito y Visa Crédito (con números y montos, sujeto a inconsistencias detectadas) |
| Restricción de permisos | Comportamiento UI | Todos los campos son estáticos (no editables, sin botones de acción, modificación o baja) |

---

## Reglas de negocio

- **Solo Lectura (Read-Only):** Ninguno de los datos mostrados en el módulo (información personal, cuentas, tarjetas) puede ser modificado, editado o eliminado desde esta interfaz.
- **Trazabilidad y Consistencia de Datos:** Los datos financieros (cuentas, tarjetas y saldos) deben mantener estricta coherencia y sincronización con la información mostrada en el Dashboard principal de la aplicación.
- **Estructura de Datos Personales:** Debe reflejar de forma fidedigna la PII (*Personally Identifiable Information*) del cliente autenticado.

---

## Flujos

### Flujo principal — Visualización de Mis Datos
1. El usuario navega al módulo "Mis Datos" desde el menú lateral o navegación principal.
2. El sistema recupera y renderiza la información personal del usuario (Nombre, DNI, Email, Teléfono, Dirección).
3. El sistema renderiza el listado de cuentas asociadas con sus respectivos saldos y CBU.
4. El sistema renderiza el listado de tarjetas asociadas al perfil.
5. El usuario visualiza la información de manera estática sin opciones de alteración.

---

## Riesgos detectados

- **Alto (Inconsistencia de Datos):** Los números de cuenta mostrados en la sección "Mis cuentas" no coinciden con los números expuestos inicialmente en el Dashboard principal. Esto genera confusión de trazabilidad para el usuario.
- **Medio (Ambigüedad en la sección de Tarjetas):** Las tarjetas de débito (Visa y Mastercard Débito) no muestran monto y sus números no guardan relación evidente con otras secciones. Falta claridad sobre su propósito o vinculación real.
- **Bajo (Falta de feedback de solo lectura):** Al no haber tooltips o aclaraciones de que los datos no son editables, un usuario podría intentar hacer clic en los campos esperando un flujo de edición de perfil.

---

## Dudas / puntos a verificar

| # | Duda | Impacto |
|---|---|---|
| 1 | ¿Por qué los números de cuenta en "Mis Datos" difieren de los mostrados en el Dashboard? | Alto — Posible bug de mock data o mapeo incorrecto de endpoints. |
| 2 | ¿A qué corresponden las tarjetas de débito que no tienen monto ni relación con el Dashboard? | Medio — Puede ser funcionalidad incompleta, datos de prueba residuales o requerimiento no especificado. |
| 3 | ¿Existe un canal o redirección prevista para modificar datos de contacto (ej. teléfono o email) si estuviera en producción? | Bajo — Define si el módulo requiere enlaces a soporte o configuración de perfil. |
