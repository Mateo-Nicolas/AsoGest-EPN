# 02. Resultados de Validación – AsoGest EPN

**Escuela Politécnica Nacional – Facultad de Ingeniería Eléctrica y Electrónica**  
**Asignatura:** Diseño y Programación de Software  
**Proyecto:** Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN – Asociación de Ingeniería Química (AsoGest EPN)  
**Grupo:** C  
**Integrantes:** Jeziel Silva, Mateo Paredes y David Vega  
**Docente:** Ing. José Naranjo  
**Periodo académico:** 2026B–2027A  
**Entregable:** PPE08 – Matriz de Trazabilidad, Validación y Cierre de la IR

---

## 1. Objetivo

Documentar la validación de los requerimientos de AsoGest EPN mediante un checklist de calidad, y registrar las observaciones y correcciones surgidas durante el análisis, el refinamiento y la negociación entre interesados.

## 2. A. Checklist de validación

El checklist se aplica a los requerimientos principales: RF-01, RF-02, RF-03, RF-05, RF-09, RNF-01, RNF-03 y RD-01. Las respuestas son Sí / No / Pendiente.

| Pregunta | RF-01 | RF-02 | RF-03 | RF-05 | RF-09 | RNF-01 | RNF-03 | RD-01 |
|---|---|---|---|---|---|---|---|---|
| ¿Representa una necesidad real? | Sí | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| ¿Es claro? | Sí | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| ¿Es consistente con los demás? | Sí | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| ¿Está completo? | Sí | Sí | Sí | Sí | Sí | Sí | Pendiente | Sí |
| ¿Es factible? | Sí | Sí | Sí | Sí | Sí | Pendiente | Sí | Sí |
| ¿Es verificable? | Sí | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| ¿Tiene fuente identificada? | Sí | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| ¿Tiene prioridad asignada? | Sí | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| ¿Fue revisado por los interesados? | Sí | Sí | Sí | Sí | Sí | Sí | Sí | Sí |

**Observaciones al checklist**

| Requerimiento | Pregunta | Respuesta | Observación |
|---|---|---|---|
| RNF-03 | ¿Está completo? | Pendiente | La elección final del algoritmo de hash queda sujeta a validación técnica antes de terminar el módulo de usuarios (SHA-256 aparece en la documentación anterior). |
| RNF-01 | ¿Es factible? | Pendiente | El catálogo lo mantiene como «Analizado»: se comprobará con una prueba cronometrada durante el diseño y las pruebas. |
| RF-01, RF-02, RF-09 | ¿Es factible? | Sí | Informe de refinamiento: debe comprobarse que el registro de la venta, el descuento de stock y la creación de la incidencia se realicen de forma conjunta para evitar información incompleta. |
| RF-05 | ¿Está completo? | Sí | Rechaza cruce total o parcial para el mismo recurso y fecha. Los intervalos contiguos (el fin de un alquiler coincide con el inicio de otro) no se consideran cruce y se aceptan; esta aclaración se incorpora en el SRS. |

**Resumen de los demás requerimientos.** Los requerimientos RF-04, RF-06, RF-07, RF-08, RF-10, RNF-02, RNF-04, RNF-05 y RD-02 cuentan con enunciado, fuente, prioridad, criterio de aceptación y dependencias definidos en el Entregable 4. Su revisión por los interesados se documenta en la sección 3.3.

## 3. B. Observaciones y correcciones

### 3.1 Observaciones y correcciones aplicadas a los requerimientos

| ID | Requerimiento(s) | Observación | Corrección aplicada | Origen |
|---|---|---|---|---|
| OBS-01 | RF-03 | Los horarios de alquiler no tenían un formato definido, lo que dificulta comparar alquileres. | Se especifica el formato HH:MM para hora de inicio y fin y se establece que nombre, cédula, recurso y fechas son obligatorios; no se guarda si falta alguno. | Informe de refinamiento (PPE05) |
| OBS-02 | RF-02, RF-09, RD-02 | Podía interpretarse que el sistema debía bloquear la venta con stock insuficiente. | Se aclara que la venta se completa y deja saldo negativo para no detener la atención; se crea una incidencia (producto, cantidad, fecha, hora y usuario) que revisa el Tesorero/Administrador Externo. RF-09 se separa como requerimiento independiente. | Informe de refinamiento (PPE05); Acuerdo de negociación (PPE07) |
| OBS-03 | RF-08 | Podía interpretarse que se generarían archivos de Excel. | Se redacta como consulta en pantalla por turno y operador; la exportación automática a Excel queda excluida (Won't). | Informe de refinamiento (PPE05); Acuerdo de negociación (PPE07) |
| OBS-04 | RNF-03 | La expresión «encriptadas mediante SHA-256» es imprecisa: SHA-256 es una función hash, no un cifrado reversible. | Se redacta como «almacenamiento mediante valores hash, sin texto plano». La confirmación del algoritmo definitivo queda pendiente de validación técnica. | Informe de refinamiento (PPE05) |
| OBS-05 | RF-04, RF-10 | La vista de calendario y el listado de horarios se confundían, pudiendo entenderse el calendario como obligatorio. | RF-04 se limita al listado (Must) y RF-10 se separa como mejora de iteración posterior (Could). | Informe de refinamiento (PPE05); Acuerdo de negociación (PPE07) |
| OBS-06 | RNF-01 | «Rápida» era una expresión subjetiva y no verificable. | Se reemplaza por una medida: venta de hasta tres productos en 10 s o menos, desde el primer producto hasta la confirmación. | Informe de refinamiento (PPE05) |
| OBS-07 | RD-01 | La redacción remitía al reglamento sin indicar qué debe comprobarse. | Se precisa que el sistema no confirma el alquiler hasta que el operador registre la recepción física del carné de la EPN o la cédula original. | Informe de refinamiento (PPE05) |

### 3.2 Conflictos entre interesados y acuerdos de negociación

| Conflicto | Situación | Resolución |
|---|---|---|
| Flexibilidad al cliente vs. garantía | Los clientes quieren alquilar sin portar el documento; el reglamento exige retener la garantía física. | La recepción de la garantía se automatiza como regla obligatoria del formulario de alquiler (RD-01), respaldando al operador con una regla objetiva. |
| Agilidad operativa vs. control y auditoría | Los operadores priorizan la velocidad en mostrador; el Presidente y el Tesorero priorizan auditoría y control de cambios. | Control de acceso por roles con un modo operativo ágil para el operador y un modo de administración y auditoría para el Presidente y el Tesorero (RF-06, RF-07, RF-08). |
| Operadores vs. Tesorero | Los operadores necesitan no detener el mostrador con stock insuficiente; el Tesorero necesita controlar diferencias. | Se permite la venta con saldo negativo (RF-02) con registro obligatorio de incidencia (RF-09, RD-02). Los tres son Must. |
| Reportes de caja | El Tesorero requiere reportes y existía la posibilidad de interpretarlos como Excel. | Consulta en pantalla (RF-08, Must); exportación automática Won't. |
| Calendario vs. listado | Operadores y clientes desean calendario; el alcance solo permite listado. | RF-04 Must (listado); RF-10 Could (iteración posterior). |
| Protección de contraseñas | Se pedía SHA-256 como mecanismo. | RNF-03 Must en cuanto a no guardar texto plano; algoritmo sujeto a validación técnica. |

### 3.3 Revisión con los interesados

Los requerimientos fueron revisados y aceptados por el vicepresidente del departamento de finanzas de la Asociación de Estudiantes de Ingeniería Química.

## 4. Aspectos que permanecen abiertos

1. Confirmar el algoritmo de hash definitivo para RNF-03.
2. Comprobar con una prueba cronometrada el cumplimiento de RNF-01.

---
**Fin del documento 02_Resultados_Validacion.md**
