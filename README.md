# Laboratorio 2. Convolución, correlación y transformación.

## Introducción.
Uno de los elementos tratados en la practica a continuación, es la convolución, para esto usamos los digitos del codigo universsitario y el documento de identificación de cada una de las integrantes, este proceso se realiza de manera manual y se implementa esto mismo de manera digital por medio de programación en Phyton mostrando la convolución de manera gráfica, con estas mismas señales se calcula la correlación. Por otro lado, se escogió una señal ECG de apnea del sueño, un trastorno caracterizado por pausas en la respiración durante el sueño, y su detección mediante señales electrocardiográficas (ECG). Se basa en la base de datos Apnea-ECG de PhysioNet, que contiene registros de ECG para el desarrollo de métodos automatizados de diagnóstico. El contenido ha sido elaborado por  Dr. Thomas Penzel de la Universidad Phillips, Marburgo, Alemania, con el objetivo de proporcionar una visión técnica sobre la apnea y su análisis a través de ECG. A partir de esta señal, aplicaremos la transformada de Fourier para analizar señales en el dominio de la frecuencia, lo que nos permitirá extraer información clave sobre su comportamiento en el dominio del tiempo (media, mediana, desviación estandar, máximos y mínimos) y el dominio de la frecuencia (la frecuencia media, frecuencia mediana y desviación etsandar de la frecuencia).

## Paso a paso.
 Seleccionar la señal EMG por medio de Physionet [link Physionet](https://physionet.org/)
- Guardar los archivos .hea, .data, .apn en una misma carpeta junto con la señal
- Abrir Python, nombrar el archivo y guardarlo en la misma carpeta donde se encuentran los archivos .hea .data y apn.
- Abrir de nuevo python y iniciar con la programación que explicaremos a continuación:
  
## Programación:
Inicialmente agregamos las librerias:
```  python
import numpy as np
import matplotlib.pyplot as plt
import wfdb
import scipy.signal as signal
import os

```
- **NumPy** ( np) nos ayuda con el manejo de matrices y operaciones matemáticas.
- **Matplotlib** ( plt) se usa para graficar datos.
- **WFDB** ( wfdb) nos permite trabajar con señales fisiológicas como el ECG.
- **SciPy Signal** ( signal) se usa para procesar señales (aunque en este código no se usa mucho).
- **OS** ( os) nos permite manejar archivos y rutas en el sistema operativo.

### Convolución:

El código define las señales \( h[n] \) y \( x[n] \) para tres personas diferentes: Gime, María José y Nicole. Estas señales son representadas como arreglos de NumPy, donde \( h[n] \) corresponde al sistema y \( x[n] \) a la señal de entrada. Cada persona tiene su propio conjunto de datos, posiblemente para comparar cómo interactúan las señales en distintas situaciones.
```
# Gime
h_gime = np.array([5, 6, 0, 0, 6, 3, 0])  # Sistema h[n]
x_gime = np.array([1, 0, 5, 6, 9, 5, 4, 4, 4, 8])  # Señal x[n]

# María José
h_maria = np.array([1, 0, 1, 9, 6, 0, 2, 1, 4, 8])
x_maria = np.array([5, 6, 0, 0, 4, 3, 5 ])

# Nicole
h_nicole = np.array([1, 1, 9, 3, 5, 6, 4, 4, 1, 5])
x_nicole = np.array([5, 6, 0, 0, 5, 7, 4])
## Análisis de resultados.

```
Graficas de convolución:
![image](https://github.com/user-attachments/assets/883476bf-7096-41a4-87c4-6cd5753c5136)
![image](https://github.com/user-attachments/assets/56129b1a-8028-4aa5-80df-14b5be747f4e)



```

```
### Grafico:

Este fragmento de código usa *Matplotlib* para visualizar las señales convolucionadas de Gime, María José y Nicole en una sola figura con tres subgráficos. Primero, se crea una figura de tamaño 12x6. Luego, se generan tres gráficos de tipo *stem*, que representan las señales discretas con líneas y marcadores.  

- En el primer *subplot*, se grafica la convolución de Gime en color amarillo (`y-` para las líneas y `yo` para los marcadores).  
- En el segundo, se muestra la convolución de María José en rojo (`r-` y `ro`).  
- En el tercero, se grafica la convolución de Nicole en verde (`g-` y `go`).  

Cada gráfico tiene su título, etiquetas para los ejes \( n \) y \( y[n] \), y *plt.tight_layout()* ajusta los espacios para que no se sobrepongan los elementos. Finalmente, *plt.show()* muestra la figura con las tres gráficas.

```

plt.figure(figsize=(12, 6))
plt.subplot(3, 1, 1)
plt.stem(y_gime, linefmt='y-', markerfmt='yo', basefmt='k-')
plt.title("Convolución de Gime")
plt.xlabel("n")
plt.ylabel("y[n]")

plt.subplot(3, 1, 2)
plt.stem(y_maria, linefmt='r-', markerfmt='ro', basefmt='k-')
plt.title("Convolución de María José")
plt.xlabel("n")
plt.ylabel("y[n]")

plt.subplot(3, 1, 3)
plt.stem(y_nicole, linefmt='g-', markerfmt='go', basefmt='k-')
plt.title("Convolución de Nicole")
plt.xlabel("n")
plt.ylabel("y[n]")

plt.tight_layout()
plt.show()

```

![image](https://github.com/user-attachments/assets/804b93e8-dd52-4aa0-903c-d986446ddf11)

### Cálculo de correlación:

El código calcula la correlación cruzada entre dos señales, un coseno y un seno de 100 Hz. Primero, define el tiempo de muestreo (`Ts = 1.25 ms`) y genera 9 muestras (`n = np.arange(9)`). Luego, crea las señales `x1` y `x2` usando funciones coseno y seno, respectivamente. Finalmente, con `np.correlate(x1, x2, mode='full')`, mide la similitud entre ambas en distintos desfases, lo que permite analizar su relación temporal.

```
Ts = 1.25e-3  
n = np.arange(9) 
f = 100  # Frecuencia en Hz


x1 = np.cos(2 * np.pi * f * n * Ts)  # Señal x1[n]
x2 = np.sin(2 * np.pi * f * n * Ts)  # Señal x2[n]


correlacion = np.correlate(x1, x2, mode='full')
```
### Correlación:

Ts = 1.25e-3  # Tiempo de muestreo en segundos
n = np.arange(9)  # Nueve muestras según el documento
f = 100  # Frecuencia en Hz

Definición de las señales:
x1 = np.cos(2 * np.pi * f * n * Ts)  # Señal x1[n]
x2 = np.sin(2 * np.pi * f * n * Ts)  # Señal x2[n]

Correlación cruzada entre ambas señales:
correlacion = np.correlate(x1, x2, mode='full')

```
```

### Gráfico: 
Este código genera una gráfica de la correlación cruzada entre las señales \( x_1[n] \) y \( x_2[n] \). Primero, se crea una figura de tamaño 8x4. Luego, con `plt.stem()`, se representa la correlación cruzada en un gráfico de líneas y marcadores azules (`b-` y `bo`), con una línea base negra (`k-`). El eje x muestra los desplazamientos de la correlación, que van desde `-len(x1) + 1` hasta `len(x1)`, indicando cómo varía la similitud entre las señales a diferentes desfases. Se añaden título, etiquetas y una cuadrícula para mejorar la visualización. Finalmente, `plt.show()` muestra el gráfico.

```
plt.figure(figsize=(8, 4))
plt.stem(np.arange(-len(x1)+1, len(x1)), correlacion, linefmt='b-', markerfmt='bo', basefmt='k-')
plt.title("Correlación cruzada entre x1[n] y x2[n]")
plt.xlabel("Desplazamiento (n)")
plt.ylabel("Correlación")
plt.grid(True)
plt.show()

```

![image](https://github.com/user-attachments/assets/e62a4770-54d6-4365-ad6d-968ec6b0eef8)

### Segundo Punto:

Primero, definimos la ruta y el nombre del archivo (`record_name = "a01"`) donde está almacenada la señal. Luego, usa la librería `wfdb` para leer tanto la señal (`wfdb.rdrecord()`) como sus anotaciones (`wfdb.rdann()`). Se extrae la señal del primer canal (`record.p_signal[:, 0]`) y la frecuencia de muestreo (`record.fs`). A partir de esto, se calcula el tiempo en segundos dividiendo el número de muestras por la frecuencia de muestreo. Finalmente, se obtienen estadísticas descriptivas de la señal, como la media, mediana, desviación estándar, valor máximo y mínimo, para analizar su comportamiento.

```
record_name = "a01"  # Nombre del archivo sin extensión
record_path = r"C:\Users\majo1\OneDrive\Escritorio\señales\lab señales\lab 2"


record = wfdb.rdrecord(os.path.join(record_path, record_name))
annotation = wfdb.rdann(os.path.join(record_path, record_name), "apn")


signal_data = record.p_signal[:, 0]  # Primer canal (ECG)
sampling_rate = record.fs  # Frecuencia de muestreo

time = np.arange(len(signal_data)) / sampling_rate

```

![image](https://github.com/user-attachments/assets/dfde83b1-392e-4f2e-a223-948ddbb6fa00)

### Estadisticas Descriptivas:

Primero, obtiene la media (np.mean), mediana (np.median), desviación estándar (np.std), valor máximo (np.max) y valor mínimo (np.min) de los datos de la señal. Luego, imprime estos valores en pantalla con un formato claro, permitiendo analizar su distribución y variabilidad. Esto es útil para entender el comportamiento general de la señal antes de aplicar otros análisis más complejos.
```

time_mean = np.mean(signal_data)
time_median = np.median(signal_data)
time_std = np.std(signal_data)
time_max = np.max(signal_data)
time_min = np.min(signal_data)

print("Estadísticas en el dominio del tiempo:")
print(f"Media: {time_mean}")
print(f"Mediana: {time_median}")
print(f"Desviación estándar: {time_std}")
print(f"Máximo: {time_max}")
print(f"Mínimo: {time_min}")

```
### Graficar la señal en el dominio del tiempo:

El código grafica la señal de ECG en función del tiempo. Primero, crea una figura de 10x4 y luego dibuja la señal con `plt.plot()`, etiquetando los ejes y agregando un título. También incluye una leyenda para identificar la señal y, al final, muestra la gráfica con `plt.show()`, permitiendo visualizar cómo varía la señal a lo largo del tiempo.

```

plt.figure(figsize=(10, 4))
plt.plot(time, signal_data, label="ECG")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud")
plt.title("Señal ECG en el dominio del tiempo")
plt.legend()
plt.show()

```
![image](https://github.com/user-attachments/assets/287b0263-ce2e-4913-8b3c-91a422e02b25)

### Transformada de Fourier y Densidad Espectral:

El código aplica la Transformada de Fourier a la señal de ECG para analizar sus frecuencias. Primero, calcula las frecuencias (`freqs`), obtiene la transformada (`fft_values`) y luego la densidad espectral de potencia (`power_spectrum`). Después, genera dos gráficas: una con la magnitud de la transformada para ver qué frecuencias están presentes y otra con la densidad espectral para visualizar cómo se distribuye la energía. Ambos gráficos incluyen etiquetas y una cuadrícula para facilitar su interpretación.

```

freqs = np.fft.rfftfreq(len(signal_data), d=1/sampling_rate)
fft_values = np.fft.rfft(signal_data)
power_spectrum = np.abs(fft_values) ** 2

-Graficar la transformada de Fourier
plt.figure(figsize=(10, 4))
plt.plot(freqs, np.abs(fft_values))
plt.xlabel("Frecuencia (Hz)")
plt.ylabel("Magnitud")
plt.title("Transformada de Fourier de la señal ECG")
plt.grid()
plt.show()

```
![image](https://github.com/user-attachments/assets/d2849c86-8598-46c2-bdf8-34b488ff68c1)


```

Graficar la densidad espectral de potencia
plt.figure(figsize=(10, 4))
plt.plot(freqs, power_spectrum)
plt.xlabel("Frecuencia (Hz)")
plt.ylabel("Densidad de Potencia")
plt.title("Densidad espectral de la señal ECG")
plt.grid()
plt.show()

```
![image](https://github.com/user-attachments/assets/232dec64-684b-4ba6-b5d8-b89372f42e81)


### Cálculo de estadísticas en el dominio de la frecuencia:

Acá se calcula y analiza estadísticas en el dominio de la frecuencia para la señal de ECG. Primero, obtiene la **frecuencia media** (`freq_mean`), ponderando cada frecuencia con su densidad espectral de potencia y dividiendo por la suma total de la potencia. Luego, calcula la **frecuencia mediana** (`freq_median`), ordenando la densidad espectral y seleccionando la frecuencia en la posición central. La **desviación estándar** (`freq_std`) se obtiene midiendo la dispersión de las frecuencias respecto a la media, también ponderada por la potencia.  

Después, imprime estos valores y genera un **histograma de frecuencias**, donde `plt.hist()` divide el rango de frecuencias en 50 bins y pondera cada una según su potencia, permitiendo visualizar cómo se distribuye la energía en el espectro de la señal. Finalmente, se añaden etiquetas y una cuadrícula para mejorar la interpretación antes de mostrar la gráfica con `plt.show()`.

```
freq_mean = np.sum(freqs * power_spectrum) / np.sum(power_spectrum)
freq_median = freqs[np.argsort(power_spectrum)[len(power_spectrum)//2]]
freq_std = np.sqrt(np.sum((freqs - freq_mean)**2 * power_spectrum) / np.sum(power_spectrum))

print("Estadísticas en el dominio de la frecuencia:")
print(f"Frecuencia media: {freq_mean}")
print(f"Frecuencia mediana: {freq_median}")
print(f"Desviación estándar de la frecuencia: {freq_std}")

# Histograma de frecuencias
plt.figure(figsize=(10, 4))
plt.hist(freqs, bins=50, weights=power_spectrum)
plt.xlabel("Frecuencia (Hz)")
plt.ylabel("Potencia")
plt.title("Histograma de frecuencias de la señal ECG")
plt.grid()
plt.show()



```
![image](https://github.com/user-attachments/assets/12727ccc-c4ed-4dbd-97fa-6cd0f6cbe6e4)

## Conclusión.

En este laboratorio, exploramos la convolución y la correlación como herramientas clave en el procesamiento digital de señales. A través de ejercicios prácticos, comprendimos cómo la convolución permite analizar la respuesta de un sistema a una señal de entrada, mientras que la correlación nos ayuda a medir la similitud entre señales en distintos momentos. Además, aplicamos la Transformada de Fourier para examinar la señal en el dominio de la frecuencia, calculando su densidad espectral de potencia y sus estadísticas descriptivas.

La implementación en Python facilitó el análisis y la visualización de los resultados, permitiéndonos interpretar mejor la información contenida en las señales. Esto es fundamental en aplicaciones como el procesamiento de señales biomédicas, donde la correcta identificación de patrones en ECG u otras señales fisiológicas puede mejorar el diagnóstico y la toma de decisiones clínicas. En general, este laboratorio reforzó la importancia de estas técnicas en el análisis y manipulación de señales digitales.

## Referencias.
- Oppenheim, AV, y Willsky, AS (1996). Señales y sistemas (2.ª ed.). Prentice Hall.
- Proakis, JG, y Manolakis, DG (2007). Procesamiento de señales digitales: principios, algoritmos y aplicaciones (4.ª ed.). Pearson
- Cohen, L. (1995). Análisis de tiempo-frecuencia . Prentice Hall.
- Clifford, GD, Azuaje, F., y McSharry, PE (2006). Métodos y herramientas avanzados para el análisis de datos de ECG . Artech House.
