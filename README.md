# Misión 6: Nuestra propia emisora FM
### Integrantes
* Juan Esteban Herreño Novoa - 2210422
* Nelson Camilo Chaparro Nore - 2220386

Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones  
Universidad Industrial de Santander  
### Fecha
20 de octubre de 2025
***
## Declaración de Originalidad y Responsabilidad
Los autores de este informe certifican que el contenido aquí presentado es original y ha sido elaborado de manera independiente. Se han utilizado fuentes externas únicamente como referencia y han sido debidamente citadas.

Asimismo, los autores asumen plena responsabilidad por la información contenida en este documento.
***

## Contenido
### Resumen
En esta sexta práctica de laboratorio, se realizó el procedimiento para realizar una transmisión de radio FM, utilizando para este propósito el software GNURadio. De esta forma, se creó primero un audio de prueba el cual sería retransmitido, y seguido de ello se generó la señal multiplex (MPX). Posterior a ello, usando un bloque modulador FM en GNURadio, tomando como señal de entrada la generada (MPX) y la radio definida por software (SDR), se realizó la transmisión del audio, tomando en cuenta para este propósito tomar una frecuencia libre de la banda comercial de radio FM, definida típicamente entre 88 y 108 MHz. 

**Palabra clave**: FM station, MPX, GNURadio, SDR

### Introducción

La modulación en frecuencia es una técnica utilizada en comunicaciones, para transmitir información a partir de las ondas de radio. De esta forma, al igual que su contraparte de modulación en amplitud, una señal portadora varía su frecuencia, en función de la variación de amplitud de la señal de información, que generalmente suele ser una señal de audio.

<img width="1444" height="375" alt="FM_Modulation_-_en" src="https://github.com/user-attachments/assets/384905b8-0ba1-450d-8456-0f2c32b74602" />

La principal ventaja de este tipo de modulación, es su alta inmunidad al ruido, aunque para su transmisión ocupe un mayor ancho de banda en comparación con su contraparte AM.

De manera formal, matemáticamente la modulación en frecuencia puede definirse como:

Partiendo de una señal modulada definida como:

$u(t)=A_ccos(2\pi f_{c}t+\phi(t))$

Donde $f_c$ representa la frecuencia de portadora, y $\phi(t)$ denota la fase variante con el tiempo. De esta forma, considerando una señal de información $m(t)$, la variación de la fase en la modulación FM se define como:

$\phi(t)=2\pi k_{f}\int_{-\infty }^{t}m(\tau)d\tau$

Donde $k_f$ es una constante de desviación de frecuencia, dado que la desviación en frecuencia respecto a la portadora para un sistema FM es proporcional a la señal de información.

De esta forma, el proceso de transmisión FM, se realiza a traves de la generación de una señal multiplex (MPX). El objetivo de este proceso es poder tomar una señal de audio estereo, y poder transformarla para así tener en la salida una señal resultante la cual se ingresa al sistema modulador FM. El proceso a realizar esta consignado en el siguiente diagrama de bloques:

<img  height="222" alt="flowgraph_FM_Mod" src="https://github.com/user-attachments/assets/406c0e15-6ca5-4842-ab00-84786d0d9891" />

Así, el espectro resultante de la señal de salida, que va a ser ingresada el modulador FM, tiene diversas características, tales como una señal mono, una señal piloto, y una señal estereo, tal como se observa en la imagen.

<img  height="322" alt="MPX_spectrum" src="https://github.com/user-attachments/assets/72433e4b-65a2-4a0d-b00a-0f05e9746881" />

### Procedimiento

<br>

**Primera fase** 


La primera fase se centró en la elaboración del material sonoro para ser reproducido en la estación. De esta forma, se hizo uso de herramientas de inteligencia artificial para generar el audio inicial de la programación de la emisora. Posteriormente se eligió una canción de nuestra preferencia, y finalmente se realizó la edición final del audio utilizando el software Audacity.

Así, la estructura del audio, quedo distribuida como una presentación inicial incluyendo el nombre de la emisora, y un fade in que dio paso a la reproducción de la canción. Se definió dentro de las propiedades del audio, que este fuera estereo, y se exportó finalmente en formato .wav. <br> <br>

**Segunda fase**  

Seguidamente, se realizó el procedimiento para generar la señal MPX en GNURadio, partiendo como entrada al audio previamente creado. Para cargar este archivo, se hizo uso del bloque WAV File Source, y se modificó para tener dos canales, correspondientes al L y R del audio estereo.  

<img  height="86" alt="wav_file_source" src="https://github.com/user-attachments/assets/34d1687a-278f-4273-a53d-a0e2afba1d68" />

Posteriormente, se realizó la construcción completa del diagrama de bloques, para representar el proceso de generación de la señal MPX. Para este propósito se uso de diversos bloques tales como el sumador (Add), restador (Substract), y multiplicador (Multiply).

<img width="1628" height="787" alt="img_gnuradio_lab6" src="https://github.com/user-attachments/assets/ac6ba58f-5597-487d-bbba-46846901ec43" />

Así, hay una primera fase, donde se genera una señal monofónica, al sumar los canales L+R. También se genera un tono piloto a partir de Signal Source, con una frecuencia de 19 $[kHz]$. Se crea la señal diferencia L-R, y se multiplica por una portadora de 38 $[kHz]$, creada en este caso en GNURadio elevando al cuadrado la señal piloto. Finalmente se suman las tres señales anteriores para formar la señal de salida MPX.

De este modo, se realizó la simulación en GNURadio para así poder visualizar el espectro resultante, con el objetivo de comprobar la correcta ubicación y amplitud de los diversos componentes de la señal MPX. Así, se obtuvieron los siguientes resultados:

<img width="1853" height="1048" alt="img2_gnuradio_lab6" src="https://github.com/user-attachments/assets/97b6b6e7-b066-4ad7-8d7c-f9420e8d3a11" />

Se puede observar efectivamente, la correcta ubicación y amplitud de cada componente de la señal MPX, coincidiendo con la descripción inicial propuesta.

<img width="4839" height="1321" alt="spectrum_MPX_GNU" src="https://github.com/user-attachments/assets/327b3a78-7b1c-4aff-8e2f-d7fe67eb04f9" /> <br> <br>

    
**Tercera fase**  

En esta ultima fase, se realizaron las actividades necesarias para lograr la emisión de la señal y poder comprobar su correcta recepción en un receptor de radio FM.

Así, se complementó el diagrama realizado en GNURadio, para, tomando la señal MPX, realizar su respectiva modulación en frecuencia, y a su vez, definir la frecuencia central y la potencia a la que sería transmitida la señal, a partir de los bloques WBFM y USRP Sink respectivamente.
<img width="1479" height="824" alt="img_parte2_gnu" src="https://github.com/user-attachments/assets/4fa47ca8-b83a-49d2-a818-597f6467b43e" />

Así, se definió una frecuencia central de 94.5 [MHz], con una ganancia inicial de 0 [dB]. De esta manera, teniendo el diagrama completo, se verificó los resultados de la implementación en GNURadio, a partir de los bloques, Waterfall Sink, y Frequency Sink, los cuales dan una visualización del espectrograma y el espectro de la señal de salida.

<img width="1845" height="1050" alt="img_fft_lab6_pt2_gnuradio" src="https://github.com/user-attachments/assets/5a01021f-909a-4b0a-9869-fbc9fdcc807b" />   <br> <br> <br>

Con estos resultados previos, se continuó conectando la SDR al analizador de espectros, y así observar la gráfica esperada. Así, se obtuvo una frecuencia centrada en 94.5 [MHz], lo cual es correcto y coincide con la frecuencia elegida y los resultados obtenidos anteriormente.

<img height="1050" src="https://github.com/user-attachments/assets/ba5c9b26-2ca4-4ff8-ab6b-06ba5ded68ba"/> <br> <br>

Finalmente se conectó la SDR a una antena para transmitir la señal, y se sintonizó la emisora en un receptor FM, obteniendo un resultado satisfactorio, escuchando apropiadamente el audio. Respecto a la calidad del audio, en principio se escuchaba saturado, motivo por el cual fue necesario ajustar el valor de ganancia para obtener así el resultado esperado.

### Conclusiones

- El sistema implementado cumple con el objetivo inicial de la práctica, la cual era implementar un transmisión FM estéreo, igual a la que utilizan las radios comerciales. Así, se realizó el proceso para generar la señal multiplexada y tomandola como entrada para la modulación en frecuencia, obteniendo como resultado, una recepción del audio realizado y la frecuencia central elegida.
- Una de las principales limitaciones del sistema está relacionado con la potencia de transmisión, debido a las antenas utilizadas y la potencia máxima a la que puede transmitir el SDR. Por esta razón, el funcionamiento de la estación está limitado a un radio de unos pocos metros de distancia respecto al sistema de transmisión.
- Una de las posibles mejoras está relacionada con la capacidad de poder transmitir audio en tiempo real, debido a que en esta práctica se limitó a transmitir un audio previamente grabado. Así, un sistema con estas características sería mucho más cercano a lo que es una radio comercial con programación continua.
- Así, se podría utilizar un mixer, para transmitir el audio en tiempo real, y así poder tener diferentes salidas de audio, tales como la voz hablada, programación musical, entre otras.
### Referencias
* J. G. Proakis and M. Salehi, Fundamentals of communication systems. Prentice Hall, 2014.
* Wikipedia contributors, “Frequency modulation,” Wikipedia, Oct. 13, 2025. https://en.wikipedia.org/wiki/Frequency_modulation
* L. Der, “Frequency Modulation (FM) Tutorial,” Silicon Laboratories Inc. https://wwwqa.silabs.com/documents/public/white-papers/FMTutorial.pdf
* “FM broadcasting.” https://helpfiles.keysight.com/csg/n7611b/Content/Main/FM_Broadcasting.htm


