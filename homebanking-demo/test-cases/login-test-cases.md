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

# Casos Funcionales

| ID     | Título                                                  | Precondición                              | Pasos                                                                                                                                | Resultado Esperado                                                               | Prioridad |
| ------ | ------------------------------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- | --------- |
| LOG-01 | Login exitoso con credenciales válidas                  | Usuario existente, activo y no bloqueado  | 1. Abrir Login.<br>2. Ingresar usuario válido.<br>3. Ingresar contraseña válida.<br>4. Presionar **Ingresar**.                       | El sistema autentica correctamente y redirige al Dashboard.                      | Alta      |
| LOG-02 | Login fallido con usuario inexistente                   | El usuario no existe                      | 1. Ingresar un usuario inexistente.<br>2. Ingresar cualquier contraseña.<br>3. Presionar **Ingresar**.                               | El sistema no autentica y muestra un mensaje genérico de credenciales inválidas. | Alta      |
| LOG-03 | Login fallido con contraseña incorrecta                 | Usuario válido y activo                   | 1. Ingresar usuario válido.<br>2. Ingresar contraseña incorrecta.<br>3. Presionar **Ingresar**.                                      | El sistema no autentica y muestra un mensaje genérico de credenciales inválidas. | Alta      |
| LOG-04 | Bloqueo de cuenta tras 3 intentos fallidos consecutivos | Usuario activo sin bloqueos previos       | 1. Ingresar usuario válido.<br>2. Ingresar contraseña incorrecta tres veces consecutivas.                                            | La cuenta queda bloqueada y se muestra el mensaje de bloqueo.                    | Alta      |
| LOG-05 | Intento de login luego del bloqueo                      | Cuenta bloqueada                          | 1. Ingresar usuario bloqueado.<br>2. Ingresar contraseña correcta.<br>3. Presionar **Ingresar**.                                     | El acceso es rechazado y se mantiene el mensaje de cuenta bloqueada.             | Alta      |
| LOG-06 | Reinicio del contador de intentos tras login exitoso    | Usuario con dos intentos fallidos previos | 1. Realizar dos intentos fallidos.<br>2. Iniciar sesión correctamente.<br>3. Cerrar sesión.<br>4. Realizar un nuevo intento fallido. | El contador de intentos se reinicia luego del login exitoso.                     | Alta      |
| LOG-07 | Login con cuenta marcada como `locked`                  | Usuario con estado `locked`               | 1. Ingresar usuario `locked`.<br>2. Ingresar cualquier contraseña.<br>3. Presionar **Ingresar**.                                     | Se muestra el mensaje de cuenta bloqueada y no se autentica.                     | Alta      |
| LOG-08 | Cuenta `locked` con contraseña correcta                 | Usuario con estado `locked`               | 1. Ingresar usuario `locked`.<br>2. Ingresar contraseña correcta.<br>3. Presionar **Ingresar**.                                      | El sistema mantiene el bloqueo y no permite el acceso.                           | Alta      |
| LOG-09 | Acceso al Dashboard sin sesión                          | Usuario sin autenticación                 | 1. Acceder directamente a la URL del Dashboard.                                                                                      | El sistema redirige automáticamente al Login.                                    | Alta      |
| LOG-10 | Acceso a otra sección protegida sin sesión              | Usuario sin autenticación                 | 1. Acceder directamente a una URL protegida.                                                                                         | El sistema redirige automáticamente al Login.                                    | Alta      |
| LOG-11 | Acceso mediante URL luego del logout                    | Usuario autenticado que cerró sesión      | 1. Iniciar sesión.<br>2. Cerrar sesión.<br>3. Acceder al Dashboard mediante URL.                                                     | El sistema redirige nuevamente al Login.                                         | Media     |
| LOG-12 | Checkbox "Recordarme" marcado                           | Usuario válido                            | 1. Marcar **Recordarme**.<br>2. Iniciar sesión.<br>3. Cerrar y volver a abrir el navegador.                                          | **Pendiente de definición funcional.**                                           | Baja      |
| LOG-13 | Login sin marcar "Recordarme"                           | Usuario válido                            | 1. No marcar **Recordarme**.<br>2. Iniciar sesión.<br>3. Cerrar y volver a abrir el navegador.                                       | Se espera solicitar nuevamente el login (pendiente de confirmación).             | Baja      |

---

# Casos de Validación

| ID     | Título                        | Precondición | Pasos                                                                             | Resultado Esperado                                                         | Prioridad |
| ------ | ----------------------------- | ------------ | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | --------- |
| VAL-01 | Login con ambos campos vacíos | Ninguna      | 1. Dejar Usuario y Contraseña vacíos.<br>2. Presionar **Ingresar**.               | El sistema valida ambos campos como obligatorios y no envía el formulario. | Media     |
| VAL-02 | Login con usuario vacío       | Ninguna      | 1. Dejar Usuario vacío.<br>2. Completar Contraseña.<br>3. Presionar **Ingresar**. | El sistema muestra la validación del campo Usuario.                        | Media     |
| VAL-03 | Login con contraseña vacía    | Ninguna      | 1. Completar Usuario.<br>2. Dejar Contraseña vacía.<br>3. Presionar **Ingresar**. | El sistema muestra la validación del campo Contraseña.                     | Media     |

---

# Casos de Seguridad
//Estos casos aplican si el backend procesa las credenciales contra una base de datos real. Si el demo simula la autenticación en frontend, estos casos quedan fuera de alcance y se documentan solo como referencia conceptual 

| ID     | Título                                            | Precondición                            | Pasos                                                                                                                    | Resultado Esperado                                                                  | Prioridad |
| ------ | ------------------------------------------------- | --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------- | --------- |
| SEC-01 | SQL Injection en Usuario                          | Ninguna                                 | 1. Ingresar `' OR '1'='1` en Usuario.<br>2. Ingresar cualquier contraseña.<br>3. Presionar **Ingresar**.                 | El acceso es rechazado y no se muestran errores técnicos.                           | Alta      |
| SEC-02 | SQL Injection en Contraseña                       | Usuario válido                          | 1. Ingresar usuario válido.<br>2. Ingresar `' OR 1=1 --` como contraseña.<br>3. Presionar **Ingresar**.                  | El sistema rechaza la autenticación sin revelar información interna.                | Alta      |
| SEC-03 | XSS en Usuario                                    | Ninguna                                 | 1. Ingresar `<script>alert('x')</script>` como usuario.<br>2. Intentar iniciar sesión.                                   | El script no se ejecuta y el acceso es rechazado.                                   | Alta      |
| SEC-04 | XSS en Contraseña                                 | Ninguna                                 | 1. Ingresar usuario válido.<br>2. Escribir `<script>alert('x')</script>` como contraseña.<br>3. Intentar iniciar sesión. | El script no se ejecuta y el acceso es rechazado.                                   | Alta      |
| SEC-05 | Mensajes de error no revelan información sensible | Usuario existente y usuario inexistente | 1. Intentar login con usuario inexistente.<br>2. Intentar login con contraseña incorrecta para un usuario válido.        | Ambos casos muestran el mismo mensaje de error.                                     | Alta      |
| SEC-06 | Acceso directo a páginas protegidas               | Usuario sin sesión                      | 1. Intentar acceder mediante URL al Dashboard u otra sección protegida.                                                  | El sistema redirige al Login.                                                       | Alta      |
| SEC-07 | Acceso mediante botón Atrás luego del logout      | Usuario autenticado                     | 1. Iniciar sesión.<br>2. Cerrar sesión.<br>3. Presionar el botón Atrás del navegador.                                    | No se muestra contenido protegido o se redirige nuevamente al Login.                | Media      |
| SEC-08 | Uso de sesión expirada                            | Usuario autenticado con sesión vencida  | 1. Iniciar sesión.<br>2. Esperar la expiración.<br>3. Actualizar la página.                                              | El sistema solicita autenticarse nuevamente.                                        | Alta      |
| SEC-09 | Bloqueo aislado por usuario                       | Existen dos usuarios activos            | 1. Bloquear la cuenta del Usuario A.<br>2. Iniciar sesión con el Usuario B.                                              | El bloqueo afecta únicamente a la cuenta correspondiente.                           | Alta      |
| SEC-10 | Múltiples solicitudes simultáneas de login        | Usuario válido                          | 1. Enviar varias solicitudes de login simultáneamente.                                                                   | El sistema procesa una única autenticación y mantiene la consistencia de la sesión. | Media     |

---

# Casos de UI / UX

| ID    | Título                                  | Precondición   | Pasos                                                                                   | Resultado Esperado                                                         | Prioridad |
| ----- | --------------------------------------- | -------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | --------- |
| UI-01 | Campo Contraseña enmascarado            | Ninguna        | 1. Escribir caracteres en el campo Contraseña.                                          | Los caracteres se muestran ocultos mediante máscara.                       | Baja      |
| UI-02 | Login utilizando la tecla Enter         | Usuario válido | 1. Completar usuario y contraseña.<br>2. Presionar la tecla **Enter**.                  | El login se ejecuta igual que al hacer clic en **Ingresar**.               | Media     |
| UI-03 | Múltiples clics sobre el botón Ingresar | Usuario válido | 1. Completar credenciales válidas.<br>2. Hacer varios clics rápidos sobre **Ingresar**. | El sistema procesa una única autenticación y evita solicitudes duplicadas. | Media     |

