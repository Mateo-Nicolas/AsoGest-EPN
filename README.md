## ESCUELA POLITÉCNICA NACIONAL FACULTAD DE INGENIERÍA ELÉCTRICA Y ELECTRÓNICA AsoGest EPN — README del Proyecto

Sistema de Gestión Administrativa para las Asociaciones de Estudiantes de la EPN — Caso de Estudio: Asociación de Ingeniería Química

| Asignatura | Diseño y Programación | Proyecto | AsoGest EPN (Grupo |
| --- | --- | --- | --- |
|   | de Software |   | C) |
| Docente | Ing. Jose Naranjo | Integrantes | Jeziel Silva, Mateo |
|   |   |   | Paredes, David Vega |

## 1. Descripción del Proyecto

AsoGest EPN es una aplicación de escritorio diseñada para automatizar y centralizar la gestión operativa, comercial y contable de las asociaciones estudiantiles de la Escuela Politécnica Nacional (EPN), tomando como caso de estudio la Asociación de Estudiantes de Ingeniería Química.

## 2. Problemática

Actualmente, la comercialización de productos (alimentos, bebidas, copias, útiles) y el alquiler tem- poral de recursos e instalaciones (mandiles, puntas de prueba, material de laboratorio, consolas, mesas de billar/ping-pong y casilleros) se registran de forma manual mediante hojas de cálculo (Excel) y ano- taciones en papel. Esta dinámica ocasiona:

- \- Inconsistencias contables y descuadres diarios de caja.

- \- Retrasos en la atención durante los recesos universitarios (horas pico).

- \- Traslape de turnos entre operadores estudiantiles sin cierre de sesión individual.

- \- Dobles reservas de equipos o inconsistencias en los bloques horarios asignados.

- \- Dificultad para auditar anulaciones, desfases de inventario y retención de garantías físicas.

## 3. Solución Propuesta

Desarrollar un sistema de escritorio local, ágil y seguro que separe la operación diaria de la supervisión administrativa mediante Control de Acceso Basado en Roles (RBAC):

- \- Gestión de Usuarios y Roles (RBAC): Perfiles diferenciados para Presidente, Tesorero/Administrador Externo y Operador Estudiantil, con auditoría de sesiones y contraseñas cifradas mediante SHA- 256.

- \- Administración de Catálogo e Inventario: Control centralizado de productos y tarifas con des- cuento automático de stock en tiempo real y soporte para saldos negativos auditables mediante registro de incidencias.

- \- Punto de Venta (POS) Ágil en Mostrador: Flujo optimizado para registrar ventas en menos de 10 segundos vinculadas al operador activo.

- \- Gestión de Alquileres y Garantías: Registro de préstamos por bloques horarios (HH:MM) con validación obligatoria de retención de garantía física (carné universitario EPN o cédula original).


- \- Validación Automática de Disponibilidad: Bloqueo inmediato ante cualquier solapamiento de horarios para un mismo recurso.

- \- Cuadre de Caja y Operación Offline: Consulta de movimientos y cortes diarios por turno en pantalla sobre una base de datos relacional local sin depender de conexión a Internet.

## 4. Tecnologías Utilizadas

|   | Tecnología / Herramienta |
| --- | --- |
| Componente |   |
| Lenguaje y Framework | C# / .NET 8 (o superior) |
| Interfaz Gráfica | Windows Forms (WinForms) para escritorio |
| Base de Datos | SQLite (motor relacional embebido local, migrable a |
|   | MySQL/PostgreSQL) |
| Seguridad | Control de Acceso Basado en Roles (RBAC) y hashing SHA-256 |
| Documentación | LATEX (especificaciones SRS, Visión y Alcance, Matriz de Interesados) |

## 5. Estructura del Repositorio

| AsoGest-EPN/ |   |
| --- | --- |
| |– docs/ | # Entregables academicos en LaTeX y PDF |
| | |– 01_Vision_y_Alcance.tex |   |
| | |– 02_Matriz_Interesados.tex |   |
| |– src/ | # Codigo fuente de la solucion (.NET 8) |
| | |– AsoGestEPN.UI/ # Formularios Windows Forms (Login, POS, Alquileres, Caja) |   |
| | |– AsoGestEPN.BLL/ # Logica de negocio (RBAC, stock, cruce de horarios) |   |
| | |– AsoGestEPN.DAL/ # Acceso a datos y conexion SQLite |   |
| | |– AsoGestEPN.Entities/ # Modelos (Usuario, Producto, Venta, Alquiler, Incidencia) |   |
| |– database/ | # Scripts SQL de creacion y datos semilla |
| |– README.md | # Documentacion general del proyecto |
