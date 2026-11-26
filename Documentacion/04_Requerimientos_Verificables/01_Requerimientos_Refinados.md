# 01. Requerimientos Refinados y Verificables – AsoGest EPN

**Escuela Politécnica Nacional**  
**Asignatura:** Diseño y Programación de Software  
**Proyecto:** Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN – Asociación de Ingeniería Química (AsoGest EPN)  
**Grupo:** Grupo C  
**Integrantes:** Jeziel Silva, Mateo Paredes y David Vega  
**Docente:** Ing. José Naranjo  
**Periodo académico:** 2026B–2027A  
**Entregable:** PPE06 – Entregable 4: Requerimientos Refinados y Verificables

## 1. Objetivo

Presentar la versión refinada de los requerimientos de AsoGest EPN para que cada uno tenga una redacción clara, verificable y relacionada con su fuente. Se conserva la identificación utilizada en el catálogo del Entregable 3.

## 2. Alcance del sistema

AsoGest EPN es una aplicación de escritorio para apoyar la administración de ventas, inventario, alquileres, usuarios y caja de la Asociación de Estudiantes de Ingeniería Química. La solución está planteada con Windows Forms, C# y .NET 8 o superior, y utiliza una base de datos local SQLite. La primera versión no contempla aplicaciones móviles, reservas remotas, pasarelas de pago, facturación electrónica ni exportación automática de reportes a Excel.

## 3. Criterios utilizados

Los enunciados comienzan con la expresión “El sistema deberá” o, para condiciones de calidad, con “La interfaz deberá”. Cada enunciado expresa una condición principal. Se evitaron expresiones subjetivas y se redactaron criterios de aceptación que pueden comprobarse mediante revisión o pruebas. La prioridad se asignó con MoSCoW: Must (indispensable), Should (importante), Could (deseable) y Won't (fuera de esta versión).

## 4. Nota sobre el alcance y las decisiones anteriores

RF-10 se mantiene como una mejora de una iteración posterior y recibe prioridad Could. La consulta de disponibilidad de la primera versión se realiza mediante un listado. RNF-03 no fija SHA-256 como decisión técnica definitiva: el Entregable 3 ya advertía que su uso para proteger contraseñas debía validarse. Por ello, el requerimiento exige almacenamiento mediante valores hash y deja la elección final del algoritmo sujeta a validación técnica.

## 5. Fichas de requerimientos

### RF-01 – Registro de ventas

- **Identificador:** RF-01
- **Nombre:** Registro de ventas
- **Enunciado:** El sistema deberá registrar cada venta con el identificador del producto, la cantidad, el precio unitario, la fecha, la hora, el total calculado y el identificador del operador con sesión activa.
- **Fuente:** Estudiantes operadores; registro I-03; documento de Visión y Alcance, sección 2.1.
- **Prioridad:** Must
- **Criterio de aceptación:** Al confirmar una venta, el sistema guarda todos los datos indicados y muestra la venta en el historial. El total almacenado coincide con la suma de los precios unitarios multiplicados por sus cantidades.
- **Dependencias:** Ninguna.

### RF-02 – Actualización del inventario

- **Identificador:** RF-02
- **Nombre:** Actualización del inventario
- **Enunciado:** El sistema deberá actualizar las existencias de cada producto al confirmar una venta, restando la cantidad vendida de la existencia registrada.
- **Fuente:** Tesorero/Administrador Externo; Matriz de Interesados, sección 3.2; documento de Visión y Alcance, sección 2.1.
- **Prioridad:** Must
- **Criterio de aceptación:** Después de confirmar una venta, la existencia del producto disminuye exactamente en la cantidad vendida. Si el resultado es negativo, la venta se completa y el saldo negativo queda registrado.
- **Dependencias:** RF-01.

### RF-03 – Registro de alquileres

- **Identificador:** RF-03
- **Nombre:** Registro de alquileres
- **Enunciado:** El sistema deberá registrar cada alquiler con el nombre del cliente, número de cédula, identificador del recurso, fecha, hora de inicio y hora de finalización en formato HH:MM.
- **Fuente:** Operadores y clientes; registro I-04; formato actual de alquileres.
- **Prioridad:** Must
- **Criterio de aceptación:** Al guardar un alquiler, el registro contiene los seis datos solicitados. Si falta uno de ellos, el sistema impide guardar el alquiler e identifica el campo pendiente.
- **Dependencias:** RD-01.

### RF-04 – Consulta de disponibilidad

- **Identificador:** RF-04
- **Nombre:** Consulta de disponibilidad
- **Enunciado:** El sistema deberá mostrar, mediante un listado, los horarios libres y ocupados de cada recurso para la fecha seleccionada.
- **Fuente:** Estudiantes clientes y operadores; registro I-05; documento de Visión y Alcance, sección 2.1.
- **Prioridad:** Must
- **Criterio de aceptación:** Al seleccionar una fecha y un recurso, el sistema presenta un listado que identifica los intervalos ocupados y los intervalos disponibles para esa fecha.
- **Dependencias:** RF-03.

### RF-05 – Validación de horarios

- **Identificador:** RF-05
- **Nombre:** Validación de horarios
- **Enunciado:** El sistema deberá impedir la confirmación de un alquiler cuando su intervalo de tiempo se cruce total o parcialmente con otro alquiler confirmado para el mismo recurso y fecha.
- **Fuente:** Estudiantes operadores; registro I-05; definición de solapamiento del documento de Visión y Alcance.
- **Prioridad:** Must
- **Criterio de aceptación:** Al intentar confirmar un alquiler que comparte cualquier parte de su intervalo con otro alquiler confirmado del mismo recurso y fecha, el sistema rechaza la confirmación. Un intervalo sin cruce puede confirmarse si cumple las demás condiciones.
- **Dependencias:** RF-03, RF-04.

### RF-06 – Administración de usuarios

- **Identificador:** RF-06
- **Nombre:** Administración de usuarios
- **Enunciado:** El sistema deberá permitir al Administrador Principal crear, modificar y suspender cuentas de usuario, asignar roles y registrar los inicios y cierres de sesión.
- **Fuente:** Presidente de la Asociación; registro I-07; Matriz de Interesados.
- **Prioridad:** Must
- **Criterio de aceptación:** El Administrador Principal puede crear, editar y suspender una cuenta, asignar un rol y consultar el registro de inicios y cierres de sesión. Un usuario sin ese perfil no puede ejecutar esas acciones.
- **Dependencias:** RNF-03.

### RF-07 – Administración de productos y tarifas

- **Identificador:** RF-07
- **Nombre:** Administración de productos y tarifas
- **Enunciado:** El sistema deberá permitir la creación y modificación de productos y tarifas únicamente a los perfiles Administrador Principal y Tesorero/Administrador Externo.
- **Fuente:** Presidente y Tesorero/Administrador Externo; registro I-06; documento de Visión y Alcance, sección 2.1.
- **Prioridad:** Must
- **Criterio de aceptación:** Los perfiles Administrador Principal y Tesorero/Administrador Externo pueden crear y modificar productos y tarifas. El perfil Operador Estudiantil no puede realizar esas acciones.
- **Dependencias:** RF-06.

### RF-08 – Consulta de caja

- **Identificador:** RF-08
- **Nombre:** Consulta de caja
- **Enunciado:** El sistema deberá mostrar en pantalla el resumen de caja del día y los movimientos registrados por turno y operador.
- **Fuente:** Tesorero/Administrador Externo; documento de Visión y Alcance, sección 2.1 y exclusiones de la sección 2.2.
- **Prioridad:** Must
- **Criterio de aceptación:** Al consultar una fecha, el sistema muestra el resumen de caja y los movimientos asociados, agrupados por turno y operador. La primera versión no genera archivos de Excel.
- **Dependencias:** RF-01, RF-06.

### RF-09 – Registro de incidencias de inventario

- **Identificador:** RF-09
- **Nombre:** Registro de incidencias de inventario
- **Enunciado:** El sistema deberá registrar una incidencia cuando una venta produzca existencias negativas, incluyendo el producto afectado, la cantidad involucrada, la fecha, la hora y el usuario responsable.
- **Fuente:** Tesorero/Administrador Externo; Matriz de Interesados, sección 2; documento de Visión y Alcance, sección 2.1.
- **Prioridad:** Must
- **Criterio de aceptación:** Al confirmar una venta que deja existencias negativas, el sistema crea una incidencia que contiene los cinco datos indicados y permite que el responsable administrativo la consulte.
- **Dependencias:** RF-01, RF-02, RD-02.

### RF-10 – Vista gráfica de horarios

- **Identificador:** RF-10
- **Nombre:** Vista gráfica de horarios
- **Enunciado:** En una iteración posterior, el sistema deberá mostrar en una vista gráfica tipo calendario los intervalos libres y ocupados de cada recurso.
- **Fuente:** Clientes y operadores; registro I-05; documento de Visión y Alcance, sección 2.1.
- **Prioridad:** Could
- **Criterio de aceptación:** En la iteración que incluya esta mejora, al seleccionar un recurso y una fecha, el calendario representa los intervalos libres y ocupados y coincide con los datos consultados mediante el listado. Esta función no es obligatoria para la primera versión.
- **Dependencias:** RF-03, RF-04, RF-05.

### RNF-01 – Tiempo de respuesta en ventas

- **Identificador:** RNF-01
- **Nombre:** Tiempo de respuesta en ventas
- **Enunciado:** La interfaz deberá permitir completar el registro de una venta de hasta tres productos en un tiempo igual o inferior a 10 segundos, medido desde la selección del primer producto hasta la confirmación.
- **Fuente:** Estudiantes operadores; declaración 3 de adquisición; documento de Visión y Alcance, sección 3.
- **Prioridad:** Must
- **Criterio de aceptación:** En una prueba con hasta tres productos, el tiempo transcurrido entre la selección del primer producto y la confirmación de la venta es de 10 segundos o menos.
- **Dependencias:** RF-01.

### RNF-02 – Funcionamiento local

- **Identificador:** RNF-02
- **Nombre:** Funcionamiento local
- **Enunciado:** El sistema deberá permitir realizar las operaciones principales desde la computadora del mostrador sin depender de una conexión a Internet.
- **Fuente:** Personal de T.I. y Decanato; registro I-01; documento de Visión y Alcance, sección 3.
- **Prioridad:** Must
- **Criterio de aceptación:** Con la conexión a Internet desactivada, el usuario puede iniciar el sistema y ejecutar las operaciones principales definidas para la primera versión utilizando los datos locales.
- **Dependencias:** RNF-04, RNF-05.

### RNF-03 – Protección de credenciales

- **Identificador:** RNF-03
- **Nombre:** Protección de credenciales
- **Enunciado:** El sistema deberá almacenar las contraseñas únicamente mediante valores hash y no deberá conservar contraseñas en texto plano.
- **Fuente:** Responsable de Seguridad; documento de Visión y Alcance, secciones 2.1 y 3; observación del análisis del Entregable 3.
- **Prioridad:** Must
- **Criterio de aceptación:** Al revisar los datos almacenados, no se encuentran contraseñas en texto plano. Durante el inicio de sesión, el sistema verifica la contraseña ingresada mediante el mecanismo de hashing definido para el proyecto. La selección técnica definitiva del algoritmo queda pendiente de validación.
- **Dependencias:** RF-06.

### RNF-04 – Tecnología de desarrollo

- **Identificador:** RNF-04
- **Nombre:** Tecnología de desarrollo
- **Enunciado:** La aplicación deberá implementarse como software de escritorio utilizando Windows Forms con C# y .NET 8 o superior.
- **Fuente:** Restricción tecnológica del proyecto; documento de Visión y Alcance, sección 3.
- **Prioridad:** Must
- **Criterio de aceptación:** La solución compila y se ejecuta como aplicación Windows Forms desarrollada en C# sobre .NET 8 o una versión superior.
- **Dependencias:** Ninguna.

### RNF-05 – Almacenamiento local

- **Identificador:** RNF-05
- **Nombre:** Almacenamiento local
- **Enunciado:** El sistema deberá almacenar la información operativa en una base de datos relacional local SQLite, sin requerir servidores en la nube para la primera versión.
- **Fuente:** Personal de T.I.; documento de Visión y Alcance, sección 3.
- **Prioridad:** Must
- **Criterio de aceptación:** Al ejecutar las operaciones principales, los registros se guardan y se recuperan desde una base de datos SQLite local. El funcionamiento de la primera versión no requiere conexión a un servidor en la nube.
- **Dependencias:** RNF-02.

### RD-01 – Garantía física obligatoria

- **Identificador:** RD-01
- **Nombre:** Garantía física obligatoria
- **Enunciado:** El sistema deberá impedir la confirmación de un alquiler hasta que el operador registre la recepción física del carné universitario de la EPN o de la cédula de ciudadanía original como garantía.
- **Fuente:** Reglamento interno de la Asociación; Presidente; Matriz de Interesados, sección 3.2.
- **Prioridad:** Must
- **Criterio de aceptación:** Si el operador no marca la recepción de uno de los documentos válidos, el sistema no confirma el alquiler. Cuando registra la recepción, el sistema permite continuar si se cumplen las demás condiciones.
- **Dependencias:** RF-03.

### RD-02 – Control de existencias negativas

- **Identificador:** RD-02
- **Nombre:** Control de existencias negativas
- **Enunciado:** El sistema deberá identificar como incidencia cada movimiento de venta que genere existencias negativas para su revisión por el Tesorero/Administrador Externo.
- **Fuente:** Acuerdo operativo descrito en la Matriz de Interesados, sección 3.2; documento de Visión y Alcance, sección 2.1.
- **Prioridad:** Must
- **Criterio de aceptación:** Cada venta que produzca una existencia negativa queda asociada a una incidencia consultable por el Tesorero/Administrador Externo.
- **Dependencias:** RF-02, RF-09.

## 6. Revisión de las reglas de redacción

Se revisaron las 17 fichas incluidas en este documento. Los enunciados utilizan verbos de acción o condición que permiten identificar qué debe hacer el sistema. Se evitó incluir términos subjetivos como “rápido”, “amigable”, “óptimo” o “adecuado”. Cada ficha conserva el identificador del catálogo anterior y señala la fuente que originó la necesidad.

Los criterios de aceptación describen resultados observables que pueden comprobarse mediante pruebas funcionales, revisión de los datos almacenados o verificación de la tecnología utilizada. Las dependencias indican los requerimientos que deben estar disponibles para implementar o comprobar cada función.

## 7. Observaciones

- RF-02 describe la actualización de existencias y RF-09 describe el registro de la incidencia asociada. RD-02 mantiene la regla de dominio que exige identificar estos movimientos para su revisión.
- RF-03 se relaciona con RD-01 porque todo alquiler debe cumplir la regla de garantía física.
- RF-04 representa la consulta mediante listado para la primera versión. RF-10 queda como mejora futura.
- RNF-03 mantiene pendiente la validación del algoritmo específico de hashing, tal como se indicó en el análisis anterior.

## 8. Conclusión

Con este refinamiento, los requerimientos de AsoGest EPN cuentan con una identificación estable, una fuente, una prioridad, un criterio de aceptación y las dependencias correspondientes. La redacción permite comprender qué se espera del sistema y cómo se puede comprobar su cumplimiento durante el desarrollo y las pruebas.

---
**Fin del documento 01_Requerimientos_Refinados.md**
