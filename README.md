<img src="logo.svg" width="56" alt="eDocHub">

# eDocHub

**Documentos electrónicos de la DIAN, campo a campo.** Empieza con la factura electrónica de venta, anexo técnico v1.9.

eDocHub es una herramienta web **no oficial** para consultar rápido el Anexo Técnico de Factura Electrónica de Venta, versión 1.9, adoptado por la Resolución DIAN 000165 del 1 de noviembre de 2023.

Sirve para desarrolladores, proveedores tecnológicos, consultores de ERP (SAP, Oracle, Siesa, etc.) y equipos contables que trabajan con facturación electrónica en Colombia.

## Qué hace

- **474 campos** de la factura de venta (`Invoice`) con XPath, tipo, formato, tamaño, ocurrencia y observaciones (sección 6.1 del anexo).
- **470 reglas de validación** (sección 8.2), enlazadas a cada campo y marcadas como **rechazo (R)** o **notificación (N)**.
- Búsqueda por nombre de campo, XPath, código de regla (`FAD06`, `FAU14b`) o por el texto del mensaje que devuelve la DIAN.
- Bloque **«Qué debe enviar»** en cada campo: tipo de dato, tamaño, obligatoriedad, efecto de las reglas, valor fijo o ejemplo y fragmento XML listo para copiar.
- **36 catálogos de códigos** (26 de la factura de venta y 10 de notas, eventos y servicios), con los códigos cargados desde los Excel de la Caja de herramientas DIAN: tipos de identificación, tributos, tarifas, responsabilidades fiscales, unidades (1.093 códigos), monedas, medios de pago, etc. Enlazados a los 153 campos que los usan, con búsqueda por código o descripción y sugerencias de qué homologar.
- Vista **Estructura XML** tipo editor: etiquetas de apertura y cierre, plegado, líneas guía entre padre e hijos, atributos dentro de su etiqueta y valores de ejemplo.
- Navegación por parte de la factura (emisor, adquiriente, líneas, tributos, totales…) con lo que es siempre obligatorio, condicional u opcional.
- Filtros por sección, obligatoriedad, tipo de nodo y tipo de regla.
- Avisos donde el anexo oficial tiene inconsistencias en un XPath o en el nombre de un campo.
- Enlace directo a cada campo: `.../#FAJ20`.

## Publicarlo en GitHub Pages

1. Cree un repositorio público en GitHub llamado `edochub`.
2. Suba el contenido de esta carpeta: `index.html`, la carpeta `data/`, `README.md` y `.nojekyll`.
3. En el repositorio, vaya a **Settings → Pages**.
4. En **Build and deployment**, elija **Deploy from a branch**, rama `main`, carpeta `/ (root)` y guarde.
5. En uno o dos minutos la herramienta queda publicada en `https://<su-usuario>.github.io/edochub/`.

## Probarlo en su computador

El navegador no deja leer `data/factura-venta.json` si abre `index.html` con doble clic. Use un servidor local:

```bash
python -m http.server 8000
```

Y abra `http://localhost:8000`.

## Estructura de los datos

`data/factura-venta.json` tiene tres listas:

- `secciones`: agrupación funcional del XML (encabezado, emisor, adquiriente, tributos, líneas, etc.).
- `campos`: un registro por campo del anexo, con `id`, `xpath`, `xpathAnexo` (tal como lo publica la DIAN), `tipo`, `formato`, `tam`, `oc`, `desc`, `obs`, `reglas`, `pag` (página del anexo), `cat` (catálogos), `literal`, `ejemplo`, `guia` (texto en lenguaje claro) y `xml` (fragmento de ejemplo).
- `catalogos`: los catálogos del capítulo 13, con su tabla, los elementos que la usan, notas, sugerencia de homologación, `campos` enlazados y `codigos` (vacío cuando el código está solo en la Caja de herramientas).
- `reglas`: un registro por regla de validación, con `id`, `campo`, `efecto` (`R` o `N`), `regla`, `mensaje` y `pag`.

Separar los datos del HTML permite agregar notas crédito, notas débito u otra versión del anexo sin tocar la página.

## Fuente y alcance

- Fuente: Anexo técnico de factura electrónica de venta, versión 1.9, publicado por la DIAN (páginas 21–110 y 375–460).
- Los textos se conservan como aparecen en el anexo, incluidos sus errores tipográficos. Algunas referencias cruzadas del PDF oficial salen como «numeral 0»: remiten a las tablas de códigos del capítulo 13.
- En la versión 1.9 los códigos de cada catálogo no están en el PDF: la DIAN los publica en Excel en la Caja de herramientas de factura electrónica (carpeta «Tablas Referenciadas»). La herramienta los carga tal como aparecen en esos archivos.
- Aún faltan las tablas de países (13.4.1), departamentos (13.4.2), municipios (13.4.3) y códigos postales.
- Aún no incluye notas crédito, notas débito ni eventos (ApplicationResponse/RADIAN).

> **Aviso:** proyecto independiente, sin relación con la DIAN. Verifique siempre contra el anexo técnico vigente antes de implementar.

## Nombre

eDocHub es un proyecto independiente, sin relación con la DIAN ni con SAP ni con DocHub.

## Licencia

Código bajo licencia MIT. El contenido del anexo técnico es un documento público de la DIAN.
