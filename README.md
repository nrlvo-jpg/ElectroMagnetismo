# ElectroMagnetismo
# Simulación de Campo Magnético de un Solenoide

Este proyecto en MATLAB simula, calcula y visualiza el campo magnético tridimensional generado por un conjunto de espiras, aplicando la ley de Biot-Savart.

## Características

* Generación paramétrica de la geometría de las espiras.
* Cálculo numérico del campo magnético vectorial ($B_x, B_y, B_z$) sobre una cuadrícula 3D.
* Visualización del campo magnético mediante mapas de intensidad y líneas de flujo.
* Cálculo del flujo magnético a través de la superficie circular del aro conductor.
* Obtención de derivadas espaciales del flujo magnético y del campo axial.
* Simulación de fuerzas inducidas por corrientes de Foucault (Eddy Currents).
* Resolución numérica de la ecuación de movimiento utilizando el método de Runge-Kutta de cuarto orden.
* Comparación entre caída libre y caída bajo frenado electromagnético.

## Estructura del Proyecto

El código está modularizado en Live Scripts de MATLAB (`.mlx`):

* **`MainEspiras.mlx`**: Script principal de ejecución. Define los parámetros iniciales físicos y geométricos (corriente, número de espiras, radio, separación) y coordina el flujo del programa.
* **`dibujar_espiras_y_dl.mlx`**: Función encargada de calcular los puntos espaciales ($x, y, z$) del alambre y los vectores de longitud diferencial ($dl_x, dl_y, dl_z$).
* **`campoB.mlx`**: Motor de cálculo. Crea la cuadrícula espacial (grid 3D) y aplica la integración numérica de Biot-Savart para obtener los vectores de campo magnético.
* **`visualizar_campo.mlx`**: Módulo de graficación. Extrae un corte en el plano XZ ($y=0$), calcula la magnitud neta del campo y plotea las gráficas de superficie y flujo.
* **`trayectoria.m`**: Función que resuelve la ecuación de movimiento mediante el método de Runge-Kutta de cuarto orden.
* **`flujoB.m`**: Función que calcula el flujo magnético a través de una superficie circular a partir de la componente B_z.
* **`a_total_eddy.m`**: Función que calcula la aceleración instantánea tomando en cuenta la fuerza electromagnética inducida, la fuerza de fricción y la fuerza gravitacional.

## Requisitos

* **MATLAB** R2025b

## Uso

1. Descarga todos los archivos `.mlx` y `.m` en un mismo directorio.
2. Abre MATLAB y navega hasta dicho directorio.
3. Abre el archivo **`MainEspiras.mlx`**.

## Variables Principales

A continuación se detallan los parámetros y variables clave que controlan la física y geometría de la simulación:

### Parámetros Iniciales (Físicos y Geométricos)

* **`nI`**: Número total de espiras que conforman el solenoide.
* **`N`**: Resolución de la curva; define cuántos puntos espaciales se calculan para trazar cada espira.
* **`R`**: Radio de las espiras expresado en metros (m).
* **`sz`**: Separación longitudinal (sobre el eje Z) entre cada espira contigua (m).
* **`I`**: Corriente eléctrica que circula por el alambre, dada en Amperios (A).
* **`rw`**: Tamaño de paso para la creación de la cuadrícula 3D (actúa también como tolerancia para evitar singularidades matemáticas cerca del alambre).
* **`mo`**: Permeabilidad magnética del vacío ($4\pi \times 10^{-7} \, \text{T}\cdot\text{m/A}$).
* **`km`**: Constante precalculada de Biot-Savart ($\frac{\mu_0 \cdot I}{4\pi}$) para optimizar las iteraciones.
* **`R2`**: Radio del aro conductor que cae a través de solenoide (m).
* **`r`**: Resistencia del aro conductor (Ω).
* **`m_masa`**: Masa del aro conductor (kg).
* **`gamma`**: Coeficiente de Fricción mecánica (N x s/m).
  
### Condiciones Iniciales de la Trayectoria

* **`z0`**: Posición inicial del aro sobre el eje z (m).
* **`v0`**: Velocidad inicial del aro (m/s).
* **`t_final`**: Tiempo total de simulación (s).
* **`dt`**: Paso temporal para la integración numérica (s).
  
### Coordenadas y Geometría

* **`x, y, z`**: Arreglos que contienen las coordenadas tridimensionales de la trayectoria del alambre.
* **`dlx, dly, dlz`**: Componentes cartesianas del vector diferencial de longitud ($d\vec{l}$), indispensables para la integración numérica.
* **`Mx, My, Mz`**: Vectores que definen los ejes de la cuadrícula espacial (Grid 3D) en la que se evaluará el campo electromagnético.

### Variables de Salida

* **`Bx, By, Bz`**: Matrices 3D que almacenan la intensidad del campo magnético vectorial en cada coordenada de la cuadrícula.
* **`Bmag`**: Magnitud neta del campo magnético en un punto específico ($\sqrt{B_x^2 + B_y^2 + B_z^2}$).
* **`phiB`**: Vector que almacena el flujo magnético a través del aro en cada plano z (Wb).
* **`dPhi_dz`**: Gradiente del flujo magnético respecto a la posición z, obtenido por diferencias finitas (Wb/m).
* **`dBz_dz`**: Derivada espacial de la componente axial del campo magnético respecto a z (T/m).
* **`z_mid`**: Puntos medios entre nodos de `Mz`, usados para interpolar `dPhi_dz` durante el RK4.
* **`pos`**: Posición del aro conductor a lo largo del eje z (m).
* **`vel`**: Velocidad del aro conductor (m/s).

## Referencias

	Juárez Osorio, S. L. (2026). Frenos magnéticos [Diapositivas de PowerPoint]. Facultad de Ciencias, Tecnológico de Monterrey. https://www.canva.com/design/DAGm1AwEIBw/bUV-D2ljb00Xl0nD6Vh7VQ/edit

## Autores

* Ángel Raúl Luna Tirado - A01648221
* Gabriel Vallarta Ramirez - A01648413
* Franco Alan Martínez Vargas - A01648766
* Sofia Arredondo Alvarado - A01643986

