<div align="center">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/java/java-original.svg" width="82" alt="Logo de Java">

  # DPA · Avisos de Baja

  **Aplicación de escritorio para registrar, consultar y documentar avisos de baja de asegurados.**

  ![Java](https://img.shields.io/badge/Java-Swing-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-5.x-4479A1?style=flat-square&logo=mysql&logoColor=white)
  ![JasperReports](https://img.shields.io/badge/JasperReports-6.0.0-8A2BE2?style=flat-square)
  ![Apache Ant](https://img.shields.io/badge/Apache_Ant-Build-A81C7D?style=flat-square&logo=apacheant&logoColor=white)
</div>

---

## Sobre el proyecto

DPA Avisos de Baja centraliza el registro de bajas de asegurados y la emisión de su documentación asociada. La aplicación reúne en una interfaz de escritorio los datos personales y laborales de cada asegurado, almacena el historial en una base de datos y genera el formulario institucional en PDF.

El sistema fue desarrollado para el flujo del **Departamento de Personal Académico de la Universidad Mayor de San Simón (UMSS)**. Los formatos incluidos corresponden al aviso de baja destinado al Seguro Social Universitario y al reporte consolidado de una gestión.

## Funcionalidades principales

- Registro de avisos con fecha de emisión, nombre completo, matrícula, último salario cotizado, fecha y motivo de baja.
- Clasificación por motivos predefinidos —fin de nombramiento, fallecimiento, jubilación, regularización y renuncia voluntaria— con opción para registrar otros motivos.
- Consulta de registros por gestión y búsqueda por nombre o apellidos.
- Edición y eliminación de avisos desde el listado principal.
- Generación automática de un formulario PDF individual al crear o modificar un registro.
- Acceso al PDF asociado directamente desde la tabla de avisos.
- Visualización de un reporte anual con el detalle y la cantidad de registros de la gestión seleccionada.

## Flujo de trabajo

1. La aplicación carga los avisos de la gestión seleccionada desde MySQL.
2. El usuario registra los datos del asegurado y la causa de baja.
3. El registro se guarda en la tabla `avisos`.
4. JasperReports completa el formulario institucional y lo exporta como PDF en el escritorio del usuario.
5. El documento queda vinculado al registro para su posterior consulta; también puede generarse una vista consolidada por año.

## Tecnologías

| Tecnología | Uso en el proyecto |
| --- | --- |
| Java y Swing | Lógica e interfaz gráfica de escritorio |
| MySQL Connector/J 5.0.8 | Conexión JDBC y persistencia de registros |
| JasperReports 6.0.0 | Procesamiento de plantillas y reportes |
| iText 5.5.4 | Soporte para la generación de documentos PDF |
| Groovy 2.4.5 | Lenguaje de expresiones de las plantillas JasperReports |
| Apache Ant / NetBeans | Compilación y estructura del proyecto Java SE |

## Estructura del repositorio

```text
.
├── src/
│   ├── clases/
│   │   ├── Conexion.java          # Conexión JDBC con MySQL
│   │   ├── Render.java            # Renderizado de acciones en la tabla
│   │   └── VistaFormulario.java   # Interfaz y flujo principal
│   └── reportes/
│       ├── Aviso.jrxml            # Formulario individual de baja
│       └── RepAnualAvis.jrxml     # Reporte consolidado por gestión
├── nbproject/                     # Configuración del proyecto NetBeans
├── build.xml                      # Definición de compilación con Ant
└── dist/                          # JAR ejecutable y dependencias
```

## Datos y documentos

La persistencia utiliza la base MySQL `registros_avisos` y la tabla `avisos`. El modelo manejado por la aplicación contiene:

- fecha de emisión;
- apellidos y nombres;
- matrícula del asegurado;
- último salario cotizado;
- fecha y motivo de baja;
- ruta del PDF generado.

Las plantillas JasperReports se conservan en formato editable (`.jrxml`) y compilado (`.jasper`). Los PDF individuales se guardan, agrupados por gestión, bajo `AVISOS DE BAJA UMSS` en el escritorio del usuario.

## Ejecución

El repositorio incluye una distribución compilada. Desde la raíz del proyecto puede iniciarse con:

```bash
java -jar dist/CuartoProyectoAvisosDPA.jar
```

También puede abrirse como proyecto Java SE en NetBeans y compilarse mediante Apache Ant; la clase principal configurada es `clases.VistaFormulario`.

> [!IMPORTANT]
> La aplicación espera una instancia local de MySQL y una base `registros_avisos` con la tabla `avisos`. El repositorio no contiene un script de creación o datos iniciales, por lo que la ejecución desde cero requiere disponer previamente de esa estructura compatible y revisar la configuración de conexión definida en `Conexion.java`.

## Contexto de uso

La herramienta acompaña un proceso administrativo concreto: documentar la baja de asegurados del Departamento de Personal Académico de la UMSS, emitir el formulario correspondiente para el Seguro Social Universitario y mantener una consulta histórica organizada por gestión.

