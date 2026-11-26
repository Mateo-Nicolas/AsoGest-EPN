# 02. Informe de Análisis y Refinamiento – AsoGest EPN

**Escuela Politécnica Nacional – Facultad de Ingeniería Eléctrica y Electrónica**  
**Asignatura:** Diseño y Programación de Software  
**Proyecto:** Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN – Asociación de Ingeniería Química (AsoGest EPN)  
**Grupo:** C  
**Integrantes:** Jeziel Silva, Mateo Paredes y David Vega  
**Docente:** Ing. José Naranjo  
**Entregable:** PPE05 – Entregable 3: Catálogo de Requerimientos y Análisis de Refinamiento

---

## 1. Introducción

En este documento se realiza una revisión de los requerimientos del sistema AsoGest EPN. La finalidad es encontrar partes que no estén suficientemente claras, posibles contradicciones o aspectos que puedan causar problemas al momento de desarrollar el sistema.

Para realizar el análisis se tomaron como referencia el documento de Visión y Alcance y la Matriz de Interesados que fueron elaborados anteriormente por el Grupo C. Se busca que los requerimientos tengan una redacción más clara y que estén de acuerdo con las decisiones tomadas para la primera versión del proyecto.

## 2. Problemáticas detectadas

Durante la revisión se encontraron algunas situaciones que necesitaban aclaración o una mejor redacción.

### 2.1 Problema en el registro de horarios de alquiler (RF-03)

**Problemática:** En la primera descripción se indicaba que el sistema debía registrar el tiempo del alquiler, pero no se explicaba claramente cómo se debían guardar las horas.

**Justificación:** Si cada operador registra los horarios de una manera diferente, pueden aparecer errores al revisar la disponibilidad de los recursos. También sería más complicado comparar dos alquileres para saber si se cruzan.

**Corrección:** Se especificó que se debe registrar la fecha, la hora de inicio y la hora de finalización en formato HH:MM. También se aclaró que los datos del cliente y del recurso son obligatorios.

### 2.2 Problema con el inventario negativo (RF-02)

**Problemática:** En una primera interpretación se podía entender que el sistema debía bloquear una venta cuando no existieran suficientes unidades del producto.

**Justificación:** En los documentos anteriores se establece que el operador puede continuar con la venta aunque el stock llegue a cero o tenga un valor negativo. Esta decisión se tomó para no detener la atención en el mostrador, pero el movimiento debe quedar registrado para que el responsable administrativo lo revise.

**Corrección:** Se aclaró que el sistema permitirá completar la venta y actualizará el inventario. Si el resultado es negativo, también generará una incidencia para su revisión.

### 2.3 Problema con los reportes de caja (RF-08)

**Problemática:** Se podía interpretar que el sistema debía generar archivos de Excel con los reportes diarios.

**Justificación:** En el documento de Visión y Alcance se indica que la exportación automática de reportes avanzados a Excel queda fuera de la primera versión. Sin embargo, sí se necesita consultar los movimientos y totales diarios.

**Corrección:** Se aclaró que el sistema mostrará los movimientos y totales en pantalla, organizados por turno y operador. La exportación a Excel se deja para una versión futura.

### 2.4 Problema con la protección de contraseñas (RNF-03)

**Problemática:** En los documentos anteriores se utiliza la expresión “contraseñas encriptadas mediante SHA-256”.

**Justificación:** La expresión puede causar confusión porque SHA-256 es una función de hashing y no un cifrado que permita recuperar la contraseña original. Por esta razón, es mejor utilizar el término correcto al describir cómo se guardarán las credenciales.

**Corrección:** Se cambió la redacción para indicar que las contraseñas no se guardarán en texto plano y que se utilizará un mecanismo de hashing. Se mantiene la referencia a SHA-256 porque aparece en el documento anterior, pero se deja pendiente confirmar técnicamente si será el mecanismo definitivo para las contraseñas.

### 2.5 Problema con la consulta de horarios (RF-04 y RF-10)

**Problemática:** En la descripción de la solución se menciona una vista gráfica tipo calendario, pero también se indica que inicialmente se utilizará un listado de horarios.

**Justificación:** Si no se diferencia entre estas dos opciones, podría pensarse que el calendario gráfico es obligatorio para la primera entrega, aumentando el trabajo que debe realizar el grupo.

**Corrección:** Se separaron las funciones. RF-04 corresponde al listado de horarios para la primera versión y RF-10 queda como una mejora propuesta para una iteración posterior.

## 3. Dependencias entre requerimientos

Al revisar las funciones del sistema se encontró que algunas necesitan de otras para poder trabajar correctamente. Las principales dependencias son las siguientes:

**Dependencia 1: RF-02 depende de RF-01.**  
La actualización del inventario necesita que primero se registre y confirme una venta. A partir de la cantidad vendida, el sistema puede calcular cuántas unidades deben descontarse del stock.

**Dependencia 2: RF-09 depende de RF-01 y RF-02.**  
Para generar una incidencia, el sistema necesita conocer qué producto se vendió y cuál fue el resultado de la actualización del inventario. De esta manera puede identificar cuándo se produjo un valor negativo.

**Dependencia 3: RF-05 depende de RF-03 y RF-04.**  
Para evitar que dos alquileres se crucen, el sistema necesita tener los datos del alquiler, como el recurso, la fecha y las horas. También necesita consultar los horarios que ya se encuentran ocupados.

**Dependencia 4: RF-10 depende de RF-03, RF-04 y RF-05.**  
La vista gráfica de calendario necesita la información de los alquileres y de los horarios disponibles. Además, debe respetar la validación que impide reservar un recurso en un horario que ya está ocupado.

**Dependencia 5: RF-07 depende de RF-06.**  
Para controlar quién puede modificar los productos y las tarifas, primero es necesario que el sistema identifique al usuario y conozca el rol con el que inició sesión.

**Dependencia 6: RF-08 depende de RF-01 y RF-06.**  
La consulta de caja necesita la información de las ventas registradas y la identificación del operador que realizó cada una de ellas.

**Dependencia 7: RF-01, RF-03, RF-07 y RF-08 dependen de RNF-02, RNF-04 y RNF-05.**  
Estas funciones deben trabajar utilizando la aplicación de escritorio, la base de datos local y el funcionamiento sin conexión a Internet que se definieron para el proyecto.

**Dependencia 8: RF-06 depende de RNF-03.**  
La administración de usuarios y el inicio de sesión necesitan que las credenciales se almacenen de acuerdo con la condición de seguridad definida.

**Dependencia 9: RF-03 depende de RD-01.**  
El registro de un alquiler debe respetar la regla de la asociación que exige recibir una garantía física antes de confirmar el alquiler.

**Dependencia 10: RF-02 y RF-09 se relacionan con RD-02.**  
La regla de dominio establece que las existencias negativas deben quedar identificadas como incidencias para que el tesorero pueda revisarlas.

## 4. Análisis de viabilidad

### 4.1 Requerimiento seleccionado: RF-03 – Registro de alquileres

Se seleccionó el registro de alquileres porque es una de las actividades principales de la asociación. Además, necesita cumplir otras condiciones importantes, como evitar horarios cruzados y confirmar que se recibió la garantía física.

**Viabilidad técnica**

El requerimiento es posible de desarrollar con las herramientas definidas para el proyecto. Windows Forms permite crear un formulario para ingresar los datos del cliente y del recurso. C# permite realizar las validaciones de fechas y horas, mientras que SQLite permite guardar la información de los alquileres.

Para evitar que existan dos alquileres del mismo recurso en el mismo horario, se puede comparar la fecha y los intervalos registrados antes de confirmar una nueva reserva.

**Resultado:** Es técnicamente viable.

**Viabilidad económica**

El desarrollo utilizará las herramientas que ya fueron consideradas para el proyecto. No es necesario contratar un servidor en la nube ni implementar una plataforma de pagos para realizar el registro de alquileres.

**Resultado:** Es económicamente viable porque no requiere gastos adicionales importantes para esta función.

**Viabilidad temporal**

El requerimiento puede desarrollarse por partes. Primero se puede crear el formulario y guardar los datos en la base de datos. Después se pueden implementar las validaciones de horarios y la confirmación de la garantía física.

La vista gráfica de calendario se puede dejar para una siguiente iteración, ya que para la primera versión se acordó utilizar un listado de horarios.

**Resultado:** Es viable dentro del tiempo disponible si se desarrolla por etapas y se mantiene el alcance acordado.

**Viabilidad organizacional**

Los operadores ya realizan el registro de alquileres, aunque actualmente utilicen anotaciones o formatos manuales. Por eso, el cambio principal será realizar el mismo proceso desde el sistema. Los responsables de la asociación deberán explicar a los operadores cómo registrar los datos y confirmar la recepción de la garantía.

**Resultado:** Es organizacionalmente viable porque el sistema mantiene el proceso que ya conoce la asociación, pero lo organiza de manera digital.

### 4.2 Resultado general de la viabilidad

Después de revisar los cuatro aspectos, se considera que RF-03 puede implementarse en AsoGest EPN. Se recomienda comenzar con el formulario básico, el almacenamiento de los datos y las validaciones obligatorias. De esta manera se puede cumplir con la función principal sin agregar características que corresponden a versiones posteriores.

También se considera viable el registro de ventas y la actualización del inventario. Sin embargo, se debe comprobar que el registro de la venta, el descuento del stock y la creación de una incidencia se realicen correctamente para evitar que la información quede incompleta.

## 5. Versiones refinadas de los requerimientos

Después de revisar los problemas anteriores, se mejoró la redacción de los siguientes requerimientos.

### RF-02 – Actualización del inventario

**Versión inicial:**  
“El sistema descontará automáticamente el stock de productos en base a las ventas confirmadas”.

**Versión refinada:**  
“Cuando se confirme una venta, el sistema actualizará las existencias del producto según la cantidad vendida. Si el resultado es negativo, permitirá completar la operación y registrará una incidencia con el producto, la cantidad, la fecha, la hora y el usuario responsable”.

**Motivo del cambio:** Se explicó qué sucede cuando la cantidad vendida supera las existencias disponibles.

### RF-03 – Registro de alquileres

**Versión inicial:**  
“El sistema registrará los datos de la persona que alquila un recurso por el tiempo necesario”.

**Versión refinada:**  
“El sistema solicitará el nombre del cliente, número de cédula, recurso seleccionado, fecha, hora de inicio y hora de finalización en formato HH:MM. No permitirá guardar el alquiler si falta alguno de estos datos”.

**Motivo del cambio:** Se especificaron los datos que deben registrarse para evitar información incompleta.

### RF-04 – Consulta de disponibilidad

**Versión inicial:**  
“El sistema mostrará una interfaz gráfica tipo calendario con los intervalos libres y ocupados de cada recurso”.

**Versión refinada:**  
“En la primera versión, el sistema permitirá consultar mediante un listado los horarios libres y ocupados de cada recurso para una fecha seleccionada. La vista gráfica tipo calendario se considera una mejora para una iteración posterior”.

**Motivo del cambio:** Se separó lo que se realizará en la primera versión de las mejoras futuras.

### RF-08 – Consulta de caja

**Versión inicial:**  
“El sistema generará reportes diarios de balance contable y movimientos por turno en formato exportable”.

**Versión refinada:**  
“El sistema mostrará en pantalla el resumen de caja del día y los movimientos registrados por turno y operador. La exportación automática a Excel no estará disponible en la primera versión”.

**Motivo del cambio:** Se ajustó el requerimiento al alcance que se estableció anteriormente.

### RF-09 – Registro de incidencias de inventario

**Versión inicial:**  
Este requerimiento no estaba separado como una función independiente.

**Versión refinada:**  
“Cuando una venta genere existencias negativas, el sistema registrará una incidencia que contenga el producto, la cantidad involucrada, la fecha, la hora y el usuario responsable”.

**Motivo del cambio:** Se detalló cómo se registrarán los casos de inventario negativo para que puedan ser revisados.

### RNF-01 – Tiempo de respuesta

**Versión inicial:**  
“La interfaz de ventas debe ser rápida para atender de inmediato a los estudiantes”.

**Versión refinada:**  
“La interfaz deberá permitir completar una venta de hasta tres productos en un tiempo igual o inferior a 10 segundos, desde la selección del primer producto hasta la confirmación de la operación”.

**Motivo del cambio:** Se agregó una medida de tiempo para poder comprobar si se cumple el requerimiento.

### RNF-03 – Protección de credenciales

**Versión inicial:**  
“Las credenciales deben almacenarse encriptadas mediante SHA-256”.

**Versión refinada:**  
“El sistema no almacenará contraseñas en texto plano. Las credenciales se almacenarán mediante un mecanismo de hashing y se verificarán durante el inicio de sesión. El uso específico de SHA-256 deberá validarse técnicamente, ya que es el mecanismo mencionado en la documentación anterior”.

**Motivo del cambio:** Se corrigió el uso del término y se dejó pendiente confirmar el mecanismo definitivo.

### RD-01 – Garantía física

**Versión inicial:**  
“Las transacciones de alquiler exigen la retención de garantía conforme al reglamento interno de cada asociación”.

**Versión refinada:**  
“El sistema no permitirá confirmar un alquiler hasta que el operador indique que recibió físicamente el carné universitario de la EPN o la cédula de ciudadanía original como garantía”.

**Motivo del cambio:** Se explicó de forma directa qué debe comprobar el operador antes de confirmar el alquiler.

## 6. Aspectos que todavía deben revisarse

Después del análisis, se considera importante tener presentes los siguientes puntos:

- Se mantendrá el registro de existencias negativas, pero el Tesorero/Administrador Externo deberá revisar las incidencias generadas.
- Los reportes se consultarán en pantalla. La exportación a Excel no se incluirá en esta primera versión.
- La consulta de horarios se realizará inicialmente mediante un listado. El calendario gráfico quedará como una mejora.
- Se debe confirmar el mecanismo definitivo para proteger las contraseñas antes de terminar el módulo de usuarios.
- Los permisos para administrar productos y tarifas deberán respetar los roles establecidos en el documento de Visión y Alcance.

## 7. Conclusiones

- Al revisar los requerimientos se encontraron algunos puntos que podían causar confusión durante el desarrollo, por lo que fue necesario mejorar su redacción.
- Se aclaró el funcionamiento del inventario cuando una venta produce cantidades negativas y se estableció que estos casos deben generar una incidencia.
- Se identificaron dependencias entre las funciones de ventas, inventario, alquileres, usuarios y caja. Esto ayuda a conocer qué partes del sistema se deben desarrollar primero.
- El registro de alquileres es viable con las herramientas y el tiempo considerados para el proyecto, siempre que se implemente por etapas.
- Con las versiones refinadas, los requerimientos quedan más claros y será más fácil utilizarlos como referencia durante el diseño y la programación de AsoGest EPN.

## 8. Documentos utilizados

- Grupo C. **01_Vision_y_Alcance – Documento de Visión y Alcance del Sistema AsoGest EPN**. Escuela Politécnica Nacional, 21 de noviembre de 2026.
- Grupo C. **02_Matriz_Interesados – Matriz de Interesados (Stakeholders)**. Escuela Politécnica Nacional, 21 de noviembre de 2026.
- Grupo C. **Taller de Ingeniería de Requerimientos – Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN**.
- **PPE05 – Catálogo de Requerimientos y Análisis de Refinamiento**, instrucciones del entregable.

---

**Fin del documento 02_Informe_Analisis_Refinamiento.md**
