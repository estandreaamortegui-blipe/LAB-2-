# LAB-2-
# Convolución, correlación y transformada de Fourier

## Asignatura

Procesamiento Digital de Señales

## Programa

Ingeniería Biomédica – Universidad Militar Nueva Granada

## Práctica de laboratorio

**Convolución, correlación y transformada de Fourier**

## Integrantes

Andrea Carolina Amórtegui Carrillo – Código 5600963


---

## Descripción
El laboratorio se divide en tres secciones principales. En la primera parte se analiza la convolución entre dos señales discretas, lo cual permite estudiar el comportamiento de sistemas lineales e invariantes en el tiempo. En la segunda parte se calcula la correlación cruzada entre dos señales sinusoidales, herramienta utilizada para determinar similitudes y desplazamientos temporales entre señales. Finalmente, en la tercera parte se realiza el análisis estadístico y espectral de una señal biomédica EOG, adquirida previamente mediante un sistema de adquisición de datos.

Durante el desarrollo se implementan técnicas fundamentales del procesamiento digital de señales, tales como análisis estadístico, transformada rápida de Fourier (FFT) y cálculo de la densidad espectral de potencia (PSD)

---


## Metodología

El desarrollo del laboratorio se dividió en tres partes principales. En cada etapa se emplearon herramientas de programación en Python para el procesamiento y análisis de las señales biomédicas.

En primer lugar, se realizo una convolución teniendo en cuenta las señales dadas en la guía de laboratiorio, seguido a esto se correlacionaron dos señales y finalmente con ayuda del generador de señales se aplico la transformada de fourier.

---

## Explicación del código

En esta sección se explica el funcionamiento del código donde se reconoce la importancia de la aplicación de convolución y correlación en el área.

### Importación de librerías

Primero se importan las librerías necesarias para la lectura y el procesamiento de los calculos deseados:
* `nidaqmx`:Se utiliza para adquirir señales desde una tarjeta de adquisición de datos (DAQ).
* `numpy`: facilita el manejo de arreglos y operaciones numéricas.
* `matplotlib.pyplot`: se emplea para generar gráficos y sus analisis.
* `os`: Permite gestionar rutas de archivos en el sistema operativo.

Estas herramientas son fundamentales para el análisis de señales biomédicas en Python.

<p align="center">
<img width="1171" height="1600" alt="image" src="https://github.com/user-attachments/assets/ee68f36e-d8f0-44db-b6f9-e58095695041" />
</p>
<p align="center">
  <em>Diagrama de flujo del codigo</em></p


---

### Parte A
Se definieron dos señales discretas:

x[n]=[5,6,0,0,9,6,3,1,1,1,8,8,2,1,6,9,7]

y[n]=[1,1,1,8,8,2,1,6,9,7,5,6,0,0,9,6,3] 

La convolución entre ambas señales se calcula mediante:
```python
y_python = np.convolve(x, h, mode='full')
```
Esta permite visualizar como el sistema representado por h(n) modifica la señal de entrada x(n). 
Tambien se realuzo la convolucion a mano donde se utilizo el metodo mas sencillo por medio de tablas, como se muestra en la imagen:

<p align="center">
<img width="899" height="730" alt="image" src="https://github.com/user-attachments/assets/a67f41a6-e195-4da8-a9e8-eac907ba972d" />

</p>
<p align="center">
  <em>CGráfica X(n)</em></p



<p align="center">
<img width="900" height="725" alt="image" src="https://github.com/user-attachments/assets/85fc7918-23df-4cf3-a9f4-641533ca3891" />
</p>
<p align="center">
  <em>Gráfica H(n)</em></p



  <p align="center">
<img width="725" height="889" alt="image" src="https://github.com/user-attachments/assets/82706218-1426-4bb1-ad1f-ff9afba33a46" />
</p>
<p align="center">
  <em>Convolución a mano</em></p



  <p align="center">
<img width="1100" height="959" alt="image" src="https://github.com/user-attachments/assets/b18cffd4-eb49-4088-ba8c-4c13b52a09ff" />
</p>
<p align="center">
  <em>Gráfica y(n)</em></p


Para verificar el resultado obtenido manualmente, se implemento el cálculo d la convolución en Python. En este caso se uso la función * `numpy.convolve()`, y esta también nos permitió observar gráficamente el comportamiento de las señales.

### Representación gráfica de las señales

Las señales fueron representadas utilizando gráficos discretos tipo stem, los cuales permiten visualizar claramente kis vakires de cada muestra en el tiempo discreto.

A partir de estas gráficas se puede observar cómo la señal de salida y(n) corresponde al efecto ue porduce la respuesta al impulso h(n) sobre la señal de entrada x(n).
<p align="center">
<img width="1300" height="646" alt="image" src="https://github.com/user-attachments/assets/09fffd32-fd22-4615-af7f-f8d17dda0c57" />
</p>
<p align="center">
  <em>Gráfica x(n)</em></p>

  <p align="center">
<img width="1301" height="654" alt="image" src="https://github.com/user-attachments/assets/4e986b16-c054-469f-8b43-9ec956a47b16" />

</p>
<p align="center">
  <em>Gráfica h(n)</em>
</p>

---

### Resultado parte A

La convolución representa el comportamiento de un sistema lineal e invariante en el tiempo. En este caso, la señal resultante y(n) descrive cómo el sistema modifica la señal de entrada de acuerdo con su respuesta impulso.
<p align="center">
<img width="1305" height="548" alt="image" src="https://github.com/user-attachments/assets/15033aba-d145-4c19-adac-0efc158bb2a6" />
</p>
<p align="center">
  <em>Gráfica y(n)</em>
</p>

---

### Parte B

En esta parte se analizan dos señales discretan generadas a partir de funciones trigonométricas. La primera señal está definida como:
<p align="center">
  <em>x1​[nTs​]=cos(2π100nTs)</em>
</p>
y la segunda señal como:
<p align="center">
  <em>x2​[nTs​]=sin(2π100nTs​)</em>
</p>

Donde Ts= 1.25ms que corresponde al periodo de muestro y el índice n toma valores entre 0 y 9.

Estas señales representan versiones discretizadas de una señal cosenoidal y una señal senoidal con la misma frecuenci. Debido a que el seno y el coseno estan desfasados 90°, se espera que exista un relacion entre ambas señales que puede analizarse mediante la correlación cruzada.

Las figuras muestran la representación gráfica de las secuencias discretas X1(n) y X2(n), donde cada punto representa una muestra de la señal en el instante n.
<p align="center">
 <img width="836" height="637" alt="image" src="https://github.com/user-attachments/assets/49a10ebd-4217-49eb-827e-599c86e427ce" />
</p>
<p align="center">
  <em>Gráfica X1(n)</em>
</p>

<p align="center">
<img width="842" height="626" alt="image" src="https://github.com/user-attachments/assets/508e965d-9a36-4b0e-9012-5ea85759d969" />
</p>
<p align="center">
  <em>Gráfica X2(n)</em>
</p>
​
---

### Representación gráfica de correlación cruzada

La correlación cruzada mide el grado de similitud entre dos señales cuando una de ellas se desplaza en el tiempo.

En la graica obtenida se representa el valor de la correlación para distintos desplazamientos positivos y negativos. Cada punto indica cuánto se parecen las señales cuando una de ellas se desplaza cierta cantidad de muestras respecto a la otra.

<p align="center">
<img width="830" height="626" alt="image" src="https://github.com/user-attachments/assets/e36494d2-6387-4e15-9fcc-a4741fdf3810" />
</p>
<p align="center">
  <em>Gráfica de correlación entre X1(n) y X2(n)</em>
</p>

En la figura de correlación cruzada se observan valores positivos y negativos, lo cual indica que dependiendo del desplazamiento kas señales pueden estar en fase.

El valor máximo de correlación indica el desplazamiento en el cual las señales representan mayor similitud.

---

### ¿En qué situaciones es útil la correlación cruzada?

Es una herramienta que es utilizada para analizar la relacion entre dos señales mediante aplicaciones como la detección de retrasos temporales en sistemas de comunicación, localización de fuentes sonoras y análisis bimédica; el reconocimiento de vox y detección de señales en entornos ruidosos; y el procesamiento de señales biomédicas coo ECG, EMG para comparar patrones y detectar similitudes entre registros.

---
### Parte C 

En esta sección se trabja con una señal adquirida por el generador de señales biologicas. Donde se analizan sus características tanto del tiempo como el dominio de la frecuencia.

Para esto. primero se determina la frecuencia de Nyquist de la señal generada, posteriormente se digitaliza utilizando un frecuencia de muestreo afecuada y se analizan diferentes parámetros estadísticos y espectrales de la señal.

---

### Frecuencia de Nyquist
La frecuencia de Nyquist corresponde a la mitad de la frecuencia de muestreo y representa la máxima frecuencia que puede representarse correctamente sin que ocurra aliasing.

En esta practica se utilizó una frecuencia de muestreo equivalente a cuatro veces la frecuencia de Nyquist, lo que garantiza que la señal pueda digitalizarse adecuadamente y evita problemas de aliasing.
```python
nyquist=fs/2
print("Frecuencia de Nyquist: ",nyquist, "Hz")
frecuencian= 4*nyquist
print("Frecuencia digitalizada: ",frecuencian, "Hz")
factor = int(frecuencian / fs)
if factor< 1:
    factor= 1


```

---

### Digitalización de la señal
La señal biológica generada fue adquirida mediante el microcontrolador DAQ y convertida en una señal digital mediante un proceso de muestreo.

Durante este proceso:

1. La señal analógica es capturada por el sistema DAQ.

2. Se toman muestras en intervalos definidos por el período de muestreo.

3. Estas muestras se almacenan como valores discretos que representan la señal digital.

Este proceso permite que la señal pueda ser procesada posteriormente utilizando herramientas computacionales como Python.

Una vez digitalizada la señal, se calcularon diferentes estadísticos descriptivos para analizar su comportamiento en el dominio del tiempo.

Media

La media representa el valor promedio de la señal, este valor permite identificar si la señal presenta un desplazamiento respecto a cero o si está centrada alrededor del eje horizontal.

Mediana

La mediana corresponde al valor central de los datos cuando estos se ordenan de menor a mayor.

Este estadístico es útil porque no se ve afectado por valores extremos o ruido presente en la señal.

Desviación estándar

La desviación estándar mide qué tanto se dispersan los valores de la señal alrededor de la media. Un valor alto de desviación estándar indica que la señal presenta mayor variabilidad o fluctuaciones.

Valor máximo y mínimo

Estos valores permiten identificar como amplitud máxima de la señal y amplitud mínima de la señal. Lo cual es importante para conocer el rango dinámico de la señal biológica.

```python
media = np.mean(senal)
mediana = np.median(senal)
desv = np.std(senal)
maximo = np.max(senal)
minimo = np.min(senal)

```

---

### Clasificación de la señal

La señal EOG se clasifica como análogica en su origen, digitalizada para su procesamiento, aleatoria y aperiódica ya que, es análogica en origen porque el generador produce una tensión eléctrica continua variable en el timpo, pero al ser adquirida con la DAQ y muestreada a una frecuencia de 300 Hz, se convierte en una señal digital discreta; es aleatoia debido a su alta variabilidd en valores, la imposibilidad de predecir los movimientos oculares exactos simulados y la presencia de ruido fisiológico y de medición del sistema de adquisición, y por ultimo es aperiodica porque su frecuencia es continua, no presenta un perioso fundamental constante y los movimientos oculares ocurren en momentos aleatorios,sin seguir un patron.


<p align="center">
<img width="1018" height="429" alt="image" src="https://github.com/user-attachments/assets/dd764fcd-b49d-4c72-8f2d-b3838bb1722e" />

</p>

<p align="center">
  <em>Señal EOG</em>
</p

---

### Transformada de Fourier

La FFT permite descomponer la señal en las diferentes frecuencias que la componen.

El resultado de la FFT muestra qué frecuencias están presentes en la señal y con qué intensidad.

En la gráfica obtenida se observa la magnitud del espectro de frecuencias, lo que permite identificar los componentes dominantes de la señal.


<p align="center">
<img width="1003" height="427" alt="image" src="https://github.com/user-attachments/assets/21d81451-fb71-4d63-a956-ebebefc08ebf" />

</p>

<p align="center">
  <em>Transformada Fourier</em>
</p

---

### Densidad espectral de potencia (PSD)
La densidad espectral de potencia describe cómo se distribuye la potencia de la señal a lo largo de las diferentes frecuencias. La PSD permite identificar en qué frecuencias se concentra la mayor energía de la señal, lo cual es muy útil en el análisis de señales biológicas.

---

### Estadísticos en el dominio de la frecuencia

Además del análisis espectral, se calcularon algunos estadísticos sobre las frecuencias obtenidas.

Frecuencia media

Representa el valor promedio de las frecuencias presentes en el espectro.

Frecuencia mediana

Corresponde al valor central dentro del conjunto de frecuencias analizadas.

Desviación estándar de las frecuencias

Mide la dispersión de las frecuencias alrededor del promedio.

Esto permite analizar qué tan concentradas o dispersas están las componentes espectrales.

```python
print("\nEstadísticos en el dominio de la frecuencia:")
freq_media = np.sum(frecuencias * magnitud) / np.sum(magnitud)
magnitud_acum = np.cumsum(magnitud) / np.sum(magnitud)
freq_mediana = frecuencias[np.where(magnitud_acum >= 0.5)[0][0]]
freq_std = np.sqrt(np.sum(((frecuencias - freq_media)**2) * magnitud) / np.sum(magnitud))

```

Histograma de frecuencias

El histograma permite visualizar cómo se distribuyen las frecuencias presentes en la señal.

Cada barra representa la cantidad de frecuencias dentro de un intervalo determinado.

Este tipo de representación es útil para identificar zonas del espectro donde se concentra mayor cantidad de componentes frecuenciales.

<p align="center">
<img width="1003" height="423" alt="image" src="https://github.com/user-attachments/assets/dfc3ec7b-ad21-4d21-915f-2d8bcf921d6c" />


</p>

<p align="center">
  <em>Histograma de frecuencias</em>
</p


  ---
  

### Analisis de resultados y preguntas 

En el laboratorio se exploraron diferentes herramientas con el objetivo de comprender su comportamiento en el tiempo y la frecuencia. A partir de la convoluvión de dos secuencias discretas se pudo observar cómo la interacción entre una señal de entrada y la respuesta de un sistema genera una nueva señal, lo que resultó veridico al comparar el cálculo manual con el obtenido mediante herramientas computacionales. 

Se abordó la correlación cruzada entre dos señales sinusoidales desfasada, lo que permitió cuantificar su similitud en función del desplazamiento relativo. Los resultados reflejaron que, debido a la diferencia de fase de 90 grados entre el seno y el coseno, la máxima correlación no se alcanza en el desplazamiento cero, sino en aquellos puntos donde las señales se alinean mejor. Es importante la diferencia conceptual entre correlación cruzada y convolución: mientras que la convolución implica una inversión temporal de una de las señales y se utiliza para describir la salida de sistemas lineales, la correlación cruzada mide la similitud sin inversión; la convolución se usa para aplicar filtros a las imágenes, por ejemplo para suavizar la imagen o resaltar los bordes. Por otro lado, la correlación cruzada se utiliza para comparar una imagen con un patrón conocido y así encontrar regiones que se parezcan a ese patrón.

La Transformada Rápida de Fourier, aplicada a una señal de electrooculografía adquirida con un sistema de adquisición de datos. El análisis frecuencial permitió descomponer la señal en sus componentes espectrales y visualizar cómo se distribuye su energía a través de la densidad espectral de potencia. Complementariamente, se calcularon estadísticos en frecuencia como la frecuencia media, la mediana y la desviación estándar, que aportaron una caracterización cuantitativa del contenido espectral. Este enfoque resultó clave para identificar las frecuencias predominantes en la señal biomédica y para comprender su comportamiento oscilatorio. La transformada de Fourier ofrece un conjunto de características con mayor poder discriminativo que el dominio temporal en contextos donde la información relevante reside en la composición frecuencial, ya que permite distinguir patrones espectrales que no son evidentes en la evolución temporal de la señal.

Tanto la convolución como la correlación son importantes en el procesamiento digital por su capacidad para modelar sistemas lineales y medir similitudes entre señales. Sin embargo, su aplicación en entornos reales enfrenta desafíos derivados de la naturaleza no estacionaria y no lineal de las bioseñales, así como de la presencia inevitable de ruido y artefactos, que pueden distorsionar los resultados y exigir técnicas de preprocesamiento adicionales. 

La Transformada de Fourier ofrece una ventaja al contenido frecuencial de las señales, pero su uso en aplicaciones de tiempo real se ve condicionado por la necesidad de procesar bloques completos de datos, lo que produce retrasos y dificulta el seguimiento de cambios rápidos en la señal. La pérdida de información temporal inherente a la transformada global y los artefactos de borde derivados del enventanado son aspectos que deben gestionarse cuidadosamente, especialmente en entornos clínicos donde la respuesta inmediata es crítica. A pesar de estas limitaciones, la combinación de estas herramientas con técnicas como la transformada de Fourier de tiempo corto o filtros adaptativos permite extender su utilidad, logrando un equilibrio entre resolución espectral y capacidad de respuesta temporal.

---


---
### Conclusiones

- La convolución permitió verificar experimentalmente la respuesta de un sistema discreto, confirmando que la señal obenida mediante el calculo manual coincide con la generada a través de Python. esto valida la implementación computaciomal de la convolución como herramienta para modelar sistemas nvariantes en el tiempo.
- La correlación cruzada demostró ser eficaz para cuantificar la similitud entre señales en función del desplazamiento temporal, evidenciado en el análisis del seno y coseno desfasados 90°, donde el máximo de correlación no ocurre en el desplazamiento cero sino cuando ambas señales se alinean mejor.
- El análisis en tiempo y frecuencia de la señal EOG permitió caracterizar su comportamiento estadístico y espectral, obteniendo parámetros descriptivos como media, mediana, desviación estándar, frecuencia media y densidad espectral de potencia. Estos indicadores proporcionan una visión integral de la señal, revelando que las señales biomédicas presentan una distribución de energía en un rango continuo de frecuencias y una variabilidad significativa, lo que confirma su naturaleza aleatoria y aperiódica.
- La Transformada de Fourier demostró su utilidad para identificar el contenido frecuencial de la señal biomédica, permitiendo visualizar cómo se distribuye la energía en las diferentes bandas de frecuencia. Sin embargo, su aplicación en tiempo real presenta limitaciones importantes como la necesidad de trabajar con bloques completos de datos.

---
### Referencias 
 A. V. Oppenheim, A. S. Willsky y S. H. Nawab, Signals and systems. Upper
Saddle River, NJ, USA: Pearson Educación, 1997.

S. K. Jena, “Convolution, cross-correlation, and stochastic analysis,” en
Fourier, Laplace, and the Tangled Love Affair with Transforms: The Art of
Signal Synthesis and Analysis, Cham, Switzerland: Springer Nature
Switzerland, 2025, pp. 275-363. https://doi.org/10.1007/978-3-031-80165-
5_8.

W. T. Rhodes, “Acousto-optic signal processing: convolution and
correlation,” Proceedings of the IEEE, vol. 69, no. 1, pp. 65-79, 2005.
https://doi.org/10.1109/JPROC.1981.11946.
Z. He, Y. Fan, J. Zhuang, Y. Dong y H. Bai, “Correlation filters with weighted
convolution responses,” en Proceedings of the IEEE International
Conference on Computer Vision Workshops, Venice, Italy, 22-29 Oct. 2017,
pp. 1992-2000. https://doi.org/10.1109/ICCVW.2017.234. 


Sörnmo, L., & Laguna, P. (2005). Bioelectrical signal processing in cardiac and neurological applications. Elsevier Academic Press.
