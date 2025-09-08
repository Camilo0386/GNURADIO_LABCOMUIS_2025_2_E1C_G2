# Misión 2: El enlace crítico
### Integrantes
* Juan Esteban Herreño Novoa - 2210422
* Nelson Camilo Chaparro Nore - 2220386

Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones  
Universidad Industrial de Santander  
### Fecha
7 de septiembre de 2025
***
## Declaración de Originalidad y Responsabilidad
Los autores de este informe certifican que el contenido aquí presentado es original y ha sido elaborado de manera independiente. Se han utilizado fuentes externas únicamente como referencia y han sido debidamente citadas.

Asimismo, los autores asumen plena responsabilidad por la información contenida en este documento.
***
## Contenido
### Resumen
En esta segunda práctica se estudió el efecto de la atenuación en las señales de comunicaciones, cuál son sus efectos principales al momento de visualizar las señales, como se calcula la atenuación a partir de los valores medidos a partir del analizador de espectros, y al final poder determinar el efecto que tienen la longitud de los cables de conexión de transmisión de señales en este fenómeno de la atenuación. Finalmente se calculó la atenuación con respecto a una medición de referencia y se realizó una tabla para comparar los valores calculados a varias frecuencias para distintas longitudes de cable, y se comparó con los datos proporcionados por un fabricante. 

**Palabras Clave:** Atenuación, Cables, Analizador de espectros, RG58, SDR

### Introducción
La atenuación en las comunicaciones se refiere principalmente a la pérdida de potencia que sufre una señal, al atravesar un medio de transmisión. Este efecto sucederá siempre, y su intensidad dependerá de diversas condiciones relacionadas al medio en específico.La atenuación suele medirse en unidades logarítmicas, principalmente dB o dBm.  

Las ondas electromagnéticas no son el único tipo de onda que sufre la atenuación, siendo realmente un fenómeno general a todas las ondas, aun así, las razones por las que podría producirse atenuación en la ondas electromagnéticas está relacionado más especificamente con condiciones como las interferencias, la absorción debido a medios físicos, o la dispersión; siendo todos estos fenómenos que producen una atenuación respecto a la señal original

De esta forma, la práctica se enfocó en analizar uno de estas condiciones que producen atenuación, como es la longitud del medio de transmisión, y así poder determinar que tanto impacto tiene este fenómeno en la potencia de la señal.

### Procedimiento
La primer fase consistió en generar una señal de prueba, para este caso, de una frecuencia central de 200 MHz, y una potencia de 0 dB.

<img width="1039" height="591" alt="conf_inicial_gnu_radio" src="https://github.com/user-attachments/assets/6fa7a3b6-02cc-4539-95d7-199eeac0a49e" />

<img width="1041" height="610" alt="ini_signal_spec_ana" src="https://github.com/user-attachments/assets/57a9291a-7df0-41a2-9052-5d8d09680ca6" />

De esta forma se registró una potencia de referencia de -12.23 dBm.

Posterior a ello, se realizó una segunda medición, en este caso con un cable con referencia RG58A, el cual se determinó que para esta primera toma el cable tenía una longitud de:

37170-37108=62 ft = 18.8976 m

![medicion_200MHz_cable1](https://github.com/user-attachments/assets/ea5260ce-c04a-47b6-bebe-4af11dadd222)

A su vez, tomando otro cable RG58 con una longitud de:

36968-37104= 136 ft = 41.4528 m

![medicion_200MHz_cable2](https://github.com/user-attachments/assets/ec7bfa87-22e7-44df-b752-958663ca25ac)


De esta forma, se realizaron distintas mediciones a distintas frecuencias con el objetivo de calcular las atenuaciones para estos dos cables. Las mediciones realizadas fueron a 100, 200, 300 y 400 MHz:

Para el cable 1, se registraron las siguiente mediciones


![medicion_100MHz_cable1](https://github.com/user-attachments/assets/8985ceb2-51f3-4fa3-8ecd-5eea385291cc)
Medición 100 MHz, cable 1

![medicion_200MHz_cable2](https://github.com/user-attachments/assets/71a39001-c1d6-460e-8548-0a5f6662a4aa)
Medición 200 MHz, cable 1

![medicion_300MHz_cable1](https://github.com/user-attachments/assets/a23bea9d-0d0c-4a7c-b913-7fa35978cd1a)
Medición 300 MHz, cable 1

![medicion_400MHz_cable1](https://github.com/user-attachments/assets/dc40c234-7177-4f6c-9d61-f2af9f7887ad)
Medición 400 MHz, cable 1


Y para el cable 2 se registraron las siguientes mediciones:


![medicion_100MHz_cable2](https://github.com/user-attachments/assets/54f5cfe4-f25d-4303-9095-27367023e13b)
Medición 100 MHz, cable 2

![medicion_200MHz_cable2](https://github.com/user-attachments/assets/81d3f86a-5265-4d43-b927-9bf58151ef1e)
Medición 200 MHz, cable 2

![medicion_300MHz_cable2](https://github.com/user-attachments/assets/ebf83af9-ac0a-4112-9062-ebadf29c128a)
Medición 300 MHz, cable 2

![medicion_400MHz_cable2](https://github.com/user-attachments/assets/99178dc1-98b9-4f90-90fc-bb453beb7179)
Medición 400 MHz, cable 2

De esta forma los resultados observados, junto con las atenuaciones calculadas se resumen en la siguiente tabla

| Cable  | Frecuencia (MHz) |P_in (dBm)| P_out (dBm)  | Atenuación (dB) |
|-----------|-----------|-----------|-----------|-----------|
| cable 1 |100 | -12.23 | -16.37 | 4.14 |
| cable 1 |200 | -12.23  |-18.06| 5.83 |
| cable 1 |300 | -12.23  | -19.63 | 7.4 |
| cable 1 | 400 | -12.23  |-21 | 8.77 |
| cable 2 | 100| -12.23  | -20.86 | 8.63 |
| cable 2 |200 | -12.23  | -24.81| 12.58 |
| cable 2 | 300 |-12.23  |-28.24 | 16.01 |
| cable 2 |400| -12.23 |-30.90 |18.67|

De esta forma calculando teóricamente las atenuaciones en base a la hoja de datos del fabricante del cable utilizado (RG58)

Para el cable 1 con una medición de 62 ft: Dada la hoja de datos, en base a la medición de 100 MHz, dice que tiene una atenuación de 4.3 dB/100ft, esto quiere decir, que para 62 ft, 62*(4.3/100) = 2.666 dB
Para la medición de 200 MHz: 62*(6.4/100)=3.968 dB

Y para el cable 2 con una medición de 136 ft: Siguiendo la base de datos, para la medición de 100 MHz: 136*(4.3/100)= 5.848 dB
Para la medición de 200 MHz: 136*(6.4/100) = 8.704 dB

Así, al observar los resultados obtenidos en la tabla, se puede observar que el cable que presenta una mayor atenuación es el cable 2, debido principalmente a que es más largo en comparación al cable 1, teniendo en cuenta que ambos son de la misma referencia (RG58)

Aparte de la longitud de los conductores, otros aspectos relacionados al mismo que también podrían ocasionar atenuaciones tan altas como las obtenidas en la práctica son principalmente fallas físicas en el conductor, como roturas o fatiga, deterioro del aislamiento, o debido también a malas conexiones. Estas razones también son una explicación a la diferencia en los valores obtenidos entre las atenuaciones calculadas debido a los valores experimentales, y las atenuaciones calculadas teóricamente.

### Conclusiones
Se pudo observar a partir de la práctica el efecto que tiene la atenuación en las señales de comunicaciones, como la calidad y el correcto funcionamiento de las líneas de transmisión si pueden marcar una gran diferencia al momento de transmitir señales, y a su vez analizar el reto al que se encuentran los sistemas de comunicaciones de grandes distancias para poder entregar y garantizar en su totalidad la integridad de un enlace de comunicaciones.
### Referencias
* Wikipedia contributors, “Attenuation,” Wikipedia, Aug. 01, 2025. https://en.wikipedia.org/wiki/Attenuation#cite_note-14  
* Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones y Universidad Industrial de Santander, “Communications I - Wireless transmission.”
* alldatasheet.com, “RG58-P PDF.” https://www.alldatasheet.com/datasheet-pdf/view/1025138/PASTERNACK/RG58-P.html
***








