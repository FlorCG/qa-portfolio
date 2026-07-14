# Análisis Funcional — Transferencias

**Módulo:** Transferencias  
**Prioridad:** Alta  

> Este análisis está basado en la exploración de la aplicación. No existe documentación oficial de requisitos — los comportamientos esperados fueron inferidos a partir del comportamiento observado y estándares de usabilidad en aplicaciones financieras.

---

## Objetivo  

Permitir al usuario transferir dinero entre sus propias cuentas o a cuentas de terceros de manera segura. Es una de las funcionalidades más críticas del homebanking ya que maneja operaciones financieras reales. 

---

## Elementos de la interfaz  

| Elemento | Tipo | Descripción |
|---|---|---|
| Selector de tipo | Dropdown | Elige entre "Entre mis cuentas" o "A terceros" |
| Cuenta origen | Dropdown | Selecciona Cuenta Corriente o Caja de Ahorro |
| Cuenta destino | Dropdown | Selecciona Cuenta Corriente o Caja de Ahorro *(solo para transferencias entre mis cuentas)* |
| Alias/CBU destino | Campo de texto | Ingresa alias o CBU del tercero *(solo para transferencias a terceros)* |
| Monto | Campo numérico | Monto a transferir |
| Descripción | Campo de texto | Descripción opcional de la transferencia |
| Transferir | Botón | Envía el formulario |
| Modal de confirmación | Modal | Muestra datos de la transferencia antes de confirmar |
| Confirmar | Botón | Confirma la transferencia en el modal |
| Cancelar | Botón | Cancela la transferencia en el modal |  

---

## Reglas de negocio

- **Monto mínimo:** $1
- **Monto máximo:** $50.000 por transferencia
- **Límite diario:** $100.000 en transferencias por día (persiste entre sesiones)
- **Validación de origen y destino:** No se puede transferir de una cuenta a sí misma
- **Validación de alias:** Debe cumplir un formato específico (ej: `DEMO.HOLA.COSO`)
- **Validación de CBU:** Debe ser un número de 22 dígitos *(comportamiento inconsistente detectado)*
- **Descripción:** Campo opcional
- **Modal de confirmación:** Muestra resumen antes de ejecutar la transferencia
- **Persistencia de límites:** El límite diario se mantiene entre sesiones, incluso después de logout

---

## Flujo principal — Transferencia entre mis cuentas

1. Usuario selecciona "Entre mis cuentas" en el dropdown
2. Sistema muestra campos: Cuenta origen, Cuenta destino, Monto, Descripción (opcional)
3. Usuario completa los datos
4. Ingresa monto válido (entre $1 y $50.000)
5. Hace click en "Transferir"
6. Sistema valida los datos
7. Abre un modal con el resumen (cuenta origen, destino, monto)
8. Usuario revisa y hace click en "Confirmar"
9. Sistema procesa la transferencia
10. Muestra mensaje: *"Transferencia realizada exitosamente"*
11. El saldo de la cuenta origen disminuye
12. El saldo de la cuenta destino aumenta

---

## Flujo principal — Transferencia a terceros

1. Usuario selecciona "A terceros" en el dropdown
2. Sistema muestra campos: Cuenta origen, Alias/CBU destino, Monto, Descripción (opcional)
3. Usuario completa los datos (alias o CBU válido)
4. Ingresa monto válido (entre $1 y $50.000)
5. Hace click en "Transferir"
6. Sistema valida los datos
7. Abre un modal con el resumen
8. Usuario revisa y hace click en "Confirmar"
9. Sistema procesa la transferencia
10. Muestra mensaje: *"Transferencia realizada exitosamente"*

---

## Flujos alternativos / excepciones

**Monto vacío o cero**
- Sistema muestra: *"El valor debe ser superior o igual a 0.01"*
- No permite avanzar

**Monto menor a $1**
- Si ingresa $0.01, el sistema permite avanzar a confirmación
- Al confirmar, muestra: *"El monto mínimo para transferir es $1"*
- No procesa la transferencia

**Monto mayor a $50.000**
- Sistema muestra: *"El monto máximo por transferencia es $50.000"*
- No permite avanzar

**Monto con decimales inválidos**
- Si ingresa valores como $50.001, muestra: *"Introduce un valor válido. Los dos valores válidos más aproximados son 50 y 50.01"*
- No permite avanzar

**Transferencia a la misma cuenta**
- Sistema valida que origen y destino sean diferentes
- Si son iguales, muestra: *"La cuenta origen y destino no pueden ser la misma"*

**Alias de tercero inválido**
- Formato no reconocido (ej: "pepe")
- Sistema muestra: *"CBU o Alias de destino no válido"*
- No permite avanzar

**CBU de tercero inválido**
- Menos de 22 dígitos *(comportamiento inconsistente detectado)*
- Sistema parece aceptar CBUs incompletos en ciertos casos

**Excede límite diario**
- Tras acumular transferencias que superan $100.000 en el día
- Sistema muestra: *"Has excedido el límite diario de transferencias ($100.000)"*
- Persiste aunque cierre sesión y vuelva a ingresar

**Saldo insuficiente**
- Monto superior al saldo disponible de la cuenta origen
- Comportamiento no verificado durante la exploración *(a validar)*

**Modal de confirmación - Cancelar**
- Usuario hace click en "Cancelar" en el modal
- Sistema cierra el modal sin procesar la transferencia
- Vuelve al formulario

---

## Validaciones identificadas

| Campo | Validación |
|---|---|
| Cuenta origen | Obligatoria, dropdown con opciones disponibles |
| Cuenta destino | Obligatoria (transferencias entre mis cuentas), dropdown |
| Alias/CBU destino | Obligatorio (transferencias a terceros), formato específico requerido |
| Monto | Obligatorio, numérico, entre $1 y $50.000, solo 2 decimales válidos |
| Descripción | Opcional, máximo de caracteres *(a confirmar)* |

---

## Riesgos detectados

- **Crítico:** Maneja operaciones financieras reales — errores tienen impacto directo en dinero del usuario
- **Crítico:** El límite diario persiste entre sesiones — puede confundir al usuario si no entiende que es un límite de 24 horas
- **Alto:** Validación inconsistente de CBU — acepta formatos incompletos en ciertos casos *(posible bug)*
- **Alto:** El dropdown cambia de estado de forma inconsistente tras realizar una transferencia a terceros *(posible bug)*
- **Medio:** Validación de decimales es compleja y poco clara para el usuario
- **Medio:** El mensaje de error de $0.01 pasa la validación inicial pero falla en confirmación — confunde el flujo

---

## Dudas / puntos a verificar

| # | Duda | Impacto |
|---|---|---|
| 1 | ¿Qué pasa si intentas transferir un monto mayor al saldo disponible de la cuenta origen? | No se verificó — el máximo permitido ($50.000) se valida primero, bloqueando intentos de montos mayores |
| 2 | ¿Por qué el CBU acepta valores incompletos en ciertos casos (ej: 19 dígitos)? | Posible bug de validación |
| 3 | ¿El comportamiento del dropdown (vuelve a "Entre mis cuentas" después de transferencia a terceros) es intencional? | Posible bug de UX |
| 4 | ¿El límite diario se resetea a medianoche o después de 24 horas desde la primer transferencia? | Define comportamiento en test cases |
| 5 | ¿La descripción tiene un límite de caracteres? | Validación de campo |
| 6 | ¿Los montos decimales válidos son solo .00 y .01, o hay más opciones? | Regla de negocio no clara |
| 7 | ¿Qué sucede si falla la conexión a internet durante una transferencia confirmada? | Caso de error de red |

---

## Casos de prueba relacionados

*Se completará después de escribir los test cases*

---

## Bugs encontrados

*Se completará después de la ejecución*

---























