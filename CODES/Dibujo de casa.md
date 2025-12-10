```python
import cv2 as cv

import numpy as np

  

# Crear una imagen blanca (fondo)

img = np.ones((500, 500, 3), np.uint8) * 255

  

# Casa en general

cv.rectangle(img, (150, 250), (350, 450), (179, 222, 245), -1)

  

# Puerta - marrón

cv.rectangle(img, (230, 350), (270, 450), (33, 67, 101), -1)

  

# Ventana izquierda - ámbar  

cv.rectangle(img, (170, 280), (210, 320), (91, 114, 226), -1)

# Borde negro ventana izquierda

cv.rectangle(img, (170, 280), (210, 320), (0, 0, 0), 2)

  

# Ventana derecha - terracota

cv.rectangle(img, (290, 280), (330, 320), (91, 114, 226), -1)

# Borde negro ventana derecha

cv.rectangle(img, (290, 280), (330, 320), (0, 0, 0), 2)

  

# Techo - teja

puntos_triangulo = np.array([[150, 250], [350, 250], [250, 150]], np.int32)

cv.fillPoly(img, [puntos_triangulo], (34, 34, 178))

  

# Mostrar la imagen

cv.imshow('Casa dibujo', img)

cv.waitKey(0)

cv.destroyAllWindows()
```

Se crea un dibujo usando cuadrados de diferentes tamaños para hacer el diseño de la puerta y ventanas.

# Techo Casa

Para hacer el techo de la casa utilizamos la fillpoly que nos permite crear un polígono y rellenarlo del color que nosotros necesitemos.