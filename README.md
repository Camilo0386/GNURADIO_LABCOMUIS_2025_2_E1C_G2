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

### Referencias
* J. G. Proakis and M. Salehi, Fundamentals of communication systems. Prentice Hall, 2014.
* Wikipedia contributors, “Frequency modulation,” Wikipedia, Oct. 13, 2025. https://en.wikipedia.org/wiki/Frequency_modulation
* L. Der, “Frequency Modulation (FM) Tutorial,” Silicon Laboratories Inc. https://wwwqa.silabs.com/documents/public/white-papers/FMTutorial.pdf
* “FM broadcasting.” https://helpfiles.keysight.com/csg/n7611b/Content/Main/FM_Broadcasting.htm


