# Misión 5: Creando nuestra propia antena
### Integrantes
* Juan Esteban Herreño Novoa - 2210422
* Nelson Camilo Chaparro Nore - 2220386

Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones  
Universidad Industrial de Santander  
### Fecha
5 de octubre de 2025
***
## Declaración de Originalidad y Responsabilidad
Los autores de este informe certifican que el contenido aquí presentado es original y ha sido elaborado de manera independiente. Se han utilizado fuentes externas únicamente como referencia y han sido debidamente citadas.

Asimismo, los autores asumen plena responsabilidad por la información contenida en este documento.
***
## Contenido
### Resumen
En esta quinta práctica de laboratorio, se estudió el procedimiento para diseñar y crear una antena bi-quad, la cual es utilizada para distintas aplicaciones como Wi-Fi y el internet de las cosas (IoT). De esta forma, para realizar el diseño, se hicieron unos cálculos previos, con el objetivo de definir las dimensiones de la antena, dependiendo de la frecuencia de operación específica elegida. Posteriormente, se utilizó Matlab utilizando la aplicación Antenna Designer, con el objetivo de visualizar gráfica de interés como S11 o el patrón de radiación, y así definir de forma precisa las dimensiones apropiadas de la antena. Finalmente, se realizó el proceso de construcción de la antena, y se realizaron mediciones experimentales tales como el cálculo de la gráfica de S11, visualización del espectro y comprobación de la correcta direccionalidad de la antena.  

**Palabras clave**:Bi-Quad Antenna, Matlab, Antenna Designer, VNA  

## Introducción
Una antena es una estructura metálica que captura y/o transmite ondas electromagnéticas. Las primera antenas fueron construidas en 1886 por el físico alemán Heinrich Hertz, cuando comprobó la existencia de las ondas electromagnéticas. La importancia de las antenas es innegable, debido a que son un componente fundamental en todo sistema de comunicaciones, siendo el instrumento por medio del cual se puede transmitir y recibir la información.

De esta forma, la antena construida por Hertz, la cual es denominada como una antena dipolo, puede ser analizada de forma equivalente, a como si fuera un circuito en paralelo entre un inductor y un capacitor. De esta forma, si se abren las placas del capacitor y se reemplaza al inductor por la propia inductancia del cable, se obtiene la antena dipolo. Eso hace que el análisis del comportamiento de la antena, sea muy parecido al análisis del comportamiento de un circuito resonante LC.

<img width="676" height="296" alt="imagen_dipole_ant" src="https://github.com/user-attachments/assets/d25875c9-94d5-46d3-9304-01b132b694ad" />

Las antenas tiene diversas formas y tamaños, dependiendo de la aplicación que se requiera.

### Referencias
* C. G. Manning, “What is an antenna? - NASA,” NASA, Sep. 26, 2023. https://www.nasa.gov/general/what-is-an-antenna/
* Wikipedia contributors, “Antenna (radio),” Wikipedia, Aug. 24, 2025. https://en.wikipedia.org/wiki/Antenna_(radio)
* R. & S. G. & C. Kg, “Antenna Basics,” Rohde & Schwarz. https://www.rohde-schwarz.com/fi/applications/antenna-basics-white-paper_230854-59777.html
