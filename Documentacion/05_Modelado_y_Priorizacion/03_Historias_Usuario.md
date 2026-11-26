# 03. Historias de Usuario – AsoGest EPN

**Escuela Politécnica Nacional – Facultad de Ingeniería Eléctrica y Electrónica**  
**Asignatura:** Diseño y Programación de Software  
**Proyecto:** Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN – Asociación de Ingeniería Química (AsoGest EPN)  
**Grupo:** C  
**Integrantes:** Jeziel Silva, Mateo Paredes y David Vega  
**Docente:** Ing. José Naranjo  
**Periodo académico:** 2026B–2027A  
**Entregable:** PPE07 – Modelado de Casos de Uso, Historias de Usuario y Priorización

---

## 1. Objetivo

Expresar las necesidades de los usuarios de AsoGest EPN mediante historias de usuario con criterios de aceptación en formato Dado/Cuando/Entonces. Cada historia se deriva de uno o más requerimientos del Entregable 4 (PPE06) y se relaciona con los casos de uso de `01_Modelo_Casos_Uso.md`.

## 2. Resumen

| ID | Historia | Rol | Requerimiento(s) | Caso(s) de uso | Prioridad |
|---|---|---|---|---|---|
| HU-01 | Registrar una venta | Operador Estudiantil | RF-01, RNF-01 | CU-02 | Must |
| HU-02 | Vender con existencias insuficientes | Operador Estudiantil | RF-02, RF-09, RD-02 | CU-02, CU-03, CU-04 | Must |
| HU-03 | Registrar un alquiler con garantía | Operador Estudiantil | RF-03, RD-01 | CU-05, CU-07 | Must |
| HU-04 | Evitar alquileres con horarios cruzados | Operador Estudiantil | RF-05 | CU-05, CU-06 | Must |
| HU-05 | Consultar disponibilidad de un recurso | Operador Estudiantil | RF-04 | CU-08 | Must |
| HU-06 | Administrar cuentas de usuario | Administrador Principal | RF-06, RNF-03 | CU-01, CU-09 | Must |
| HU-07 | Administrar productos y tarifas | Tesorero/Administrador Externo | RF-07 | CU-10 | Must |
| HU-08 | Consultar la caja del día | Tesorero/Administrador Externo | RF-08 | CU-11 | Must |
| HU-09 | Revisar incidencias de inventario | Tesorero/Administrador Externo | RF-09, RD-02 | CU-12 | Must |
| HU-10 | Ver los horarios en un calendario gráfico | Operador Estudiantil | RF-10 | CU-13 | Could |

---

## 3. Historias de usuario

### HU-01 – Registrar una venta

**Historia:** Como **Operador Estudiantil**, quiero **registrar una venta de hasta tres productos desde el mostrador**, para **atender rápidamente a los estudiantes y dejar constancia de cada operación**.

**Requerimiento asociado:** RF-01, RNF-01

**Criterios de aceptación**

1. **Dado que** tengo una sesión activa y los productos están registrados, **cuando** confirmo una venta, **entonces** el sistema guarda el producto, la cantidad, el precio unitario, la fecha, la hora, el total calculado y mi identificador de operador, y muestra la venta en el historial.
2. **Dado que** registro una venta con varios productos, **cuando** el sistema calcula el total, **entonces** el total almacenado coincide con la suma de los precios unitarios multiplicados por sus cantidades.
3. **Dado que** registro una venta de hasta tres productos, **cuando** mido el tiempo entre la selección del primer producto y la confirmación, **entonces** el tiempo es de 10 segundos o menos.

---

### HU-02 – Vender con existencias insuficientes

**Historia:** Como **Operador Estudiantil**, quiero **poder completar una venta aunque la cantidad supere las existencias registradas**, para **no detener la atención en el mostrador y que el Tesorero revise después la diferencia**.

**Requerimiento asociado:** RF-02, RF-09, RD-02

**Criterios de aceptación**

1. **Dado que** el stock de un producto es 2, **cuando** confirmo una venta de 3 unidades, **entonces** el sistema completa la venta y registra el saldo de existencias en −1.
2. **Dado que** una venta deja existencias negativas, **cuando** se confirma, **entonces** el sistema crea una incidencia con el producto afectado, la cantidad involucrada, la fecha, la hora y el usuario responsable.
3. **Dado que** una venta no deja existencias negativas, **cuando** se confirma, **entonces** el stock disminuye exactamente en la cantidad vendida y no se genera ninguna incidencia.

---

### HU-03 – Registrar un alquiler con garantía

**Historia:** Como **Operador Estudiantil**, quiero **registrar un alquiler con los datos del cliente, del recurso y del horario, y confirmar la garantía recibida**, para **tener un registro completo y respaldar la entrega del recurso**.

**Requerimiento asociado:** RF-03, RD-01

**Criterios de aceptación**

1. **Dado que** ingreso nombre del cliente, cédula, recurso, fecha, hora de inicio y hora de finalización en formato HH:MM, **cuando** guardo el alquiler, **entonces** el registro contiene los seis datos.
2. **Dado que** falta alguno de los seis datos, **cuando** intento guardar, **entonces** el sistema impide guardar el alquiler e identifica el campo pendiente.
3. **Dado que** no he marcado la recepción del carné de la EPN o de la cédula original, **cuando** intento confirmar el alquiler, **entonces** el sistema no lo confirma.
4. **Dado que** marqué la recepción de una garantía válida, **cuando** confirmo el alquiler y se cumplen las demás condiciones, **entonces** el sistema lo confirma y lo guarda.

---

### HU-04 – Evitar alquileres con horarios cruzados

**Historia:** Como **Operador Estudiantil**, quiero **que el sistema rechace un alquiler cuyo horario se cruce con otro del mismo recurso**, para **evitar que dos personas usen el mismo recurso al mismo tiempo**.

**Requerimiento asociado:** RF-05

**Criterios de aceptación**

1. **Dado que** existe un alquiler confirmado de 10:00 a 12:00 para un recurso en una fecha, **cuando** intento confirmar otro de 11:00 a 13:00 para el mismo recurso y fecha, **entonces** el sistema rechaza la confirmación.
2. **Dado que** existe un alquiler confirmado de 10:00 a 12:00, **cuando** intento confirmar otro de 10:30 a 11:30 para el mismo recurso y fecha, **entonces** el sistema rechaza la confirmación por cruce total.
3. **Dado que** existe un alquiler confirmado de 10:00 a 12:00, **cuando** confirmo otro de 14:00 a 15:00 para el mismo recurso y fecha, **entonces** el sistema lo acepta si cumple las demás condiciones.
4. **Dado que** existe un alquiler confirmado para el recurso A, **cuando** confirmo otro en el mismo horario para el recurso B, **entonces** el sistema lo acepta, porque el cruce solo aplica al mismo recurso y fecha.

---

### HU-05 – Consultar disponibilidad de un recurso

**Historia:** Como **Operador Estudiantil**, quiero **consultar en un listado los horarios libres y ocupados de un recurso para una fecha**, para **informar al cliente qué horarios puede solicitar**.

**Requerimiento asociado:** RF-04

**Criterios de aceptación**

1. **Dado que** selecciono un recurso y una fecha, **cuando** realizo la consulta, **entonces** el sistema muestra un listado que identifica los intervalos ocupados y los intervalos disponibles.
2. **Dado que** acabo de confirmar un alquiler para ese recurso y fecha, **cuando** vuelvo a consultar, **entonces** el intervalo del alquiler aparece como ocupado.

---

### HU-06 – Administrar cuentas de usuario

**Historia:** Como **Administrador Principal**, quiero **crear, modificar y suspender cuentas, asignar roles y consultar los inicios y cierres de sesión**, para **controlar quién opera el sistema y con qué permisos**.

**Requerimiento asociado:** RF-06, RNF-03

**Criterios de aceptación**

1. **Dado que** tengo el perfil de Administrador Principal, **cuando** creo, edito o suspendo una cuenta y asigno un rol, **entonces** el sistema guarda el cambio y lo refleja en el acceso de ese usuario.
2. **Dado que** un usuario inicia o cierra sesión, **cuando** consulto el registro de sesiones, **entonces** veo esos eventos asociados al usuario.
3. **Dado que** un usuario no tiene el perfil de Administrador Principal, **cuando** intenta administrar cuentas, **entonces** el sistema no se lo permite.
4. **Dado que** reviso los datos almacenados, **cuando** busco las contraseñas, **entonces** solo existen valores hash y ninguna contraseña en texto plano.

---

### HU-07 – Administrar productos y tarifas

**Historia:** Como **Tesorero/Administrador Externo**, quiero **crear y modificar productos y tarifas**, para **mantener actualizados los precios sin que los operadores puedan alterarlos**.

**Requerimiento asociado:** RF-07

**Criterios de aceptación**

1. **Dado que** inicié sesión como Tesorero/Administrador Externo o Administrador Principal, **cuando** creo o modifico un producto o una tarifa, **entonces** el sistema guarda el cambio.
2. **Dado que** inicié sesión como Operador Estudiantil, **cuando** intento crear o modificar un producto o una tarifa, **entonces** el sistema no me lo permite.

---

### HU-08 – Consultar la caja del día

**Historia:** Como **Tesorero/Administrador Externo**, quiero **ver en pantalla el resumen de caja del día y los movimientos por turno y operador**, para **revisar el dinero recaudado sin depender de hojas de cálculo**.

**Requerimiento asociado:** RF-08

**Criterios de aceptación**

1. **Dado que** existen ventas registradas en una fecha, **cuando** consulto esa fecha, **entonces** el sistema muestra el resumen de caja y los movimientos agrupados por turno y operador.
2. **Dado que** consulto la caja, **cuando** reviso las opciones disponibles, **entonces** el sistema no genera archivos de Excel, porque la exportación queda fuera de la primera versión.

---

### HU-09 – Revisar incidencias de inventario

**Historia:** Como **Tesorero/Administrador Externo**, quiero **consultar las incidencias generadas por ventas con existencias negativas**, para **controlar las diferencias de inventario y tomar las acciones correspondientes**.

**Requerimiento asociado:** RF-09, RD-02

**Criterios de aceptación**

1. **Dado que** existen incidencias de inventario, **cuando** abro el listado de incidencias, **entonces** veo, por cada una, el producto afectado, la cantidad involucrada, la fecha, la hora y el usuario responsable.
2. **Dado que** una venta produjo existencias negativas, **cuando** busco esa venta, **entonces** puedo identificar la incidencia asociada.

---

### HU-10 – Ver los horarios en un calendario gráfico *(iteración posterior)*

**Historia:** Como **Operador Estudiantil**, quiero **ver los horarios de un recurso en una vista gráfica tipo calendario**, para **identificar de un vistazo los intervalos libres y ocupados**.

**Requerimiento asociado:** RF-10

**Criterios de aceptación**

1. **Dado que** la iteración incluye esta mejora y selecciono un recurso y una fecha, **cuando** abro el calendario, **entonces** este representa los intervalos libres y ocupados.
2. **Dado que** consulto el mismo recurso y fecha en el listado y en el calendario, **cuando** comparo ambos, **entonces** los datos coinciden.
3. **Dado que** intento confirmar un alquiler desde el calendario, **cuando** su horario se cruza con otro confirmado, **entonces** se mantiene el rechazo definido en RF-05.

---

## 4. Trazabilidad de historias con requerimientos

| Requerimiento | Historias |
|---|---|
| RF-01 | HU-01 |
| RF-02 | HU-02 |
| RF-03 | HU-03 |
| RF-04 | HU-05 |
| RF-05 | HU-04 |
| RF-06 | HU-06 |
| RF-07 | HU-07 |
| RF-08 | HU-08 |
| RF-09 | HU-02, HU-09 |
| RF-10 | HU-10 |
| RNF-01 | HU-01 |
| RNF-03 | HU-06 |
| RD-01 | HU-03 |
| RD-02 | HU-02, HU-09 |

Los requerimientos RNF-02 (funcionamiento sin Internet), RNF-04 (Windows Forms, C#, .NET 8 o superior) y RNF-05 (SQLite local) son condiciones técnicas transversales: no se expresan como historias de usuario, sino que se verifican sobre el conjunto del sistema (véase `04_Matriz_Priorizacion_MoSCoW.md`).

---
**Fin del documento 03_Historias_Usuario.md**
