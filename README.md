# Misión 4: Vigilancia del Espectro legal
### Integrantes
* Juan Esteban Herreño Novoa - 2210422
* Nelson Camilo Chaparro Nore - 2220386

Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones  
Universidad Industrial de Santander  
### Fecha
22 de septiembre de 2025
***
## Declaración de Originalidad y Responsabilidad
Los autores de este informe certifican que el contenido aquí presentado es original y ha sido elaborado de manera independiente. Se han utilizado fuentes externas únicamente como referencia y han sido debidamente citadas.

Asimismo, los autores asumen plena responsabilidad por la información contenida en este documento.
***
## Contenido
### Resumen
Para esta cuarta práctica de laboratorio, se estudió el procedimiento para la vigilancia del espectro FM, para este propósito, se utilizaron las páginas oficiales del ministerio TIC, con el objetivo de obtener una lista de las emisoras FM autorizadas para su operación en Bucaramanga y su área metropolitana. Después de obtener esta lista oficial, se realizó un escaneo a partir de la SDR, con el fin de comprobar la información recopilada anteriormente. Se recolectaron datos relevantes para las emisoras encontradas en barrido en la SDR tales como la frecuencia y la potencia estimada de la estación. A su vez, se observó detenidamente para intentar encontrar transmisiones no identificadas en los registros oficiales.

**Palabras Clave:** Vigilancia, espectro, ANE, SDR

### Introducción
El espectro radioeléctrico es un recurso natural limitado, por esta razón, es necesario administrarlo de forma eficiente con el objetivo de que todos los servicios de comunicaciones operen de forma adecuada sin interferirse unos con otros. Es por ello que la vigilancia del espectro es una tarea importante en el correcto funcionamiento de los sistemas de comunicaciones de un país. En Colombia, la entidad encargada de la vigilancia y el control del espectro radioeléctrico es la Agencia Nacional del Espectro (ANE), una unidad administrativa especial adscrita el Ministerio de las Tecnologías de la Información y Comunicaciones (MinTIC), creada en el 2009 a partir de la expedición de la ley 1341 del mismo año.

De esta forma el MinTIC posee documentos específicos en donde establecen diversas normativas para los distintos servicios del espectro radioeléctrico, tales como el Plan técnico de radiodifusión sonora para FM, el cual establece específicamente "la ordenación técnica del espectro radioeléctrico del servicio, señala las condiciones técnicas para las diversas formas de transmisión y define los parámetros técnicos esenciales de las estaciones de radiodifusión sonora". A su vez, el ministerio tiene a disposición diversas páginas web interactivas donde se pueden hacer consultas acerca de las emisoras autorizadas para prestar el servicio en el territorio nacional, de esta forma, en el micrositio se pueden hacer consultas para los distintos servicios tanto AM como FM, y filtrar las emisoras autorizadas tanto para departamentos como para municipios.

### Procedimiento

**Primera fase**  
Para la primera fase se recolectó la información de las emisoras FM registradas en Bucaramanga y su área metropolitana y se consignaron en la siguiente tabla:

#### Tabla emisoras FM registradas para Bucaramanga y su área metropolitana
<img width="920" height="1086" alt="listaEmisorasFM_Bucaramanga" src="https://github.com/user-attachments/assets/333e1c67-974d-402d-a8a6-4f5d0e6c13c6" />

**Segunda fase**  
Para la segunda fase, se configuró el SDR a partir de GNURadio para poder sintonizar las distintas emisoras de FM, desde un rango de 88 a 108 MHz. Se registraron las emisoras detectadas, junto con su potencia estimada.

<img width="1857" height="1045" alt="cap_mision4" src="https://github.com/user-attachments/assets/43f51925-d3cf-48be-9243-61e31d635c41" />

La información de las emisoras halladas y la estimación de su potencia se encuentra en la siguiente tabla:

<img width="211" height="382" alt="listaEmisorasFM_halladas" src="https://github.com/user-attachments/assets/4fc3a313-4213-4a98-a5af-c894b60d1e59" />

### Referencias
* “Agencia Nacional del Espectro | La entidad.” https://www.ane.gov.co/SitePages/la-entidad/index.aspx?p=231
* “MINTIC Colombia - Plan técnico nacional,” MINTIC Colombia. https://www.mintic.gov.co/portal/inicio/Micrositios/Sector-de-Radiodifusion-Sonora/Plan-Tecnico-Nacional/
* “Radioemisoras Colombia” https://www.mintic.gov.co/portal/maparadio/842/w3-channel.html
***
