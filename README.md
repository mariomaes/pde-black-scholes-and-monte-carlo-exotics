# Valoración Numérica de Derivados: EDPs en Diferencias Finitas y Simulación de Monte Carlo para Exóticas

Implementación desde cero en Python (`NumPy`, `SciPy`) de métodos numéricos avanzados para la valoración de opciones financieras y el cálculo de sensibilidades (Griegas), estructurado en dos bloques principales:

## 1. Resolución de la EDP de Black-Scholes por Diferencias Finitas
Discretización espacio-temporal de la Ecuación en Derivadas Parciales de Black-Scholes mediante la resolución iterativa de sistemas matriciales tridiagonales:
* **Esquema de Crank-Nicholson:** Formulación matricial e imposición de condiciones iniciales (*payoff*) y de contorno específicas para valorar:
  * **Opciones Europeas (Call y Put).**
  * **Opciones Binarias / Digitales** (modeladas mediante la función escalón de Heaviside).
  * **Estrategias Estructuradas:** *Bull Spread* y *Straddle*.
* **Esquema Implícito BTCS y Superficies de Griegas:** Estimación numérica mediante diferencias finitas centradas de **Delta ($\Delta$), Gamma ($\Gamma$), Theta ($\Theta$), Vega ($\nu$) y Rho ($\rho$)** a lo largo del precio del subyacente $S$ y para múltiples horizontes temporales hasta el vencimiento ($\tau$). Incluye el análisis del desplazamiento del máximo de *Vega* hacia el nivel *At-The-Money Forward* ante tipos de interés elevados.

## 2. Simulación de Monte Carlo y Reducción de Varianza en Opciones Exóticas
Simulación estocástica de trayectorias bajo la medida neutral al riesgo (Movimiento Browniano Geométrico) para la valoración de **Opciones Asiáticas**:
* **Validación en Opciones Europeas:** Contraste del estimador de Monte Carlo ($M = 10.000$ trayectorias) frente a la solución analítica cerrada de Black-Scholes dentro del intervalo de confianza al 95%.
* **Opciones Asiáticas con Variables de Control (*Control Variates*):** Valoración de una *Call Asiática sobre la media aritmética* (sin solución analítica cerrada) empleando una *Call Asiática sobre la media geométrica* (con solución exacta conocida) evaluada sobre los mismos números aleatorios comunes.
* **Eficiencia Computacional:** La técnica de Variable de Control reduce el error estándar (SE) de **0,274 a 0,019**, logrando un **Factor de Reducción de Varianza de 14,7x** (equivalente a reducir en $\approx 216\times$ el número de simulaciones necesarias en un Monte Carlo estándar).
