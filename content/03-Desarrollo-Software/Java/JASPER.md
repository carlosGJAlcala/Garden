---
title: "Qué es realmente Jasper"
date: 2026-01-26
tags:
  - desarrollo-software
  - java
---

# Qué es realmente Jasper


> **Relacionado**: [[01-Ciberseguridad/Herramientas/IDOR|IDOR]]. [[03-Desarrollo-Software/Java/XDocReport|XDocReport]]. [[06-Infraestructura/Servidores/DispositivosOT/CENT|CENT]].

JasperReports es un motor de informes en Java. Su trabajo es tomar un diseño de reporte, mezclarlo con datos y producir una salida lista para entregar: PDF, DOCX, XLSX, HTML y más. Piensa en él como una imprenta programable: tú defines la maqueta y la lógica de paginación, le das los datos y él compone el documento con precisión milimétrica.

# El corazón: JRXML y .jasper

El diseño se define en un archivo JRXML, que es simplemente XML con una gramática de Jasper. Ese JRXML se compila a un binario .jasper que el runtime usa para correr rápido. En el JRXML describes páginas, márgenes y bandas (título, cabecera, detalle, pie, sumarios). También declaras campos, parámetros y variables. Los campos son los datos que van a imprimirse, los parámetros son valores externos que ayudan a personalizar (por ejemplo un rango de fechas o un logo) y las variables sirven para cálculos dentro del informe, desde contadores hasta acumulados por grupo.

# Bandas, grupos y la idea de “paginación”

Jasper está hecho para documentos paginados. Por eso la estructura por bandas es clave. El detalle se repite por cada registro del datasource y todo lo demás ocurre alrededor: cabeceras por página, pies por página, cabeceras por grupo, sumarios al final de cada grupo, totales generales en el summary. Si vas a emitir extractos bancarios, facturas con subtotales por cliente o listados largos con saltos de página controlados, esta mentalidad de “banda y grupo” te resuelve la vida.

# De dónde salen los datos

Puedes dejar la consulta SQL dentro del propio reporte y pasarle una conexión JDBC para que Jasper la ejecute, o puedes traer los datos desde Java y entregárselos como colecciones con JRBeanCollectionDataSource. También admite JSON, XML y datasources personalizados. Poner la SQL en el JRXML simplifica cuando el equipo de reporting controla el diseño y el filtro, pero separarla hacia Java te da más control, reutilización, seguridad y testabilidad. Una regla útil es: si necesitas orquestación de datos, cachés, servicios externos o lógica compleja, prepara todo en Java y entrégalo a Jasper ya “masticado”.

# Subreportes, datasets y tablas

Cuando el informe no es plano sino jerárquico, se usan subreportes o componentes de tabla con subdatasets. Un maestro‑detalle clásico (factura con sus líneas) se resuelve asociando un dataset secundario a la sección apropiada. La ventaja es que cada parte puede diseñarse y probarse por separado, y que puedes reutilizar subreportes en distintas maquetas.

# Estilos, tipografías e internacionalización

Para mantener consistencia visual conviene centralizar estilos y fuentes. Jasper permite definir estilos y plantillas de estilos, y empaquetar fuentes como extensiones para que el PDF y el DOCX salgan idénticos en cualquier servidor. La internacionalización se resuelve con resource bundles y patrones de formato, de modo que un campo monetario, una fecha o una etiqueta cambien automáticamente según el locale y el bundle que le pases.

# El ciclo en tiempo de ejecución

En ejecución casi siempre ocurre lo mismo. Se carga el .jasper, se construye un mapa de parámetros, se elige la fuente de datos, se llama a fillReport y se obtiene un JasperPrint. A partir de ahí, los exportadores transforman ese JasperPrint en el formato deseado. PDF suele ser el más robusto para distribución; DOCX es útil cuando se necesita editar después; XLSX es cómodo para exportar listados, aunque si quieres una hoja de cálculo “viva” tal vez te interese generar Excel directamente con otras librerías.

# Rendimiento y memoria

Jasper puede generar miles de páginas, pero hay que ser cuidadoso. Si el dataset es enorme, la paginación completa en memoria puede penalizar. Conviene usar consultas paginadas o streams, calcular agregados en la base de datos cuando tenga sentido, y limitar imágenes y subreportes costosos. El diseño también influye: sombras, bordes complejos y muchos elementos superpuestos pueden ralentizar la exportación a PDF.

# Seguridad y gobierno del dato

Meter credenciales de base de datos en un JRXML es mala idea. Mejor parametrizar conexiones desde la aplicación, gestionar secretos en el runtime y validar todo lo que venga del exterior antes de pasarlo al reporte. Si trabajas con información sensible, genera PDF con restricciones o usa marcas de agua y numeración por ejemplar. Y si el reporte admite filtros proporcionados por el usuario, valida tipos y rangos para evitar inyecciones en la capa de datos.

# JasperReports Library vs JasperReports Server

La librería te da control total dentro de tu aplicación: tú invocas, tú despliegas, tú escalas. JasperReports Server añade catálogo, ejecución programada, permisos, repositorio y una capa web para usuarios de negocio. Si tu caso es 100% embebido en una app y el equipo técnico controla todo, la librería basta. Si necesitas programación de informes, seguridad por roles y autoservicio, el server puede tener sentido.

# Cuándo usar SQL en el JRXML y cuándo no

La SQL en el reporte es cómoda para prototipos y equipos orientados a reporting. Cuando los informes son parte de un sistema mayor, con lógica, validaciones, cacheo y orquestación, separar la obtención de datos en Java y alimentar a Jasper con beans da mejor arquitectura, pruebas más sencillas y menos acoplamiento. También es la vía natural si una IA u otro servicio te entrega datos en JSON que transformas y pasas a JRBeanCollectionDataSource.

# Excel, Word y el “pixel perfect”

Jasper destaca en “pixel perfect”: que el PDF se vea exactamente como lo definiste. Para Word, el exportador OOXML funciona bien, pero recuerda que DOCX es editable, por lo que pequeñas diferencias de fuente o reflow pueden aparecer si no incrustas tipografías y no ajustas tamaños. Si lo que buscas es que el documento sea originalmente una plantilla de Word con placeholders, entonces conviene usar librerías específicas como XDocReport o Apache POI; Jasper también exporta a DOCX, pero su mentalidad sigue siendo la del informe paginado.

# Trabajo con imágenes, códigos de barras y gráficos

El soporte de imágenes abarca recursos internos, ficheros y BLOBs. Los códigos de barras y QR son componentes nativos, fáciles de parametrizar. Los gráficos (charts) permiten desde barras y líneas hasta pie y XY, con datasets simples. Para crosstabs y resúmenes tipo “pivot” el componente crosstab es muy útil, aunque diseñarlo bien requiere pensar primero en el dataset agregado.

# Pruebas y mantenibilidad

Un buen proyecto de reporting tiene JRXML con nombres claros, estilos compartidos, parámetros documentados y datasets acotados. Es sano escribir pruebas unitarias que llenen el reporte con datos sintéticos y confirmen que al menos compila y exporta sin errores. Un pipeline que genere PDFs de ejemplo en cada commit ayuda a detectar regresiones visuales. Y si hay varios diseñadores, establecer guías de márgenes, tipografías y espaciados ahorra horas de microajustes.

# Errores típicos y cómo evitarlos

Los descuadres suelen venir de fuentes no instaladas o no incrustadas; las páginas en blanco, de bandas con alturas mínimas o saltos mal configurados; los informes lentos, de subreportes que repiten consultas sin caché o de imágenes enormes sin escalar. La receta es simple: fuentes como extensión, consultas con límites y claves, logging activado durante el fill y prueba de exportación a varios formatos antes de cerrar un diseño.

# Integración con agentes y automatización

Si una IA va a alimentar tus informes, no le pidas que “escriba el documento”; pídele que devuelva un JSON validable con exactamente los campos que el JRXML espera. Tu servicio Java hace la validación, construye datasources y llama a Jasper. Esto reduce errores, mantiene el layout bajo control y te permite auditar cada salida.

# ¿Cuándo elegir Jasper y cuándo otra cosa?

Usa Jasper cuando la paginación, los grupos, los totales y la precisión visual importan, y cuando necesitas múltiples formatos desde un mismo diseño. Si el documento es, ante todo, un Word corporativo editable con marcadores, una plantilla DOCX con XDocReport o POI será más natural. Si es un dashboard interactivo, quizá un frontend web con gráficos y exportación a PDF sea mejor. La elección no es ideológica: es pragmática según el tipo de salida, quién la mantiene y cómo se distribuye.



---

**Flujo ampliado sin meter el `SELECT` en el .jasper**

1. **Generar o recuperar los datos en Java**
    
    - Realizas el `SELECT` directamente en tu código Java usando JDBC, JPA, Hibernate u otra librería.
        
    - Guardas los resultados en una `List<MiObjeto>` donde `MiObjeto` tiene las propiedades que el `.jasper` espera como campos.
        
2. **Cargar el diseño del reporte**
    
    - Usas `JRLoader.loadObjectFromFile(path)` para cargar el `.jasper` ya compilado desde disco o desde el classpath.
        
3. **Asociar los datos al reporte**
    
    - Creas un `JRBeanCollectionDataSource` con tu lista para que Jasper pueda iterar sobre ella:
        
        ```java
        JRBeanCollectionDataSource dataSource = new JRBeanCollectionDataSource(listaDatos);
        ```
        
4. **Rellenar el informe**
    
    - Con `JasperFillManager.fillReport(reporte, parametros, dataSource)` pasas el objeto `.jasper`, un `Map<String, Object>` con parámetros (si aplica) y el `JRBeanCollectionDataSource`.
        
5. **Exportar o visualizar**
    
    - Puedes exportar con `JasperExportManager.exportReportToPdfFile(...)` o mostrarlo en pantalla con `JasperViewer.viewReport(...)`.
        

---

**Flujo con la consulta dentro del `.jasper`**  
En este caso, el `.jasper` ya tiene la SQL incrustada. Solo necesitas pasar una conexión JDBC:

```java
JasperPrint print = JasperFillManager.fillReport(rutaJasper, parametros, conexion);
```

Esto hace que Jasper ejecute la consulta y genere el reporte directamente, sin que Java haga el `SELECT`.

---

**Ventajas de no meter el `SELECT` en el `.jasper`**

- Separas la lógica de negocio (código Java) de la lógica de presentación (diseño del reporte).
    
- Reutilizas el mismo reporte para diferentes fuentes de datos o consultas.
    
- Mejor control sobre optimización de queries y caché.
    
- Evitas exponer SQL dentro del reporte, lo que puede mejorar seguridad y mantenibilidad.
    

---

Aquí tienes un ejemplo completo en **Java** para generar un **Word (.docx)** con **JasperReports**. Te doy dos variantes:

1. **Sin SQL en el .jasper** (alimentando con una lista Java).
    
2. **Con SQL dentro del .jasper** (pasando una `Connection`).
    

---

### 0) Dependencias (Maven)

```xml
<dependencies>
  <dependency>
    <groupId>net.sf.jasperreports</groupId>
    <artifactId>jasperreports</artifactId>
    <version>6.21.3</version>
  </dependency>
  <!-- Si usas JDBC, añade tu driver; ejemplo para PostgreSQL -->
  <dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.7.3</version>
  </dependency>
</dependencies>
```

---

### 1) Sin SQL en el reporte (DOCX desde una lista Java)

#### 1.1 Plantilla `reporte.jrxml` (simple)

Guárdalo como `src/main/resources/reporte.jrxml`. Define campos que coincidan con tu bean.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports
              http://jasperreports.sourceforge.net/xsd/jasperreport.xsd"
              name="reporte" pageWidth="595" pageHeight="842" columnWidth="555"
              leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20"
              uuid="12345678-aaaa-bbbb-cccc-1234567890ab">

    <!-- Campos que vendrán del JRBeanCollectionDataSource -->
    <field name="nombre" class="java.lang.String"/>
    <field name="importe" class="java.lang.Double"/>

    <!-- Parámetro opcional para un título -->
    <parameter name="TITULO" class="java.lang.String"/>

    <title>
        <band height="40">
            <textField>
                <reportElement x="0" y="0" width="555" height="30"/>
                <textElement textAlignment="Center" verticalAlignment="Middle">
                    <font size="16" isBold="true"/>
                </textElement>
                <textFieldExpression><![CDATA[$P{TITULO} != null ? $P{TITULO} : "Informe de Ejemplo"]]></textFieldExpression>
            </textField>
        </band>
    </title>

    <columnHeader>
        <band height="20">
            <staticText>
                <reportElement x="0" y="0" width="300" height="20"/>
                <text><![CDATA[Nombre]]></text>
            </staticText>
            <staticText>
                <reportElement x="300" y="0" width="255" height="20"/>
                <text><![CDATA[Importe]]></text>
            </staticText>
        </band>
    </columnHeader>

    <detail>
        <band height="20">
            <textField>
                <reportElement x="0" y="0" width="300" height="20"/>
                <textFieldExpression><![CDATA[$F{nombre}]]></textFieldExpression>
            </textField>
            <textField pattern="#,##0.00">
                <reportElement x="300" y="0" width="255" height="20"/>
                <textFieldExpression><![CDATA[$F{importe}]]></textFieldExpression>
            </textField>
        </band>
    </detail>
</jasperReport>
```

#### 1.2 Bean de datos

```java
public class Linea {
  private String nombre;
  private Double importe;
  public Linea(String nombre, Double importe) {
    this.nombre = nombre; this.importe = importe;
  }
  public String getNombre() { return nombre; }
  public Double getImporte() { return importe; }
}
```

#### 1.3 Código Java para compilar, llenar y exportar a DOCX

```java
import net.sf.jasperreports.engine.*;
import net.sf.jasperreports.engine.data.JRBeanCollectionDataSource;
import net.sf.jasperreports.export.SimpleExporterInput;
import net.sf.jasperreports.export.SimpleOutputStreamExporterOutput;
import net.sf.jasperreports.engine.export.ooxml.JRDocxExporter;

import java.util.*;

public class GenerarDocxSinSQL {
  public static void main(String[] args) throws Exception {
    // 1) Prepara datos en memoria
    List<Linea> data = Arrays.asList(
        new Linea("Producto A", 1234.56),
        new Linea("Producto B", 789.10),
        new Linea("Producto C", 45.00)
    );
    JRBeanCollectionDataSource ds = new JRBeanCollectionDataSource(data);

    // 2) Compila el .jrxml a .jasper (o carga el .jasper si ya lo tienes)
    JasperReport jr = JasperCompileManager.compileReport(
        GenerarDocxSinSQL.class.getResourceAsStream("/reporte.jrxml")
    );

    // 3) Parámetros opcionales
    Map<String, Object> params = new HashMap<>();
    params.put("TITULO", "Ventas por Producto");

    // 4) Llenado
    JasperPrint jp = JasperFillManager.fillReport(jr, params, ds);

    // 5) Exportar a DOCX
    JRDocxExporter exporter = new JRDocxExporter();
    exporter.setExporterInput(new SimpleExporterInput(jp));
    exporter.setExporterOutput(new SimpleOutputStreamExporterOutput("informe.docx"));
    exporter.exportReport();

    System.out.println("Generado: informe.docx");
  }
}
```

---

### 2) Con SQL dentro del reporte (DOCX desde JDBC)

En el `.jrxml` defines la consulta; luego solo pasas una `Connection`.

#### 2.1 Plantilla `reporte_sql.jrxml` (con query)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports
              http://jasperreports.sourceforge.net/xsd/jasperreport.xsd"
              name="reporte_sql" pageWidth="595" pageHeight="842" columnWidth="555"
              leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20"
              uuid="abcdefab-1111-2222-3333-abcdefabcdef">

    <parameter name="TITULO" class="java.lang.String"/>
    <!-- Ejemplo con parámetro de filtro -->
    <parameter name="MIN_IMPORTE" class="java.lang.Double"/>

    <queryString>
        <![CDATA[
          SELECT nombre, importe
          FROM ventas
          WHERE (:MIN_IMPORTE IS NULL OR importe >= :MIN_IMPORTE)
          ORDER BY importe DESC
        ]]>
    </queryString>

    <field name="nombre" class="java.lang.String"/>
    <field name="importe" class="java.lang.Double"/>

    <title>
        <band height="40">
            <textField>
                <reportElement x="0" y="0" width="555" height="30"/>
                <textElement textAlignment="Center" verticalAlignment="Middle">
                    <font size="16" isBold="true"/>
                </textElement>
                <textFieldExpression><![CDATA[$P{TITULO} != null ? $P{TITULO} : "Informe SQL"]]></textFieldExpression>
            </textField>
        </band>
    </title>

    <columnHeader>
        <band height="20">
            <staticText>
                <reportElement x="0" y="0" width="300" height="20"/>
                <text><![CDATA[Nombre]]></text>
            </staticText>
            <staticText>
                <reportElement x="300" y="0" width="255" height="20"/>
                <text><![CDATA[Importe]]></text>
            </staticText>
        </band>
    </columnHeader>

    <detail>
        <band height="20">
            <textField>
                <reportElement x="0" y="0" width="300" height="20"/>
                <textFieldExpression><![CDATA[$F{nombre}]]></textFieldExpression>
            </textField>
            <textField pattern="#,##0.00">
                <reportElement x="300" y="0" width="255" height="20"/>
                <textFieldExpression><![CDATA[$F{importe}]]></textFieldExpression>
            </textField>
        </band>
    </detail>
</jasperReport>
```

#### 2.2 Código Java con JDBC y exportación a DOCX

```java
import net.sf.jasperreports.engine.*;
import net.sf.jasperreports.export.SimpleExporterInput;
import net.sf.jasperreports.export.SimpleOutputStreamExporterOutput;
import net.sf.jasperreports.engine.export.ooxml.JRDocxExporter;

import java.sql.Connection;
import java.sql.DriverManager;
import java.util.HashMap;
import java.util.Map;

public class GenerarDocxConSQL {
  public static void main(String[] args) throws Exception {
    // 1) Conexión JDBC (ajusta URL, usuario y pass)
    String url = "jdbc:postgresql://localhost:5432/mi_db";
    String user = "mi_usuario";
    String pass = "mi_password";
    try (Connection conn = DriverManager.getConnection(url, user, pass)) {

      // 2) Compilar plantilla con SQL
      JasperReport jr = JasperCompileManager.compileReport(
          GenerarDocxConSQL.class.getResourceAsStream("/reporte_sql.jrxml")
      );

      // 3) Parámetros (puedes pasar null en MIN_IMPORTE si no quieres filtrar)
      Map<String, Object> params = new HashMap<>();
      params.put("TITULO", "Ventas (SQL)");
      params.put("MIN_IMPORTE", 100.00);

      // 4) Llenado: Jasper ejecuta la query usando la Connection
      JasperPrint jp = JasperFillManager.fillReport(jr, params, conn);

      // 5) Exportar a DOCX
      JRDocxExporter exporter = new JRDocxExporter();
      exporter.setExporterInput(new SimpleExporterInput(jp));
      exporter.setExporterOutput(new SimpleOutputStreamExporterOutput("informe_sql.docx"));
      exporter.exportReport();

      System.out.println("Generado: informe_sql.docx");
    }
  }
}
```

---

### Tips rápidos

- Si ya tienes el `.jasper` compilado, puedes cargarlo con `JRLoader.loadObjectFromFile("ruta/reporte.jasper")` en vez de compilar el `.jrxml`.
    
- Para **parámetros** tipo fecha, moneda o i18n, puedes añadir _Resource Bundles_ y patrones en los `textField`.
    
- DOCX sale “listo para editar” en Word; si quieres un resultado “cerrado”, exporta a PDF con `JasperExportManager.exportReportToPdfFile(...)`.
    

Si quieres, adapto este ejemplo a tu esquema de datos real (nombres de columnas/tabla y estilos del documento).