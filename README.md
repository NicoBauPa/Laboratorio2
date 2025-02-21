# Laboratorio 2. Convolución, correlación y transformación.

## Introducción.
En este laboratorio, exploraremos estos conceptos tanto de forma teórica como práctica. Realizaremos cálculos manuales y luego implementaremos los métodos en Python para visualizar los resultados de manera más clara. También aplicaremos la transformada de Fourier para analizar señales en el dominio de la frecuencia, lo que nos permitirá extraer información clave sobre su comportamiento. A demás, la convolución y la correlación juegan un papel fundamental. La convolución nos permite entender cómo un sistema responde a una señal de entrada, algo esencial en el diseño de filtros y en el análisis de sistemas lineales. Por su parte, la correlación nos ayuda a medir la similitud entre dos señales, lo que resulta útil en detección de patrones, reconocimiento de señales y muchas otras aplicaciones. 

Este documento analiza la apnea del sueño, un trastorno caracterizado por pausas en la respiración durante el sueño, y su detección mediante señales electrocardiográficas (ECG). Se basa en la base de datos Apnea-ECG de PhysioNet, que contiene registros de ECG para el desarrollo de métodos automatizados de diagnóstico. El contenido ha sido elaborado por  Dr. Thomas Penzel de la Universidad Phillips, Marburgo, Alemania, con el objetivo de proporcionar una visión técnica sobre la apnea y su análisis a través de ECG.

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
### Grafico:

Este fragmento de código usa *Matplotlib* para visualizar las señales convolucionadas de Gime, María José y Nicole en una sola figura con tres subgráficos. Primero, se crea una figura de tamaño 12x6. Luego, se generan tres gráficos de tipo *stem*, que representan las señales discretas con líneas y marcadores.  

- En el primer *subplot*, se grafica la convolución de Gime en color amarillo (`y-` para las líneas y `yo` para los marcadores).  
- En el segundo, se muestra la convolución de María José en rojo (`r-` y `ro`).  
- En el tercero, se grafica la convolución de Nicole en verde (`g-` y `go`).  

Cada gráfico tiene su título, etiquetas para los ejes \( n \) y \( y[n] \), y *plt.tight_layout()* ajusta los espacios para que no se sobrepongan los elementos. Finalmente, *plt.show()* muestra la figura con las tres gráficas.

## Conclusión.


## Referencias.
