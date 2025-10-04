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
En esta quinta práctica de laboratorio, se estudió el procedimiento para diseñar y crear una antena bi-quad, la cual es utilizada para distintas aplicaciones como Wi-Fi y el internet de las cosas (IoT). De esta forma, para realizar el diseño, se hicieron unos cálculos previos, con el objetivo de definir las dimensiones de la antena, dependiendo de la frecuencia de operación específica elegida. Posteriormente, se utilizó Matlab utilizando la aplicación Antenna Designer, con el objetivo de visualizar gráfica de interés como S11 o el patrón de radiación, y así definir de forma precisa las dimensiones apropiadas de la antena. Finalmente, se realizó el proceso de construcción, y se realizaron mediciones experimentales tales como el cálculo de la gráfica de S11, visualización del espectro y comprobación de su correcta direccionalidad.  

**Palabras clave**:Bi-Quad Antenna, Matlab, Antenna Designer, VNA  

## Introducción
Una antena es una estructura metálica que captura y/o transmite ondas electromagnéticas. Las primera antenas fueron construidas en 1886 por el físico alemán Heinrich Hertz, cuando comprobó la existencia de las ondas electromagnéticas. La importancia de las antenas es innegable, debido a que son un componente fundamental en todo sistema de comunicaciones, siendo el instrumento por medio del cual se puede transmitir y recibir la información.

De esta forma, la antena construida por Hertz, la cual es denominada como una antena dipolo, puede ser analizada de forma equivalente, a como si fuera un circuito en paralelo entre un inductor y un capacitor. De esta forma, si se abren las placas del capacitor y se reemplaza al inductor por la propia inductancia del cable, se obtiene la antena dipolo. Eso hace que el análisis del comportamiento de la antena, sea muy parecido al análisis del comportamiento de un circuito resonante LC.

<img width="676" height="296" alt="imagen_dipole_ant" src="https://github.com/user-attachments/assets/d25875c9-94d5-46d3-9304-01b132b694ad" />

Las antenas tiene diversas formas y tamaños, dependiendo de la aplicación que se requiera.

### Procedimiento

**Primera fase**

La primera fase consistió en realizar el diseño de las dimensiones de la antena, y después ajustar estas dimensiones de forma precisa a través de la app Antenna Designer en Matlab.

De esta forma, se seleccionó una frecuencia de interés de 915 MHz. Para calcular la longitud de onda:  

$\lambda=\frac{c}{f}=\frac{3\times 10^{8}}{915\times 10^{6}}= 0.328\text{ m} = 32.8 \text{ cm}$  

Y la aproximación de los lados de cada cuadrado:  

$L=\frac{\lambda}{4}=\frac{0.328}{4}=0.082 \text{ m}=8.2 \text{ cm}$

A su vez, se definió una distancia al reflector inicial igual a $\lambda/8$

$\frac{\lambda}{8}=\frac{0.328}{8}=0.041 \text{ m}=4.1 \text{ cm}$

Así, estos valores obtenidos se ingresaron en la app Antenna Designer de Matlab, incluida las dimensiones del reflector, que para este caso en particular fueron de 10x20 cm.

<img width="1364" height="593" alt="ini_design_bq_matlab" src="https://github.com/user-attachments/assets/c7c4aa13-d1d5-4bac-a61f-8de05a03e920" />

De esta forma, se ajustaron levemente estos parámetros con el fin de obtener la frecuencia centrada en 915 MHz al momento de observar las gráficas de S11 y el patrón de radiación:

Gráfico de S11:
<img width="1363" height="594" alt="graph_S11" src="https://github.com/user-attachments/assets/53177e5f-197a-47c6-bdc2-577735080f7d" />

Gráfico de patrón de radiación:
<img width="1348" height="929" alt="graph_3d_pattern" src="https://github.com/user-attachments/assets/d9e7d9cb-04b0-4033-81ed-2d98f27c6863" />

Observando el gráfico del 3D pattern, se observan dos lóbulos principales, radiando de forma perpendicular al reflector.

De esta forma, las cantidades relevantes definidas para el diseño de la antena están consignadas en la siguiente tabla
|            |          |
|-----------|-----------|
| Frecuencia |915 MHz|
| Dimensiones reflector |10x20 cm |
| Longitud de lado (L) |0.086 m | 
| Spacing del reflector |0.04 m |

**Segunda fase**

Posteriormente, se realizó la construcción de la antena bi-quad, utilizando para este propósito alambre de cobre 16 AWG, alicates para darle la forma a la antena, una regla para medir las longitudes de lado de la antena, y un cautin para soldar los puntos de conexión y fijar la antena al conector SMA y el reflector.

<img width="720" src="https://github.com/user-attachments/assets/36a72012-8931-4cc0-b181-3388d5721e55" />

**Tercera fase**
Para esta fase, se hizo uso de un analizador vectorial de redes (VNA), con el objetivo de poder medir el parámetro S11 experimentalmente de la antena construida. Los resultados fueron los siguientes:

<img width="1348" src="https://github.com/user-attachments/assets/678da6ec-706c-4099-bde4-45dcf44caab3" />

Como se puede observar, hay diferencias respectado a lo observado en Matlab, teniendo en este caso una frecuencia de 775 MHz, y una potencia de -7.803 dB. En comparación con los 915 MHz y -13.69 dB observados en Matlab.          



Posteriormente se utilizo un generador de señales conectado a una antena Yagi transmisora, con el objetivo de transmitir señales a esta frecuencia hallada con el VNA (775 MHz). De esta forma, se realizó una medición de la potencia observada en el analizador de espectros:

<img width="1348" src="https://github.com/user-attachments/assets/ec1c3863-6e2c-4f61-8a8a-906f1149634a" />

A su vez se realizó una nueva medición, pero en este caso utilizando una antena de RF elaborada en PCB, para medir su potencia a esta frecuencia, obteniendo los siguientes resultados en el analizador de espectros:

<img width="1348" src="https://github.com/user-attachments/assets/8ff73864-0691-456c-aeb3-c37ba05f9a59" />




### Referencias
* C. G. Manning, “What is an antenna? - NASA,” NASA, Sep. 26, 2023. https://www.nasa.gov/general/what-is-an-antenna/
* Wikipedia contributors, “Antenna (radio),” Wikipedia, Aug. 24, 2025. https://en.wikipedia.org/wiki/Antenna_(radio)
* R. & S. G. & C. Kg, “Antenna Basics,” Rohde & Schwarz. https://www.rohde-schwarz.com/fi/applications/antenna-basics-white-paper_230854-59777.html
