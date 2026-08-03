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
- LOG-SC-11: Verificar comportamiento del checkbox "Recordarme" (Pendiente de confirmación)
- LOG-SC-12: Verificar comportamiento del checkbox "Recordarme" (Pendiente de confirmación)
 
  
## 2. Dashboard / Panel Principal

- DASH-SC-13: Verificar visualización correcta del resumen de cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito)
- DASH-SC-14: Verificar visualización de los Últimos Movimientos
- DASH-SC-15: Verificar que los saldos se muestren correctamente ($0.00 en demo)
- DASH-SC-16: Verificar navegación hacia otros módulos desde el Dashboard

## 3. Transferencias

- TRANS-SC-17: Verificar realización de transferencia exitosa entre cuentas propias
- TRANS-SC-18: Verificar transferencia a CBU/CVU/Alias
- TRANS-SC-19: Verificar validaciones de monto en transferencias (monto cero, negativo, superior al saldo)
- TRANS-SC-20: Verificar mensaje de confirmación después de transferencia exitosa

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
