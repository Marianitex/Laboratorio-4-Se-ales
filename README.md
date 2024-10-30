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

<a name="teorico"></a> 
## Fundamento teorico

Antes de iniciar la práctica, se realizo una investigación teórica de los siguientes temas:

### 1. **Actividad simpática y parasimpática del sistema nervioso autónomo**
   - **Sistema Nervioso Autónomo (SNA)**: El SNA regula funciones involuntarias como la frecuencia cardíaca, la digestión y la respiración.
   ![image](https://github.com/user-attachments/assets/277d8c0c-7e45-4618-ac94-de76c42777ae)
   Se divide en:
      - **Simpático**: Activa respuestas de "lucha o huida". Prepara al cuerpo para situaciones de estrés o emergencia, incrementando la frecuencia cardíaca, la presión arterial y la liberación de glucosa.
      - **Parasimpático**: Promueve el estado de "descanso y digestión", reduciendo la frecuencia cardíaca y facilitando funciones regenerativas.
   - **Balance entre simpático y parasimpático**: La interacción entre ambas actividades regula la homeostasis corporal. Estos sistemas actúan de manera complementaria para mantener el equilibrio fisiológico.

### 2. **Efecto de la actividad simpática y parasimpática en la frecuencia cardíaca**
   - **Efecto simpático**: Al activarse, el sistema simpático libera noradrenalina y epinefrina, que estimulan los receptores adrenérgicos del corazón, aumentando la frecuencia y la contractilidad cardíaca.
   - **Efecto parasimpático**: A través de la liberación de acetilcolina, el sistema parasimpático actúa sobre los receptores muscarínicos en el corazón, reduciendo la frecuencia cardíaca.
   - **Balance entre ambos efectos**: La variabilidad de la frecuencia cardíaca (HRV) refleja este balance, indicando el nivel de adaptabilidad del organismo. Cuando el sistema simpático domina, se observa un incremento en la frecuencia cardíaca, mientras que la activación parasimpática provoca su reducción.

### 3. **Variabilidad de la frecuencia cardiaca (HRV) y fluctuaciones en el intervalo R-R**
   - **Definición de HRV**: La HRV mide la variación temporal entre intervalos R-R consecutivos en un electrocardiograma (ECG). Es un indicador de la actividad autónoma sobre el corazón y de la capacidad de adaptación del sistema cardiovascular.
   - **Análisis en el dominio del tiempo y la frecuencia**: 
      - **Dominio del tiempo**: Se analizan métricas como la media de los intervalos R-R y su desviación estándar.
      - **Dominio de la frecuencia**: Incluye bandas de baja frecuencia (LF, 0.04-0.15 Hz) asociadas a la actividad simpática y bandas de alta frecuencia (HF, 0.15-0.4 Hz) relacionadas con el parasimpático.
   - **Importancia del análisis de HRV**: Permite evaluar el equilibrio autonómico. Altos valores de HRV reflejan una buena capacidad de adaptación del sistema cardiovascular, mientras que valores bajos pueden indicar estrés, enfermedad o desregulación autonómica.

### 4. **Transformada Wavelet: definición, usos y tipos de wavelet en señales biológicas**
   - **Definición**: La transformada wavelet es una herramienta de análisis que permite estudiar señales en función del tiempo y la frecuencia simultáneamente. A diferencia de la transformada de Fourier, que ofrece sólo información de frecuencia, la wavelet permite capturar variaciones temporales en las frecuencias de una señal.
   - **Usos en señales biológicas**: 
      - Análisis de señales ECG para identificar variaciones en la HRV.
      - Detección de cambios en la potencia espectral a lo largo del tiempo, útil en estudios de actividad autonómica.
   - **Tipos de wavelets comunes en biología**:
      - **Wavelet de Morlet**: Ofrece buena resolución en tiempo y frecuencia, útil para análisis de HRV.
      - **Wavelet de Daubechies**: Adecuada para capturar señales no estacionarias y variaciones rápidas, usada en la detección de picos y análisis de ECG.
   - **Selección de la wavelet**: La elección depende del tipo de señal y del análisis deseado. Las wavelets Morlet y Daubechies son comunes en biología por su precisión en señales fisiológicas complejas.

---

Estos temas te proporcionarán una base teórica sólida para realizar la práctica sobre variabilidad de la frecuencia cardíaca y su análisis usando la transformada wavelet.

<a name="diagrama"></a> 
## Diagrama de flujo


<a name="aadquisicion"></a> 
## Adquisicion de la señal

```c

```

<a name="librerias"></a> 
## Librerias

```c

```

<a name="filtros"></a> 
## Pre-procesamiento de la señal

```c

```

<a name="intervalos"></a> 
## Análisis de la HRV en el dominio del tiempo

```c

```

<a name="wavelet"></a> 
## Aplicación de transformada Wavelet

```c

```
<a name="menu"></a> 
## Menu

```c

```

<a name="contacto"></a> 
## Contacto
* Creado por [Marianitex](https://github.com/Marianitex) - sígueme en mis redes sociales como @_mariana.higuera
