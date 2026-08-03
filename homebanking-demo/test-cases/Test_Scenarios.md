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

- DASH-SC-13: Verificar visualización correcta del resumen de cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito)
- DASH-SC-14: Verificar visualización de los Últimos Movimientos
- DASH-SC-15: Verificar que los saldos se muestren correctamente ($0.00 en demo)
- DASH-SC-16: Verificar navegación hacia otros módulos desde el Dashboard

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

- SC-15: Verificar creación de un nuevo Plazo Fijo
- SC-16: Verificar cálculo correcto de intereses según días y monto
- SC-17: Verificar visualización de Plazos Fijos activos
- SC-18: Verificar validaciones en el formulario de Plazo Fijo (campos obligatorios, montos mínimos/máximos)

## 5. Préstamos

- SC-19: Verificar solicitud de nuevo préstamo dentro del límite ($500.000)
- SC-20: Verificar rechazo de préstamo que supera el límite permitido
- SC-21: Verificar visualización de préstamos activos
- SC-22: Verificar validaciones de monto y cuotas en el formulario de préstamo

## 6. Pago de Servicios

- SC-23: Verificar pago de servicio exitoso
- SC-24: Verificar validaciones en el formulario de pago de servicios
- SC-25: Verificar mensaje de confirmación de pago

## 7. Tarjetas Virtuales

- SC-26: Verificar generación exitosa de una tarjeta virtual
- SC-27: Verificar que solo se permita generar 1 tarjeta virtual por cuenta
- SC-28: Verificar visualización de los datos de la tarjeta virtual generada

## 8. Mis Datos

- SC-29: Verificar visualización correcta de información personal
- SC-30: Verificar visualización de cuentas y tarjetas asociadas

## 9. Pruebas Generales / No Funcionales

- SC-31: Verificar mensajes de error claros y en español
- SC-32: Verificar comportamiento responsive básico (cambio de tamaño de ventana)
- SC-33: Verificar que no existan errores de JavaScript en consola (Smoke)

---

**Total de Test Scenarios identificados:** 33

**Próximo paso:** Desarrollar los Test Cases detallados basados en estos scenarios.
