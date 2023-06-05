<div align="center">
  <h1>Análisis de datos con Power BI</h1>
</div>

<div align="center"> 
  <img src="readme_img/Microsoft-Power-BI-analisis.png" width="">
</div>

## Introducción al documento

El contenido de este documento son **apuntes teoricos y prácticos** y un proyecto de **Análisis de datos** de una tienda llamada **"SUPERMAYORISTA"** y busca ser una guía para futuros trabajos personales. El mismo está hecho por mi persona [José Eduardo Galván Salvador](https://www.linkedin.com/in/eduardo-galvan1208/) para el grupo de estudio [Data Growth Community](https://www.linkedin.com/company/datagrowthcommunity/).

## Objetivos del documento

- Ejecutar operaciones básicas de Pandas.
- Comprender el significado y uso de los DataFrames en Ciencia de Datos.
- Usar Computational Tools de Pandas para realizar cálculos básicos.
- Trabajar con Statisticals tools.
- Hacer preprocesamiento de datos para crear modelos. 
- Extraer información de Data Sets usando Time Series y Date Functionality.

## Tabla de contenido
- [Planificación del proyecto](#Planificación-del-proyecto)
  - [Alcance del negocio](#Alcance-del-negocio)
- [Definición de requerimientos para la empresa SUPERMAYORISTA](#Definición-de-requerimientos-para-la-empresa-SUPERMAYORISTA)
  - [Requisitos del negocio](#Requisitos-del-negocio)
  - [Base de Datos transaccional en SQL Server](#Base-de-Datos-transaccional-en-SQL-Server)
  - [Diccionario de datos del origen a nivel general de la base de datos transaccional en SQL Server 2017](#Diccionario-de-datos-del-origen-a-nivel-general-de-la-base-de-datos-transaccional-en-SQL-Server-2017)
    - [Tablas](#Tablas)
    - [Diccionario de datos de la base de datos transaccional en SQL Server 2017](#Diccionario-de-datos-de-la-base-de-datos-transaccional-en-SQL-Server-2017)
      - [VENTA](#VENTA)
      - [DETALLE_VENTA](#DETALLE_VENTA)
      - [PRODUCTO](#PRODUCTO)
      - [CLIENTE](#CLIENTE)
      - [VENDEDOR](#VENDEDOR)
      - [TIPO_DOCUMENTO](#TIPO_DOCUMENTO)
- [Modelo Dimensional](#Modelo-Dimensional)
  - [Elección de dimensiones](#Elección-de-dimensiones)
- [Dimensiones encontradas](#Dimensiones-encontradas)
- [Diseño lógico](#Diseño-lógico)
- [Diseño físico](#Diseño-físico)
  - [Tablas del modelo dimensional](#Tablas-del-modelo-dimensional)


## Planificación del proyecto

### Alcance del negocio

El presente proyecto busca ayudar con la gestión del área de ventas de la empresa SuperMayorista mediante informes de análisis de la información completos, veraces y en tiempo real que permita apoyar en la toma de decisiones.

## Definición de requerimientos para la empresa SUPERMAYORISTA

### Requisitos del negocio

<table>
    <thead>
        <tr>
            <th><strong>Identificador</strong></th>
            <th><i>R-01</i></th>
            <th><strong>Nombre</strong></th>
            <th><i>TOP N V VS T</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>Tipo</strong></td>
            <td align="center"><i>Funcional</i></td>
            <td align="center"><strong>Fecha</strong></td>
            <td align="center"><i>08/12/2022</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Prioridad</strong></td>
            <td align="center"><i>Alta</i></td>
            <td align="center"><strong>Necesidad</strong></td>
            <td align="center"><i>Si</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Descripción</strong></td>
            <td colspan=3 align="center"><i>"El total de ventas por periodo"</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Datos dimensionales</strong></td>
            <td align="center"><i>Producto</i></td>
            <td align="center"><strong>Datos Hechos</strong></td>
            <td align="center"><i>Más vendidos</i></td>
        </tr>
    </tbody>
</table>


<table>
    <thead>
        <tr>
            <th><strong>Identificador</strong></th>
            <th><i>R-02</i></th>
            <th><strong>Nombre</strong></th>
            <th><i>TOP N PROD</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>Tipo</strong></td>
            <td align="center"><i>Funcional</i></td>
            <td align="center"><strong>Fecha</strong></td>
            <td align="center"><i>08/12/2022</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Prioridad</strong></td>
            <td align="center"><i>Alta</i></td>
            <td align="center"><strong>Necesidad</strong></td>
            <td align="center"><i>Si</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Descripción</strong></td>
            <td colspan=3 align="center"><i>"Cuáles fueron los productos más vendidos"</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Datos dimensionales</strong></td>
            <td align="center"><i>Periodo</i></td>
            <td align="center"><strong>Datos Hechos</strong></td>
            <td align="center"><i>Cantidad de ventas</i></td>
        </tr>
    </tbody>
</table>

<table>
    <thead>
        <tr>
            <th><strong>Identificador</strong></th>
            <th><i>R-03</i></th>
            <th><strong>Nombre</strong></th>
            <th><i>TOP N VE</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>Tipo</strong></td>
            <td align="center"><i>Funcional</i></td>
            <td align="center"><strong>Fecha</strong></td>
            <td align="center"><i>08/12/2022</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Prioridad</strong></td>
            <td align="center"><i>Alta</i></td>
            <td align="center"><strong>Necesidad</strong></td>
            <td align="center"><i>Si</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Descripción</strong></td>
            <td colspan=3 align="center"><i>"Quiénes fueron los vendedores con las mayores ventas realizadas"</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Datos dimensionales</strong></td>
            <td align="center"><i>Vendedor</i></td>
            <td align="center"><strong>Datos Hechos</strong></td>
            <td align="center"><i>Mayor cantidad de ventas</i></td>
        </tr>
    </tbody>
</table>

<table>
    <thead>
        <tr>
            <th><strong>Identificador</strong></th>
            <th><i>R-04</i></th>
            <th><strong>Nombre</strong></th>
            <th><i>TOP N S VS F</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>Tipo</strong></td>
            <td align="center"><i>Funcional</i></td>
            <td align="center"><strong>Fecha</strong></td>
            <td align="center"><i>08/12/2022</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Prioridad</strong></td>
            <td align="center"><i>Alta</i></td>
            <td align="center"><strong>Necesidad</strong></td>
            <td align="center"><i>Si</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Descripción</strong></td>
            <td colspan=3 align="center"><i>"Quiénes fueron los supervisores que tuvieron baja efectividad (cantidad de ventas en cuerto periodo)"</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Datos dimensionales</strong></td>
            <td align="center"><i>Vendedor</i></td>
            <td align="center"><strong>Datos Hechos</strong></td>
            <td align="center"><i>Cantidad de ventas</i></td>
        </tr>
    </tbody>
</table>

<table>
    <thead>
        <tr>
            <th><strong>Identificador</strong></th>
            <th><i>R-05</i></th>
            <th><strong>Nombre</strong></th>
            <th><i>TOP N V AND C</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>Tipo</strong></td>
            <td align="center"><i>Funcional</i></td>
            <td align="center"><strong>Fecha</strong></td>
            <td align="center"><i>08/12/2022</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Prioridad</strong></td>
            <td align="center"><i>Alta</i></td>
            <td align="center"><strong>Necesidad</strong></td>
            <td align="center"><i>Si</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Descripción</strong></td>
            <td colspan=3 align="center"><i>"Cuál es la zona con maores ventas y mayores cantidades de productos vendidos"</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Datos dimensionales</strong></td>
            <td align="center"><i>Zona</i></td>
            <td align="center"><strong>Datos Hechos</strong></td>
            <td align="center"><i>Mayor cantidad de ventas, mayor cantidad de productos vendidos</i></td>
        </tr>
    </tbody>
</table>

<table>
    <thead>
        <tr>
            <th><strong>Identificador</strong></th>
            <th><i>R-06</i></th>
            <th><strong>Nombre</strong></th>
            <th><i>TOP N B VS AC</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>Tipo</strong></td>
            <td align="center"><i>Funcional</i></td>
            <td align="center"><strong>Fecha</strong></td>
            <td align="center"><i>08/12/2022</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Prioridad</strong></td>
            <td align="center"><i>Alta</i></td>
            <td align="center"><strong>Necesidad</strong></td>
            <td align="center"><i>Si</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Descripción</strong></td>
            <td colspan=3 align="center"><i>"Cuál es el banco más factible para solicitar un ajuste de comisión"</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Datos dimensionales</strong></td>
            <td align="center"><i>Banco</i></td>
            <td align="center"><strong>Datos Hechos</strong></td>
            <td align="center"><i>Mayor comisión obtenida por las ventas</i></td>
        </tr>
    </tbody>
</table>

<table>
    <thead>
        <tr>
            <th><strong>Identificador</strong></th>
            <th><i>R-07</i></th>
            <th><strong>Nombre</strong></th>
            <th><i>TOP N VE VS V AND C AND M</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>Tipo</strong></td>
            <td align="center"><i>Funcional</i></td>
            <td align="center"><strong>Fecha</strong></td>
            <td align="center"><i>08/12/2022</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Prioridad</strong></td>
            <td align="center"><i>Alta</i></td>
            <td align="center"><strong>Necesidad</strong></td>
            <td align="center"><i>Si</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Descripción</strong></td>
            <td colspan=3 align="center"><i>"El top de los vendedores que más comisionan por ventas"</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Datos dimensionales</strong></td>
            <td align="center"><i>Vendedor</i></td>
            <td align="center"><strong>Datos Hechos</strong></td>
            <td align="center"><i>Mayor comisión obtenida en base a la venta</i></td>
        </tr>
    </tbody>
</table>

### Base de Datos transaccional en SQL Server

<div align="center"> 
  <img src="readme_img/fig_1.png" width="">
</div>

### Diccionario de datos del origen a nivel general de la base de datos transaccional en SQL Server 2017

#### Tablas

<table>
    <thead>
        <tr>
            <th>Tabla</th>
            <th>Descripción</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>VENTA</strong></td>
            <td><i>Se registran los movimiento de las ventas realizadas.</i></td>
        </tr>
        <tr>
            <td align="center"><strong>DETALLE_VENTA</strong></td>
            <td><i>Se registran los detalle de las ventas realizadas.</i></td>
        </tr>
        <tr>
            <td align="center"><strong>PRODUCTO</strong></td>
            <td><i>Se registran los productos de la empresa.</i></td>
        </tr>
        <tr>
            <td align="center"><strong>CLIENTE</strong></td>
            <td><i>Se registran los clientes de la empresa.</i></td>
        </tr>
        <tr>
            <td align="center"><strong>VENDEDOR</strong></td>
            <td><i>Se registran los vendedores de la empresa.</i></td>
        </tr>
        <tr>
            <td align="center"><strong>TIPO_DOCUMENTO</strong></td>
            <td><i>Se registran los tipos de documentos que maneja la empresa.</i></td>
      </tr>
    </tbody>
</table>

#### Diccionario de datos de la base de datos transaccional en SQL Server 2017

##### VENTA

<table>
    <thead>
        <tr>
            <th>Nombre Columna</th>
            <th>Tipo de Dato</th>
            <th>Null Option</th>
            <th>Descripción</th>
            <th>PK</th>
            <th>FK</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>cod_documento</strong></td>
            <td><i>Char(10)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Código del documento</i></td>
            <td><i>PK</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>dni_cliente</strong></td>
            <td><i>Char(8)</i></td>
            <td><i>Not Null</i></td>
            <td><i>DNI del cliente</i></td>
            <td><i>-</i></td>
            <td><i>FK</i></td>
        </tr>
        <tr>
            <td align="center"><strong>vendedor</strong></td>
            <td><i>Varchar(50)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre del vendedor</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>nombre_tipo_documento</strong></td>
            <td><i>Varchar(20)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre del tipo de documento</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>estado</strong></td>
            <td><i>Varchar(10)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Estado de la venta</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>fecha_venta</strong></td>
            <td><i>datetime</i></td>
            <td><i>Not Null</i></td>
            <td><i>fecha de la venta</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
      </tr>
    </tbody>
</table>

##### DETALLE_VENTA

<table>
    <thead>
        <tr>
            <th>Nombre Columna</th>
            <th>Tipo de Dato</th>
            <th>Null Option</th>
            <th>Descripción</th>
            <th>PK</th>
            <th>FK</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>cod_documento</strong></td>
            <td><i>int</i></td>
            <td><i>Not Null</i></td>
            <td><i>Número de orden de compra</i></td>
            <td><i>-</i></td>
            <td><i>FK</i></td>
        </tr>
        <tr>
            <td align="center"><strong>cod_producto</strong></td>
            <td><i>Char(9)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Código del producto</i></td>
            <td><i>-</i></td>
            <td><i>FK</i></td>
        </tr>
        <tr>
            <td align="center"><strong>cantidad</strong></td>
            <td><i>int</i></td>
            <td><i>Not Null</i></td>
            <td><i>Cantidad de productos vendidos</i></td>
            <td><i>-</i></td>
            <td><i>FK</i></td>
        </tr>
    </tbody>
</table>

##### PRODUCTO

<table>
    <thead>
        <tr>
            <th>Nombre Columna</th>
            <th>Tipo de Dato</th>
            <th>Null Option</th>
            <th>Descripción</th>
            <th>PK</th>
            <th>FK</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>cod_producto</strong></td>
            <td><i>Char(9)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Código del producto</i></td>
            <td><i>PK</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>nombre_producto</strong></td>
            <td><i>Varchar(50)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre del producto</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>categoria_producto</strong></td>
            <td><i>Varchar(50)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre de la categoría del producto</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>subcategoria_producto</strong></td>
            <td><i>Varchar(50)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre de la subcategoría del producto</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>precio_unitario</strong></td>
            <td><i>decimal(8,2)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Precio Unitario del producto</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
    </tbody>
</table>

##### CLIENTE

<table>
    <thead>
        <tr>
            <th>Nombre Columna</th>
            <th>Tipo de Dato</th>
            <th>Null Option</th>
            <th>Descripción</th>
            <th>PK</th>
            <th>FK</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>dni_cliente</strong></td>
            <td><i>Char(11)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Código del cliente</i></td>
            <td><i>PK</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>departamento_cliente</strong></td>
            <td><i>Varchar(50)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre del departamento</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>distrito_cliente</strong></td>
            <td><i>Varchar(50)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre del distrito</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>punto_geografico</strong></td>
            <td><i>Varchar(50)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Punto geográfico</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>ubigeo_cliente</strong></td>
            <td><i>Varchar(50)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Ubigeo del cliente</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
    </tbody>
</table>

##### VENDEDOR

<table>
    <thead>
        <tr>
            <th>Nombre Columna</th>
            <th>Tipo de Dato</th>
            <th>Null Option</th>
            <th>Descripción</th>
            <th>PK</th>
            <th>FK</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>cod_vendedor</strong></td>
            <td><i>Char(7)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Código del empleado</i></td>
            <td><i>PK</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>apellido_vendedor</strong></td>
            <td><i>Varchar(30)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Apellido del vendedor</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>nombre_vendedor</strong></td>
            <td><i>Varchar(20)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre del vendedor</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>supervisor</strong></td>
            <td><i>Char(7)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Apellido del empleado</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
    </tbody>
</table>

##### TIPO_DOCUMENTO

<table>
    <thead>
        <tr>
            <th>Nombre Columna</th>
            <th>Tipo de Dato</th>
            <th>Null Option</th>
            <th>Descripción</th>
            <th>PK</th>
            <th>FK</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center"><strong>cod_tipo_documento</strong></td>
            <td><i>Char(6)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Código del tipo de documento</i></td>
            <td><i>PK</i></td>
            <td><i>-</i></td>
        </tr>
        <tr>
            <td align="center"><strong>nombre_tipo_documento</strong></td>
            <td><i>Varchar(20)</i></td>
            <td><i>Not Null</i></td>
            <td><i>Nombre del tipo de documento</i></td>
            <td><i>-</i></td>
            <td><i>-</i></td>
        </tr>
    </tbody>
</table>

### Modelo Dimensional

Tras analizar las entrevistas y requerimientos se continuará determinando las medidas y funciones orientadas a analizar diferentes niveles de información.

#### Elección de dimensiones

Para poder determinar las dimensiones a usar en el Datamart, primero debemos elegir las variables a analizar y que los usuarios suelen utilizar para realizar sus informes. Destacan:

- [x] Fecha
- [x] Estado de la venta
- [x] Nombre del Producto
- [x] Categoría del producto
- [x] Sub categoría del producto
- [x] Nombre del vendedor
- [x] Apellido del vendedor
- [x] Supervisor del vendedor
- [x] DNI del cliente
- [x] Nombre del departamento
- [x] Nombre del distrito
- [x] Nombre del banco
- [x] Comisión del banco
- [x] Tipo de documento

<table>
    <thead>
        <tr>
            <th colspan=2 align="center">Dimensiones</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=3 align="center"><strong>Vendedor</strong></td>
        </tr>
        <tr>
            <td><i>Nombre-Vendedor</i></td>
        </tr>
        <tr>
            <td><i>Apellido-Vendedor</i></td>
        </tr>
        <tr>
            <td><i>Supevisor-Vendedori></td>
        </tr>
        <tr>
            <td align="center"><strong>Subcategoría</strong></td>
            <td><i>Subcategoría-Producto</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Categoría</strong></td>
            <td><i>Categoría-Producto</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Distrito</strong></td>
            <td><i>Distrito-Distrito</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Departamento</strong></td>
            <td><i>Departamento-Departamento</i></td>
        </tr>
        <tr>
            <td rowspan=2 align="center"><strong>Banco</strong></td>
            <td><i>Nombre-Banco</i></td>
            <td><i>Comisión-Banco</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Periodo</strong></td>
            <td><i>Fecha-Periodo</i></td>
        </tr>
        <tr>
            <td align="center"><strong>Documento</strong></td>
            <td><i>Tipo-Documento</i></td>
        </tr>
    </tbody>
</table>

### Dimensiones encontradas

### Diseño lógico

### Diseño físico

#### Tablas del modelo dimensional

