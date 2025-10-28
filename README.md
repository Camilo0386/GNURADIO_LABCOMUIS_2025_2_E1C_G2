# Misión 7: Inteligencia artificial con GNURadio
### Integrantes
* Juan Esteban Herreño Novoa - 2210422
* Nelson Camilo Chaparro Nore - 2220386

Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones  
Universidad Industrial de Santander  
### Fecha
28 de octubre de 2025
***
## Declaración de Originalidad y Responsabilidad
Los autores de este informe certifican que el contenido aquí presentado es original y ha sido elaborado de manera independiente. Se han utilizado fuentes externas únicamente como referencia y han sido debidamente citadas.

Asimismo, los autores asumen plena responsabilidad por la información contenida en este documento.
***

## Contenido
### Resumen
En esta septima práctica de laboratorio, se hizo uso de la inteligencia artificial generativa, con el propósito de agilizar el proceso en la construcción del diagrama de bloques en GNURadio necesario para observar el efecto del ruido en las señales, e identificar sus principales características, tales como su potencia, su promedio y su desviación estándar. De esta forma, los resultados obtenidos correspondientes a distintas mediciones de ruido y una señal senoidal, fueron consignados en una tabla, donde se especificó la potencia, media y desviación estándar obtenidas tanto para el caso teórico como el obtenido experimentalmente.

**Palabra clave**: IA, LLM, Noise, GNURadio

### Procedimiento

<br>

**Primera fase** 

La primera fase consistió en la obtención de los códigos en Python para generar los bloques Embedded en GNURadio. De esta forma, se hizo uso de la inteligencia artificial, donde se le suministraron dos prompts con el objetivo de obtener los códigos respectivos.

El primero de ellos consistió en el codigo de estimador de potencia, donde se suministró exactamente el prompt sugerido como ejemplo: "Necesito el código para un bloque 'Embedded Python Block' de GNU Radio. El bloque debe tener una entrada (vector, tipo complex) y una salida (un solo ítem, tipo float). La función work debe calcular la potencia promedio de la ventana de entrada. La potencia se define como la media del cuadrado de la magnitud de las muestras. Asegúrese de importar la biblioteca numpy."

Para el segundo bloque, el cual correspondía a estadísticas de amplitud, se realizó el mismo procedimiento, suministrando el prompt dado como ejemplo: "Genere el código para un 'Embedded Python Block' de GNU Radio con una entrada (vector, tipo complex) y dos salidas (un solo ítem por salida, ambas tipo float). La salida out[0] debe ser la media de la magnitud de las muestras de entrada (calculada como numpy.mean(numpy.abs(in_sig[0]))). La salida out[1] debe ser la desviación estándar de la magnitud de esas mismas muestras."

El código generado para el primer bloque, denominado power_avg es el siguiente:

```python
import numpy as np
from gnuradio import gr

class blk(gr.sync_block):
    """
    Bloque Embedded Python para calcular la potencia promedio de una ventana (vector) de complejos.
    Entrada: vector de complex (configurar el 'Vector Length' en la interfaz del bloque)
    Salida: float (potencia promedio por ventana)
    """
    def __init__(self, vlen=1):
        # vlen: longitud del vector de entrada (configurar también en GRC)
        gr.sync_block.__init__(
            self,
            name="power_avg",
            in_sig=[(np.complex64, int(vlen))],
            out_sig=[np.float32]
        )

    def work(self, input_items, output_items):
        xin = input_items[0]   # para vector input: puede ser 1D (un vector) o 2D (varios vectores)
        # Si recibimos varios vectores a la vez, xin tendrá forma (n_vectors, vlen).
        if xin.ndim == 1:
            # un solo vector: devolver un float
            p = np.mean(np.abs(xin)**2)
            output_items[0][0] = np.float32(p)
            return 1
        else:
            # varios vectores: calcular potencia promedio por fila
            p = np.mean(np.abs(xin)**2, axis=1)
            # copiar resultados a la salida
            output_items[0][:len(p)] = p.astype(np.float32)
            return len(p)

```

De la misma forma, el código generado para el segundo bloque, denominado como mag_mean_std:

```python
import numpy as np
from gnuradio import gr

class blk(gr.sync_block):
    """
    Bloque Embedded Python que calcula:
      out[0]: media de la magnitud de las muestras de entrada
      out[1]: desviación estándar de la magnitud de las muestras de entrada

    Entrada: vector de complex (por ejemplo, longitud N)
    Salida: dos valores float (uno por vector de entrada)
    """
    def __init__(self, vlen=1):
        gr.sync_block.__init__(
            self,
            name="mag_mean_std",
            in_sig=[(np.complex64, int(vlen))],
            out_sig=[np.float32, np.float32]
        )
        self.vlen = vlen

    def work(self, input_items, output_items):
        xin = input_items[0]  # matriz de forma (n_vectors, vlen)
        mags = np.abs(xin)

        # Calcular media y desviación estándar de cada vector
        mean_vals = np.mean(mags, axis=1)
        std_vals = np.std(mags, axis=1)

        # Asignar a las salidas
        output_items[0][:len(mean_vals)] = mean_vals.astype(np.float32)
        output_items[1][:len(std_vals)] = std_vals.astype(np.float32)

        return len(mean_vals)

```

Como se puede observar, una revisión inicial permite determinar que el código es adecuado, importa correctamente las librerias necesarias como numpy y gnuradio, y define apropiadamente las variables de entradas y de salida respectivas para cada bloque.

**Segunda fase** 

En la segunda fase, se realizó la construcción del diagrama de bloques en GNURadio, importando los bloques embedded previamente creados. El diagrama de bloques resultante es el siguiente:

<img height="720" alt="img_prueba1_lab7" src="https://github.com/user-attachments/assets/40c2aaa6-17cc-4c2c-857e-40bd1f8b8306" />

<br> <br> 

Para que el sistema funcionara apropiadamente, fue necesario modificar el código `mag_mean_std` para que se comportara de forma sincrónica. De esta forma, se le ingresó esta petición a la herramienta ChatGPT para que generara nuevamente el codigo tomando en cuenta esas correcciones. De esta forma, el código obtenido fue el siguiente:

```python
import numpy as np
import math
from gnuradio import gr

def _is_power_of_two(n):
    return (n > 0) and ((n & (n - 1)) == 0)

def _next_power_of_two(n):
    if n <= 0:
        return 1
    return 1 << ((n - 1).bit_length())

class blk(gr.sync_block):
    """
    Bloque síncrono: entrada vector complex (longitud vlen)
    Salidas: out0 = mean(|x|), out1 = std(|x|)
    vlen se fuerza a potencia de 2 (si no lo es, se redondea hacia la siguiente potencia de 2).
    """
    def __init__(self, vlen=1024, force_next_pow2=True):
        # validar vlen y forzar potencia de 2 si corresponde
        vlen = int(vlen)
        if not _is_power_of_two(vlen):
            if force_next_pow2:
                new_vlen = _next_power_of_two(vlen)
                print("WARNING: vlen no es potencia de 2 ({}). Usando siguiente potencia: {}"
                      .format(vlen, new_vlen))
                vlen = new_vlen
            else:
                raise ValueError("vlen debe ser potencia de 2, recibió: {}".format(vlen))

        self.vlen = vlen

        gr.sync_block.__init__(
            self,
            name="mag_mean_std_pow2",
            in_sig=[(np.complex64, int(self.vlen))],
            out_sig=[np.float32, np.float32]
        )

    def work(self, input_items, output_items):
        xin = input_items[0]

        # Si no hay datos, no producir nada
        if xin is None or xin.size == 0:
            return 0

        # Asegurarnos de tener una matriz de forma (n_vectors, vlen)
        if xin.ndim == 2:
            # forma esperada: (n_vectors, vlen)
            if xin.shape[1] != self.vlen:
                # si no coincide, intentar reajustar si posible
                total = xin.size
                if total % self.vlen == 0:
                    xin = xin.reshape(-1, self.vlen)
                else:
                    # recortar sobrante para formar vectores completos
                    nvec = total // self.vlen
                    if nvec == 0:
                        return 0
                    xin = xin.reshape(-1)[:nvec * self.vlen].reshape(nvec, self.vlen)
        else:
            # xin es 1D (caso común cuando solo llega 1 vector o GRC pasa aplanado)
            total = xin.shape[0]
            if total < self.vlen:
                # no hay vector completo => esperar (descartar)
                return 0
            if total == self.vlen:
                xin = xin.reshape(1, self.vlen)
            else:
                # si viene un múltiplo de vlen, dividir en vectores
                if total % self.vlen == 0:
                    xin = xin.reshape(-1, self.vlen)
                else:
                    # recortar sobrante
                    nvec = total // self.vlen
                    if nvec == 0:
                        return 0
                    xin = xin[:nvec * self.vlen].reshape(nvec, self.vlen)

        # cálculo: magnitud, media y desviación estándar por vector
        mags = np.abs(xin)                # shape (n_vectors, vlen)
        mean_vals = np.mean(mags, axis=1)
        std_vals = np.std(mags, axis=1)

        n_out = len(mean_vals)
        # escribir salidas (asegurarse de no exceder el buffer de salida)
        output_items[0][:n_out] = mean_vals.astype(np.float32)
        output_items[1][:n_out] = std_vals.astype(np.float32)

        return n_out

```
<br>

Así, se continuó ejecutando este diagrama de flujo con las correciones realizadas, para el caso de cuando se tiene como entrada una fuente de ruido.

<img  height="720" alt="img2_prueba1_lab7" src="https://github.com/user-attachments/assets/e5b00bb0-a2e7-4ae7-bee5-54de79d8b13f" />

<br> 

Como se puede observar, la potencia, la media y la desviación estándar se comportan como valores estables. Al cambiar, para esta caso aumentando la amplitud de la fuente de ruido, se observó que tanto la potencia, como la media y la desviación estándar aumentaban.

<br>
<img  height="720" alt="img3_prueba1_lab7" src="https://github.com/user-attachments/assets/a3e0df5c-e081-4c85-9676-506ab74cf033" />
<br> <br>

Ahora, reemplazando la fuente por una señal senoidal de amplitud 1 y frecuencia 1[kHz], se obtuvo el siguiente diagrama de flujo:
<br> <br>
<img  height="720" alt="img_prueba2_lab7" src="https://github.com/user-attachments/assets/81542aed-1ec1-450d-9367-117d86527cd8" />
<br> <br>

Al ejecutar el diagram de flujo, se obtuvo lo siguientes valores de potencia, media y desviación estándar:

<br> <br>
<img  height="720" alt="img2_prueba2_lab7" src="https://github.com/user-attachments/assets/6bf39f14-b0b9-4b5f-8b57-951e8f9fb2f4" />

### Conclusiones

- El código con IA, no fue completamente correcto en el primer intento, dado que fue necesario realizar una pequeña corrección para el bloque que calculaba la media y la desviación estándar.
- El principal error de la IA, relacionado a este mismo bloque, fue no interpretar en un primer momento al código como sincrónico.
- Realizar este proceso utilizando la IA como asistente es muy eficiente comparado con escribir el código manualmente, dado que no es necesario consultar como integrar bloques de Python en GNURadio, ni consultar como se pueden usar las distintas funciones específicas de numpy al momento de realizar los cálculo estadísticos.
- Un estimador de potencia en tiempo real puede ser muy util, dado que en muchos sistemas y procesos es necesario medir la potencia recibida a cada instante, como por ejemplo, en las emisoras de radio u otros tipos de transmisión.
- La parte más compleja de la práctica fue solucionar los errores presentados al momento de intentar ejecutar el diagrama de flujo sin hacer las correcciones al bloque que calculaba la media y la desviación estándar. Luego de ello, se presentaron algunas dificultades al momento de interpretar los resultados obtenidos para el caso de la señal senoidal, en donde era necesario hacer el cálculo teorico respectivo.
