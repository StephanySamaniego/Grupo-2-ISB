# Laboratorio 6: Procesamiento de EMG 

1. [Introducción](#intro)
2. [Metodología](#met)
3. [Resultados](#resul)
6. [Archivos](#arch)
7. [Referencias](#ref)


## **Introducción** <a name="intro"></a>
---
**Electrocardiagrama**
<p align="justify"> Hoy en día, la prueba de ECG es relativamente barata y, por tanto, asequible para la mayoría de los pacientes. También es la base para diagnosticar enfermedades relacionadas con el corazón, ya que las pruebas más avanzadas requieren mucho tiempo o son muy costosas. Por lo tanto, existe la necesidad de mejorar aún más el análisis de la señal de ECG para que sea confirmatorio, proporcionando beneficios tales como la detección temprana de enfermedades cardíacas, una alternativa económica para los pacientes, etc [1]. 

<p align="center">
  <img src="img\caaracterísticas.png"  width="400" height="200"> </p>
  <em><p align="center">Fig. 1: Electrocardiograma con sus ondas, intervalos, segmentos y su relación con el ciclo cardiaco. P= contracción auricular, QRS= despolarización ventricular, T= relajación ventricular. Extraído de [2].</p></em> 



**Extracción de características de una señal ECG**
<p align="justify">La transformada wavelet es una herramienta eficaz para extraer características discriminativas en la clasificación de señales de ECG para el diagnóstico automático de arritmia cardíaca. En este artículo propusimos un algoritmo mejorado para detectar características complejas QRS basado en la transformada wavelet multi resolución para clasificar cuatro tipos de latidos de ECG [3].

<p align="justify">El procesamiento de señales ha contribuido significativamente a la comprensión del ECG y sus propiedades dinámicas, expresadas por cambios en el ritmo y la morfología de los latidos [4]. 

<p align="center">
  <img src="img\esquema.png"  width="400" height="200"> </p>
  <em><p align="center">Figura 1. Esquema de análisis de la señal ECG [4]</p></em> 



## **Metodología EMG** <a name="met"></a>
--- 
1. **Adquisición** 
<p align="justify"> Las señales fueron tomadas siguiendo el protocolo de BITalino ®evolution Lab Guide, experimental guides to meet & learn your biosignals. Se ubicaron los electrodos positivo y negativo en la muñeca, en la arteria radial, para medir el pulso radial, se eligió esta ubicación, ya que es el más fiable. La zona del cuello palpando la carótida también es fiable, sin embargo, en algunas personas puede afectar a la disminución de la frecuencia cardíaca [5]

2. **Filtrado**
<p align="justify">Se utiliza un filtro pasa banda diseñado para el rango de frecuencias de 0.1 Hz a 150 Hz. Las señales de ECG se han filtrado con un filtro bidireccional de Butterworth de orden 6, pasa bandas, con frecuencia de corte inferior de 0,6 Hz y superior de 45 Hz. La segmentación de latidos que se emplea es centrada alrededor del punto R con ventana simétrica de ±90 (180) muestras. 
Por otro lado, también se puede usar la transformada de wavelet Daubechies9 (Db9)para filtrar el ruido relacionado con los artefactos de movimiento.se puede usar un orden entre el 1 y el 10, experimentalmente se obtuvo un orden de nivel 7 como el nivel óptimo de trabajo; y experimentalmente también se halló el coeficiente de aproximación óptimo, el cual es 𝑐𝐴7 [6]


5. **Extracción de características**
<p align="justify">En la literatura existen numerosos trabajos donde se presentan las principales técnicas para la caracterización de señales ECG, pero la de mejor eficiencia y costo computacional es el método de coeficientes Wavelet [S1].

<p align="justify">Para la extracción de características, se usa comúnmente una frecuencia de 30 Hz, ya que en esta generalmente se encuentra la mayor información de las ondas P, complejo QRS y onda T.
La frecuencia del complejo QRS está distribuido entre 7 y 27 Hz,  centralizado principalmente en 17 Hz. [8]

<p align="center">
  <img src="img\tabla.png"  width="400" height="200"> </p>
  <em><p align="center">Tabla 1: Conjunto de mediciones caracterizando cada latido. Extraído de [9]
</p></em> 


- **Ancho del QRS**

El complejo QRS representa la llegada de la señal a ambos ventrículos, cuenta con una duración entre 0.06 y 0.10 s y un voltaje menor que 3.5mV. Un complejo QRS ancho a pesar del ritmo sinusal es el sello distintivo del bloqueo de rama del haz [a].

- **Nivel del segmento ST**

El segmento ST representa el tiempo que transcurre entre el final del complejo QRS y el inicio de la onda T. Una elevación cóncava hacia arriba en este segmento es diagnóstica de pericarditis.

- **Intervalo PR**

Determina si la conducción del pulso desde las aurículas a los ventrículos es normal, dura aproximadamente entre 0,10 s y 0,25 s, si es mayor, se sospecha de un bloqueo AV de 1er grado.

- **Amplitud de la onda T**

La onda T representa la repolarización de los ventrículos, tiene una menor amplitud que el QRS, la amplitud máxima es menor de 5 mm y 15 mm.

- **Intervalo QT**

Es el periodo entre el comienzo de la despolarización y el final de la repolarización ventricular, la duración de este intervalo ya corregido es entre 340 ms y 450 ms.


## **Resultados y Discusiones** <a name="met"></a>
--- 
<p align="justify">Se utilizaron dos filtros Notch en 60Hz y 120Hz para eliminar el ruido, luego se implementó un filtro Wavelet mencionado líneas arriba. Depués, se realiza una comparación entre  la señal filtrada y la literatura.

1. **Filtrado**

| |Señal Cruda | Espectro de frecuencia|
|-------------|-------------|-------------|
|Señal propia| <img src="img\porción_señal.png"  width="300" height="300">  | <img src="img\Espectro_frecuencias.png"  width="300" height="300">  |
|Señal referencial| <img src="img\cruda_ref.png"  width="300" height="300">  | <img src="img\espectro_ref.png"  width="300" height="300">  |
|Dsicusiones| <p align="justify">Observamos la señal ECG, en el que se puede observar que la duración del complejo QRS dura aproximadamente 0.04s, lo cual está por debajo de la duración mínima normal de 0.06s; por otro lado la duración del intervalo RR es de 0.09 aproximadamente|<p align="justify"> Para el espectro de frecuencias ECG sin filtrar la señal generada, con respecto a la señal referencial, se puede apreciar con un mayor ruido o interferencias entre 0 y 50 Hz lo cual puede deberse a errores en la adquisición.En ambas gráficas se puede observar un pico cerca a la frecuencia de 50 Hz. |


- **Filtros Notch**

|Señal filtrada completa |Señal filtrada recortada| Espectro de frecuencia |
|-------------|-------------|-------------|
| <img src="img\señal_ecg_filtros_notch_completa.png"  width="300" height="300">   |<img src="img\señal_ecg_filtros_notch_recortada.png"  width="300" height="300"> |<img src="img\Analisis_frecuencial_filtros_notch.png"  width="300" height="300"> |
| |<p align="justify">Con este filtro se pueden apreciar mejor los intervalos y se puede sacar una mejor aproximación de sus duraciones, por ejemplo, se puede apreciar mejor la región del intervalo PR que tiene una duración de aproximadamente 0.4 s, lo cual es bajo considerando que lo mínimo es de 0.10 s.|<p align="justify">Tal cual la teoría, al aplicar el filtro Notch se hace uso de un filtro de 60 Hz, por lo que podemos apreciar que a comparación de la Figura 6 en este caso, se ha reducido el tamaño de los picos ubicados cerca de la frecuencia de 60 Hz.|


- **Filtro Wavelet**

|||
|-------------|-------------|
| <img src="img\Wavelet_1.png"  width="300" height="300">|<img src="img\Wavelet_2.png"  width="300" height="300"> |


|Señal filtrada completa |Señal filtrada recortada| Espectro de frecuencia |
|-------------|-------------|-------------|
| <img src="img\Completa.png"  width="300" height="300">   |<img src="img\Recortada.png"  width="300" height="300"> |<img src="img\Análisis_Frecuencial.png"  width="300" height="300"> |

<p align="justify">Con este filtro la señal se ve mucho más limpia, se pueden diferenciar el complejo QRS, el intervalo RR, el intervalo PR y la onda T, el cual en este caso tiene una duración de aproximadamente de 0.04 s.


2. **Extracción de características**

### **Identificación del complejo QRS**
<p align="justify">Para hallar el complejo QRS ploteamos las señales de Identificación, de Operador Cuadrático, de Operador Derivativo y el Operador Moving Window Integration. 

<p align="justify">Además, se usó la librería Biosignalsnotebooks, que la librería biosignalsnotebooks te permite extraer una lista de características por medio de la función hrv_parameters, también nos permite hacer la identificación de diferentes tipos de picos de manera directa con la función "detect_r_peaks”.

<p align="justify">Luego realizamos un Análisis de Threshold para la identificación del inicio y fin del complejo QRS. Aquí también analizamos los picos y vemos la duración del complejo QRS gracias a los Threshold. El Tacograma nos ayuda a extraer información y parámetros del ECG.


- **Operador derivativo**
|Filtro derivativo|Señal completa|Señal recortada|
|-------------|-------------|-------------|
| <img src="img\Filtro_Derivativo.png"  width="300" height="300">   |<img src="img\Completa_der.png"  width="300" height="300"> |<img src="img\Recortada_der.png"  width="300" height="300"> |

- **Operador cuadrático**

|Señal completa|Señal recortada|
|-------------|-------------|
|<img src="img\Complea_operador.png"  width="300" height="300"> |<img src="img\Recortada_operador.png"  width="300" height="300"> |

- **Operdador Moving Window Integration**

|Señal completa|Señal recortada|
|-------------|-------------|
|<img src="img\Completa_w.png"  width="300" height="300"> |<img src="img\Recortada_w.png"  width="300" height="300"> |

### **Buscando los picos**

<p align="center">
  <img src="img\ecg_find_peaks.png"  width="400" height="200"> </p>
  <em><p align="center">Picos del complejo QRS encontrados en la señal</p></em> 

### **Análisis del Threshold**

Para la identificación del inicio y fin del complejo QRS

<p align="center">
  <img src="img\Threshold.png"  width="400" height="200"> </p>
  <em><p align="center">Señal con análisis de threshold</p></em> 

||||
|-------------|-------------|-------------|
| <img src="img\Treshold_ECG_1.png"  width="300" height="300">   |<img src="img\Treshold_ECG_2.png"  width="300" height="300"> |<img src="img\Treshold_ECG_3.png"  width="300" height="300"> |


### **Extracción BPM y  duración R-R**

Para la extracción de algunas características es necesario trabajar con el tacograma de la señal

|||
|-------------|-------------|
| <img src="img\Tacograma.png"  width="300" height="300">   |<img src="img\Tacogra_after_ectopic_beat_removal.png"  width="300" height="300"> |

Además, la libreria biosignalsnotebooks te permite extraer una lista de características por medio de la función hrv_parameters.

|||
|-------------|-------------|
| <img src="img\características_biosignals.png"  width="300" height="300">   |<img src="img\extracción_características.png"  width="300" height="300"> |

### **Picos encontrados usando BioSignals**

<p align="center">
  <img src="img\Find_peaks_biosignals.png"  width="400" height="200"> </p>


<p align="center">
  <img src="img\Find_peaks_biosignals_2.png"  width="400" height="200"> </p>
  
Se pudieron identificar los picos de la señal, sin embargo no son tan precisos.

## **Archivos** <a name="arch"></a>

- [Código para procesar la señal en Python](https://github.com/StephanySamaniego/ISB_Grupo2-2023-2/tree/6ff4cfff06c539e3f96778536c82a64bf7267348/ISB/Laboratorios/Laboratorio%2008%20-%20Procesamiento%20de%20ECG/Archivos)



## **Referencias** <a name="ref"></a>
---

[1] V. Gupta, M. Mittal, V. Mittal, and Nitin Kumar Saxena, “A Critical Review of Feature Extraction Techniques for ECG Signal Analysis,” Journal of The Institution of Engineers (India): Series B, vol. 102, no. 5, pp. 1049–1060, Jun. 2021, doi: https://doi.org/10.1007/s40031-021-00606-5. Available: https://link.springer.com/article/10.1007/s40031-021-00606-5. 

[2] Eder, Zamarrón López, M. Alberto, and O. Rubén, “Electrocardiografía dirigida para áreas críticas I,” ResearchGate, Jun. 07, 2019. Available: https://www.researchgate.net/publication/333649418_Electrocardiografia_dirigida_para_areas_criticas_I. [Accessed: Oct. 30, 2023]

[3] S. Sahoo, Bhupen Kanungo, Suresh Kumar Behera, and Sukanta Sabut, “Multiresolution wavelet transform based feature extraction and ECG classification to detect cardiac abnormalities,” Measurement, vol. 108, pp. 55–66, Oct. 2017, doi: https://doi.org/10.1016/j.measurement.2017.05.022. Available: https://www.sciencedirect.com/science/article/abs/pii/S026322411730297X. [Accessed: Oct. 30, 2023]

[4] L. Romero, "Análisis de señales electrocardiográficas usando técnicas de procesamiento digital," 2015.

[5] J. Felipe, "Frecuencia cardíaca, todo lo que necesitas saber," Mundo Entrenamiento, Jul. 24, 2014. [En línea]. Disponible en: https://mundoentrenamiento.com/frecuencia-cardiaca/.

[6] U. Seljuq, F. Himayun, and H. Rasheed, “Selection of an optimal mother wavelet basis function for ECG signal denoising,” 17th IEEE International Multi Topic Conference: Collaborative and Sustainable Development of Technologies, IEEE INMIC 2014 - Proceedings, pp. 26–30, 2014, doi: 10.1109/INMIC.2014.7096905.

[7]

[8] J. Li, G. Deng, W. Wei, H. Wang, and Z. Ming, “Design of a Real-Time ECG Filter for Portable Mobile Medical Systems,” IEEE Access, vol. 5, pp. 696–704, 2017, doi: 10.1109/ACCESS.2016.2612222.

[9] V. Eugenia, G. A. Guarín, and Castellanos Domínguez, Germán, “Extracción de características de ECG basadas en transformaciones no lineales y wavelets,” Ingeniería e Investigación, vol. 25, no. 3, pp. 39–48, 2023, Available: http://www.scielo.org.co/scielo.php?script=sci_arttext&pid=S0120-56092005000300006. [Accessed: Oct. 30, 2023]