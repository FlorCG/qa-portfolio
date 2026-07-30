# Test Cases – Login

## Información general

- **Campos:** Usuario (texto), Contraseña (texto enmascarado), Checkbox "Recordarme", botón Ingresar
- **Reglas de negocio consideradas:**
  - Requiere usuario y contraseña válidos para autenticar.
  - Se bloquea la cuenta tras 3 intentos fallidos consecutivos.
  - Al bloquearse, se muestra el mensaje: `Tu cuenta ha sido bloqueada temporalmente. Contacta con soporte.`
  - Una cuenta con credencial `locked` muestra el mismo mensaje de bloqueo, sin necesidad de fallar intentos.
  - El checkbox "Recordarme" debería mantener sesión activa entre sesiones (**a confirmar — pendiente de definición**).
  - Si se intenta acceder al Dashboard u otra sección sin login, redirige automáticamente a Login.

---

## Casos de prueba

| ID | Título | Precondición | Pasos | Resultado esperado | Prioridad |
|----|--------|--------------|-------|---------------------|-----------|
| TC-01 | Login exitoso con credenciales válidas | Usuario existente, cuenta activa (no bloqueada) | 1. Ingresar a la pantalla de Login.<br>2. Completar campo Usuario con credencial válida.<br>3. Completar campo Contraseña con credencial válida.<br>4. Hacer clic en "Ingresar". | El sistema autentica correctamente y redirige al Dashboard. | Alta |
| TC-02 | Login fallido con contraseña incorrecta | Usuario existente, cuenta activa | 1. Ingresar a la pantalla de Login.<br>2. Completar Usuario con credencial válida.<br>3. Completar Contraseña con valor incorrecto.<br>4. Hacer clic en "Ingresar". | El sistema no autentica. Se muestra mensaje de error genérico (credenciales inválidas). No redirige al Dashboard. | Alta |
| TC-03 | Login fallido con usuario inexistente | No existe el usuario ingresado | 1. Ingresar a la pantalla de Login.<br>2. Completar Usuario con un valor no registrado.<br>3. Completar Contraseña con cualquier valor.<br>4. Hacer clic en "Ingresar". | El sistema no autentica. Se muestra mensaje de error genérico, sin indicar si el usuario existe o no. | Alta |
| TC-04 | Login fallido con campos vacíos | Cuenta activa | 1. Ingresar a la pantalla de Login.<br>2. Dejar Usuario y Contraseña vacíos.<br>3. Hacer clic en "Ingresar". | El sistema no permite el envío o muestra validación indicando que los campos son obligatorios. | Media |
| TC-05 | Login fallido con solo un campo completo (Usuario sin Contraseña) | Cuenta activa | 1. Ingresar a la pantalla de Login.<br>2. Completar solo Usuario válido.<br>3. Dejar Contraseña vacía.<br>4. Hacer clic en "Ingresar". | El sistema muestra validación de campo obligatorio y no autentica. | Media |
| TC-06 | Login fallido con solo un campo completo (Contraseña sin Usuario) | Cuenta activa | 1. Ingresar a la pantalla de Login.<br>2. Dejar Usuario vacío.<br>3. Completar solo Contraseña válida.<br>4. Hacer clic en "Ingresar". | El sistema muestra validación de campo obligatorio y no autentica. | Media |
| TC-07 | Bloqueo de cuenta tras 3 intentos fallidos consecutivos | Cuenta activa, no bloqueada previamente | 1. Ingresar Usuario válido.<br>2. Ingresar Contraseña incorrecta y hacer clic en "Ingresar" (intento 1).<br>3. Repetir con Contraseña incorrecta (intento 2).<br>4. Repetir con Contraseña incorrecta (intento 3). | Tras el tercer intento fallido consecutivo, la cuenta se bloquea y se muestra el mensaje: "Tu cuenta ha sido bloqueada temporalmente. Contacta con soporte." | Alta |
| TC-08 | Intento de login luego del bloqueo por intentos fallidos | Cuenta bloqueada tras 3 intentos fallidos (ver TC-07) | 1. Ingresar Usuario de la cuenta bloqueada.<br>2. Ingresar Contraseña correcta.<br>3. Hacer clic en "Ingresar". | El sistema no permite el acceso, aunque las credenciales sean correctas, y muestra el mensaje de cuenta bloqueada. | Alta |
| TC-09 | Reinicio del contador de intentos fallidos tras login exitoso | Cuenta activa, con 1 o 2 intentos fallidos previos (sin llegar al bloqueo) | 1. Realizar 1 o 2 intentos fallidos.<br>2. Realizar un login exitoso con credenciales correctas.<br>3. Verificar que la cuenta no quede bloqueada en intentos posteriores. | El contador de intentos fallidos se reinicia tras un login exitoso; la cuenta no se bloquea con intentos fallidos posteriores acumulados de antes del login exitoso. | Media |
| TC-10 | Cuenta ya marcada como `locked` sin intentos fallidos previos | Cuenta con credencial de estado `locked` configurada de antemano | 1. Ingresar Usuario cuya cuenta está en estado `locked`.<br>2. Ingresar cualquier Contraseña (correcta o incorrecta).<br>3. Hacer clic en "Ingresar". | El sistema muestra el mensaje: "Tu cuenta ha sido bloqueada temporalmente. Contacta con soporte." sin necesidad de que se hayan producido intentos fallidos. | Alta |
| TC-11 | Cuenta `locked` con credenciales correctas | Cuenta con credencial de estado `locked` | 1. Ingresar Usuario en estado `locked`.<br>2. Ingresar la Contraseña correcta.<br>3. Hacer clic en "Ingresar". | El sistema no autentica pese a que la contraseña es correcta; se muestra el mensaje de cuenta bloqueada. | Alta |
| TC-12 | Redirección automática al Login al acceder al Dashboard sin sesión | Usuario sin sesión iniciada (no logueado) | 1. Sin iniciar sesión, intentar acceder directamente a la URL/ruta del Dashboard.<br>2. Observar comportamiento del sistema. | El sistema redirige automáticamente a la pantalla de Login, sin mostrar contenido del Dashboard. | Alta |
| TC-13 | Redirección automática al Login al acceder a otra sección protegida sin sesión | Usuario sin sesión iniciada | 1. Sin iniciar sesión, intentar acceder directamente a la URL/ruta de otra sección protegida (ej. Transferencias, Perfil).<br>2. Observar comportamiento del sistema. | El sistema redirige automáticamente a la pantalla de Login, sin exponer contenido de la sección protegida. | Alta |
| TC-14 | Acceso a sección protegida tras expiración o cierre de sesión | Usuario con sesión previamente iniciada y luego cerrada/expirada | 1. Iniciar sesión correctamente.<br>2. Cerrar sesión (o esperar expiración de la misma).<br>3. Intentar acceder nuevamente al Dashboard u otra sección protegida usando la URL directa. | El sistema detecta que no hay sesión activa y redirige a Login. | Media |
| TC-15 | Checkbox "Recordarme" mantiene la sesión entre sesiones del navegador | Cuenta activa, válida | 1. Marcar el checkbox "Recordarme".<br>2. Completar Usuario y Contraseña válidos.<br>3. Hacer clic en "Ingresar".<br>4. Cerrar el navegador (o la pestaña) por completo.<br>5. Volver a abrir el navegador y acceder a la URL de la app. | **Pendiente de confirmación.** Comportamiento esperado no definido por el equipo funcional; se requiere definición de negocio antes de validar (¿debería mantener la sesión activa sin requerir nuevo login?). | Baja |
| TC-16 | Login sin marcar el checkbox "Recordarme" | Cuenta activa, válida | 1. Dejar el checkbox "Recordarme" sin marcar.<br>2. Completar Usuario y Contraseña válidos.<br>3. Hacer clic en "Ingresar".<br>4. Cerrar el navegador por completo.<br>5. Volver a abrir el navegador y acceder a la URL de la app. | **Pendiente de confirmación.** Se espera, como comportamiento estándar, que la sesión no se mantenga y se solicite nuevo login; a validar con el equipo funcional. | Baja |

---

## Notas 

- Los casos **TC-15** y **TC-16** dependen de una definición de negocio pendiente sobre el comportamiento del checkbox "Recordarme". No deben ejecutarse como PASS/FAIL hasta contar con dicha definición; se recomienda documentarlos como **bloqueados** en el gestor de test cases (ej. Jira/Xray, TestRail) hasta su confirmación.
- Se recomienda validar también el mensaje de error mostrado en los casos negativos (TC-02, TC-03) para asegurar que no revele información sensible (ej. si el usuario existe o no), por buenas prácticas de seguridad.
- Sería conveniente confirmar si el bloqueo por intentos fallidos (TC-07) es temporal con expiración automática, o si requiere intervención de soporte para desbloquear.
