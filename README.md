# Laboratorio-4-Señales
>  Variabilidad de la Frecuencia Cardiaca usando la Transformada Wavelet 
---
Octubre 2024

## Tabla de contenidos
* [¿Qué se va a realizar?](#introduccion)
* [Fundamento teorico](#teorico)
* [Diagrama de flujo](#diagrama)
* [Adquisicion de la señal](#adquisicion)
* [Librerias](#librerias)
* [Pre-procesamiento de la señal](#filtros)
* [Análisis de la HRV en el dominio del tiempo](#intervalos)
* [Aplicación de transformada Wavelet](#wavelet)
* [Menu](#menu)
* [Contacto](#contacto)
---
<a name="introduccion"></a> 
## ¿Qué se va a realizar?

### a. **Adquisición de la Señal ECG**
1. **Seleccionar un Sujeto de Prueba:**
   - Elige una persona en reposo como sujeto de prueba para la medición.

2. **Configuración de la Medición:**
   - Usa un dispositivo de ECG para medir la señal del sujeto de prueba durante 5 minutos en estado de reposo.
   - Ajusta la frecuencia de muestreo (idealmente entre 500 Hz a 1 kHz) y los niveles de cuantificación adecuados para captar correctamente la señal.

3. **Reducción de Ruido:**
   - Minimiza las fuentes de ruido (movimiento, interferencias eléctricas, etc.) para garantizar la calidad de la señal registrada.

### b. **Pre-procesamiento de la Señal**
1. **Filtrado de Ruido:**
   - Aplica filtros digitales (como filtros paso-bajo o paso-alto) para eliminar el ruido de la señal ECG.
   - Documenta el diseño del filtro y los parámetros usados (frecuencia de corte, orden del filtro, etc.).

2. **Identificación de los Picos R:**
   - Usa un algoritmo de detección de picos para identificar los picos R en la señal ECG.
   - Calcula los intervalos R-R a partir de la distancia temporal entre picos R consecutivos.

### c. **Análisis de la HRV en el Dominio del Tiempo**
1. **Parámetros de HRV en el Dominio del Tiempo:**
   - Calcula la media de los intervalos R-R y su desviación estándar como medidas básicas de HRV.

2. **Análisis de los Parámetros:**
   - Realiza un análisis de los valores obtenidos en el dominio del tiempo para determinar patrones o variabilidad en los intervalos R-R.
  
### d. **Aplicación de la Transformada Wavelet**
1. **Generación del Espectrograma de HRV:**
   - Aplica la transformada Wavelet continua a la señal R-R para obtener un espectrograma de HRV.
   - Selecciona una función wavelet adecuada para señales biológicas (por ejemplo, Morlet o Daubechies) y ajusta el rango de frecuencias que te interese analizar (bandas de baja y alta frecuencia).

2. **Análisis de las Frecuencias en el Tiempo:**
   - Observa cómo cambian las frecuencias de HRV en el espectrograma y analiza cualquier variación en la potencia espectral.
   - Compara las diferencias entre la banda de baja frecuencia y la de alta frecuencia, describiendo cualquier patrón notable y los posibles efectos de la actividad simpática y parasimpática en estas frecuencias.
---
<a name="teorico"></a> 
## Fundamento teorico

Antes de iniciar la práctica, se realizo una investigación teórica de los siguientes temas:

### Actividad simpática y parasimpática del sistema nervioso autónomo
El **Sistema Nervioso Autónomo** se encarga de controlar automáticamente funciones importantes del cuerpo, como la respiración, los latidos del corazón y la digestión, sin que la persona tenga que pensarlo. Este sistema tiene dos partes principales:
- **Actividad simpática**: Es el sistema de “modo acción”. Se activa cuando el cuerpo necesita energía rápida para enfrentar algo, como en situaciones de estrés, miedo o ejercicio. Hace que el corazón lata más rápido y que el cuerpo esté listo para reaccionar.
- **Actividad parasimpática**: Es el sistema de “modo descanso”. Se activa cuando el cuerpo necesita relajarse y recuperar fuerzas, como al descansar después de comer o antes de dormir. Hace que el corazón lata más despacio y ayuda en procesos como la digestión.

Estas dos partes trabajan juntas y se equilibran según lo que el cuerpo necesite en cada momento.

### Efecto de la actividad simpática y parasimpática en la frecuencia cardíaca
La **frecuencia cardíaca** es la velocidad a la que late el corazón. La actividad simpática y la parasimpática afectan esta frecuencia de diferentes maneras:
- **Actividad simpática**: Aumenta la frecuencia cardíaca. Esto es útil cuando la persona necesita estar alerta o reaccionar rápidamente.
- **Actividad parasimpática**: Reduce la frecuencia cardíaca, ayudando al cuerpo a descansar y recuperarse.

Cuando estos dos sistemas funcionan bien juntos, mantienen la frecuencia cardíaca en un rango saludable que varía según las necesidades del cuerpo en cada situación.

### Variabilidad de la frecuencia cardíaca (HRV)
La **variabilidad de la frecuencia cardíaca (HRV)** mide los cambios en el tiempo que pasa entre cada latido del corazón. Esta variabilidad se observa en los intervalos R-R, que son los tiempos entre los picos más altos de cada latido en un electrocardiograma (ECG). 
- **¿Por qué es importante?** La HRV muestra el equilibrio entre los sistemas simpático y parasimpático. Por ejemplo, una buena variabilidad indica que el cuerpo puede adaptarse bien a diferentes situaciones, mientras que una baja variabilidad podría señalar que el cuerpo está bajo mucho estrés o no se adapta bien a los cambios.
- **Frecuencias de interés**: En el análisis de HRV, hay dos tipos de frecuencias importantes:
   - **Baja frecuencia (LF)**: Relacionada con la actividad simpática.
   - **Alta frecuencia (HF)**: Relacionada con la actividad parasimpática.

Estas frecuencias ayudan a entender cómo están funcionando los sistemas simpático y parasimpático en el cuerpo.

### Transformada Wavelet: definición, usos y tipos de wavelet en señales biológicas
La **transformada wavelet** es una técnica matemática que permite analizar cómo cambia una señal en el tiempo y en la frecuencia al mismo tiempo. Es especialmente útil para estudiar señales complejas, como las del cuerpo, que varían rápidamente.
- **¿Qué hace?** Permite observar detalles en diferentes momentos de una señal (como un ECG) y ver cómo cambia a lo largo del tiempo.
- **Usos en biología**: En el análisis de señales biológicas, la transformada wavelet permite identificar patrones y cambios que pueden ser muy pequeños o rápidos, como variaciones en los latidos del corazón.
- **Tipos de wavelet**:
   - **Wavelet de Morlet**: Ofrece una buena resolución tanto en tiempo como en frecuencia y es útil en el análisis de señales biológicas.
   - **Wavelet de Daubechies**: Permite captar variaciones rápidas y ayuda en la detección de picos en señales como el ECG.

La transformada wavelet es una herramienta poderosa para entender mejor cómo el cuerpo cambia y reacciona en diferentes situaciones.
---
<a name="diagrama"></a> 
## Diagrama de flujo
Este diagrma representa el plan de acción para cumplir el objetivo de la práctica:



---
<a name="librerias"></a> 
## Librerias

```c
import numpy as np
import pandas as pd
import scipy.signal as signal
import pywt
import matplotlib.pyplot as plt
```
### 1. `import numpy as np`

**NumPy** es una librería fundamental para el trabajo con datos numéricos y operaciones matemáticas en Python. Se utiliza para crear y manipular arreglos de datos numéricos (vectores y matrices), lo cual es clave en el procesamiento de señales. NumPy permite:
   - Almacenar los datos de la señal ECG en arreglos y realizar cálculos rápidamente.
   - Calcular promedios, desviaciones estándar y otros estadísticos necesarios para el análisis de la variabilidad de la frecuencia cardíaca (HRV).
   - Realizar operaciones matemáticas avanzadas, como la generación de secuencias de tiempo para graficar y analizar los datos de ECG.
### 2. `import pandas as pd`

**Pandas** es una librería para el manejo y análisis de datos en estructuras llamadas DataFrames. En esta práctica, Pandas facilita:
   - Leer y almacenar los datos de la señal ECG en un archivo **Excel** (o CSV) para manipularlos y analizarlos fácilmente.
   - Organizar los datos en una tabla intuitiva donde cada fila representa una muestra de la señal ECG y cada columna puede ser un atributo como el tiempo o el valor de la señal.
   - Manipular grandes cantidades de datos, aplicar filtros y realizar análisis estadísticos.
### 3. `import scipy.signal as signal`

**SciPy** es una librería de Python para aplicaciones científicas, y su módulo `signal` incluye herramientas específicas para el procesamiento de señales. En el análisis de la señal ECG, `scipy.signal` es útil para:
   - Aplicar filtros digitales que eliminan el ruido de la señal ECG y ayudan a obtener una señal más clara.
   - Detectar picos en la señal, como los picos R, que son necesarios para calcular los intervalos R-R.
   - Realizar transformaciones y análisis en el dominio de la frecuencia, útil para entender características de la HRV.
### 4. `import pywt`

**PyWavelets** permite aplicar **transformadas wavelet**, una técnica que descompone una señal en componentes de frecuencia y tiempo. En esta práctica, `pywt` se emplea para:
   - Aplicar una transformada wavelet continua a la señal ECG, lo cual permite analizar la HRV en tiempo y frecuencia.
   - Seleccionar diferentes tipos de wavelets, como la **wavelet de Morlet**, que es adecuada para señales biológicas.
   - Obtener un espectrograma que muestra cómo cambian las frecuencias a lo largo del tiempo, facilitando la observación de las bandas de baja y alta frecuencia.
### 5. `import matplotlib.pyplot as plt`

**Matplotlib** es una librería para la visualización de datos en gráficos. En esta práctica, `matplotlib.pyplot` se usa para:
   - Graficar la señal ECG en función del tiempo, lo cual facilita la identificación de picos y patrones.
   - Visualizar los resultados del análisis de HRV, como los intervalos R-R y la variabilidad a lo largo del tiempo.
   - Crear espectrogramas a partir de la transformada wavelet para observar las variaciones de frecuencia en el tiempo.
---
<a name="aadquisicion"></a> 
## Adquisicion de la señal

Para la adquisición de la señal ECG (electrocardiograma) usando un microcontrolador **STM32** y un módulo **AD8232**, el proceso se estructura en varios pasos para obtener una señal clara, almacenarla en **Excel** y luego analizarla en **Python**. La configuración específica de la señal incluye una **frecuencia de muestreo de 250 Hz**, lo que corresponde a un **tiempo de muestreo de 0.004 segundos** y **914 niveles de cuantificación** para captar con precisión las variaciones de la señal ECG.

El primer paso consiste en conectar el módulo AD8232 al STM32. El AD8232 es un sensor que mide la actividad eléctrica del corazón de manera segura y precisa. Esta conexión se realiza mediante cables, de forma que las salidas de datos del AD8232 queden enlazadas a los pines de entrada analógica del STM32, que recibirá la señal ECG.

![Imagen de WhatsApp 2024-10-30 a las 17 23 17_e598c08d](https://github.com/user-attachments/assets/622b380d-96c5-42ef-b14e-729c3d699edd)

Luego, es necesario configurar el STM32 para que lea la señal proveniente del AD8232. Esto implica programar el puerto de entrada analógica del STM32 para que procese la señal de voltaje del módulo, representando la actividad del corazón. Además, se define la frecuencia de muestreo de 250 Hz y el tiempo de muestreo de 0.004 segundos, que garantiza una captura precisa de la señal ECG. También se configura el STM32 para procesar la señal de entrada, minimizando la interferencia o ruido antes de almacenar los datos.

Para asegurar la calidad de la señal, se deben tomar medidas para reducir el ruido durante la captura. Esto incluye el uso de cables cortos, evitar movimientos durante la medición y realizar el registro en un ambiente con baja interferencia eléctrica. La persona debe permanecer en **reposo** durante los **5 minutos** de grabación para obtener una señal estable y clara.

El almacenamiento de datos es el siguiente paso. El STM32 procesa la señal y la envía a una computadora mediante una conexión serial (como **UART** o **USB**), lo cual permite la transmisión de la señal desde el STM32 a la computadora. En la computadora, un programa (como en **Python** o con software del STM32) captura los datos y los guarda en un archivo **Excel** para facilitar su posterior análisis. Para visualizar esta señal en el sistema de adquisición, se puede acceder a través del menú introduciendo el número "1".

![Imagen de WhatsApp 2024-10-30 a las 17 23 17_952178e8](https://github.com/user-attachments/assets/cd8ccf8f-18ff-4b51-b109-38af0b5427bf)


En Excel, los datos se organizan en filas, donde cada una representa una lectura de la señal ECG en el tiempo. La primera columna puede corresponder al **tiempo**, y la segunda columna, al **valor de voltaje** de cada muestra de ECG. Esta organización facilita la carga y el análisis en **Python**.

Es importante mencionar que no se registra ninguna información personal del sujeto de prueba. Solo se almacenan los datos de la señal ECG sin asociarlos a ninguna identificación para garantizar la **confidencialidad** y proteger la **privacidad** del participante.

Una vez que los datos están en Excel, se pueden importar a Python para realizar el análisis de la señal ECG. Python permite el procesamiento de la señal, la identificación de los picos R y el cálculo de los intervalos R-R, aspectos claves para el análisis de la variabilidad de la frecuencia cardíaca (HRV).

```c
# Parámetros de simulación
fs = 250  # Frecuencia de muestreo en Hz
duration_target = 5 * 60  # Duración objetivo en segundos (5 minutos)
samples_target = duration_target * fs  # Número de muestras objetivo

# Función para cargar y procesar el archivo CSV de ECG
def cargar_datos_ecg(filepath):
    try:
        ecg_data = pd.read_csv(filepath, skiprows=1, names=['Elapsed_time', 'ECG'], quotechar="'")
        ecg_data['Elapsed_time'] = pd.to_numeric(ecg_data['Elapsed_time'], errors='coerce')
        ecg_data['ECG'] = pd.to_numeric(ecg_data['ECG'], errors='coerce')
        ecg_data.dropna(inplace=True)
        
        # Extender la señal para que dure al menos 5 minutos
        ecg_signal = np.tile(ecg_data['ECG'].values, (samples_target // len(ecg_data) + 1))[:samples_target]
        ecg_data = pd.DataFrame({'Elapsed_time': np.arange(len(ecg_signal)) / fs, 'ECG': ecg_signal})
        
        return ecg_data
    except Exception as e:
        print("Error al cargar el archivo de ECG:", e)
        return None

# Función para graficar señal cruda
def graficar_senal_cruda(ecg_signal):
    tiempo = np.arange(len(ecg_signal)) / fs
    plt.figure(figsize=(12, 4))
    plt.plot(tiempo, ecg_signal, label='Señal ECG cruda')
    plt.title("Señal ECG cruda")
    plt.xlim(0,30)
    plt.xlabel("Tiempo (s)")
    plt.ylabel("Amplitud")
    plt.legend()
    plt.show()
```
---
<a name="filtros"></a> 
## Pre-procesamiento de la señal

```c

```

<a name="intervalos"></a> 
## Análisis de la HRV en el dominio del tiempo

```c

```
---
<a name="wavelet"></a> 
## Aplicación de transformada Wavelet

```c

```
---
<a name="menu"></a> 
## Menu

```c

```
---
<a name="contacto"></a> 
## Contacto
* Creado por [Marianitex](https://github.com/Marianitex) - sígueme en mis redes sociales como @_mariana.higuera
