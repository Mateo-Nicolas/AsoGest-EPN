# 04. Matriz de Priorización MoSCoW – AsoGest EPN

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

Clasificar los 17 requerimientos refinados del Entregable 4 (PPE06) con la técnica MoSCoW y documentar cómo se resolvieron los conflictos entre interesados y qué se implementará en cada iteración. Las prioridades conservan las asignadas en las fichas del Entregable 4.

**Escala MoSCoW:** **Must** = indispensable para la primera versión; **Should** = importante, pero la versión puede operar sin ello; **Could** = deseable, se incorpora si hay tiempo o en una iteración posterior; **Won't** = queda fuera de esta versión.

## 2. A. Matriz de priorización

| ID | Nombre del requerimiento | Prioridad (MoSCoW) | Justificación |
|---|---|---|---|
| RF-01 | Registro de ventas | Must | Es la operación central del mostrador y la base de RF-02, RF-08 y RF-09. |
| RF-02 | Actualización del inventario | Must | Mantiene las existencias al día y permite vender aunque el resultado sea negativo, según el acuerdo operativo. |
| RF-03 | Registro de alquileres | Must | El alquiler es una de las actividades principales de la asociación y reemplaza el registro manual. |
| RF-04 | Consulta de disponibilidad | Must | Sin consultar horarios libres y ocupados no se pueden ofrecer ni validar los alquileres; en la primera versión se resuelve con un listado. |
| RF-05 | Validación de horarios | Must | Evita que dos clientes usen el mismo recurso en horarios cruzados. |
| RF-06 | Administración de usuarios | Must | Permite identificar al responsable de cada operación y asignar roles; de ella dependen RF-07, RF-08 y RNF-03. |
| RF-07 | Administración de productos y tarifas | Must | Impide que el Operador Estudiantil modifique precios y protege la información de caja. |
| RF-08 | Consulta de caja | Must | El Tesorero/Administrador Externo necesita revisar los movimientos del día; se entrega en pantalla, sin exportación. |
| RF-09 | Registro de incidencias de inventario | Must | Es la contrapartida de RF-02: si se permite vender con saldo negativo, la diferencia debe quedar registrada para su revisión. |
| RF-10 | Vista gráfica de horarios | Could | Aporta comodidad, pero la primera versión opera con el listado de RF-04. |
| RNF-01 | Tiempo de respuesta en ventas | Must | La atención en el mostrador exige completar una venta de hasta tres productos en 10 segundos o menos. |
| RNF-02 | Funcionamiento local | Must | El mostrador debe operar sin depender de Internet. |
| RNF-03 | Protección de credenciales | Must | Las contraseñas no pueden guardarse en texto plano; la elección final del algoritmo de hash queda pendiente de validación técnica. |
| RNF-04 | Tecnología de desarrollo | Must | Es una restricción del proyecto: Windows Forms, C# y .NET 8 o superior. |
| RNF-05 | Almacenamiento local | Must | Es la base de datos SQLite local sobre la que opera todo el sistema, sin servidores en la nube. |
| RD-01 | Garantía física obligatoria | Must | Es una regla del reglamento interno de la asociación: sin garantía no se confirma el alquiler. |
| RD-02 | Control de existencias negativas | Must | Formaliza la regla de dominio que obliga a identificar como incidencia cada venta con saldo negativo. |

### Exclusiones de la primera versión (Won't)

Estos elementos no son requerimientos del catálogo, pero se registran como **Won't** porque el documento de Visión y Alcance y el Entregable 4 los dejan fuera de esta versión.

| Elemento excluido | Prioridad (MoSCoW) | Justificación |
|---|---|---|
| Exportación automática de reportes a Excel | Won't | La caja se consulta en pantalla (RF-08); la exportación queda para una versión futura. |
| Aplicaciones móviles | Won't | El sistema es de escritorio y se ejecuta en la computadora del mostrador. |
| Reservas remotas | Won't | Los alquileres se registran presencialmente en el mostrador. |
| Pasarelas de pago | Won't | No se procesan pagos electrónicos en esta versión. |
| Facturación electrónica | Won't | No forma parte del alcance de la primera versión. |

### Resumen por prioridad

| Prioridad | Cantidad | Requerimientos |
|---|---|---|
| Must | 16 | RF-01 a RF-09, RNF-01 a RNF-05, RD-01, RD-02 |
| Should | 0 | — |
| Could | 1 | RF-10 |
| Won't | 5 | Exclusiones listadas arriba (no pertenecen al catálogo) |

## 3. B. Acuerdo de negociación documentado

Los conflictos entre las necesidades de los interesados se resolvieron aplicando MoSCoW de acuerdo con el alcance de la primera versión. Primero, los Estudiantes Operadores necesitan no detener la atención cuando el stock es insuficiente, mientras que el Tesorero/Administrador Externo necesita controlar las diferencias de inventario. Se acordó permitir la venta con saldo negativo (RF-02) y compensar el riesgo con el registro obligatorio de una incidencia para su revisión (RF-09 y RD-02), por lo que los tres son **Must**. Segundo, el Tesorero requiere reportes de caja y existía la posibilidad de interpretarlos como archivos de Excel; se acordó que la consulta se haga en pantalla (RF-08, **Must**) y que la exportación automática sea **Won't** en esta versión. Tercero, los operadores y clientes desean una vista de calendario, pero el alcance y el tiempo disponible solo permiten un listado de horarios; por ello RF-04 es **Must** y RF-10 se clasifica como **Could** para una iteración posterior. Cuarto, el requisito de proteger las contraseñas con SHA-256 se mantiene como **Must** en cuanto a no guardarlas en texto plano (RNF-03), pero la elección final del algoritmo de hash se somete a validación técnica antes de terminar el módulo de usuarios.

**Planificación por iteraciones**

| Iteración | Contenido | Requerimientos | Motivo |
|---|---|---|---|
| **Iteración 1 – Base, seguridad y ventas** | Estructura técnica, usuarios y roles, productos y tarifas, ventas, inventario e incidencias | RNF-04, RNF-05, RNF-02, RF-06, RNF-03, RF-07, RF-01, RF-02, RF-09, RD-02, RNF-01 | Son la base de la que dependen las demás funciones (RF-06 para los permisos, RF-01 para el inventario y la caja) y las operaciones de mayor frecuencia en el mostrador. |
| **Iteración 2 – Alquileres y caja** | Registro de alquileres, garantía, validación de horarios, listado de disponibilidad y consulta de caja | RF-03, RD-01, RF-05, RF-04, RF-08 | Dependen de la infraestructura y los usuarios de la Iteración 1; se desarrollan por etapas (formulario y almacenamiento, luego validaciones y garantía). |
| **Iteración posterior (fuera de la primera versión)** | Vista gráfica tipo calendario | RF-10 | Es una mejora (**Could**) que requiere RF-03, RF-04 y RF-05 ya operativos y conserva la validación de RF-05. |

> **Nota:** La distribución en iteraciones es una propuesta del Grupo C derivada de las dependencias del Entregable 4; las fechas concretas de cada iteración deben ajustarse al cronograma de la asignatura.

---
**Fin del documento 04_Matriz_Priorizacion_MoSCoW.md**
