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
