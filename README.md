# Misión 3: Modulación de onda continua
### Integrantes
* Juan Esteban Herreño Novoa - 2210422
* Nelson Camilo Chaparro Nore - 2220386

Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones  
Universidad Industrial de Santander  
### Fecha
15 de septiembre de 2025
***
## Declaración de Originalidad y Responsabilidad
Los autores de este informe certifican que el contenido aquí presentado es original y ha sido elaborado de manera independiente. Se han utilizado fuentes externas únicamente como referencia y han sido debidamente citadas.

Asimismo, los autores asumen plena responsabilidad por la información contenida en este documento.
***
## Contenido
### Resumen
Para esta tercera práctica de laboratorio, se estudió el efecto que tienen las modulaciones en las formas de onda de las señales, más específicamente para esta práctica el caso de las modulaciones de amplitud. Así, se identificaron características importantes, como la de diferenciar la señal de información y la portadora, y como definir apropiadamente las características principales de la portadora, tales como su frecuencia, su tasa de muestreo y su ganancia. A su vez, se analizó el procedimiento para realizar una modulación de amplitud (AM) a partir de una SDR, utilizando para este propósito el software GNURadio. Finalmente, además de estudiar el efecto de varias señales fundamentales definidas como información, tales como la senoidal, cuadrada y triangular, se analizó también el efecto al utilizar una señal de audio. 

**Palabras Clave:** Modulación, AM, SDR, GNURadio

### Introducción
La modulación es el proceso de variar una o más propiedades de una onda periódica, que es la señal portadora, con una señal de información, obteniendo como resultado una señal modulada.

Matemáticamente se puede definir una portadora como una señal portadora con una frecuencia $f_m$ y una amplitud de la portadora $A_c$:

$c(t)=A_ccos(2\pi f_ct)$

De esta forma, el proceso de modulación en amplitud es simplemente multiplicar la portadora y la señal de información, para así tener la señal modulada:

$s(t)=A_c\left[ 1+K_acos(2\pi f_mt) \right]cos(2\pi f_ct)$

<img width="732.2" height="254.1" alt="img_proceso_modulacion" src="https://github.com/user-attachments/assets/e128a0dc-4067-4c5e-a9da-0cc32c9f99c1" />

Así, el proceso de modulación en amplitud, como su nombre lo dice, la amplitud de la señal portadora varía de acuerdo a la amplitud en ese instante de la señal de información. Esta técnica de comunicaciones fue muy importante, dado que fue la primera técnica utilizada a principios del siglo XX para transmitir audio a través de la radio. En la actualidad, aun es utilizada para transmisiones de emisoras de radio, radio amateur y radio aeronaútica.

### Procedimiento

**Primera fase**  
La primera fase consistió en definir y configurar apropiadamente el diagrama de bloques en GNURadio, en donde se definió la operación antes descrita con el fin de obtener la señal s(t) ya definida matemáticamente. A su vez, se definieron los parámetros de la señal portadora, con una frecuencia de portador de 1 kHz, una tasa de muestreo de 3.125 MHz, y una ganancia de transmisión de 0 dB.

<img width="1449" height="869" alt="flowgraph_modAM_gnuradio" src="https://github.com/user-attachments/assets/a6b8dd66-2b62-46ce-9c23-fe85302080d1" />


**Segunda fase**  

Para la segunda fase, se registraron medidas en el osciloscopio, en el cual se visualizaron señales de entrada de información a una onda senoidal, una onda cuadrada y una señal de audio. Se comprobó a través de la medición del voltaje Vpp que la amplitud de la señal envolvente no superara la amplitud de 0.5 para cada uno de los casos observados. Al momento de observar las señales en el osciloscopio, no se requirió el uso del atenuador, debido a que la señales tenían un voltaje del orden de los mV.

![img1_senoidal_osc](https://github.com/user-attachments/assets/f4737cbc-ff1a-4256-b855-bf88df0ea100)

En esta imagen se puede visualizar la forma de onda observada para el caso donde la señal de información es una senoidal. Al cambiar la configuración para obtener una onda cuadrada, se observó lo siguiente en el osciloscopio:

![img1_cuadrada_osc](https://github.com/user-attachments/assets/20092ceb-5840-4207-a916-472b32c8f170)
![img2_cuadrada_osc](https://github.com/user-attachments/assets/15db9028-08e9-45f5-ad2a-f469c5a32b74)

Como puede observarse en la imagen, la amplitud de la onda varía de acuerdo al coeficiente de modulación.

Finalmente, se utilizó uno de los audios de prueba suministrados, para poder observar el comportamiento de la modulación en una señal de audio.

![img1_audio_osc](https://github.com/user-attachments/assets/853d879f-9ce7-45e1-a1b3-2543fda95ca6)
<img src="https://github.com/user-attachments/assets/932c58a6-f51d-4f4b-a05b-28ba444ae26b" width="1449">
Así, se ve como varía la amplitud de la onda a medida que se va transmitiendo el sonido

**Tercera fase**  

#### Tabla comparativa
Para esta tercera fase, se realizó un cuadro comparativo con el objetivo de apreciar las diferencias que existen en el dominio del frecuencia, entre la señal moduladora senoidal y otros tipos de ondas moduladoras como la cuadrada, y la señal de audio. Para la frecuencia de mensaje se definió un valor para todos los casos de 7.2 kHz.

|Señal | Análisis |
|-----------|-----------|
| Senoidal | <img width="768" height="434.4" alt="img2_senoidal_gnuradio" src="https://github.com/user-attachments/assets/7ab4585f-bb16-4566-b141-b06d78fd2846" /> <img src="https://github.com/user-attachments/assets/bbf07d44-24bc-4866-b028-f9351df21778" width="768"> <br> Se reconoce que la magnitud del espectro de una señal senoidal está descrita por $X(\omega)= A\pi\left[ \delta(\omega-\omega_0) +\delta(\omega+\omega_0)\right]$ . Aún así, en la representación en el analizador de espectros se observa un impulso adicional en $\omega=0$, lo cual significa que esta señal tiene una componente DC distinta de cero|
| Cuadrada |<img width="768" alt="img2_cuadrada_gnuradio" src="https://github.com/user-attachments/assets/bd25514a-f36c-4d7f-a0bb-997008e3b9f1" /> <img src="https://github.com/user-attachments/assets/a2051e8f-64d2-4fe8-86ee-2b05fb17fa46" width="768"> <br> Por su parte, la onda cuadrada puede definirse como una suma infinita de senoidales, por este motivo sus componentes téoricamente serán infinitas y representaran sendos impulsos que decaen simétricamente a medida que se aleja de la frecuencia central. Esto es distinto a la onda senoidal pura, la cual solo tiene dos componentes a una frecuencia definida. Formalmente, la onda cuadrada se define como: $x(t)=\frac{4}{\pi}\sum_{k=1}^{\infty }\frac{sen(2\pi(2k-1)ft))}{2k-1}$| 
| Audio |<img width="768" alt="img1_audio_gnuradio" src="https://github.com/user-attachments/assets/48f6fba3-ef7e-4097-b590-456e4f666879" /> <img src="https://github.com/user-attachments/assets/87e5366e-0797-4c17-82e1-dee7a2f386ed" width="768"> <br> Para esta forma de onda, se puede observar que su forma es compleja debido a los diversos componentes que posee, teniendo en cuenta todos los instrumentos utilizados para realizar la canción. Esto contrasta con respecto a la señal senoidal, la cual es más simple debido a los únicos dos componentes que definen su espectro. En la señal se puede observar su frecuencia central a 100 MHz, y un ancho de 44 kHz, el cual es el ancho de banda típico usado en los archivos de música digitales. | 
<br>

Al observar las distintas formas de onda en el dominio del tiempo en el osciloscopio, se puede observar, teniendo una vista más amplia de la señal, el tipo de onda que se estaba ingresando. Para poder observar de forma directa el efecto de modulación que se estaba presentando en cada caso, fue necesario ajustar la escala de tiempo-horizontal, debido a las altas frecuencias de las señales de entrada.

Con respecto a los espectros de las señales observados en el analizador, puede verse que la forma de onda que ocupa el mayor ancho de banda, es la onda cuadrada, dado que teóricamente se extiende de forma infinita.

El espectro resultante de la onda cuadrada contiene más componentes armónica que la señal senoidal, dado que, como se dijo anteriormente, la onda cuadrada se define como la sumatoria de distintas ondas senoidales de diferente amplitud.

Con respecto a las dificultades presentadas al momento de realizar la practica, se presentaron principalmente al momento de visualizar las señales en el osciloscopio, dado que había que configurar la escala de tiempo adecuadamente para ver el efecto de la modulación de la amplitud de la señal. No se presentaron problemas de saturación ni al momento de ajustar la ganancia, dado que con los parámetros configurados inicialmente fue posible visualizar las señales directamente sin necesidad de hacer uso de un atenuador. Se presentaron algunos problemas al visualizar el espectro de las señales, y ver su concordancia con sus gráfica equivalentes proporcionadas por GNURadio.

### Conclusiones

- Una de las principales ventajas del AM está relacionado con la facilidad con la que se pueden enviar señales a partir de este procedimiento, dado que es solo realizar una multiplicación entre la señal portadora y la señal de información.
- Una de las principales desventajas en ciertos casos, es que la modulación en amplitud puede aumentar la amplitud total de la señal, elevando el nivel de voltaje a niveles que podrían ser perjudiciales para el correcto funcionamiento de los equipos y poner en riesgo potencial la salud de las personas.
- Otra de las desventajas de este tipo de modulación está relacionada con la saturación que presenta la señal debido a un ajuste incorrecto de la ganancia de la señal, así, esto provocaría que la forma de la onda cambiara afectando significativamente la calidad de la información que se quiere transmitir.
- Las siguientes etapas de desarrollo de este proyecto podrían estar enfocadas en que el sistema tenga la capacidad de enviar señales de audio en tiempo real, como ocurre por ejemplo en las emisoras de radio; y a su vez poder transmitir señales a más largas distancias utilizando las antenas apropiadas que garanticen la potencia de salida requerida del sistema.

### Referencias
* J. G. Proakis y M. Salehi, Fundamentals of communication systems. Prentice Hall, 2014.
* Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones, Universidad Industrial de Santander, “Lesson 1-7 - Passband Transmission". https://lms.uis.edu.co/ava/pluginfile.php/535767/mod_folder/content/0/Lesson_1_7_Passband%20Transmission.pdf
* Wikipedia contributors, “Amplitude modulation,” Wikipedia, May 31, 2025. https://en.wikipedia.org/wiki/Amplitude_modulation
***



