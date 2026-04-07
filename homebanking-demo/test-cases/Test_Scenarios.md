# Test Scenarios - Home Banking Demo

**Proyecto:** Home Banking Demo  
**Versión:** 1.0

## Introducción
Este documento contiene los **Test Scenarios** (casos de alto nivel) identificados para la aplicación.  
Cada scenario representa una funcionalidad o flujo que será probado posteriormente con casos de prueba detallados.

## 1. Login

- SC-01: Verificar login exitoso con credenciales válidas
- SC-02: Verificar login fallido con credenciales inválidas
- SC-03: Verificar mensaje de error al ingresar usuario o contraseña incorrecta
- SC-04: Verificar comportamiento de cuenta bloqueada (credenciales locked/locked)
- SC-05: Verificar login con campos vacíos
- SC-06: Verificar que después de login exitoso se redirija al Dashboard

## 2. Dashboard / Panel Principal

- SC-07: Verificar visualización correcta del resumen de cuentas (Corriente, Caja de Ahorro, Tarjeta de Crédito)
- SC-08: Verificar visualización de los Últimos Movimientos
- SC-09: Verificar que los saldos se muestren correctamente ($0.00 en demo)
- SC-10: Verificar navegación hacia otros módulos desde el Dashboard

## 3. Transferencias

- SC-11: Verificar realización de transferencia exitosa entre cuentas propias
- SC-12: Verificar transferencia a CBU/CVU/Alias
- SC-13: Verificar validaciones de monto en transferencias (monto cero, negativo, superior al saldo)
- SC-14: Verificar mensaje de confirmación después de transferencia exitosa

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
