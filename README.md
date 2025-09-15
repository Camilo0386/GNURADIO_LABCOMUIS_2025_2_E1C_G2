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

### Referencias
* J. G. Proakis y M. Salehi, Fundamentals of communication systems. Prentice Hall, 2014.
* Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones, Universidad Industrial de Santander, “Lesson 1-7 - Passband Transmission". https://lms.uis.edu.co/ava/pluginfile.php/535767/mod_folder/content/0/Lesson_1_7_Passband%20Transmission.pdf
* Wikipedia contributors, “Amplitude modulation,” Wikipedia, May 31, 2025. https://en.wikipedia.org/wiki/Amplitude_modulation
***



