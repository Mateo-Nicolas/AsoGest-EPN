## ESCUELA POLITÉCNICA NACIONAL FACULTAD DE INGENIERÍA ELÉCTRICA Y ELECTRÓNICA Documento de Visión y Alcance del Sistema

Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN — Caso de Estudio: Asociación de Ingeniería Química (AsoGest EPN)

| Asignatura | Diseño y Programación | Entregable | 01_Vision_y_Alcance |
| --- | --- | --- | --- |
|   | de Software |   |   |
| Docente | Ing. Jose Naranjo | Fecha realizacion | 21 de Noviembre de |
|   |   |   | 2026 |
| Integrantes (Grupo | Jeziel Silva, Mateo | Fecha de entrega | 26 de Noviembre de |
| C) | Paredes, David Vega |   | 2026 |

## 1. Introducción

## 1.1 Propósito del Documento

El presente documento establece la visión general, los límites funcionales y las restricciones operativas del software AsoGest EPN. Su objetivo es unificar todas las expectativas de los involucrados como: presidente de la asociación, tesorero o administrador externo, estudiantes operadores, clientes y decanato. Además, servir como referencia principal para el diseño, desarrollo y validación de la solución.

## 1.2 Contexto

En la Escuela Politécnica Nacional (EPN), las asociaciones estudiantiles gestionadas por alumnos y/o administradores externos comercializan productos de consumo (alimentos, bebidas, copias y útiles, entre otros) y administran el alquiler temporal de recursos e instalaciones (mandiles, puntas de prueba, material de laboratorio, consolas de videojuegos, mesas de billar/ping-pong y casilleros, entre otros). Actualmente, el registro se lo realiza mediante hojas de cálculo (Excel) y anotaciones en papel que genera inconsistencias contables, descuadres de caja, retrasos en horas pico, traslape de turnos sin cierre de sesión individual y en algunos casos dobles reservas o inconsistencias en las horas.

## 2. Alcance del Sistema

## 2.1 Funcionalidades Incluidas (Dentro del Alcance)

De acuerdo con la priorización MoSCoW realizada anteriormente y los acuerdos de negociación establecidos con los interesados para la primera versión operativa del sistema, la solución comprenderá los siguientes módulos y capacidades:

- \- Gestión de Usuarios y Control de Acceso (RBAC): Creación, modificación y suspensión de cuentas de usuario con asignación de roles diferenciados [1], de los cuales tenemos: administrador principal/presidente, tesorero/administrador externo y operador estudiantil, incluyendo registro de inicios y cierres de sesión y almacenamiento de contraseñas cifradas mediante hashing SHA-256 [3]. [URL 🔗](#page-0)

- \- Administración del Catálogo e Inventario: Gestión centralizada de productos y tarifas restringida exclusivamente al Administrador Principal y/o Tesorero/Administrador externo, acompañada del descuento automático de stock en tiempo real al confirmar cada venta. Cabe recalcar el uso de valores negativos en los registros para evitar desfases de productos, con su debido registro de incidencia.


- \- Registro Transaccional de Ventas en Mostrador: Captura ágil de ventas registrando producto, cantidad, precio unitario, fecha/hora exacta e identificador del operador en sesión activa, eliminando las anotaciones intermedias en papel.

- \- Gestión de Alquileres y Control de Garantías: Registro obligatorio de alquileres con nombre del cliente, número de cédula, recurso seleccionado, hora/minuto de inicio y fin (formato HH:MM) y verificación de retención de garantía física (carné universitario o cédula original) conforme al reglamento interno de cada asociación.

- \- Validación Automática de Disponibilidad: Consulta de horarios disponibles (mediante listado estructurado en la entrega inicial y vista gráfica tipo calendario en iteración posterior) con bloqueo automático ante cualquier intento de solapamiento de intervalos para un mismo recurso.

- \- Consulta de Cuadre de Caja y Respaldo Local: Visualización en pantalla de los movimientos y totales diarios por turno para auditoría del Tesorero/Administrador Externo, operando sobre una base de datos relacional local.

## 2.2 Funcionalidades Excluidas (NO Alcance)

Con el fin de evitar la inflación del alcance y cumplir con los plazos académicos del bimestre, quedan explícitamente fuera de esta versión los siguientes requerimientos:

- \- Aplicaciones Móviles o Portales Web de Autogestión: No se desarrollarán aplicaciones nativas para iOS/Android ni reservas remotas realizadas directamente por los estudiantes desde fuera del mostrador.

- \- Pasarelas de Pago Electrónico y Facturación SRI: El sistema no integrará cobros con tarjetas de crédito/débito, transferencias bancarias automatizadas ni emisión de comprobantes electrónicos ante el Servicio de Rentas Internas.

- \- Exportación Automática de Reportes Avanzados en Excel: Conforme al acuerdo de negocia- ción con el Tesorero, la generación automatizada de archivos de balance exportables se difiere para una versión futura; en esta etapa los cortes se consultarán directamente en pantalla.

- \- Cálculo Automático de Multas por Mora o Daños: El sistema registrará los horarios pactados de inicio y fin, pero la liquidación económica por devoluciones tardías o daños físicos a equipos se gestionará manualmente según el reglamento de la asociación.

- \- Integración con Sistemas Institucionales de la EPN: No existirá conexión directa con bases de datos académicas del SAEw ni del Decanato.

## 3. Restricciones del Proyecto

El diseño e implementación de AsoGest EPN se sujetan a las siguientes limitaciones técnicas, operativas y organizacionales:

- \- Restricción Tecnológica y de Plataforma: La aplicación debe desarrollarse exclusivamente co- mo software de escritorio en Windows Forms (C# / .NET 8 o superior) para ejecutarse en la computadora del mostrador de la asociación.

- \- Restricción de Conectividad (Arquitectura Local): Dado que la conectividad a Internet puede presentar intermitencias, el sistema debe operar de forma local utilizando un motor de base de datos relacional embebido propuesto (SQLite [2], con posibilidad de migrar a MySQL/PostgreSQL) abierto a futuras modificaciones, sin depender de servidores en la nube. [URL 🔗](#page-0)

- \- Restricción de Rendimiento en Mostrador: Para evitar filas durante los recesos universitarios, el flujo de registro de una venta se debe completarse en un tiempo igual o inferior a 10 segundos.


- \- Restricción Normativa y de Seguridad: El sistema no puede autorizar ningún alquiler si no se confirma la recepción de la garantía física institucional (carné EPN o cédula), y todas las credenciales deben almacenarse encriptadas mediante SHA-256 sin texto plano [3]. [URL 🔗](#page-0)

- \- Restricción Presupuestaria y de Tiempo: El desarrollo debe completarse dentro del cronograma del periodo académico 2026B–2027A por los tres integrantes del Grupo C, sin incurrir en costos de licenciamiento de software propietario o hardware adicional.

## 4. Definiciones y Abreviaturas

|   | Definición Contextual en el Negocio |
| --- | --- |
| Término / Sigla |   |
| Aso / Asociación | Asociación de Estudiantes de la Escuela Politécnica Nacional (ej. Inge- |
|   | niería Química), entidad estudiantil que administra la venta de productos |
|   | y alquiler de recursos. |
| Producto Comercial | Artículo de consumo directo o papelería (alimentos, bebidas, copias, úti- |
|   | les) sujeto a control de existencias (stock) e inventario. |
| Recurso / Insumo | Bien reutilizable o espacio de entretenimiento propiedad de la asocia- |
|   | ción (mandiles, puntas de prueba, consolas de videojuegos, mesas de |
|   | billar/ping-pong, casilleros) disponible por bloques horarios. |
| Operador Estudiantil | Estudiante integrante de la directiva o colaborador de turno encargado |
|   | de atender en mostrador, registrar ventas y gestionar alquileres. |
| Administrador Externo | Gestor permanente o tesorero contratado/designado para supervisar la |
|   | contabilidad, el arqueo de caja y el cumplimiento normativo de la aso- |
|   | ciación. |
| Garantía Física | Documento oficial (carné universitario de la EPN o cédula de ciudadanía |
|   | original) retenido temporalmente durante el lapso de un alquiler como |
|   | respaldo de devolución. |
| Cuadre / Arqueo de Ca- | Proceso de conciliación diaria entre el dinero físico recaudado en el mos- |
| ja | trador y los registros digitales generados por cada operador durante su |
|   | turno. |
| Solapamiento | Intersección temporal (total o parcial) entre dos solicitudes de alquiler |
|   | para un mismo recurso dentro de una misma fecha y franja horaria. |
| RBAC | Role-Based Access Control (Control de Acceso Basado en Roles); meca- |
|   | nismo que restringe permisos operativos y administrativos según el perfil |
|   | autenticado [1]. |
| SRS | Software Requirements Specification (Especificación de Requerimientos |
|   | de Software). |

Nota de Trazabilidad: Este documento de Visión y Alcance guarda estricta correspondencia con los requeri- mientos funcionales (RF-01 a RF-08), no funcionales (RNF-01 a RNF-03) y de dominio (RD-01) levantados y validados en el Taller de Ingeniería de Requerimientos del Grupo C.

## 5. Bibliografía

- [1] Kosinski, G. L. M. (2026, 16 de agosto). ¿Qué es el control de acceso basado en roles (RBAC)? IBM. https://www.ibm.com/mx-es/think/topics/rbac [URL 🔗](https://www.ibm.com/mx-es/think/topics/rbac)


- [2] SQLite: La Base de Datos Embebida. (s. f.). SG Buzz. https://sg.com.mx/revista/17/ sqlite-la-base-datos-embebida [URL 🔗](https://sg.com.mx/revista/17/sqlite-la-base-datos-embebida)

- [3] Team, E. (2026, 26 de julio). ¿Qué es SHA-256? | Consultoría de cifrado. Encryption Consulting LLC. https://www.encryptionconsulting.com/es/education-center/sha-256/ [URL 🔗](https://www.encryptionconsulting.com/es/education-center/sha-256/)
