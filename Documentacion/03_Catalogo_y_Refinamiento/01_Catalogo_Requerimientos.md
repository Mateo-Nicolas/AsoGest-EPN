# 01. Catálogo de Requerimientos – AsoGest EPN

**Escuela Politécnica Nacional – Facultad de Ingeniería Eléctrica y Electrónica**  
**Asignatura:** Diseño y Programación de Software  
**Proyecto:** Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN – Asociación de Ingeniería Química (AsoGest EPN)  
**Grupo:** C  
**Integrantes:** Jeziel Silva, Mateo Paredes y David Vega  
**Docente:** Ing. José Naranjo  
**Periodo académico:** 2026B–2027A  
**Entregable:** PPE05 – Entregable 3: Catálogo de Requerimientos y Análisis de Refinamiento

---

## 1. Objetivo

Organizar los requerimientos identificados para AsoGest EPN, clasificándolos por tipo, nivel, fuente y estado. El catálogo sirve como referencia para mantener la trazabilidad entre las necesidades de los interesados, el documento de Visión y Alcance y las decisiones tomadas durante el análisis del sistema.

## 2. Contexto del sistema

AsoGest EPN busca reemplazar el registro de ventas, inventario y alquileres que actualmente se realiza mediante hojas de cálculo y anotaciones en papel. El sistema permitirá controlar las operaciones de mostrador, administrar productos y usuarios, registrar alquileres y garantías, consultar la disponibilidad de recursos y revisar los movimientos de caja.

La solución se plantea como una aplicación de escritorio desarrollada con Windows Forms, C# y .NET 8 o superior, con almacenamiento local mediante una base de datos relacional SQLite. La primera versión no contempla aplicaciones móviles, reservas remotas, pasarelas de pago, facturación electrónica ni exportación automática de reportes avanzados.

## 3. Criterios de clasificación

- **Tipo:** RF = Requerimiento Funcional; RNF = Requerimiento No Funcional; RD = Requerimiento de Dominio.
- **Nivel:** Usuario = expresa una necesidad visible para un interesado; Sistema = establece una función o condición interna que debe cumplir el software.
- **Estado:** Aprobado = respaldado por los acuerdos y documentos vigentes; Analizado = definido, pero requiere comprobación o ajuste durante el diseño; Propuesto = ampliación que requiere validación antes de incorporarse al alcance.
- **Fuente:** interesado, documento o registro de información del que procede la necesidad.

## 4. Catálogo de requerimientos

### 4.1 Requerimientos funcionales

| ID | Descripción del requerimiento | Tipo | Nivel | Fuente | Estado |
|---|---|---|---|---|---|
| RF-01 | El sistema deberá registrar cada venta con el identificador del producto, cantidad, precio unitario, fecha y hora exactas, total calculado e identificador del operador que mantiene la sesión activa. | Funcional | Sistema | Estudiantes operadores; registro I-03; Visión y Alcance, sección 2.1 | Aprobado |
| RF-02 | El sistema deberá actualizar las existencias al confirmar una venta. Si la cantidad vendida supera el stock registrado, permitirá completar la operación conforme al acuerdo operativo y generará un saldo negativo junto con una incidencia de inventario para su revisión administrativa. | Funcional | Sistema | Tesorero/Administrador externo; Matriz de Interesados, sección 3.2; Visión y Alcance, sección 2.1 | Aprobado |
| RF-03 | El sistema deberá registrar cada alquiler solicitando obligatoriamente el nombre del cliente, número de cédula, identificador del recurso, fecha, hora de inicio y hora de finalización en formato HH:MM. No permitirá guardar el registro si falta alguno de estos datos. | Funcional | Sistema | Operador y clientes; registro I-04; formato actual de alquileres | Aprobado |
| RF-04 | El sistema deberá permitir consultar la disponibilidad de cada recurso mediante un listado estructurado que muestre los horarios ocupados y libres para la fecha seleccionada. | Funcional | Usuario | Estudiantes clientes y operadores; registro I-05; Visión y Alcance, sección 2.1 | Aprobado |
| RF-05 | El sistema deberá impedir la confirmación de un alquiler cuando su intervalo de tiempo se cruce total o parcialmente con otro alquiler confirmado para el mismo recurso y fecha. | Funcional | Sistema | Estudiantes operadores; registro I-05; definición de solapamiento en Visión y Alcance | Aprobado |
| RF-06 | El sistema deberá permitir al Administrador Principal crear, modificar y suspender cuentas, asignar roles y registrar los inicios y cierres de sesión de los usuarios. | Funcional | Sistema | Presidente de la Asociación; registro I-07; Matriz de Interesados | Aprobado |
| RF-07 | El sistema deberá restringir la creación y modificación de productos y tarifas a los perfiles autorizados de Administrador Principal y Tesorero/Administrador Externo, impidiendo que el Operador Estudiantil altere dichos datos. | Funcional | Sistema | Presidente y Tesorero/Administrador externo; registro I-06; Visión y Alcance, sección 2.1 | Aprobado |
| RF-08 | El sistema deberá mostrar en pantalla el resumen de caja del día y los movimientos registrados por turno y operador, para facilitar la revisión del Tesorero/Administrador Externo. La exportación automática a Excel no formará parte de esta versión. | Funcional | Usuario | Tesorero/Administrador externo; Visión y Alcance, sección 2.1 y exclusiones de la sección 2.2 | Aprobado |
| RF-09 | El sistema deberá registrar una incidencia cuando una operación de venta produzca existencias negativas, almacenando como mínimo el producto afectado, la cantidad involucrada, la fecha y hora y el usuario responsable, para permitir su revisión administrativa. | Funcional | Sistema | Tesorero/Administrador externo; Matriz de Interesados, sección 2; Visión y Alcance, sección 2.1 | Analizado |
| RF-10 | El sistema deberá ofrecer, en una iteración posterior, una vista gráfica tipo calendario para consultar los intervalos libres y ocupados de los recursos, manteniendo la validación de solapamientos establecida en RF-05. | Funcional | Usuario | Clientes y operadores; registro I-05; Visión y Alcance, sección 2.1 | Propuesto |

### 4.2 Requerimientos no funcionales

| ID | Descripción del requerimiento | Tipo | Nivel | Fuente | Estado |
|---|---|---|---|---|---|
| RNF-01 | La interfaz deberá permitir completar el registro de una venta de hasta tres productos en un tiempo igual o inferior a 10 segundos, medido desde la selección del primer producto hasta la confirmación de la operación. | No Funcional | Sistema | Estudiantes operadores; declaración 3 de adquisición; Visión y Alcance, sección 3 | Analizado |
| RNF-02 | El sistema deberá poder realizar las operaciones principales desde la computadora del mostrador sin depender de una conexión a Internet, utilizando almacenamiento local. | No Funcional | Sistema | Personal de T.I. y Decanato; registro I-01; Visión y Alcance, sección 3 | Aprobado |
| RNF-03 | El sistema no deberá almacenar contraseñas en texto plano; las credenciales deberán guardarse mediante el mecanismo de hashing definido para el proyecto y ser verificables durante la autenticación. La especificación vigente del proyecto establece SHA-256. | No Funcional | Sistema | Responsable de Seguridad; Visión y Alcance, secciones 2.1 y 3 | Analizado |
| RNF-04 | La aplicación deberá implementarse como software de escritorio utilizando Windows Forms con C# y .NET 8 o superior, y deberá ejecutarse en la computadora destinada al mostrador de la asociación. | No Funcional | Sistema | Restricción tecnológica del proyecto; Visión y Alcance, sección 3 | Aprobado |
| RNF-05 | La información operativa deberá almacenarse en una base de datos relacional local SQLite, sin requerir servidores en la nube para el funcionamiento de la primera versión. | No Funcional | Sistema | Personal de T.I.; Visión y Alcance, sección 3 | Aprobado |

### 4.3 Requerimientos de dominio

| ID | Descripción del requerimiento | Tipo | Nivel | Fuente | Estado |
|---|---|---|---|---|---|
| RD-01 | Todo alquiler deberá contar con la recepción y retención temporal de una garantía física válida: carné universitario de la EPN o cédula de ciudadanía original. Si el operador no confirma la recepción de la garantía, el sistema no permitirá confirmar el alquiler. | Dominio | Sistema | Reglamento interno de la Asociación; Presidente; Matriz de Interesados, sección 3.2 | Aprobado |
| RD-02 | Cuando una venta genere existencias negativas, el movimiento deberá quedar identificado como una incidencia para que el Tesorero/Administrador Externo pueda revisarlo y realizar el control correspondiente. | Dominio | Sistema | Acuerdo operativo descrito en la Matriz de Interesados, sección 3.2; Visión y Alcance, sección 2.1 | Analizado |

## 5. Trazabilidad con la información adquirida

La siguiente relación permite identificar el origen de los requerimientos en los documentos anteriores:

| Registro / fuente | Necesidad identificada | Requerimientos relacionados |
|---|---|---|
| I-01 – Manejo actual en hojas de cálculo | Reemplazar registros dispersos y disponer de almacenamiento local. | RF-01, RF-08, RNF-02, RNF-05 |
| I-02 – Trazabilidad por usuario y sesión | Identificar al responsable de cada operación y controlar las sesiones. | RF-01, RF-06, RF-08 |
| I-03 – Venta y descuento de stock | Registrar ventas y actualizar inventario. | RF-01, RF-02, RF-09, RD-02 |
| I-04 – Datos obligatorios de alquiler | Registrar los datos del cliente y del recurso alquilado. | RF-03, RD-01 |
| I-05 – Control de horarios | Consultar disponibilidad y evitar reservas cruzadas. | RF-04, RF-05, RF-10 |
| I-06 – Control del catálogo | Restringir la modificación de productos y tarifas. | RF-07 |
| I-07 – Bitácora de sesiones | Registrar los inicios y cierres de sesión. | RF-06 |
| I-08 – Operación por estudiantes o externos | Diferenciar permisos según el rol del usuario. | RF-06, RF-07 |
| Visión y Alcance, sección 3 | Respetar tecnología, funcionamiento local y tiempo de atención. | RNF-01, RNF-02, RNF-04, RNF-05 |

## 6. Observaciones del catálogo

1. Los requerimientos RF-01 a RF-07 conservan la identificación y el propósito de los requerimientos funcionales establecidos en el taller anterior, con ajustes de redacción para mejorar su verificabilidad.
2. RF-08 se expresa como consulta en pantalla, debido a que el documento de Visión y Alcance excluye la exportación automática de reportes en Excel para esta versión.
3. RF-09 y RD-02 documentan el tratamiento de existencias negativas e incidencias que aparece en la Matriz de Interesados y en el documento de Visión y Alcance.
4. RF-10 representa la vista gráfica tipo calendario como una capacidad de una iteración posterior; la primera versión puede operar con un listado estructurado.
5. RNF-03 conserva SHA-256 porque es el mecanismo indicado en los documentos anteriores. Su precisión técnica se revisa en el informe de refinamiento antes de considerarlo una especificación definitiva.

---
**Fin del documento 01_Catalogo_Requerimientos.md**
