# Proyecto-Final-Sistema-de-Gesti-n-para-Negocios-de-Servicios-en-C-
Proyecto final 

Planteamiento del Problema

Las pequeñas y medianas empresas del sector de servicios técnicos y especializados (tales como hospitales veterinarios, talleres mecánicos automotrices, centros de soporte técnico en TI, clínicas odontológicas o empresas de mantenimiento eléctrico y plomería) enfrentan serios problemas operativos al gestionar sus citas, órdenes de servicio, inventarios de insumos y facturación mediante bitácoras en papel u hojas de cálculo aisladas. Esta fragmentación provoca duplicidad de horarios, pérdida de historial de atención de los clientes, errores en el cálculo de presupuestos y falta de trazabilidad financiera.

Para resolver esta problemática, el equipo d deberá elegir un giro comercial de servicios y diseñar e implementar una aplicación de escritorio en C# con Windows Forms que centralice la operación diaria del negocio. El sistema funcionará como una estación de trabajo integral para recepción y administración, permitiendo registrar clientes y sus activos/sujetos de atención (ej. mascotas, vehículos, equipos o inmuebles), agendar y dar seguimiento a órdenes de servicio, importar catálogos de refacciones o insumos desde archivos CSV, gestionar configuraciones operativas en JSON, persistir toda la información transaccional en Microsoft SQL Server y ofrecer una interfaz gráfica adaptable a múltiples idiomas (Español / Inglés) bajo principios estrictos de usabilidad y ergonomía visual.

Funcionalidades Mínimas del Sistema

El sistema deberá presentar las funcionalidades necesarias para demostrar que es útil para resolver el problema planteado y cubrir de manera integral los siguientes módulos operativos:

1.      Gestión de Configuración e Inicialización (JSON): Al arrancar, la aplicación leerá un archivo local appsettings.json que contendrá parámetros del negocio (nombre comercial, tasa de impuestos vigentes, horario de apertura/cierre, moneda e idioma por defecto). El administrador podrá modificar estos parámetros desde un panel de configuración y guardar los cambios en el mismo archivo JSON.

2.      Internacionalización Dinámica (Multi-idioma): La interfaz principal incluirá un selector de idioma (Español / Inglés). Al cambiar la selección en tiempo de ejecución, todos los controles visuales (etiquetas, botones, menús, encabezados de tablas) y los cuadros de diálogo (MessageBox) deberán actualizar su texto inmediatamente sin necesidad de reiniciar la aplicación.

3.      Módulo de Clientes y Entidades de Atención (CRUD SQL Server): Registro, consulta, búsqueda en tiempo real, actualización y baja lógica o física de clientes y sus elementos asociados (ej. dueño  mascota; propietario  vehículo), haciendo uso de Microsoft SQL Server.

4.      Importación y Exportación de Catálogo de Servicios/Insumos (CSV):

o    Importación: Permitir cargar masivamente un catálogo de servicios o refacciones desde un archivo .csv, previsualizando y auditando los datos antes de sincronizarlos con la base de datos.

o    Exportación: Permitir exportar el reporte de órdenes de servicio cerradas o el corte de caja del día hacia un archivo .csv.

5.      Gestión de Órdenes de Servicio y Agenda: Creación de órdenes de servicio vinculando un cliente, el técnico/especialista asignado, fecha/hora programada, diagnóstico, lista de servicios/insumos aplicados, cálculo automático de subtotales e impuestos, y cambio de estatus (Pendiente, En Proceso, Finalizada, Cancelada).

6.      Tablero de Auditoría e Inspección Visual: Visualización tabulada de las órdenes activas con código de colores según su urgencia o estatus, además de un panel lateral de detalle que se actualice al seleccionar cualquier fila.

 

Requisitos Técnicos y de Arquitectura

Para garantizar la calidad del código y el cumplimiento de las convenciones oficiales de Microsoft, el proyecto deberá adherirse a las siguientes especificaciones:

Entorno y Lenguaje: Desarrollado en C# utilizando Windows Forms (WinForms) en Visual Studio.
Arquitectura en Capas (Separación de Responsabilidades): El código fuente no podrá concentrarse en los formularios (Code-Behind). La solución debe dividirse lógicamente en:
Capa de Presentación (UI): Formularios WinForms responsables únicamente de capturar entradas y renderizar información.
Capa de Dominio (Modelos): Clases y registros (record) fuertemente tipados que modelan las entidades del negocio.
Capa de Servicios (Lógica de Negocio y Archivos): Clases desacopladas para cálculos, validaciones, lectura/escritura de JSON y procesamiento de CSV.
Capa de Acceso a Datos (Repositorios): Clases dedicadas exclusivamente a la comunicación con SQL Server.
Persistencia en Microsoft SQL Server: Uso de ADO.NET (Microsoft.Data.SqlClien) implementando SqlConnection, SqlCommand, SqlDataReader y SqlTransaction. Es estrictamente obligatorio el uso de consultas parametrizadas (Parameters.AddWithValue o SqlParameter) para prevenir ataques de Inyección SQL.
Manejo de Archivos CSV y JSON.
Gestión de Recursos y Estándares de Codificación: Todo recurso no administrado (conexiones SQL, lectores de archivos) debe envolverse en bloques using. Se aplicará estrictamente la nomenclatura de Microsoft: PascalCase para clases, métodos y propiedades; camelCase para variables locales y parámetros; _camelCase para campos privados de clase, y prefijos estándar en controles visuales (btn, txt, lbl, dgv, cmb, dtp).
Control de Versiones: Uso comprobable de Git y GitHub (repositorio con historial de commits descriptivos, uso de ramas por funcionalidad o integrante y archivo .gitignore configurado para proyectos .NET).
Calidad y Pruebas: Inclusión de un proyecto de pruebas dentro de la solución que contenga pruebas unitarias (para la lógica de negocio, cálculos y validaciones) y pruebas de integración (para verificar la persistencia real en SQL Server y lectura de archivos).
 

Conceptos de Programación por Aplicar

El proyecto evidencia el dominio de los objetivos de aprendizaje del curso mediante la aplicación explícita de:

Fundamentos y Gramática de C#
Programación Orientada a Objetos (POO)
Colecciones
Programación Orientada a Eventos en WinForms
 

Retos de Lógica de Programación por Resolver

Se deberán diseñar e implementar los siguientes algoritmos:

Algoritmo de Validación de No-Solapamiento de Agenda: Al intentar agendar o reprogramar una orden de servicio para un técnico o estación de trabajo específica, el sistema deberá consultar las citas existentes que estén registradas para esa fecha y verificar que el nuevo intervalo  no se traslape con ningún intervalo existente .
Algoritmo de Auditoría, Sanitización y Reconciliación CSV  SQL Server: Al importar un archivo CSV de insumos o servicios, el sistema deberá recorrer línea por línea, limpiar caracteres inválidos, validar tipos de datos sin detenerse ante filas corruptas (generando una bitácora de errores por número de línea) y detectar códigos duplicados en memoria para decidir si inserta un nuevo registro o actualiza el precio de uno existente en la base de datos.
Algoritmo de Motor de Cálculo Polimórfico y Descuentos Escalonados: Implementar una jerarquía de clases para los tipos de servicio (ej. Servicio Estándar, Servicio Urgente/Express, Servicio con Garantía) donde cada subclase calcule su costo aplicando reglas específicas (recargos por horario, descuentos por volumen de insumos o membresía de cliente) combinando los parámetros dinámicos leídos desde el archivo de configuración en JSON.
 

Entregables Obligatorios del Proyecto

Al finalizar el periodo establecido, cada equipo deberá entregar un paquete completo que incluya:

Repositorio en GitHub: Enlace al repositorio público o compartido con el maestro.  
Código Fuente Documentado: Archivo con respaldo de todo el código fuente en C#. El código deberá estar debidamente comentado en clases, propiedades y métodos, así como comentarios adicionales para explicar bloques algorítmicos complejos. Se debe incluir el script .sql con la creación de la base de datos, tablas, llaves foráneas y datos de prueba. Así como el respaldo de la base de datos.
Archivo de instalación: Se deberá contar con un archivo de instalación para el proyecto y la base de datos.
Manual de Instalación y Descripción Técnica: Documento dirigido a personal de TI que contenga: requisitos de hardware/software, arquitectura del sistema (diagrama de clases y diagrama entidad-relación de SQL Server), guía paso a paso para restaurar la base de datos, configuración de la cadena de conexión en appsettings.json y ejecución del proyecto de pruebas.
Manual de Usuario: Guía ilustrada dirigida al operador final que explique de forma clara y accesible cómo utilizar cada módulo del sistema, cómo cambiar el idioma, cómo importar/exportar archivos CSV y cómo resolver mensajes de advertencia comunes.
Evidencia de Pruebas Automatizadas: Copia del proyecto de pruebas integrado en la solución de Visual Studio ejecutándose con éxito, acompañado de una sección en el documento técnico con capturas de pantalla del Explorador de Pruebas (Test Explorer) mostrando las pruebas unitarias y de integración aprobadas.
Video de Presentación y Demostración (5 a 10 minutos): Enlace a un video (YouTube no listado, Drive o OneDrive) donde participen los integrantes del equipo mostrando:
Explicación breve de la arquitectura y del repositorio en GitHub.
Demostración en vivo del sistema funcionando (cambio de idioma, importación CSV, CRUD en SQL Server, validación de retos lógicos y exportación de reportes).
Ejecución de las pruebas unitarias y de integración.
En el vídeo se deberá demostrar el funcionamiento del sistema para cubrir con los puntos que se indican a continuación
 

Rúbrica de Evaluación del Sistema

Criterio de Evaluación

Excelente (100% del puntaje)

Satisfactorio (75% del puntaje)

En Desarrollo (50% del puntaje)

Insuficiente (0% - 25% del puntaje)

Ponderación

1. Funcionalidad Integral y Persistencia SQL Server

Todas las operaciones CRUD funcionan sin errores. Las consultas están parametrizadas, usan bloques using y manejan transacciones en operaciones críticas.

Las operaciones CRUD funcionan, pero existen detalles menores en validaciones de entrada o falta manejo de transacciones.

El sistema conecta a SQL Server y realiza consultas básicas, pero presenta fallos al actualizar o eliminar registros.

No logra conectar a SQL Server, presenta vulnerabilidades graves o el programa colapsa ante errores de BD.

25 pts

2. Arquitectura, POO y Calidad de Código C#

Estricto desacoplamiento por capas. Aplica herencia, polimorfismo, encapsulamiento y convenciones de Microsoft. Código 100% comentado con XML.

Aplica POO y separa la mayoría de la lógica, aunque persiste algo de lógica de negocio en los formularios. Comentarios parciales.

Mezcla excesiva de lógica en el Code-Behind de WinForms; uso limitado de principios de POO o convenciones de nombres.

Código monolítico ("espagueti") dentro de los eventos de botones, sin clases de dominio ni comentarios.

20 pts

3. Interfaz Gráfica (UX), Eventos y Multi-idioma

Interfaz ergonómica e intuitiva. Implementa variedad de eventos (teclado, tabla, ciclo de vida y propios). Cambio de idioma fluido en tiempo real.

Interfaz funcional y ordenada. Maneja eventos estándar y cambia de idioma, aunque algún mensaje emergente queda sin traducir.

Interfaz poco intuitiva o desalineada. El cambio de idioma requiere reiniciar la app o está incompleto.

Interfaz deficiente, sin validaciones de teclado/formulario y sin soporte multi-idioma funcional.

15 pts

4. Manejo de Archivos (CSV y JSON) y Retos Lógicos

Lee/guarda configuración JSON correctamente. Importa y exporta CSV validando errores. Resuelve los 3 retos de lógica con algoritmos eficientes.

Maneja JSON y CSV correctamente, pero uno de los 3 retos de lógica presenta casos borde sin resolver.

Importa/exporta archivos sin validar formatos corruptos; resuelve solo uno de los retos lógicos planteados.

No implementa lectura/escritura de JSON o CSV, o los algoritmos lógicos no funcionan.

15 pts

5. Pruebas Unitarias, Integración y GitHub

Repositorio en GitHub con historial claro y colaborativo. Incluye pruebas unitarias y de integración automatizadas que pasan al 100%.

Usa GitHub con varios commits. Incluye pruebas unitarias básicas, pero las pruebas de integración son limitadas.

Repositorio con un solo commit final (subida directa) y pruebas mínimas o incompletas.

No entrega evidencia de control de versiones en GitHub ni proyecto de pruebas automatizadas.

10 pts

6. Documentación Técnica, Manual de Usuario y Video

Manuales completos, profesionales y bien estructurados. Video de 5-10 min claro, fluido y demostrando todos los módulos y pruebas.

Manuales completos con detalles menores de formato. Video cumple el tiempo y muestra la funcionalidad principal.

Documentación superficial o incompleta. El video excede o no alcanza el tiempo estipulado, o omite explicar el código/pruebas.

No entrega manuales o no presenta el video de demostración del sistema.

15 pts

 

Reporte de participación. Un documento presentando que hizo cada uno de los integrantes del equipo y la calificación que le otorgan sus otros compañeros de equipo sobre el grado de cumplimiento y participación en la elaboración del proyecto
Reflexiones de lo aprendido en el curso. Un archivo con las reflexiones y conclusiones de cada uno de los miembros del equipo en que comenten:
¿Cuáles son los puntos de programación que mejoraron con el curso?
¿Cuáles son los puntos de programación que les quedan pendientes?
¿Qué tareas o actividades consideran necesarias para mejorar esos puntos pendientes?
¿Qué papel deben tener con respecto al desarrollo de sistemas, considerando el uso de herramientas de Inteligencia Artificial?
¿Qué parte de su formación como futuros profesionistas tendrá para ustedes los contenidos de este curso?
