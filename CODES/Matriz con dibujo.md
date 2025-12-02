```python
  

import numpy as np

import cv2 as cv

  

# Crear imagen de 100x100 píxeles, fondo blanco

img = np.ones((100, 100), dtype=np.uint8) * 255

  

# Cabeza (3x3 píxeles)

img[9:12, 24:27] = 0

img[54:57, 66:72] = 0

  

# Cuerpo (4 píxeles vertical)

img[12:16, 25] = 0

img[57:61, 67]= 0

# Brazos

img[13, 23] = 0

img[13, 27] = 0

img[58, 65] = 0

img[58, 69] = 0

# Piernas

img[16, 24] = 0

img[16, 26] = 0

img[17, 23] = 0

img[17, 27] = 0

img[61, 65] = 0

img[61, 69] = 0

img[62, 64] = 0

img[62, 70] = 0

  

# Mostrar imagen

cv.imshow('MONITOS', img)

cv.waitKey(0)

cv.destroyAllWindows()
```
- Se crea la imagen de 100x100 para que sea de menor tamaño y sea mas fácil de dibujar
- También se usa `[9:12,24:27]` con el fin de cambiar toda esa área de pixeles a color negro
- Se muestra el resultado como un muñeco y otro que esta medio deforme