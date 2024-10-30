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
import numpy as np  # Importa la biblioteca NumPy para operaciones numéricas
import pandas as pd  # Importa la biblioteca Pandas para manipulación de datos
import scipy.signal as signal  # Importa la subbiblioteca de señales de SciPy para el procesamiento de señales
import pywt  # Importa PyWavelets para análisis de wavelets
import matplotlib.pyplot as plt  # Importa Matplotlib para la visualización de datos

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
        # Carga el archivo CSV, omitiendo la primera fila y nombrando las columnas
        ecg_data = pd.read_csv(filepath, skiprows=1, names=['Elapsed_time', 'ECG'], quotechar="'")
        
        # Convierte las columnas a tipo numérico, ignorando errores
        ecg_data['Elapsed_time'] = pd.to_numeric(ecg_data['Elapsed_time'], errors='coerce')
        ecg_data['ECG'] = pd.to_numeric(ecg_data['ECG'], errors='coerce')
        
        # Elimina las filas con valores NaN
        ecg_data.dropna(inplace=True)
        
        # Extender la señal para que dure al menos 5 minutos
        ecg_signal = np.tile(ecg_data['ECG'].values, (samples_target // len(ecg_data) + 1))[:samples_target]
        
        # Crea un nuevo DataFrame con el tiempo y la señal ECG
        ecg_data = pd.DataFrame({'Elapsed_time': np.arange(len(ecg_signal)) / fs, 'ECG': ecg_signal})
        
        return ecg_data  # Devuelve el DataFrame procesado
    except Exception as e:
        print("Error al cargar el archivo de ECG:", e)  # Maneja excepciones
        return None  # Retorna None si hay un error

# Función para graficar la señal cruda
def graficar_senal_cruda(ecg_signal):
    tiempo = np.arange(len(ecg_signal)) / fs  # Calcula el tiempo correspondiente a cada muestra
    plt.figure(figsize=(12, 4))  # Crea una figura para la gráfica
    plt.plot(tiempo, ecg_signal, label='Señal ECG cruda')  # Grafica la señal ECG
    plt.title("Señal ECG cruda")  # Título de la gráfica
    plt.xlim(0, 30)  # Limita el eje x a 30 segundos
    plt.xlabel("Tiempo (s)")  # Etiqueta del eje x
    plt.ylabel("Amplitud")  # Etiqueta del eje y
    plt.legend()  # Muestra la leyenda
    plt.show()  # Muestra la gráfica
```
![image](https://github.com/user-attachments/assets/c27c8e34-875c-4a06-87de-ab1273b6b2e1)

La señal mostrada es una señal ECG en estado crudo que se ha adquirido, al agregar el número 6 en el menú, se puede acceder a todas las características detalladas de la señal ECG, incluyendo la frecuencia de muestreo (250 Hz), el tiempo de muestreo (0.004 s), los niveles de cuantificación (914), y los estadísticos principales (media, desviación estándar, mínimo, máximo y mediana). Esta opción del menú permite visualizar fácilmente estos parámetros para una comprensión más clara de la señal y su calidad, lo cual es útil para verificar si los datos cumplen con los requisitos necesarios para el análisis posterior.

```c
# Calcular características de la señal
def calcular_caracteristicas(ecg_data):
    frecuencia_muestreo = fs  # Almacena la frecuencia de muestreo
    tiempo_muestreo = 1 / frecuencia_muestreo  # Calcula el tiempo de muestreo
    niveles_cuantificacion = len(np.unique(ecg_data['ECG'].round(3)))  # Niveles de cuantificación

    # Calcula estadísticos principales de la señal
    estadisticos = {
        'Media': np.mean(ecg_data['ECG']),
        'Desviación estándar': np.std(ecg_data['ECG']),
        'Mínimo': np.min(ecg_data['ECG']),
        'Máximo': np.max(ecg_data['ECG']),
        'Mediana': np.median(ecg_data['ECG'])
    }

    return frecuencia_muestreo, tiempo_muestreo, niveles_cuantificacion, estadisticos  # Retorna las características

```

### Características de la señal:
1. **Frecuencia de muestreo (250 Hz)**: La frecuencia de muestreo determina la cantidad de muestras que se toman por segundo. En este caso, 250 muestras por segundo son suficientes para capturar los picos y variaciones de la señal ECG, permitiendo observar el ciclo cardíaco de manera detallada.

2. **Tiempo de muestreo (0.004 s)**: El tiempo de muestreo, que es el inverso de la frecuencia de muestreo, indica el intervalo de tiempo entre cada muestra (4 milisegundos). Esto es importante porque define la resolución temporal de la señal.

3. **Niveles de cuantificación (914)**: La cuantificación es el número de niveles que el convertidor analógico-digital (ADC) utiliza para representar el valor de la señal. Con 914 niveles, se tiene una precisión suficiente para capturar la amplitud de la señal ECG sin pérdida significativa de información.

### Estadísticos principales de la señal:
- **Media (-0.022)**: La media indica el valor promedio de la señal. En este caso, la media es cercana a cero, lo cual es común en señales de ECG después de eliminar los posibles valores de offset de la señal.
- **Desviación estándar (0.169)**: La desviación estándar refleja la variabilidad de la señal alrededor de la media. Este valor indica que la señal tiene variaciones moderadas en torno a su valor promedio.
- **Mínimo (-0.500) y Máximo (1.129)**: Estos valores representan el rango de amplitud de la señal. El valor máximo corresponde a los picos R (los puntos más altos de la señal ECG), mientras que el mínimo puede indicar puntos bajos entre latidos.
- **Mediana (-0.043)**: La mediana es un valor que divide la señal en dos mitades, indicando que el 50% de las muestras están por encima de este valor y el otro 50% por debajo. Este valor también es cercano a cero, lo cual es típico en una señal ECG bien centrada.

### Análisis de la señal:
La señal ECG capturada muestra los picos característicos de una señal cardíaca, con los picos R claramente visibles en la gráfica. La media cercana a cero sugiere que la señal está centrada, lo cual facilita su análisis. La amplitud máxima de 1.129 y el mínimo de -0.500 indican que la señal tiene un buen rango de amplitud, permitiendo observar los diferentes componentes del ECG, como las ondas P, QRS, y T.

En conjunto, las características de la señal y sus estadísticos indican que es una señal bien adquirida y adecuada para su posterior procesamiento y análisis, como el cálculo de la variabilidad de la frecuencia cardíaca (HRV) y otros análisis de dominio de tiempo o frecuencia.

---
<a name="filtros"></a> 
## Pre-procesamiento de la señal

### Filtro Pasabajo
**Propósito**: Este filtro se utiliza para eliminar componentes de alta frecuencia de la señal ECG.

- **Por qué**: En la señal ECG, las frecuencias más altas pueden ser causadas por ruido o artefactos, como interferencias eléctricas o movimiento del paciente. Al aplicar un filtro pasabajo con un corte a 15 Hz, se preservan las frecuencias relevantes para el análisis de la HRV, que típicamente están en el rango de 0.04 a 0.4 Hz (frecuencia cardíaca en reposo) y se evitan ruidos que podrían interferir en la detección de los picos R.

### Filtro Notch
**Propósito**: El filtro notch se utiliza para eliminar un tono específico de frecuencia, en este caso, 55 Hz.

- **Por qué**: La frecuencia de 50-60 Hz a menudo corresponde al ruido de la red eléctrica y otros dispositivos electrónicos. Este tipo de interferencia puede distorsionar la señal ECG y afectar la precisión de los análisis posteriores. Al aplicar un filtro notch, se eliminan estos componentes indeseados sin alterar significativamente la información relevante de la señal ECG.

### Filtro Pasaalto
**Propósito**: El filtro pasaalto se utiliza para eliminar componentes de baja frecuencia.

- **Por qué**: Las frecuencias muy bajas en la señal ECG pueden incluir movimientos de la piel o drifts de la señal que no son representativos de la actividad eléctrica del corazón. Este filtro ayuda a mantener solo las frecuencias que son relevantes para el análisis de HRV, eliminando las variaciones de baja frecuencia que pueden oscurecer la información útil.

![image](https://github.com/user-attachments/assets/f466c9f2-90a2-40e6-853e-7dbbdd41ad02)


```c
# Función de filtrado de señal con filtro notch
def filtrar_senal(ecg_signal, fs):
    # Crea un filtro pasabajo
    sos_low = signal.butter(4, 15, 'low', fs=fs, output='sos')
    ecg_filtered = signal.sosfilt(sos_low, ecg_signal)  # Aplica el filtro

    # Configuración del filtro notch para eliminar ruido a 55 Hz
    notch_freq = 55.0
    quality_factor = 30.0
    b_notch, a_notch = signal.iirnotch(notch_freq / (fs / 2), quality_factor)
    ecg_filtered = signal.filtfilt(b_notch, a_notch, ecg_filtered)  # Aplica el filtro notch

    # Crea un filtro pasaalto
    sos_high = signal.butter(4, 0.5, 'high', fs=fs, output='sos')
    ecg_filtered = signal.sosfilt(sos_high, ecg_filtered)  # Aplica el filtro

    return ecg_filtered  # Retorna la señal filtrada
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
