## ESCUELA POLITÉCNICA NACIONAL FACULTAD DE INGENIERÍA ELÉCTRICA Y ELECTRÓNICA Matriz de Interesados (Stakeholders)

Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN — Caso de Estudio: Asociación de Ingeniería Química (AsoGest EPN)

| Asignatura | Diseño y Programación | Entregable | 02_Matriz_Interesados |
| --- | --- | --- | --- |
|   | de Software |   |   |
| Docente | Ing. Jose Naranjo | Fecha realización | 21 de Noviembre de |
|   |   |   | 2026 |
| Integrantes (Grupo | Jeziel Silva, Mateo | Fecha de entrega | 26 de Noviembre de |
| C) | Paredes, David Vega |   | 2026 |

## 1. Introducción

El presente documento identifica, clasifica y analiza a los actores involucrados directa o indirectamente en la operación y supervisión del sistema AsoGest EPN, correspondiente al Producto 2 de la guía de referencia (Fase 3 del Taller de Ingeniería de Requerimientos del Grupo C). Su propósito es establecer el nivel de interés e influencia de cada interesado, documentar sus expectativas operativas y definir estrategias formales de resolución ante conflictos de intereses entre roles administrativos y operativos.


## 2. Matriz de Identificación y Análisis de Interesados

| Interesado |   | Clasificación Interés | Influencia Necesidad Principal |   | Posibles Conflictos |
| --- | --- | --- | --- | --- | --- |
| Presidente de | Interno / | Alto | Alta | Mantener el control | Exige restringir la modifi- |
| la Asociación | Directo |   |   | centralizado del catálogo | cación de precios y usua- |
|   |   |   |   | de productos, tarifas, | rios a los perfiles directi- |
|   |   |   |   | gestión de usuarios/roles | vos, lo que puede ralenti- |
|   |   |   |   | (RBAC [1]) y reportes | zar correcciones urgentes |
|   |   |   |   | institucionales. | en mostrador si no están |
|   |   |   |   |   | presentes. |
| Tesorero / | Interno / | Alto | Alta | Gestión de catálo- | Demanda controles rígi- |
| Administrador | Directo |   |   | go/tarifas (junto al | dos de autorización pa- |
| Externo |   |   |   | Presidente), auditoría | ra cada anulación y audi- |
|   |   |   |   | estricta, cuadre de caja | toría de saldos negativos, |
|   |   |   |   | diario, trazabilidad por | chocando con la agilidad |
|   |   |   |   | operador y control de | operativa que exigen los |
|   |   |   |   | incidencias de stock. | operadores en horas pico. |
| Estudiantes | Interno / | Alto | Media | Interfaz ultrarrápida | Priorizan la velocidad pa- |
| Operadores | Directo |   |   | (<10s por venta), pro- | ra despachar filas durante |
|   |   |   |   | ceso ágil de registro de | los recesos sobre los pa- |
|   |   |   |   | ventas y alquileres sin | sos de validación estric- |
|   |   |   |   | hojas sueltas, y facilidad | ta, controles de auditoría |
|   |   |   |   | de cierre de turno. | y cierres de sesión indivi- |
|   |   |   |   |   | duales. |
| Estudiantes | Externo / | Medio | Media | Visualización clara y | Desean flexibilidad en |
| (Clientes | Directo |   |   | transparente de horarios | tiempos de uso o alqui- |
| EPN) |   |   |   | disponibles de equi- | lar insumos sin portar el |
|   |   |   |   | pos/recursos, tiempos de | carné físico, contravinien- |
|   |   |   |   | espera mínimos y cobros | do el reglamento interno |
|   |   |   |   | justos. | de garantías (RD-01). |
| Decanato / | Externo / | Medio | Media | Transparencia conta- | Solicita informes formales |
| Autoridades | Indirecto |   |   | ble en la rendición de | y respaldo seguro de da- |
| EPN |   |   |   | cuentas de fondos uni- | tos, mientras la directiva |
|   |   |   |   | versitarios, cumplimiento | estudiantil prioriza la sim- |
|   |   |   |   | normativo y seguridad de | plicidad operacional del |
|   |   |   |   | la información local. | día a día. |
| Proveedores | Externo / | Bajo | Baja | Comprobantes claros y | Pueden requerir registros |
|   | Indirecto |   |   | ordenados de recepción | detallados de recepción |
|   |   |   |   | de mercadería e ingresos | que exceden el flujo bá- |
|   |   |   |   | de inventario para conci- | sico de ventas en mos- |
|   |   |   |   | liación de entregas. | trador contemplado en el |
|   |   |   |   |   | Producto Mínimo Viable. |

## 3. Análisis y Resolución de Conflictos

## 3.1 Naturaleza de los Conflictos Identificados

Durante el levantamiento de información se detectaron dos tensiones principales entre los interesados:

- \- Agilidad Operativa vs. Control y Auditoría: Existe un conflicto operativo clave entre la gestión realizada por los Estudiantes Operadores (rotativos, tiempo parcial, enfocados en despachar filas en recesos en menos de 10 segundos sin frenar ventas por desfases de inventario) y la gestión del Tesorero / Administrador Externo y el Presidente (enfocados en auditoría contable, trazabilidad individual, bloqueo de cambios de precios y control estricto de inventario).


- \- Flexibilidad al Cliente vs. Cumplimiento Normativo (Garantías): Los Estudiantes (Clientes) buscan acceder rápidamente a mandiles, material de laboratorio o consolas incluso cuando olvidan su documento universitario, mientras que el reglamento defendido por la directiva exige la retención física obligatoria de garantía (carné EPN o cédula original).

## 3.2 Estrategia y Resolución de Conflictos

Para armonizar las necesidades de todos los actores sin comprometer la integridad del sistema, el equipo de ingeniería estableció la siguiente secuencia de negociación y resolución:

- \- Implementación de Control de Acceso Basado en Roles (RBAC) Dual [1]: El sistema separa la operación en dos niveles que nos lleven a un correcto funcionamiento del sistema: un Modo Operativo Ágil para el Estudiante Operador (que permite registrar ventas sin bloqueo por stock en cero —registrando valores negativos con su respectiva incidencia automática— y procesar alquileres rápidamente bajo su sesión activa) y un Modo Administración y Auditoría exclusivo para el Presidente y Tesorero/Administrador Externo (reservado para administrar catálogo y tarifas, gestionar cuentas, auditar cortes de caja y revisar incidencias de inventario). [URL 🔗](#page-0)

- \- Acuerdos de Priorización por Fases (Negociación de Alcance): Debido al tiempo limitado del bimestre, se negociaron dos concesiones clave para la primera entrega: el Tesorero aceptó aplazar la exportación de reportes en Excel a cambio de consultar los cierres de caja diarios en pantalla detallados por operador; por su parte, los Operadores aceptaron usar inicialmente una tabla simple de horarios en lugar de un calendario visual, siempre que el sistema bloquee automáticamente cualquier cruce de reservas.

- \- Automatización de Reglas de Dominio Ineludibles: Para eliminar discusiones en el mostrador respecto a garantías, el formulario de alquiler incorpora una validación obligatoria de recepción física de documento institucional, respaldando al operador frente al cliente mediante una regla objetiva del sistema.

Nota de Trazabilidad: Esta matriz consolida los actores y mecanismos de resolución definidos en la Fase 3 (Desafíos 3.1 y 3.2), Fase 6 (Desafío 6.3) y Fase 9 (Desafío 9.3) del Taller de Ingeniería de Requerimientos del Grupo C, en concordancia con el documento 01_Vision_y_Alcance.

## 4. Bibliografía

- [1] Kosinski, G. L. M. (2026, 16 de agosto). ¿Qué es el control de acceso basado en roles (RBAC)? IBM. https://www.ibm.com/mx-es/think/topics/rbac [URL 🔗](https://www.ibm.com/mx-es/think/topics/rbac)
