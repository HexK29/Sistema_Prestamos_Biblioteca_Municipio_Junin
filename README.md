# Arcanum Library - Sistema de Inventario y Control de Préstamos

## 📌 Descripción del Proyecto
**Arcanum Library** es una aplicación de escritorio desarrollada para automatizar la gestión administrativa, el control de inventario de libros y la administración de préstamos en la **Biblioteca Pública de Rubio**, ubicada en el sector San Martín, Municipio Junín, Estado Táchira. El sistema reemplaza el registro manual por un entorno digital centralizado, permitiendo categorizar activos literarios mediante el **Sistema de Clasificación Decimal Dewey**, controlar existencias físicamente disponibles, gestionar expedientes de clientes, administrar préstamos con renovación automática de plazos e imprimir comprobantes de préstamo en PDF.

---

## 👥 Autores e Institución
* **Desarrolladores**: Henrry Ferrer, Keyner Lizarazo, Gabriel Pineda y Emily Suarez.
* **Asesor Metodológico**: Indira Medina.
* **Asesor Técnico**: Cristian Camargo.
* **Institución Académica**: Universidad Politécnica Territorial Agroindustrial del Táchira (UPTAIT), PNF en Informática (Proyecto II - Octubre 2024).
* **Entidad Beneficiaria**: Biblioteca Pública de Rubio (Municipio Junín, Estado Táchira).

---

## 🛠️ Tecnologías y Herramientas Utilizadas
* **Lenguaje de Programación**: Python (Lógica del negocio y backend).
* **Interfaz Gráfica (GUI)**: Tkinter (Framework gráfico para la interfaz de usuario).
* **Motor de Base de Datos**: MariaDB (Sistema relacional de almacenamiento).
* **Administración de BD**: HeidiSQL (Cliente de administración y ejecución de scripts SQL).
* **Generación de Reportes**: Módulo de exportación e impresión de comprobantes en formato PDF.
* **Esquema de Catalogación**: Sistema de Clasificación Decimal Dewey.

---

## 🚀 Módulos y Funcionalidades del Sistema

### 1. Autenticación y Control de Accesos (Login)
* Inicio de sesión mediante credenciales de usuario individuales.
* Menú dinámico estructurado según el nivel de privilegios (**SuperAdmin** / **Admin**).

### 2. Gestión de Libros (CRUD)
* Catalogación vinculada a Sala (Principal, Estadal, Infantil), Categoría y Asignatura.
* Registro de metadatos: Cota, N° de Registro, Edición, N° de Volumen, Título, Autor, Editorial y Año.
* Buscador y filtro dinámico en la tabla de inventario.
* Edición de características y eliminación de registros.
* Control en tiempo real de la cantidad de ejemplares disponibles.

### 3. Gestión de Clientes (CRUD)
* Registro de usuarios solicitantes de préstamos con Cédula, Nombres, Apellidos, Teléfono y Dirección.
* Búsqueda y filtrado de clientes registrados.
* Edición de información de contacto y eliminación de usuarios.

### 4. Gestión de Préstamos y Devoluciones
* Asignación de préstamos asociada a la cédula del cliente.
* Validación de reserva: Exige la existencia de al menos un ejemplar disponible de respaldo en la biblioteca para autorizar el préstamo.
* Renovación diferenciada según el tipo de literatura:
  * **Novelas**: Plazo de renovación de 8 días.
  * **Libros Generales**: Plazo de renovación de 3 días.
* Reintegración automática de ejemplares al inventario al finalizar o eliminar un préstamo.
* Exportación e impresión del **Reporte de Préstamo de Libros** en PDF con datos del cliente, libro, encargado y espacios para firmas.

### 5. Gestión de Usuarios del Sistema (CRUD)
* Módulo exclusivo para el usuario con rol **SuperAdmin** (Encargado de Servicio).
* Registro de cuentas de personal con asignación de roles (*Encargado de Servicio* o *Asistente Bibliotecario*).
* Actualización de contraseñas, cargos y eliminación de accesos al sistema.

### 6. Mi Perfil
* Consulta de la información del usuario autenticado (Nombre de usuario, rol, nombre completo, cargo y cédula).

---

## 💻 Requisitos del Sistema
* **Sistema Operativo**: Windows (32-bit o 64-bit).
* **Procesador**: Pentium® Dual-Core CPU 2.70 GHz o superior.
* **Memoria RAM**: Mínimo 2 GB.
* **Almacenamiento**: 300 GB de disco.
* **Software Requerido**:
  * Servidor MariaDB v11.5 o superior.
  * Administrador HeidiSQL v12.6 o superior.

---

## ⚙️ Guía de Instalación y Configuración

### Paso 1: Instalación del Motor de Base de Datos (MariaDB y HeidiSQL)
1. Desempaquetar el archivo .rar `Biblioteca.rar` 
2. Ejecute el instalador `mariadb-11.5.2-winx64.msi` disponible en la unidad de instalación.
3. Complete el asistente de instalación manteniendo las opciones por defecto y haga clic en **Install**.
4. Al finalizar, MariaDB y la herramienta de gestión **HeidiSQL** quedarán instaladas en el sistema.

### Paso 2: Configuración de la Base de Datos
1. Inicie la herramienta **HeidiSQL**.
2. En el *Administrador de sesiones*, seleccione **Nueva** y configure los datos de conexión:
   * **Tipo de red**: `MariaDB or MySQL (TCP/IP)`
   * **Librería**: `libmariadb.dll`
   * **Nombre del host / IP**: `localhost` o `127.0.0.1`
   * **Usuario**: `root`
   * **Contraseña**: `2525` (o la clave configurada en la instalación)
   * **Puerto**: `3306`
3. Presione **Abrir** para ingresar al servidor.
4. Vaya al menú superior y seleccione `Archivo` > `Cargar archivo SQL...`.
5. Busque y seleccione el archivo de script de la base de datos `BD_BIBLIOTECA_V1_SINPKNIAUTOINC.sql`.
6. Presione el botón **Ejecutar** (Play / `Shift+Ctrl+F9`) para crear la base de datos `basedatosbiblioteca` y la estructura de sus 10 tablas relacionales.

### Paso 3: Despliegue del Ejecutable
1. Diríjase a la carpeta del programa y ubique el ejecutable `Biblioteca Pública Rubio.exe`.
2. Haga clic derecho sobre la aplicación y seleccione `Enviar a` > `Escritorio (crear acceso directo)`.
3. Inicie el programa desde el acceso directo generado en el Escritorio.

---

## 🗄️ Estructura de la Base de Datos
El modelo relacional consta de 10 tablas interrelacionadas:
* `asignatura`: Asignaturas y materias de catalogación.
* `cargo`: Listado de cargos administrativos del personal.
* `categoria`: Categorías del catálogo de libros.
* `cliente`: Datos identificativos de los usuarios solicitantes.
* `libro`: Registros e inventario de los libros físicos.
* `prestamo`: Histórico de transacciones, fechas de salida y límites de devolución.
* `libro_prestamo`: Detalle relacional entre libros e identificadores de préstamo.
* `sala`: Ubicación física por salas (Principal, Estadal, Infantil).
* `usuarios`: Credenciales e información del personal con acceso al sistema.
* `rol`: Niveles de permisos dentro de la aplicación.

---

## 💡 Recomendaciones de Mantenimiento
1. Realizar chequeos periódicos (mensuales o trimestrales) del inventario físico para mantener actualizada la disponibilidad en base de datos.
2. Asegurarse de procesar la devolución o eliminación de los préstamos concluidos para reintegrar el stock de libros.
3. Imprimir y archivar las fichas en PDF para respaldar el control interno institucional de préstamos al día.
