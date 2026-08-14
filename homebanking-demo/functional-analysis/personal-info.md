# Análisis Funcional — Mis Datos

**Módulo:** Mis Datos
**Prioridad:** Media

> Este análisis está basado en la exploración de la aplicación. No existe documentación oficial de requisitos — los comportamientos esperados fueron inferidos a partir del comportamiento observado.

---

## Objetivo

Mostrar al usuario su información personal y el detalle de sus cuentas y tarjetas asociadas, en modo de solo lectura (sin posibilidad de edición ni eliminación).

---

## Elementos de la interfaz

| Elemento | Tipo | Descripción |
|---|---|---|
| Subtítulo | Texto | "Información personal y cuentas" |
| Sección "Información Personal" | Bloque de datos | Nombre completo, DNI, email, teléfono, dirección |
| Sección "Mis Cuentas" | Lista de cards | Cuenta Corriente, Caja de Ahorro y Tarjeta de Crédito — cada una con número de cuenta, CBU y monto |
| Sección de Tarjetas | Lista de cards | Visa Débito, Mastercard Débito y Visa Crédito — con número y monto |

---

## Reglas de negocio

- Todos los datos mostrados son de solo lectura: no se pueden modificar ni eliminar desde este módulo
- La sección "Mis Cuentas" muestra número de cuenta, CBU y monto para las 3 cuentas del usuario
- La sección de Tarjetas muestra 3 tarjetas: Visa Débito, Mastercard Débito y Visa Crédito

---

## Inconsistencias detectadas (hallazgo de exploración)

- **Los números de cuenta mostrados en "Mis Cuentas" no coinciden con los números mostrados en el Dashboard**, para las mismas cuentas (Cuenta Corriente y Caja de Ahorro) *(inconsistencia de datos — a reportar como bug)*
- **Solo la tarjeta "Visa Crédito" de la sección de Tarjetas parece corresponder con la Tarjeta de Crédito real del Dashboard.** Las otras dos (Visa Débito y Mastercard Débito) no tienen monto asociado y no está claro con qué producto real del usuario se relacionan — sus números no parecen vincularse a ninguna cuenta o tarjeta conocida
- No está claro si esta sección de Tarjetas representa datos de ejemplo/placeholder sin funcionalidad real, o si hay una relación no evidente con otros módulos (ej. las Tarjetas Virtuales generadas)

---

## Flujo principal — Visualización

1. Usuario navega a "Mis Datos"
2. El sistema muestra la información personal (nombre, DNI, email, teléfono, dirección)
3. El sistema muestra la sección "Mis Cuentas" con los datos de las 3 cuentas
4. El sistema muestra la sección de Tarjetas con las 3 tarjetas listadas
5. Ningún dato es editable ni eliminable desde esta pantalla

---

## Riesgos detectados

- **Alto:** La inconsistencia de números de cuenta entre "Mis Datos" y el Dashboard es un bug de integridad de datos — en un entorno real, este tipo de discrepancia generaría desconfianza grave en el usuario (¿cuál número es el "real"?)
- **Medio:** La falta de claridad sobre a qué se relacionan "Visa Débito" y "Mastercard Débito" sugiere que podrían ser datos de placeholder no conectados a lógica real, lo cual debería confirmarse antes de diseñar test cases que asuman una relación funcional inexistente
- **Bajo:** Al ser una sección de solo lectura, el riesgo funcional es menor que en los módulos transaccionales, pero el riesgo de "datos incorrectos mostrados al usuario" es igual de importante de testear

---

## Dudas / puntos a verificar

| # | Duda | Impacto |
|---|---|---|
| 1 | ¿Por qué los números de cuenta no coinciden entre Mis Datos y Dashboard? | Definir si es un bug de datos mockeados mal sincronizados, y reportarlo como tal |
| 2 | ¿A qué corresponden realmente "Visa Débito" y "Mastercard Débito"? ¿Son datos de ejemplo sin relación funcional? | Define si corresponde testear su contenido o solo su presencia visual |
| 3 | ¿El CBU mostrado en Mis Datos coincide con algún otro dato visible en la aplicación (ej. el usado para recibir transferencias de terceros)? | Relevante para testing cruzado con el módulo Transferencias |
| 4 | ¿Existe alguna otra sección de la app donde estos datos personales se puedan editar (fuera de alcance de este módulo)? | Confirmar que "solo lectura" es una decisión de diseño y no una funcionalidad faltante |

---

## Casos de prueba relacionados

*Ver `test-cases-mis-datos.md`*

---

## Bugs encontrados

- **BUG-DATOS-01:** Los números de cuenta mostrados en "Mis Datos" no coinciden con los mostrados en el Dashboard para las mismas cuentas (Cuenta Corriente, Caja de Ahorro). Pendiente de reproducir y documentar formalmente con capturas al momento de la ejecución.
