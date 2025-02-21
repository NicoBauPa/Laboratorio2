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

## Análisis de resultados.


## Conclusión.


## Referencias.
