
==QUE SON LAS ECUACIONES PARAMETRICAS?==

Las ecuaciones paramétricas son un método para representar curvas, trayectorias o superficies mediante una variable independiente llamada **parámetro** (usualmente t). En lugar de relacionar directamente las coordenadas entre sí (como y=f(x) y=f(x)), cada coordenada se define individualmente en función del mismo parámetro:

x=f(t)         y=g(t)   (y en 3D también z=h(t)).

Esto permite describir movimientos complejos, trayectorias cerradas, figuras geométricas y comportamientos dinámicos que serían difíciles de expresar con una sola ecuación. El parámetro t suele interpretarse como tiempo, ángulo o cualquier magnitud que controle el recorrido a lo largo de la curva.

==10 ecuaciones paramétricas simples 
==
```python
import cv2
import numpy as np

# Tamaño de la imagen
alto, ancho = 600, 600
# Variable t puede ser modificado para alterar las curvas
t = np.linspace(0, 2*np.pi, 500)

def ecuaciones(t):
    curvas = []
    # Cada curva se tiene que ajustar si no se me sale del cuadro
    
    # 1.- Círculo (radio ajustado)
    curvas.append( (np.cos(t)*150 + 300, np.sin(t)*150 + 300) )
    
    # 2.- Elipse (más ancha)
    curvas.append( (3*np.cos(t)*80 + 300, np.sin(t)*120 + 300) )
    
    # 3.- Lemniscata (más pequeña para que quede mejor)
    curvas.append( (np.cos(t)/(1+np.sin(t)**2)*100 + 300, 
                    np.cos(t)*np.sin(t)/(1+np.sin(t)**2)*100 + 300) )
    
    # 4.- Figura tipo estrella (hipocicloide modificado)
    curvas.append( (np.sin(2*t)*130 + 300, np.sin(4*t)*130 + 300) )
    
    # 5.- Figura circular con oscilaciones
    curvas.append( (np.cos(t)*(100 + 30*np.cos(5*t)) + 300, 
                    np.sin(t)*(100 + 30*np.sin(5*t)) + 300) )
    
    # 6.- Onda senoidal circular
    curvas.append( ((200 + 50*np.sin(3*t)) * np.cos(t) + 300, 
                    (200 + 50*np.sin(3*t)) * np.sin(t) + 300) )
    
    # 7.- Figura cuadrada aproximada
    curvas.append( (np.cos(t) + 0.2*np.cos(5*t) + 0.1*np.cos(9*t))*120 + 300, 
                   (np.sin(t) + 0.2*np.sin(5*t) + 0.1*np.sin(9*t))*120 + 300 )
    
    # 8.- Espiral simple
    curvas.append( (t/np.pi * np.cos(t)*50 + 300, t/np.pi * np.sin(t)*50 + 300) )
    
    # 9.- Curva con simetría horizontal
    curvas.append( (np.sin(t)*180 + 300, np.sin(2*t)*np.cos(t)*180 + 300) )
    
    # 10.- Figura tipo flor de 8 pétalos
    curvas.append( (np.cos(2*t)*np.cos(t)*180 + 300, np.cos(2*t)*np.sin(t)*180 + 300) )
    
    return curvas

curvas = ecuaciones(t)

# dibuja cada curva en su propia ventana
for idx, (x_vals, y_vals) in enumerate(curvas):
    img = np.ones((alto, ancho, 3), dtype=np.uint8) * 255
    
    # Asegura que queden dentro y no se salga a sus anchas
    x_pts = np.clip(np.array(x_vals, dtype=np.int32), 0, ancho-1)   
    y_pts = np.clip(np.array(y_vals, dtype=np.int32), 0, alto-1)

    # Dibujar puntos de referencia (centro y ejes)
    cv2.circle(img, (300, 300), 3, (200, 200, 200), -1)
    cv2.line(img, (300, 0), (300, 600), (230, 230, 230), 1)
    cv2.line(img, (0, 300), (600, 300), (230, 230, 230), 1)
    
    # Dibujar la curva
    for i in range(len(x_pts)-1):
        # Usar color diferente para cada curva
        color = (idx*25 % 255, idx*50 % 255, idx*75 % 255)
        cv2.line(img, (x_pts[i], y_pts[i]), (x_pts[i+1], y_pts[i+1]), color, 2)
    
    # Añadir número de curva
    cv2.putText(img, f"Curva {idx+1}", (20, 40), 
                cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0, 0, 0), 2)
    
    cv2.imshow(f"Curva {idx+1}", img)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

# Explicación del código

Dibuja 10 curvas matemáticas diferentes en ventanas separadas usando ecuaciones paramétricas.

En el código cree 10 imágenes de fondo blanco donde se aplica una ecuacion 
donde cada una tiene la siguiente formula 
```python
x = f(t) + 300  # +300 centra en la imagen
y = g(t) + 300
```
Ejemplo: 

- Círculo: `cos(t)*150`, `sin(t)*150`
    
- Elipse: `3*cos(t)*80`, `sin(t)*120`
    
- Lemniscata (forma ∞): fórmula especial
	
utilizando este modelo para procesar np.clip de forma segura y con la ayuda que crea ejes de referencia.