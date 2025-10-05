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

### Introducción
Una antena es una estructura metálica que captura y/o transmite ondas electromagnéticas. Las primera antenas fueron construidas en 1886 por el físico alemán Heinrich Hertz, cuando comprobó la existencia de las ondas electromagnéticas. La importancia de las antenas es innegable, debido a que son un componente fundamental en todo sistema de comunicaciones, siendo el instrumento por medio del cual se puede transmitir y recibir la información.

De esta forma, la antena construida por Hertz, la cual es denominada como una antena dipolo, puede ser analizada de forma equivalente, a como si fuera un circuito en paralelo entre un inductor y un capacitor. De esta forma, si se abren las placas del capacitor y se reemplaza al inductor por la propia inductancia del cable, se obtiene la antena dipolo. Eso hace que el análisis del comportamiento de la antena, sea muy parecido al análisis del comportamiento de un circuito resonante LC.

<img width="480" alt="imagen_dipole_ant" src="https://github.com/user-attachments/assets/d25875c9-94d5-46d3-9304-01b132b694ad" />

Las antena tienen distintas propiedades que las definen, y que las caracterizan, tales como su ancho de banda, su ganancia intrínseca, el área efectiva, su eficiencia y su patrón de radiación, entre muchas otras propiedades, las cuales varían para cada antena y aplicación. De esta forma, se tienen diferentes tipos de antenas, según su forma y tamaño, tales como por ejemplo: antena dipolo, antena parabólica, antena Yagi o la realizada en la práctica como la antena bi-quad.

De esta forma, las antenas biquad son un tipo de antena la cual tienen forma de dos cuadrados de alambre de cobre unidos entre sí por un punto de unión de soldadura, y típicamente esta antena está fijada a un reflector normalmente también de cobre, con el objetivo de añadir una direccionalidad a la antena. Usualmente se usa para la frecuencia de 2.4 GHZ del WiFi, y para aplicaciones relacionadas con el internet de las cosas (IoT).


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

### Conclusiones

- Observando las gráficas del coeficiente de reflexión S11, obtenidas en Matlab, y la obtenida a partir del VNA, se puede observar que poseen diferencias significativas con respecto a la frecuencia de resonancia y la potencia estimada en esta frecuencia, en donde se obtuvo para el caso del diseño en Matlab, una frecuencia objetivo de 915 MHz, obteniendo en la práctica con la antena una frecuencia de 775 MHz, medidos en el VNA. Para el caso de la potencia obtenida, se obtuvo -13.5379 dB y -7.803 dB respectivamente.
- Algunas de las principales razones por las cuales hay una diferencia considerable entre los resultados obtenidos al realizar el diseño en Matlab, y los medidos experimentalmente con la antena, tienen que ver principalmente con el proceso de fabricación, debido a que no se contó con instrumentos que permitieran realizar por ejemplo una medición precisa de la longitud de los lados de la antena, lo cual es fundamental dado que una pequeña desviación de algunos milímetros puede tener un efecto de un desfase del orden de MHz para la frecuencia de resonancia. Otros aspectos importante en la fabricación como darle una forma cuadrada con angulos rectos al alambre de cobre y la correcta ejecución de los puntos de soldadura para fijar la antena al reflector, también son puntos a considerar que pudieron afectar el funcionamiento esperado de la antena.
- Se comprobó la direccionalidad de la antena, al observar que la mayor potencia se obtenía en la dirección previamente observada en el patrón de radiación de Matlab, que para este caso, fue orientando la antena directamente a la antena transmisora, de forma paralela al reflector.


### Referencias
* C. G. Manning, “What is an antenna? - NASA,” NASA, Sep. 26, 2023. https://www.nasa.gov/general/what-is-an-antenna/
* Wikipedia contributors, “Antenna (radio),” Wikipedia, Aug. 24, 2025. https://en.wikipedia.org/wiki/Antenna_(radio)
* R. & S. G. & C. Kg, “Antenna Basics,” Rohde & Schwarz. https://www.rohde-schwarz.com/fi/applications/antenna-basics-white-paper_230854-59777.html
