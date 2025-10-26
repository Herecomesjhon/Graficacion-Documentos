## Mediapipe Detección
Este bloque de código hace esto hace la función para que mediapipe funcione y detecte manos en tiempo real.
``` PYTHON
import cv2 as cv


img_original = cv.imread('img.jpg')
if img_original is None:

    print("Error: No se pudo cargar 'img.jpg'")

exit()
cv.imshow('Imagen Original', img_original)

  

x, y, canales = img_original.shape  # Ahora son 3 dimensiones

print(f"Dimensiones: {img_original.shape}, Alto: {x}, Ancho: {y}, Canales: {canales}")


# 1. NEGATIVO EN COLOR

img1 = img_original.copy()

for i in range(x):

    for j in range(y):

        for c in range(canales):  # Procesar cada canal BGR

            img1[i,j,c] = 255 - img1[i,j,c]

cv.imshow('1. Negativo Color', img1)

  

# 2. UMBRAL EN COLOR (convertir a grises primero)

img2_gris = cv.cvtColor(img_original, cv.COLOR_BGR2GRAY)  # Convertir a grises

img2 = img_original.copy()

for i in range(x):

    for j in range(y):

        if img2_gris[i,j] > 128:  # Usar el valor de grises para decidir

            img2[i,j] = [255, 255, 255]  # Blanco en BGR

        else:

            img2[i,j] = [0, 0, 0]  # Negro en BGR

cv.imshow('2. Umbral Binario Color', img2)

  

# 3. CORRECCIÓN GAMMA EN COLOR

img3 = img_original.copy()

gamma = 2.0

for i in range(x):

    for j in range(y):

        for c in range(canales):

            normalized = img3[i,j,c] / 255.0

            corrected = pow(normalized, gamma)

            img3[i,j,c] = int(corrected * 255)

cv.imshow('3. Correccion Gamma Color', img3)

  

# 4. ECUALIZACIÓN EN COLOR (ecualizar cada canal por separado)

img4 = img_original.copy()

for c in range(canales):

    canal = img4[:,:,c]  # Extraer canal individual

    hist = [0] * 256

    # Calcular histograma del canal

    for i in range(x):

        for j in range(y):

            hist[canal[i,j]] += 1

    # Calcular distribución acumulativa

    cumulative = [0] * 256

    cumulative[0] = hist[0]

    for i in range(1, 256):

        cumulative[i] = cumulative[i-1] + hist[i]

    # Aplicar ecualización al canal

    total_pixels = x * y

    for i in range(x):

        for j in range(y):

            pixel_val = canal[i,j]

            new_val = int((cumulative[pixel_val] / total_pixels) * 255)

            img4[i,j,c] = new_val

cv.imshow('4. Ecualizacion Color', img4)

  

# 5. REALCE DE BORDES EN COLOR

img5 = img_original.copy()

kernel = [[-1, -1, -1],

          [-1,  9, -1],

          [-1, -1, -1]]

  

for c in range(canales):  # Aplicar a cada canal

    canal = img5[:,:,c]

    for i in range(1, x-1):

        for j in range(1, y-1):

            suma = 0

            for ki in range(3):

                for kj in range(3):

                    suma += canal[i+ki-1, j+kj-1] * kernel[ki][kj]

            img5[i,j,c] = max(0, min(255, suma))

cv.imshow('5. Realce de Bordes Color', img5)

  

print("Presiona cualquier tecla para cerrar las ventanas...")

cv.waitKey(0)

cv.destroyAllWindows()
```


# Operadores Puntuales
en esta parte se agregan los operadores para transmitir en las imágenes haciendo que en la imagen se haga un cambio de color  cambiando los canales del BGR o la natividad de la imagen original.

En el quinto filtro se agrega un kernel del tema del los kernel jugando con la matriz para hacer un cambio en la imagen basica
```python

# 1. NEGATIVO EN COLOR

img1 = img_original.copy()

for i in range(x):

    for j in range(y):

        for c in range(canales):  # Procesar cada canal BGR

            img1[i,j,c] = 255 - img1[i,j,c]

cv.imshow('1. Negativo Color', img1)

  

# 2. UMBRAL EN COLOR (convertir a grises primero)

img2_gris = cv.cvtColor(img_original, cv.COLOR_BGR2GRAY)  # Convertir a grises

img2 = img_original.copy()

for i in range(x):

    for j in range(y):

        if img2_gris[i,j] > 128:  # Usar el valor de grises para decidir

            img2[i,j] = [255, 255, 255]  # Blanco en BGR

        else:

            img2[i,j] = [0, 0, 0]  # Negro en BGR

cv.imshow('2. Umbral Binario Color', img2)

  

# 3. CORRECCIÓN GAMMA EN COLOR

img3 = img_original.copy()

gamma = 2.0

for i in range(x):

    for j in range(y):

        for c in range(canales):

            normalized = img3[i,j,c] / 255.0

            corrected = pow(normalized, gamma)

            img3[i,j,c] = int(corrected * 255)

cv.imshow('3. Correccion Gamma Color', img3)

  

# 4. ECUALIZACIÓN EN COLOR (ecualizar cada canal por separado)

img4 = img_original.copy()

for c in range(canales):

    canal = img4[:,:,c]  # Extraer canal individual

    hist = [0] * 256

    # Calcular histograma del canal

    for i in range(x):

        for j in range(y):

            hist[canal[i,j]] += 1

    # Calcular distribución acumulativa

    cumulative = [0] * 256

    cumulative[0] = hist[0]

    for i in range(1, 256):

        cumulative[i] = cumulative[i-1] + hist[i]

    # Aplicar ecualización al canal

    total_pixels = x * y

    for i in range(x):

        for j in range(y):

            pixel_val = canal[i,j]

            new_val = int((cumulative[pixel_val] / total_pixels) * 255)

            img4[i,j,c] = new_val

cv.imshow('4. Ecualizacion Color', img4)

  

# 5. REALCE DE BORDES EN COLOR

img5 = img_original.copy()

kernel = [[-1, -1, -1],

          [-1,  9, -1],

          [-1, -1, -1]]

  

```

# Imprimir las IMG
ya en esta parte se agrega en el Recorre cada canal de color individualmente (Blue, Green, Red). Extrae un solo canal a la vez para procesarlo por separado.
```python
for c in range(canales):  # Aplicar a cada canal

    canal = img5[:,:,c]

    for i in range(1, x-1):

        for j in range(1, y-1):

            suma = 0

            for ki in range(3):

                for kj in range(3):

                    suma += canal[i+ki-1, j+kj-1] * kernel[ki][kj]

            img5[i,j,c] = max(0, min(255, suma))

cv.imshow('5. Realce de Bordes Color', img5)
```
Aplica el kernel 3x3 al píxel actual y sus 8 vecinos
`i+ki-1, j+kj-1`: Accede a los píxeles vecinos (arriba, abajo, izquierda, derecha y diagonales)
Multiplica cada píxel vecino por el valor correspondiente del kernel.