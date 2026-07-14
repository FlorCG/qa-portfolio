# Análisis Funcional Login  

**Módulo:** Login  
**Prioridad:** Alta  

> Este análisis está basado en la exploración de la aplicación. No existe documentación oficial de requisitos — los comportamientos esperados fueron inferidos a partir del comportamiento observado y estándares de usabilidad.

--- 

## Objetivo  
Permitir la autenticación segura del usuario en el sistema mediante credenciales. Es el punto de entrada a la aplicación y controla el acceso a todas las funcionalidades protegidas.  

---

## Elementos de la interfaz
| Elemento | Tipo | Descripción |
|---|---|---|
| Usuario | Campo de texto | Ingreso del nombre de usuario |
| Contraseña | Campo de texto (enmascarado) | Ingreso de la contraseña |
| Recordarme | Checkbox | Opción para mantener la sesión activa |
| Ingresar | Botón | Envía el formulario y ejecuta la autenticación |

---  

## Reglas de negocio  

- La autenticación requiere usuario y contraseña válidos
- La cuenta se bloquea luego de 3 intentos fallidos consecutivos
- El bloqueo muestra un mensaje diferente: "Tu cuenta ha sido bloqueada temporalmente. Contacta con soporte."
- Una cuenta con estado bloqueado (credencial `locked`) muestra el mismo mensaje de bloqueo
- El checkbox "Recordarme" debería mantener la sesión activa entre sesiones *(a confirmar)*
- Si el usuario intenta acceder al Dashboard o a cualquier otra sección sin haber iniciado sesión, el sistema lo redirige automáticamente al Login

---

## Flujo principal  
1. Usuario accede a la página de login
2. Ingresa usuario y contraseña válidos
3. Hace click en "Ingresar"
4. El sistema valida las credenciales
5. Redirige al Dashboard
6. La sesión queda activa

---  

## Flujos alternativos/excepciones  
**Credenciales inválidas (intentos dentro del límite)**
- El sistema muestra: *"Usuario o contraseña incorrectos. Intentos restantes: X"*
- El contador comienza en 2 (máximo 3 intentos)
- El usuario puede reintentar

**Cuenta bloqueada por intentos fallidos**
- Tras agotar los 3 intentos, el sistema muestra: *"Demasiados intentos fallidos. Tu cuenta ha sido bloqueada."*
- En el cuarto intento el mensaje cambia a: *"Tu cuenta ha sido bloqueada temporalmente. Contacta con soporte."*

**Cuenta bloqueada (credencial locked)**
- Al ingresar con usuario `locked`, el sistema muestra directamente: *"Tu cuenta ha sido bloqueada temporalmente. Contacta con soporte."*

**Campos vacíos o inválidos**
- Validación de campos obligatorios *(a verificar si es antes de enviar o después)*
- Comportamiento esperado: mensaje de error indicando campos requeridos

**Acceso a ruta protegida sin sesión**
- Si el usuario intenta acceder al Dashboard sin estar logueado, el sistema redirige al Login
---

## Validaciones identificadas  
| Campo | Validación |
|---|---|
| Usuario | Obligatorio |
| Contraseña | Obligatoria, enmascarada |

---

- Es el único punto de acceso a la app — si falla, bloquea todo lo demás
- El manejo de intentos fallidos y bloqueo es crítico desde el punto de vista de seguridad
- Los mensajes de error inconsistentes (cambio entre cuarto intento) pueden confundir al usuario
- La persistencia de la sesión con "Recordarme" no es clara en esta app demo

---

## Dudas / puntos a verificar  
| # | Duda | Impacto |
|---|---|---|
| 1 | ¿El bloqueo por intentos es permanente o se resetea con el tiempo? | Define si hay caso de desbloqueo |
| 2 | ¿La inconsistencia en el mensaje de bloqueo (cambio en cuarto intento) es intencional? | Posible bug a reportar |
| 3 | ¿El checkbox "Recordarme" tiene efecto real en esta app demo? | Define si se puede testear |
| 4 | ¿La validación de campos vacíos ocurre antes de enviar o después? | Caso negativo importante |
| 5 | ¿Al hacer logout se destruye la sesión completamente o solo se redirige? | Validación de seguridad |

---

## Casos de prueba relacionados  
*Se completará después de escribir los test cases*

---

## Bugs encontrados
*Se completará después de la ejecución*


