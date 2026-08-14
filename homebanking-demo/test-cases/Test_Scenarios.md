# Test Scenarios - Home Banking Demo

**Proyecto:** Home Banking Demo  
**Versión:** 1.0

## Introducción
Este documento contiene los **Test Scenarios** (casos de alto nivel) identificados para la aplicación.  
Cada scenario representa una funcionalidad o flujo que será probado posteriormente con casos de prueba detallados.

## 1. Login

- LOG-SC-01: Verificar login exitoso con credenciales válidas
- LOG-SC-02: Verificar login fallido con credenciales inválidas
- LOG-SC-03: Verificar mensaje de error al ingresar usuario o contraseña incorrecta
- LOG-SC-04: Verificar bloqueo automático luego de tres intentos fallidos
- LOG-SC-05: Verificar comportamiento de cuenta bloqueada (credenciales locked/locked)
- LOG-SC-06: Verificar login con campos vacíos
- LOG-SC-07: Verificar que después de login exitoso se redirija al Dashboard
- LOG-SC-08: Verificar redirección automática a Login al intentar acceder a secciones protegidas sin sesión activa (Dashboard, Transferencias, u otras)
- LOG-SC-09: Verificar reinicio del contador de intentos fallidos tras un login exitoso
- LOG-SC-10: Verificar comportamiento del checkbox "Recordarme" (Pendiente de confirmación)
- LOG-SC-11: Verificar comportamiento de UI/UX del formulario de Login (máscara de contraseña, tecla Enter, doble clic en Ingresar)
- LOG-SC-12: Verificar manejo de sesión y solicitudes concurrentes (sesión expirada, bloqueo aislado por usuario, múltiples solicitudes simultáneas)
 
  
## 2. Dashboard / Panel Principal

- DASH-SC-01: Verificar visualización correcta del resumen de cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito)
- DASH-SC-02: Verificar visualización de los Últimos Movimientos (orden y contenido)
- DASH-SC-03: Verificar consistencia de saldos tras operaciones realizadas en otros módulos (pendiente de confirmación)
- DASH-SC-04: Verificar navegación hacia otros módulos desde el sidebar
- DASH-SC-05: Verificar funcionalidad del botón "Ocultar" en las tarjetas de cuenta
- DASH-SC-06: Verificar persistencia del estado "Ocultar" al navegar entre módulos (pendiente de confirmación)
- DASH-SC-07: Verificar funcionalidad del botón "Restablecer saldos"
- DASH-SC-08: Verificar cierre de sesión desde la navbar

  
## 3. Transferencias

**Flujo funcional — Entre mis cuentas**
- TRANS-SC-01: Verificar transferencia exitosa entre cuentas propias con monto válido
- TRANS-SC-02: Verificar que el saldo de cuenta origen disminuye y destino aumenta tras transferencia exitosa
- TRANS-SC-03: Verificar visualización del modal de confirmación con los datos correctos antes de procesar

**Flujo funcional — A terceros**
- TRANS-SC-04: Verificar transferencia exitosa a tercero mediante Alias válido
- TRANS-SC-05: Verificar transferencia exitosa a tercero mediante CBU válido (22 dígitos)

**Validaciones de monto**
- TRANS-SC-06: Verificar rechazo de transferencia con monto vacío o igual a cero
- TRANS-SC-07: Verificar comportamiento con monto menor al mínimo ($0.01) — incluye inconsistencia entre validación inicial y validación en el modal de confirmación *(bug detectado)*
- TRANS-SC-08: Verificar rechazo de transferencia con monto mayor al máximo permitido ($50.000)
- TRANS-SC-09: Verificar comportamiento con montos de decimales no válidos (ej. $50.001)
- TRANS-SC-10: Verificar comportamiento al transferir un monto superior al saldo disponible *(pendiente de confirmación)*

**Validación de cuentas y destino**
- TRANS-SC-11: Verificar rechazo de transferencia cuando cuenta origen y destino son la misma
- TRANS-SC-12: Verificar rechazo de Alias con formato inválido
- TRANS-SC-13: Verificar comportamiento de validación de CBU, incluyendo la inconsistencia detectada con CBUs incompletos *(bug detectado — Alta prioridad)*

**Límite diario**
- TRANS-SC-14: Verificar bloqueo de transferencias al superar el límite diario de $100.000
- TRANS-SC-15: Verificar persistencia del límite diario entre sesiones (logout/login)
- TRANS-SC-16: Verificar reseteo del límite diario *(pendiente de confirmación: medianoche vs. 24hs desde la primera transferencia)*

**Modal de confirmación**
- TRANS-SC-17: Verificar cancelación de transferencia desde el modal de confirmación (no debe procesarse ni afectar saldos ni límite diario)

**UI / UX**
- TRANS-SC-18: Verificar comportamiento del dropdown "Tipo de transferencia" después de completar una transferencia a terceros *(bug detectado — vuelve a "Entre mis cuentas")*
- TRANS-SC-19: Verificar límite de caracteres en el campo Descripción *(pendiente de confirmación)*

**Generales / No funcionales**
- TRANS-SC-20: Verificar comportamiento del sistema ante falla de conexión durante una transferencia ya confirmada *(pendiente — caso de error de red)*
  
## 4. Plazos Fijos

**Creación de Plazo Fijo**
- PF-SC-01: Verificar creación exitosa de un nuevo Plazo Fijo con datos válidos
- PF-SC-02: Verificar cálculo correcto de interés estimado, total al vencimiento y fecha de vencimiento según monto y plazo
- PF-SC-03: Verificar visualización del modal de confirmación con los datos correctos antes de crear

**Validaciones de monto**
- PF-SC-04: Verificar rechazo de monto menor al mínimo permitido ($1.000)
- PF-SC-05: Verificar rechazo por saldo insuficiente en la cuenta origen
- PF-SC-06: Verificar comportamiento con montos decimales *(pendiente de confirmación)*

**Plazo**
- PF-SC-07: Verificar que solo estén disponibles las opciones de plazo definidas (30/60/90/180/360 días)
- PF-SC-08: Verificar variación de TNA/interés según el plazo elegido *(pendiente de confirmación)*

**Visualización de Plazos Fijos activos**
- PF-SC-09: Verificar visualización correcta de los datos de cada Plazo Fijo activo
- PF-SC-10: Verificar orden de aparición de nuevos Plazos Fijos en la lista

**Cancelación**
- PF-SC-11: Verificar cancelación exitosa de un Plazo Fijo activo
- PF-SC-12: Verificar monto a reintegrar al cancelar *(pendiente de confirmación: incluye interés o no)*
- PF-SC-13: Verificar que cancelar desde el modal (botón Cancelar) no ejecute la acción

**Modal de creación**
- PF-SC-14: Verificar que cancelar la creación desde el modal no genere el Plazo Fijo

**Generales**
- PF-SC-15: Verificar si existe límite de cantidad de Plazos Fijos simultáneos por cuenta *(pendiente de confirmación)*

## 5. Préstamos

**Solicitud de préstamo**
- PREST-SC-01: Verificar solicitud exitosa de un préstamo con datos válidos
- PREST-SC-02: Verificar que solo estén disponibles las cuentas destino válidas (excluyendo la no permitida)
- PREST-SC-03: Verificar que solo estén disponibles las opciones de cuotas definidas (6/12/18/24)

**Validaciones de monto**
- PREST-SC-04: Verificar rechazo de monto menor al mínimo permitido ($1.000)
- PREST-SC-05: Verificar rechazo de monto mayor al máximo permitido ($500.000)

**Visualización de préstamos activos**
- PREST-SC-06: Verificar visualización correcta de los datos de cada préstamo activo

**Pagar total**
- PREST-SC-07: Verificar cancelación exitosa de un préstamo mediante "Pagar Total"
- PREST-SC-08: Verificar que el dropdown de cuenta de pago solo muestre cuentas con saldo suficiente
- PREST-SC-09: Verificar rechazo cuando ninguna cuenta tiene saldo suficiente para pagar el total
- PREST-SC-10: Verificar monto total a pagar (pendiente de confirmación: incluye intereses restantes o no)

**Desistir (plazo de revocación)**
- PREST-SC-11: Verificar disponibilidad del botón "Desistir" dentro del plazo de 10 días
- PREST-SC-12: Verificar desistimiento exitoso dentro del plazo, devolviendo el monto original
- PREST-SC-13: Verificar comportamiento del botón "Desistir" pasado el plazo de 10 días (pendiente de confirmación)

**Modales**
- PREST-SC-14: Verificar que cancelar desde los modales (Pagar Total / Desistir) no ejecute las acciones

**Generales**
- PREST-SC-15: Verificar si existe límite de préstamos activos simultáneos (pendiente de confirmación)

## 6. Pago de Servicios

- SERV-SC-01: Verificar pago exitoso de un servicio con el monto sugerido
- SERV-SC-02: Verificar que cada servicio muestre un monto sugerido distinto
- SERV-SC-03: Verificar edición del monto sugerido antes de pagar
- SERV-SC-04: Verificar disponibilidad de las 3 cuentas como cuenta a debitar
- SERV-SC-05: Verificar rechazo de pago con monto igual a cero
- SERV-SC-06: Verificar rechazo de pago por saldo insuficiente
- SERV-SC-07: Verificar comportamiento sin límite máximo de monto (solo limitado por saldo)
- SERV-SC-08: Verificar mensaje de éxito y disponibilidad del comprobante en PDF
- SERV-SC-09: Verificar reseteo automático del formulario tras un pago exitoso
- SERV-SC-10: Verificar que el pago se refleje en Últimos Movimientos del Dashboard
- SERV-SC-11: Verificar ausencia de modal de confirmación (el pago se ejecuta directo al hacer click)
- SERV-SC-12: Verificar comportamiento ante doble click en "Pagar Servicio" (pendiente de confirmación)

## 7. Tarjetas Virtuales

- TARJ-SC-01: Verificar generación exitosa de una tarjeta virtual para una cuenta
- TARJ-SC-02: Verificar visualización de los datos de la tarjeta generada (número, vencimiento, CVV, titular, tipo)
- TARJ-SC-03: Verificar mensaje de estado vacío cuando no hay tarjeta activa
- TARJ-SC-04: Verificar rechazo al intentar generar una segunda tarjeta para la misma cuenta
- TARJ-SC-05: Verificar que el botón "Generar nueva tarjeta" se deshabilite cuando ambas cuentas ya tienen tarjeta activa
- TARJ-SC-06: Verificar opción de copiar el número de tarjeta al hacer hover
- TARJ-SC-07: Verificar eliminación exitosa de una tarjeta virtual
- TARJ-SC-08: Verificar cancelación de la eliminación desde el modal
- TARJ-SC-09: Verificar que se pueda generar una nueva tarjeta luego de eliminar la existente de esa cuenta
- TARJ-SC-10: Verificar actualización del estado "Activa" en el menú lateral

## 8. Mis Datos

**Información Personal**
- DATOS-SC-01: Verificar visualización correcta de información personal (Nombre, DNI, Email, Teléfono, Dirección)
- DATOS-SC-02: Verificar que los campos de Información Personal sean estrictamente de solo lectura y no permitan edición

**Mis Cuentas**
- DATOS-SC-03: Verificar la visualización correcta de las cuentas asociadas (Cuenta Corriente, Caja de Ahorro, Tarjeta de Crédito) con su número, CBU y saldo correspondiente
- DATOS-SC-04: Verificar la consistencia de los números de cuenta y saldos entre el Dashboard y el módulo "Mis Datos" *(Bug detectado: divergencia de números)*
- DATOS-SC-05: Verificar la ausencia de opciones o botones para modificar o eliminar las cuentas desde esta vista

**Tarjetas Asociadas**
- DATOS-SC-06: Verificar la visualización de las tarjetas asociadas (Visa Débito, Mastercard Débito, Visa Crédito)
- DATOS-SC-07: Verificar la coherencia y asociación correcta de las tarjetas con el perfil del usuario y los datos del Dashboard *(Bug detectado: tarjetas de débito sin montos ni correlación)*
- DATOS-SC-08: Verificar la ausencia de opciones de eliminación o modificación sobre las tarjetas listadas en este módulo

**No Funcionales / UI-UX**
- DATOS-SC-09: Verificar el comportamiento responsivo del módulo en distintos tamaños de pantalla
- DATOS-SC-10: Verificar que no existan errores de consola JavaScript al cargar el módulo

## 9. Pruebas Generales / No Funcionales

- SC-31: Verificar mensajes de error claros y en español
- SC-32: Verificar comportamiento responsive básico (cambio de tamaño de ventana)
- SC-33: Verificar que no existan errores de JavaScript en consola (Smoke)

---

**Total de Test Scenarios identificados:** 33

**Próximo paso:** Desarrollar los Test Cases detallados basados en estos scenarios.
