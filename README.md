# Aplicativo de Nota de Ingreso a Almacén para Empresa Importadora Automotriz


Sistema de escritorio y arquitectura de base de datos relacional Aplicativo de Nota de Ingreso a Almacén para Empresa Importadora Automotriz. El proyecto garantiza la integridad referencial, el control transaccional de recepciones de mercadería, la vinculación documental y la trazabilidad completa del inventario.

---

## Descripción General

El sistema permite administrar de forma centralizada el flujo operativo de ingreso de repuestos, accesorios y unidades vehiculares (trimotores de carga) al almacén, conectando directamente una aplicación nativa en **Java 21** con **PostgreSQL** mediante **JDBC**, sin intermediarios web.

### Objetivos Técnicos
* **Modelado e Integridad Relacional:** Definición de claves primarias, claves foráneas, restricciones de nulidad y disparadores (*triggers*) en PostgreSQL para mantener la consistencia de los datos.
* **Control Documental:** Trazabilidad completa entre notas de ingreso, facturas comerciales, guías de remisión, declaraciones aduaneras (DAM), proveedores, transportistas y encargados de recepción.
* **Operación CRUD y Exportación:** Gestión integral de registros desde interfaz gráfica con soporte para búsqueda, validación de campos obligatorios y exportación de catálogos a formato `.csv`.

---

## Arquitectura y Tecnologías

* **Lenguaje / Aplicación Cliente:** Java 21 (Aplicación nativa de escritorio `.exe`)
* **Motor de Base de Datos:** PostgreSQL 16 / 17 (`bd_almacen_puma`)
* **Conectividad:** JDBC directo (soporte local o remoto con configuración de puerto y modo SSL)
* **Administración y Respaldo:** pgAdmin 4 (restauración mediante respaldo `Custom/Tar`)

---

## Estructura de la Base de Datos

El esquema `public` de `bd_almacen_puma` está compuesto por las siguientes entidades principales:

| Tabla | Descripción Funcional |
| :--- | :--- |
| `producto` | Catálogo maestro de repuestos, accesorios y trimotores (`cod_producto`, unidad de medida, modelo, categoría). |
| `proveedor` | Directorio de fabricantes y proveedores (`ruc`, razón social). |
| `transportista` | Registro de empresas y operadores encargados del traslado (`ruc_transportista`, nombre). |
| `encargado` | Padrón de personal autorizado de almacén para recepcionar mercadería (`dni`, nombre completo). |
| `factura` | Comprobantes comerciales asociados al ingreso (`num_factura`, precio total, puertos de carga/descarga, fecha, proveedor). |
| `guia_remision` | Documentos de sustento de traslado (`num_guia`, fechas de traslado/emisión, motivo, DAM, transportista, placa). |
| `nota_ingreso` | Cabecera del registro de ingreso a almacén (`num_ingreso`, fecha, guía, factura y encargado). |
| `detalle_nota` | Desglose de productos y cantidades recibidas por cada nota de ingreso. |
| `observacion_nota` | Registro de incidencias, conformidad o novedades técnicas vinculadas a una nota de ingreso. |

---

## Módulos del Sistema

1. **Panel General:** Indicadores en tiempo real de productos, proveedores, notas de ingreso y reportes SQL disponibles.
2. **Gestión de Catálogos:** Mantenimiento completo (crear, listar, editar, eliminar y exportar CSV) para **Productos**, **Proveedores**, **Encargados** y **Transportistas**.
3. **Gestión Documental y Operativa:** Registro y control de **Facturas**, **Guías de Remisión**, **Notas de Ingreso**, **Detalle de Notas** y **Observaciones**.
4. **Configuración de Base de Datos:** Módulo integrado para configurar dinámicamente servidor/IP, puerto (`5432`), nombre de base de datos, credenciales y modo SSL con prueba de conexión en vivo.

---

## Instalación y Despliegue Rápido

1. **Base de Datos (PostgreSQL):**
   * Crear una base de datos llamada `bd_almacen_puma` desde **pgAdmin 4**.
   * Restaurar el archivo de respaldo del proyecto (`Backup_Final`) mediante la herramienta *Restore*.
2. **Aplicación Cliente:**
   * Ejecutar el instalador de **Puma Motors EIRL 1.0.0 (`.exe`)** como administrador.
   * Abrir el programa, ingresar a **Configurar BD**, completar los parámetros de conexión a PostgreSQL, presionar **Probar Conexión** y guardar.
