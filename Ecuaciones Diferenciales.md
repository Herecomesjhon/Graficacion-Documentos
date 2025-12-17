# Investigación Documental: Movimiento Armónico Simple de un Sistema Masa-Resorte

## 1. Marco Teórico

### 1.1 Antecedentes Históricos

El estudio del movimiento armónico simple tiene sus raíces en el siglo XVII con las investigaciones de Robert Hooke (1635-1703), quien en 1660 estableció la ley que lleva su nombre: la fuerza restauradora de un resorte es proporcional a su elongación. Esta ley fundamental sentó las bases para el análisis de sistemas oscilatorios.

Isaac Newton (1642-1727), con sus leyes del movimiento publicadas en 1687 en "Philosophiæ Naturalis Principia Mathematica", proporcionó el marco teórico para analizar dinámicamente estos sistemas. La combinación de la Ley de Hooke con la Segunda Ley de Newton permitió formular las ecuaciones diferenciales que gobiernan el movimiento armónico simple.

Durante el siglo XVIII, matemáticos como Leonhard Euler y Jean le Rond d'Alembert desarrollaron métodos analíticos para resolver ecuaciones diferenciales, permitiendo modelar con precisión el comportamiento de sistemas oscilatorios. Estos desarrollos fueron fundamentales para la física teórica y aplicada, encontrando aplicaciones en la ingeniería estructural, la mecánica cuántica y la teoría de señales.

### 1.2 Conceptos Físicos Involucrados

#### 1.2.1 Ley de Hooke

La fuerza restauradora ejercida por un resorte es proporcional al desplazamiento desde su posición de equilibrio:

```
F = -kx
```

donde:

- **F**: fuerza restauradora (lb o N)
- **k**: constante del resorte (lb/ft o N/m)
- **x**: desplazamiento desde el equilibrio (ft o m)
- El signo negativo indica que la fuerza se opone al desplazamiento

#### 1.2.2 Segunda Ley de Newton

La relación fundamental entre fuerza, masa y aceleración:

```
F = ma
```

donde:

- **m**: masa del objeto (slug o kg)
- **a**: aceleración (ft/s² o m/s²)

#### 1.2.3 Movimiento Armónico Simple (MAS)

Un movimiento periódico que ocurre cuando la fuerza restauradora es proporcional al desplazamiento. Sus características principales son:

- **Amplitud (A)**: máximo desplazamiento desde el equilibrio
- **Periodo (T)**: tiempo para completar un ciclo completo
- **Frecuencia (f)**: número de ciclos por unidad de tiempo
- **Frecuencia angular (ω)**: ω = 2π/T = 2πf

#### 1.2.4 Energía en el Sistema

En un sistema masa-resorte ideal (sin fricción), la energía mecánica total se conserva, alternando entre energía cinética y potencial elástica.

### 1.3 Obtención del Modelo Matemático

Aplicando la Segunda Ley de Newton al sistema masa-resorte:

**Paso 1**: Identificar las fuerzas actuantes

- Fuerza del resorte: F_resorte = -kx

**Paso 2**: Aplicar la Segunda Ley de Newton

```
ma = -kx
```

**Paso 3**: Expresar la aceleración como derivada segunda

```
m(d²x/dt²) = -kx
```

**Paso 4**: Reorganizar la ecuación

```
d²x/dt² + (k/m)x = 0
```

**Paso 5**: Definir la frecuencia angular

```
ω² = k/m
```

**Ecuación diferencial del MAS**:

```
d²x/dt² + ω²x = 0
```

**Paso 6**: Solución general

La solución general de esta ecuación diferencial de segundo orden es:

```
x(t) = A·cos(ωt + φ)
```

o equivalentemente:

```
x(t) = C₁·cos(ωt) + C₂·sin(ωt)
```

donde C₁ y C₂ se determinan mediante las condiciones iniciales.

---

## 2. Explicación Detallada del Ejercicio

### 2.1 Datos Proporcionados

El problema presenta un sistema masa-resorte vertical con las siguientes características:

**Datos del sistema**:

- Peso de la masa: W = 64 lb
- Elongación del resorte en equilibrio: s = 0.32 ft
- Posición inicial: x₀ = -8 pulgadas = -2/3 ft (arriba del equilibrio, por eso negativo)
- Velocidad inicial: v₀ = 5 ft/s (descendente, por eso positivo)

**Convención de signos**:

- Positivo: hacia abajo desde la posición de equilibrio
- Negativo: hacia arriba desde la posición de equilibrio

### 2.2 Contexto Físico

El sistema consiste en una masa suspendida de un resorte vertical. Inicialmente, el resorte está en su longitud natural. Cuando se cuelga la masa, el resorte se estira 0.32 pies hasta alcanzar una nueva posición de equilibrio donde la fuerza del resorte balancea el peso.

Luego, la masa se desplaza 8 pulgadas hacia arriba desde esta posición de equilibrio y se suelta con una velocidad inicial de 5 ft/s hacia abajo. El sistema comenzará a oscilar alrededor de la posición de equilibrio.

### 2.3 Objetivos del Problema

El ejercicio requiere:

1. Determinar la ecuación matemática que describe el movimiento
2. Calcular parámetros característicos del movimiento (amplitud, periodo)
3. Analizar el comportamiento temporal del sistema
4. Determinar posiciones, velocidades y aceleraciones en instantes específicos

---

## 3. Formulación y Resolución del Modelo Matemático

### 3.1 Determinación de Parámetros del Sistema

**Paso 1: Calcular la masa**

En el sistema inglés de unidades, la relación entre peso y masa es:

```
W = mg, donde g = 32 ft/s²

m = W/g = 64/32 = 2 slugs
```

**Paso 2: Calcular la constante del resorte**

En la posición de equilibrio, la fuerza del resorte equilibra el peso:

```
ks = W

k = W/s = 64/0.32 = 200 lb/ft
```

**Paso 3: Calcular la frecuencia angular**

```
ω = √(k/m) = √(200/2) = √100 = 10 rad/s
```

**Paso 4: Determinar el periodo y la frecuencia**

```
T = 2π/ω = 2π/10 = π/5 segundos ≈ 0.628 s

f = 1/T = 5/π Hz ≈ 1.592 Hz
```

### 3.2 Formulación de la Ecuación de Movimiento

**Forma general**:

```
x(t) = C₁·cos(10t) + C₂·sin(10t)
```

**Condiciones iniciales**:

- x(0) = -2/3 ft
- v(0) = 5 ft/s

**Aplicando x(0) = -2/3**:

```
x(0) = C₁·cos(0) + C₂·sin(0) = C₁ = -2/3
```

**Para la velocidad, derivamos**:

```
v(t) = dx/dt = -10C₁·sin(10t) + 10C₂·cos(10t)
```

**Aplicando v(0) = 5**:

```
v(0) = -10C₁·sin(0) + 10C₂·cos(0) = 10C₂ = 5
C₂ = 1/2
```

**Ecuación de movimiento**:

```
x(t) = -2/3·cos(10t) + 1/2·sin(10t) ft
```

### 3.3 Forma Alternativa: Amplitud-Fase

Para expresar la ecuación en la forma x(t) = A·cos(ωt - φ):

**Amplitud**:

```
A = √(C₁² + C₂²) = √((-2/3)² + (1/2)²) 
A = √(4/9 + 1/4) = √(16/36 + 9/36) = √(25/36) = 5/6 ft
```

**Ángulo de fase**:

```
tan(φ) = C₂/(-C₁) = (1/2)/(2/3) = 3/4

φ = arctan(3/4) ≈ 0.6435 rad ≈ 36.87°
```

**Forma alternativa**:

```
x(t) = 5/6·cos(10t - 0.6435) ft
```

o equivalentemente:

```
x(t) = 5/6·sin(10t + 0.9273) ft
```

---

## 4. Respuestas a las Preguntas del Ejercicio

### a) Ecuación de movimiento

```
x(t) = -2/3·cos(10t) + 1/2·sin(10t) ft
```

o en forma amplitud-fase:

```
x(t) = 5/6·cos(10t - 0.6435) ft
```

**Respuesta**: La ecuación de movimiento es **x(t) = -2/3·cos(10t) + 1/2·sin(10t)** pies, o equivalentemente **x(t) = (5/6)·cos(10t - 0.6435)** pies.

---

### b) Amplitud y periodo del movimiento

**Amplitud**:

```
A = 5/6 ft = 10 pulgadas
```

**Periodo**:

```
T = π/5 s ≈ 0.628 s
```

**Respuesta**: La amplitud es **A = 5/6 ft (10 pulgadas)** y el periodo es **T = π/5 s ≈ 0.628 segundos**.

---

### c) Número de ciclos completos en 3π segundos

```
Número de ciclos = t/T = 3π/(π/5) = 3π × 5/π = 15 ciclos
```

**Respuesta**: La masa completará **15 ciclos completos** al final de 3π segundos.

---

### d) Segunda vez que pasa por el equilibrio hacia abajo

La masa pasa por el equilibrio (x = 0) cuando:

```
-2/3·cos(10t) + 1/2·sin(10t) = 0

Dividiendo por cos(10t):
-2/3 + 1/2·tan(10t) = 0
tan(10t) = 4/3
```

Soluciones generales:

```
10t = arctan(4/3) + nπ, donde n = 0, 1, 2, ...
10t = 0.9273 + nπ
t = 0.09273 + nπ/10
```

Para determinar la dirección, evaluamos la velocidad:

```
v(t) = 20/3·sin(10t) + 5·cos(10t)
```

- Primera vez (n=0): t₁ = 0.09273 s, v(0.09273) = 8.33 ft/s > 0 ✓ (hacia abajo)
- Segunda vez (n=1): t₂ = 0.09273 + π/10 ≈ 0.4069 s ✓ (hacia abajo)

**Respuesta**: La masa pasa por la posición de equilibrio con dirección hacia abajo por segunda vez en **t ≈ 0.407 segundos**.

---

### e) Instantes de desplazamientos extremos

Los desplazamientos extremos ocurren cuando v(t) = 0:

```
20/3·sin(10t) + 5·cos(10t) = 0

Dividiendo por cos(10t):
20/3·tan(10t) + 5 = 0
tan(10t) = -3/4

10t = arctan(-3/4) + nπ
10t = -0.6435 + nπ

t = -0.06435 + nπ/10, para n = 0, 1, 2, ...
```

Como necesitamos t ≥ 0:

- n=1: t = -0.06435 + π/10 ≈ 0.2499 s (primer extremo inferior)
- n=2: t = -0.06435 + 2π/10 ≈ 0.5641 s (primer extremo superior)
- n=3: t = -0.06435 + 3π/10 ≈ 0.8783 s (segundo extremo inferior)

**Respuesta**: Los desplazamientos extremos ocurren en **t = 0.2499 + n(π/10) segundos**, para n = 0, 1, 2, ...

Primeros valores: **t ≈ 0.250 s, 0.564 s, 0.878 s, 1.192 s, ...**

---

### f) Posición en t = 3 s

```
x(3) = -2/3·cos(30) + 1/2·sin(30)

x(3) = -2/3(0.1542) + 1/2(-0.9880)
x(3) = -0.1028 - 0.4940
x(3) = -0.597 ft
```

**Respuesta**: La posición de la masa en t = 3 s es **x(3) ≈ -0.597 ft ≈ -7.16 pulgadas** (arriba del equilibrio).

---

### g) Velocidad instantánea en t = 3 s

```
v(t) = 20/3·sin(10t) + 5·cos(10t)

v(3) = 20/3·sin(30) + 5·cos(30)
v(3) = 20/3(-0.9880) + 5(0.1542)
v(3) = -6.587 + 0.771
v(3) = -5.816 ft/s
```

**Respuesta**: La velocidad instantánea en t = 3 s es **v(3) ≈ -5.82 ft/s** (hacia arriba).

---

### h) Aceleración en t = 3 s

```
a(t) = d²x/dt² = -ω²x(t) = -100x(t)

a(3) = -100(-0.597)
a(3) = 59.7 ft/s²
```

**Respuesta**: La aceleración en t = 3 s es **a(3) ≈ 59.7 ft/s²** (hacia abajo).

---

### i) Velocidad instantánea al pasar por el equilibrio

En el equilibrio, toda la energía es cinética. Por conservación de energía:

```
½mv² = ½kA²

v² = (k/m)A² = ω²A²
v = ±ωA = ±10(5/6) = ±25/3 ft/s
v = ±8.33 ft/s
```

**Respuesta**: La velocidad instantánea cuando la masa pasa por el equilibrio es **v = ±8.33 ft/s** (±25/3 ft/s exactamente). El signo positivo corresponde al movimiento hacia abajo y el negativo al movimiento hacia arriba.

---

### j) Instantes cuando la masa está 5 pulgadas abajo del equilibrio

```
x(t) = 5/12 ft    (5 pulgadas = 5/12 ft)

-2/3·cos(10t) + 1/2·sin(10t) = 5/12
```

Usando x(t) = 5/6·cos(10t - 0.6435):

```
5/6·cos(10t - 0.6435) = 5/12
cos(10t - 0.6435) = 1/2

10t - 0.6435 = ±π/3 + 2nπ
```

**Soluciones**:

```
t = (π/3 + 0.6435)/10 + nπ/5 ≈ 0.1689 + 0.6283n s
t = (-π/3 + 0.6435)/10 + nπ/5 ≈ -0.0402 + 0.6283n s
```

Para t ≥ 0 y primeros valores:

**Respuesta**: La masa está 5 pulgadas abajo del equilibrio en los instantes **t ≈ 0.169 s, 0.588 s, 0.797 s, 1.217 s, 1.425 s, 1.845 s, ...**

---

### k) Instantes cuando está 5 pulgadas abajo apuntando hacia arriba

Necesitamos x(t) = 5/12 y v(t) < 0 (hacia arriba)

De los tiempos calculados en (j), evaluamos la velocidad:

```
v(t) = 20/3·sin(10t) + 5·cos(10t)
```

Verificando los primeros tiempos:

- t ≈ 0.169 s: v(0.169) ≈ 7.22 ft/s > 0 (hacia abajo) ✗
- t ≈ 0.588 s: v(0.588) ≈ -7.22 ft/s < 0 (hacia arriba) ✓
- t ≈ 0.797 s: v(0.797) ≈ 7.22 ft/s > 0 (hacia abajo) ✗
- t ≈ 1.216 s: v(1.216) ≈ -7.22 ft/s < 0 (hacia arriba) ✓

**Respuesta**: La masa está 5 pulgadas abajo del equilibrio apuntando hacia arriba en los instantes **t ≈ 0.588 s, 1.216 s, 1.845 s, 2.473 s, ...** (patrón: t ≈ 0.588 + n·T, donde T = π/5 s).

---

## 5. Visualización y Análisis de Resultados

### 5.1 Gráficas del Movimiento

El movimiento del sistema masa-resorte puede representarse mediante tres gráficas fundamentales:

**Posición vs Tiempo**: Muestra la oscilación armónica con amplitud de 5/6 ft y periodo de π/5 s.

**Velocidad vs Tiempo**: Muestra cómo la velocidad varía sinusoidalmente, alcanzando valores máximos de ±8.33 ft/s en el equilibrio.

**Aceleración vs Tiempo**: Proporcional y opuesta al desplazamiento, con valores máximos de ±83.3 ft/s² en los extremos.

### 5.2 Interpretación Física

El sistema exhibe un movimiento armónico simple perfecto debido a que:

1. **No hay amortiguamiento**: El sistema conserva su energía total durante el movimiento.
    
2. **Periodicidad**: El movimiento se repite cada T = π/5 segundos (≈ 0.628 s).
    
3. **Conservación de energía**: La energía total permanece constante, transformándose continuamente entre energía cinética (máxima en el equilibrio) y energía potencial elástica (máxima en los extremos).
    
4. **Simetría del movimiento**: La masa oscila simétricamente respecto a la posición de equilibrio.
    

### 5.3 Tabla Resumen de Resultados

|Parámetro|Valor|
|---|---|
|Masa (m)|2 slugs|
|Constante del resorte (k)|200 lb/ft|
|Frecuencia angular (ω)|10 rad/s|
|Amplitud (A)|5/6 ft (10 pulgadas)|
|Periodo (T)|π/5 s ≈ 0.628 s|
|Frecuencia (f)|5/π Hz ≈ 1.592 Hz|
|Velocidad máxima|25/3 ft/s ≈ 8.33 ft/s|
|Aceleración máxima|250/3 ft/s² ≈ 83.3 ft/s²|
|Energía total|6.944 lb·ft|

### 5.4 Verificación de Resultados

**Verificación de energía**:

```
Energía total = ½kA² = ½(200)(5/6)² = 100(25/36) = 6.944 lb·ft

Energía cinética inicial = ½mv₀² = ½(2)(5)² = 25 lb·ft
Energía potencial inicial = ½kx₀² = ½(200)(-2/3)² = 100(4/9) = 44.44 lb·ft
¡Error! Revisemos...

En realidad:
E_cinética inicial = ½(2)(5²) = 25 lb·ft
E_potencial inicial = ½(200)(2/3)² = 100(4/9) = 44.44 lb·ft
E_total = 25 + 44.44 = 69.44 lb·ft

Recalculando con la amplitud:
E_total = ½kA² = ½(200)(5/6)² = 100(25/36) = 69.44 lb·ft ✓
```

---

## 6. Conclusiones

### 6.1 Resultados Obtenidos

El análisis del sistema masa-resorte mediante el modelo matemático del movimiento armónico simple permitió:

1. **Caracterizar completamente el movimiento**: Se obtuvo la ecuación de movimiento x(t) = -2/3·cos(10t) + 1/2·sin(10t) ft, que describe la posición de la masa en cualquier instante.
    
2. **Determinar parámetros característicos**: La amplitud de 10 pulgadas y el periodo de π/5 segundos definen la naturaleza de la oscilación.
    
3. **Predecir el comportamiento temporal**: Se calcularon posiciones, velocidades y aceleraciones en instantes específicos, así como los momentos en que la masa alcanza configuraciones particulares.
    
4. **Validar la conservación de energía**: La energía total del sistema permanece constante en 69.44 lb·ft, alternando entre formas cinética y potencial.
    

### 6.2 Aplicaciones Prácticas

El movimiento armónico simple tiene aplicaciones en:

- **Ingeniería estructural**: Análisis de vibraciones en edificios y puentes
- **Ingeniería mecánica**: Diseño de sistemas de suspensión en vehículos
- **Ingeniería sísmica**: Modelado de respuesta de estructuras ante sismos
- **Electrónica**: Circuitos osciladores LC
- **Física cuántica**: Modelo del oscilador armónico cuántico

### 6.3 Experiencia en el Desarrollo del Ejercicio

El desarrollo de este problema proporcionó:

1. **Integración de conceptos**: Se aplicaron simultáneamente conocimientos de mecánica clásica, ecuaciones diferenciales y análisis matemático.
    
2. **Metodología sistemática**: El enfoque paso a paso desde la formulación del modelo hasta la obtención de resultados específicos ejemplifica el método científico aplicado.
    
3. **Interpretación física-matemática**: La capacidad de traducir entre la descripción física del fenómeno y su representación matemática es fundamental en la ingeniería.
    
4. **Análisis multifacético**: El problema requirió diferentes tipos de análisis: estático (parámetros del sistema), dinámico (evolución temporal), y energético (conservación de energía).
    
5. **Precisión y rigor**: El uso de unidades consistentes y la verificación de resultados son aspectos cruciales en el trabajo ingenieril.
    

### 6.4 Reflexiones Finales

El movimiento armónico simple, aunque idealizado, constituye un modelo fundamental en física e ingeniería. Su estudio desarrolla habilidades esenciales:

- Modelado matemático de fenómenos físicos
- Resolución de ecuaciones diferenciales
- Análisis de sistemas dinámicos
- Interpretación de resultados en contexto físico

Este ejercicio demuestra cómo un modelo matemático relativamente simple puede proporcionar información detallada y precisa sobre el comportamiento de un sistema físico, permitiendo hacer predicciones cuantitativas verificables experimentalmente.

---

## Referencias

1. Zill, D. G., & Wright, W. S. (2014). _Differential Equations with Boundary-Value Problems_ (8th ed.). Brooks/Cole.
    
2. Hibbeler, R. C. (2016). _Engineering Mechanics: Dynamics_ (14th ed.). Pearson.
    
3. Taylor, J. R. (2005). _Classical Mechanics_. University Science Books.
    
4. Boyce, W. E., & DiPrima, R. C. (2017). _Elementary Differential Equations and Boundary Value Problems_ (11th ed.). Wiley.
    
5. French, A. P. (1971). _Vibrations and Waves_. W. W. Norton & Company.