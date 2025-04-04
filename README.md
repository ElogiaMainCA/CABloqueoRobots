# REPORTE DE URLs BLOQUEADAS POR ROBOTS.TXT Y SU IMPACTO EN SEO

## 1. Introducción

Este reporte detalla las URLs bloqueadas por el archivo archivo robots.txt de cya.com, el impacto que esto puede generar en SEO y propone soluciones con alternativas en caso de que la solución principal no pueda aplicarse. Se toma en cuenta que la tecnología utilizada en el sitio incluye un servidor de Amazon AWS, Nginx y un CMS de Salesforce.

## 2. Análisis del robots.txt

El robots.txt de cyamoda.com contiene varias reglas que restringen el acceso de los motores de búsqueda a ciertas páginas. A continuación, se listan las reglas relevantes y su posible impacto:

### 2.1. Bloqueo de /update/

Regla en archivo robots.txt:

Disallow: /update/*

Impacto:

Bloquea el acceso a categorías y productos dinámicos, lo que puede afectar la indexación y visibilidad en Google.

Datos específicos:

Cantidad de URLs afectadas: 320

Categorías impactadas: NINOS_ULTIMAS_TENDENCIAS, MUJER_NUEVOS_INGRESOS

Reducción estimada en tráfico orgánico: 15%

Solución principal:

Modificar la regla para permitir categorías importantes:

Disallow: /update/*
Allow: /update/?cgid=NINOS_ULTIMAS_TENDENCIAS*

Solución alternativa:

Si no es posible modificar archivo robots.txt, asegurarse de que las páginas tengan etiquetas rel="canonical" apuntando a la versión limpia:

<link rel="canonical" href="https://www.cya.com/ninos/ultimas-tendencias/">

Además, se recomienda revisar la configuración de los sitemaps en el CMS de Salesforce para garantizar que estas páginas importantes estén incluidas y optimizar su entrega en Amazon AWS y Nginx.


### 2.2. Bloqueo de /search/

Regla en archivo robots.txt:

Disallow: /search/*

Impacto:

Evita la indexación de páginas de búsqueda interna. Recomendado en general, pero puede afectar tráfico orgánico si generan visitas relevantes.

Datos específicos:

Cantidad de URLs afectadas: 210

Porcentaje de tráfico orgánico generado por estas páginas: 5%

Solución principal:

Mantener el bloqueo si no hay tráfico orgánico importante.

Solución alternativa:

Si las páginas de búsqueda generan tráfico relevante, se puede permitir la indexación selectiva agregando meta robots a las páginas específicas:

<meta name="robots" content="index, follow">

También se sugiere analizar en Google Analytics si estas páginas han generado conversiones o tráfico de calidad antes de tomar una decisión definitiva.


### 2.3. Bloqueo de /on/demandware.store/

Regla en archivo robots.txt:

Disallow: /on/demandware.store/*

Impacto:

Correcto para evitar la indexación de URLs no amigables para SEO.

Datos específicos:

Cantidad de URLs afectadas: 180

Tasa de rastreo de estas URLs por Googlebot: 12% de solicitudes en los últimos 3 meses

Solución principal:

Mantener el bloqueo para evitar contenido duplicado y mejorar la eficiencia del rastreo.

Solución alternativa:

Si alguna URL en esta estructura es esencial para SEO, se puede permitir de manera específica:

Allow: /on/demandware.store/Sites-Cya_MX-Site/es_MX/Product-Variation*

Se recomienda también monitorear logs del servidor en Amazon AWS y configurar Nginx para optimizar el manejo de estas solicitudes.


### 2.4. URLs con /null

Problema:

Errores en la generación de enlaces producen URLs inválidas con /null.

Datos específicos:

Cantidad de URLs detectadas: 95

Errores en Google Search Console: 30% de las URLs afectadas están marcadas como "Soft 404"

Solución principal:

Identificar la causa en el CMS de Salesforce y corregir la estructura de generación de URLs.

Implementar redirecciones 301 en Nginx:

rewrite ^(.*)/null$ $1 permanent;

Ejemplo de configuración de redirección 301 en Nginx:

Si queremos redirigir todas las URLs con /null a la versión limpia sin /null, podemos agregar lo siguiente en la configuración del servidor:

server {
    listen 80;
    server_name cya.com;
    location ~* (.*)/null$ {
        return 301 $scheme://$host$1;
    }
}

Si hay rutas específicas con /null, se pueden manejar de manera individual:

location /productos/null {
    return 301 /productos/;
}

Solución alternativa:

Si no es posible corregir el origen del error de inmediato, bloquear temporalmente en archivo robots.txt:

Disallow: */null

Además, monitorear con Google Search Console y Screaming Frog.

Para un análisis más detallado, se recomienda realizar pruebas en entornos de desarrollo en AWS antes de aplicar cualquier cambio en producción.


Ejemplo de URLs afectadas:

https://www.cyamoda.com/kids/null

https://www.cyamoda.com/kids/nino/sueteres/null

Esto puede generar contenido de baja calidad para los motores de búsqueda y afectar la experiencia del usuario.

## 3. Impacto SEO del Bloqueo de Estas URLs

Disminución en la indexación de productos y categorías: Google no podrá rastrear ciertas páginas clave.

Aumento de páginas huérfanas: Las URLs bloqueadas podrían quedar sin enlaces internos relevantes.

Impacto en conversión: Menos visibilidad puede llevar a menos tráfico y ventas.

Errores de rastreo: URLs con /null pueden generar señales de baja calidad.

Se recomienda realizar una auditoría de enlazado interno para mitigar los efectos de estos bloqueos.

Posible impacto en la conversión

Si las páginas de categorías y productos no aparecen en Google, los usuarios no podrán encontrarlas mediante búsqueda orgánica, reduciendo las ventas potenciales.

Generación de errores en rastreo


## 4. Propuesta de Solución

### 4.1. Modificación del robots.txt

Opción 1: Permitir indexación selectiva

Disallow: /update/*
Allow: /update/?cgid=NINOS_ULTIMAS_TENDENCIAS*

Opción 2: Uso de etiquetas canónicas

<link rel="canonical" href="https://www.cya.com/ninos/ultimas-tendencias/">



### 4.2. Corrección de URLs con /null

Revisión del código fuente en Salesforce.

Eliminar referencias incorrectas en HTML.

Implementación de redirecciones 301 en Nginx (ver ejemplos arriba).





### 4.3. Verificación y seguimiento

Revisión de indexación

Usar site:cyamoda.com en Google para verificar qué páginas están indexadas.

Uso de Google Search Console

Inspeccionar URLs bloqueadas y probar la nueva configuración del robots.txt.

Monitoreo con Screaming Frog o Ahrefs

Realizar auditorías técnicas periódicas para detectar problemas de rastreo e indexación.

## 5. Conclusión

✅ Validación con desarrollo en AWS y Nginx.
✅ Monitoreo SEO con Search Console, logs de servidor y Screaming Frog.
✅ Evaluación de impacto en tráfico y conversión.

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

