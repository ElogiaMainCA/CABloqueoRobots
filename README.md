# REPORTE DE URLs BLOQUEADAS POR ROBOTS.TXT Y SU IMPACTO EN SEO

## 1. Introducción

El presente reporte detalla las URLs que están siendo bloqueadas por el archivo robots.txt del sitio web cyamoda.com. Se analizan las causas del bloqueo, el impacto SEO que esto puede generar y se proponen soluciones detalladas con ejemplos claros para corregir estos problemas.

#### 2. Análisis del robots.txt

El robots.txt de cyamoda.com contiene varias reglas que restringen el acceso de los motores de búsqueda a ciertas páginas. A continuación, se listan las reglas relevantes y su posible impacto:

### 2.1. Bloqueo de /update/

Regla en robots.txt:

Disallow: /update/*

Impacto:

Esta regla bloquea todas las URLs que contienen /update/, lo que impide que Google acceda a páginas de categorías y productos dinámicos que dependen de esta estructura.

Ejemplo de URL bloqueada:

https://www.cyamoda.com/update/?cgid=NINOS_ULTIMAS_TENDENCIAS&srule=Sorting Manual 2024&start=0&sz=24

Si Google no puede acceder a estas URLs, la indexación de productos y categorías puede verse afectada negativamente, reduciendo la visibilidad en los resultados de búsqueda.

### 2.2. Bloqueo de /search/

Regla en robots.txt:

Disallow: /search/*

Impacto:

Impide que las páginas de búsqueda interna sean indexadas, lo cual es una práctica recomendada para evitar contenido duplicado y reducir el rastreo innecesario.

Sin embargo, si las páginas de búsqueda están generando tráfico orgánico, este bloqueo podría afectar su rendimiento en SEO.

### 2.3. Bloqueo de /on/demandware.store/

Regla en robots.txt:

Disallow: /on/demandware.store/*

Impacto:

Las URLs de Salesforce Commerce Cloud (Demandware) están bloqueadas, lo cual es correcto para evitar la indexación de versiones no amigables para SEO.

Ejemplo de URL bloqueada:

https://www.cyamoda.com/on/demandware.store/Sites-Cya_MX-Site/es_MX/Product-Variation?dwvar_3102767_color=BLANCO

### 2.4. URLs con /null

Problema:

Se han detectado múltiples URLs que terminan en /null, lo que indica un posible error en la generación de enlaces dentro del sitio.

Ejemplo de URLs afectadas:

https://www.cyamoda.com/kids/null

https://www.cyamoda.com/kids/nino/sueteres/null

Esto puede generar contenido de baja calidad para los motores de búsqueda y afectar la experiencia del usuario.

## 3. Impacto SEO del Bloqueo de Estas URLs

Disminución en la indexación de productos y categorías

Google no puede acceder a páginas de productos y categorías, lo que reduce la posibilidad de que aparezcan en los resultados de búsqueda.

Las páginas de productos pueden quedar fuera del índice de Google, afectando el tráfico orgánico.

Aumento del número de páginas huérfanas

Si las URLs bloqueadas no tienen enlaces internos adecuados, pueden convertirse en páginas huérfanas que no son rastreadas ni indexadas.

Posible impacto en la conversión

Si las páginas de categorías y productos no aparecen en Google, los usuarios no podrán encontrarlas mediante búsqueda orgánica, reduciendo las ventas potenciales.

Generación de errores en rastreo

URLs con /null pueden generar problemas de rastreo y señales de baja calidad para los motores de búsqueda.

## 4. Propuesta de Solución

### 4.1. Modificación del robots.txt

Opción 1: Permitir indexación selectiva de /update/

Si algunas URLs bajo /update/ contienen contenido relevante, se puede modificar la regla:

Disallow: /update/*
Allow: /update/?cgid=NINOS_ULTIMAS_TENDENCIAS*

Esto permitirá la indexación de categorías importantes.

Opción 2: Asegurar que las canónicas no apunten a /update/

Si /update/ solo se usa para filtros y paginación, es importante que las páginas tengan etiquetas rel="canonical" apuntando a la versión limpia.
Ejemplo:

<link rel="canonical" href="https://www.cyamoda.com/ninos/ultimas-tendencias/">

### 4.2. Corrección de URLs con /null

Identificar la causa del error en la generación de URLs

Revisar si los enlaces en el CMS están mal estructurados.

Comprobar si hay productos sin categorías asignadas que generan estas URLs.

Implementar redirecciones 301

Si ya existen URLs con /null, se recomienda redirigirlas a la versión correcta.

Ejemplo en .htaccess:

RedirectMatch 301 ^(.*)/null$ $1

Revisión en Google Search Console

Analizar el informe de cobertura y corregir cualquier URL afectada.

### 4.3. Verificación y seguimiento

Revisión de indexación

Usar site:cyamoda.com en Google para verificar qué páginas están indexadas.

Uso de Google Search Console

Inspeccionar URLs bloqueadas y probar la nueva configuración del robots.txt.

Monitoreo con Screaming Frog o Ahrefs

Realizar auditorías técnicas periódicas para detectar problemas de rastreo e indexación.

## 5. Conclusión

El robots.txt actual de cyamoda.com está bloqueando URLs clave que pueden afectar la indexación y visibilidad del sitio en los motores de búsqueda.

La solución propuesta busca corregir estos problemas sin afectar el rendimiento del sitio, asegurando que las páginas de productos y categorías más importantes sean indexadas sin exponer URLs innecesarias.

Se recomienda implementar los cambios gradualmente y monitorear los resultados en Google Search Console para evitar cualquier impacto negativo en la indexación del sitio.

#  Reporte detallado de la segunda auditoria auditoría

REPORTE DETALLADO DE AUDITORÍA Y SOLUCIÓN TÉCNICA: BLOQUEO DE PÁGINAS POR robots.txt Y URLs CON /null

## 1. Introducción

Este documento tiene como objetivo presentar un reporte técnico completo sobre la auditoría de URLs bloqueadas por el archivo robots.txt del sitio cyamoda.com, identificar errores en la generación de URLs (incluyendo aquellas con la terminación /null), y proponer soluciones claras con ejemplos específicos.

## 2. Auditoría de Páginas Bloqueadas por robots.txt

### 2.1. Identificación de páginas bloqueadas

Se realizó un rastreo completo del sitio usando Google Search Console, Screaming Frog y validación directa del archivo robots.txt.

Ejemplos de URLs bloqueadas:

https://www.cyamoda.com/update/?cgid=NINOS_ULTIMAS_TENDENCIAS&srule=Sorting%20Manual%202024&start=0&sz=24

https://www.cyamoda.com/search/?q=playera

https://www.cyamoda.com/on/demandware.store/Sites-Cya_MX-Site/es_MX/Product-Variation?...

### 2.2. Validación de posibles errores de código

Algunas URLs bloqueadas no deberían existir. Se detectaron rutas terminadas en /null, lo que indica que el problema no es solo de bloqueo, sino de generación de código.

Ejemplos:

https://www.cyamoda.com/kids/null

https://www.cyamoda.com/kids/nino/sueteres/null

https://www.cyamoda.com/playera-manga-corta-the-office/null

### 2.3. Inspección del código fuente

Se identificó un iframe como posible responsable:

<iframe src="about:blank" id="tmx_tags_iframe" title="empty" tabindex="-1" aria-disabled="true" aria-hidden="true" data-time="1734472684892" style="width: 0px; height: 0px; border: 0px; position: absolute; top: -5000px;"></iframe>

Este iframe puede estar generando referencias erróneas y contribuyendo a la aparición de /null en las URLs.

## 3. Detalle Técnico: Problema de URLs con /null

### 3.1. Causa identificada:

iframe con src="about:blank"

Variables no inicializadas en las plantillas o scripts de generación de enlaces.

### 3.2. Solución recomendada:

✅ Eliminar src="about:blank" del iframe:

<iframe id="tmx_tags_iframe" title="empty" tabindex="-1" aria-disabled="true" aria-hidden="true" style="width: 0px; height: 0px; border: 0px; position: absolute; top: -5000px;"></iframe>

✅ Validar que las URLs se construyan con ID de producto:

Incorrecto:

<a href="/kids/null">Ver producto</a>

Correcto:

<a href="/kids/3102767">Ver producto</a>

✅ Implementar redirecciones 301 para URLs con /null:

RedirectMatch 301 ^(.*)/null$ $1

## 4. Bloqueo Temporal en robots.txt y Ajustes Propuestos

### 4.1. Bloquear rutas problemáticas temporalmente:

Hasta que el error sea corregido, se recomienda bloquear estas rutas:

Disallow: */null
Disallow: /update/*
Disallow: /search/*
Disallow: /on/demandware.store/*

### 4.2. Identificar páginas innecesarias ya indexadas y solicitar eliminación en Search Console:

Usar el reporte de cobertura.

Utilizar herramienta de "Retiro de URLs" para evitar impacto en SEO.

## 5. Validación del archivo robots.txt

✅ Revisar que el robots.txt NO bloquee:

Páginas de productos reales

Categorías principales

Rutas amigables permanentes

✅ Validar con desarrollo:

Que la eliminación del src en el iframe no afecte ningún componente funcional.

Que los IDs de producto estén bien enlazados en base de datos y scripts.

✅ Integrar nuevo robots.txt en Salesforce:

Subir el archivo desde el backend o según el proceso de despliegue del entorno.

✅ Enviar nuevo rastreo a Google:

Desde Search Console:

"Inspección de URL"

Solicitar indexación de homepage y sitemap actualizado

✅ Analizar impacto:

Revisión de cobertura e impresiones tras 7-10 días.

Si hay caída notable, evaluar retroceso parcial.

## 6. Implementación y Seguimiento

✅ Validar implementación del ajuste técnico con desarrollo.

✅ Validar si se eliminan nuevas apariciones de /null.

✅ Monitorear:

Google Search Console

Logs del servidor

Screaming Frog y/o Ahrefs

## 7. Segunda Conclusión

El problema de URLs con /null se origina en un uso incorrecto de iframes y estructuras dinámicas sin validación de datos. Este documento detalla las acciones necesarias para:

Corregir el código fuente

Ajustar temporalmente el robots.txt

Validar implementación

Minimizar el impacto SEO

Se recomienda aplicar los ajustes de inmediato y documentar las pruebas de QA para validar su eficacia.



## Archivo con 1000 URLs observadas para este reporte
https://docs.google.com/spreadsheets/d/1UsY4eHQ9yq1_5j7Vsm_kEDwvddAlCe4zP2Y4kbStO04/edit?usp=sharing

