# Manos Unión
Este programa utiliza la cámara web para detectar manos en tiempo real usando MediaPipe y OpenCV.
``` python
import cv2

import mediapipe as mp

import math

  

# Inicializar MediaPipe Hands

mp_hands = mp.solutions.hands

mp_drawing = mp.solutions.drawing_utils

hands = mp_hands.Hands(min_detection_confidence=0.5, min_tracking_confidence=0.5)

  

# Captura de video

cap = cv2.VideoCapture(0)

  

while cap.isOpened():

    ret, frame = cap.read()

    if not ret:

        break

  

    # Convertir imagen a RGB

    frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

    # Detectar manos

    results = hands.process(frame_rgb)

  

    # Lista para almacenar las coordenadas de los dedos índices

    index_fingers = []

  

    # Dibujar los puntos clave y conexiones

    if results.multi_hand_landmarks:

        for hand_landmarks in results.multi_hand_landmarks:

            # Dibujar puntos y conexiones

            mp_drawing.draw_landmarks(frame, hand_landmarks, mp_hands.HAND_CONNECTIONS)

            # Obtener coordenada del dedo índice (punto 8)

            h, w, _ = frame.shape

            index_finger_tip = hand_landmarks.landmark[mp_hands.HandLandmark.INDEX_FINGER_TIP]

            x_index = int(index_finger_tip.x * w)

            y_index = int(index_finger_tip.y * h)

            # Almacenar coordenadas del dedo índice

            index_fingers.append((x_index, y_index))

            # También puedes dibujar un círculo más grande en el dedo índice para destacarlo

            cv2.circle(frame, (x_index, y_index), 8, (0, 255, 0), -1)

  

    # Dibujar línea entre los dedos índices si hay exactamente 2 manos detectadas

    if len(index_fingers) == 2:

        # Obtener coordenadas de ambos dedos índices

        x1, y1 = index_fingers[0]

        x2, y2 = index_fingers[1]

        # Dibujar línea entre los dedos índices

        cv2.line(frame, (x1, y1), (x2, y2), (0, 0, 255), 3)

        # Calcular y mostrar distancia entre los dedos

        distance = math.sqrt((x2 - x1)**2 + (y2 - y1)**2)

        cv2.putText(frame, f"Distancia: {int(distance)}px",

                   (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 255, 255), 2)

  

    # Mostrar la imagen

    cv2.imshow("Salida", frame)

  

    # Salir con 'q'

    if cv2.waitKey(1) & 0xFF == ord('q'):

        break

  

cap.release()

cv2.destroyAllWindows()
```

## Mediapipe Detección
Este bloque de código hace esto hace la función para que mediapipe funcione y detecte manos en tiempo real.
``` PYTHON

# Inicializar MediaPipe Hands

mp_hands = mp.solutions.hands

mp_drawing = mp.solutions.drawing_utils

hands = mp_hands.Hands(min_detection_confidence=0.5, min_tracking_confidence=0.5)

```
# Captura de video
En esta parte captura la cámara web 

``` PYTHON
cap = cv2.VideoCapture(0)

  

while cap.isOpened():

    ret, frame = cap.read()

    if not ret:

        break
```


## Convertir IMG a RGB y Dibujar conexiones
En esta parte ya se configura la parte de dibujar los puntos en las manos y 

``` PYTHON
if results.multi_hand_landmarks:

        for hand_landmarks in results.multi_hand_landmarks:

            # Dibujar puntos y conexiones

            mp_drawing.draw_landmarks(frame, hand_landmarks, mp_hands.HAND_CONNECTIONS)

            # Obtener coordenada del dedo índice (punto 8)

            h, w, _ = frame.shape

            index_finger_tip = hand_landmarks.landmark[mp_hands.HandLandmark.INDEX_FINGER_TIP]

            x_index = int(index_finger_tip.x * w)

            y_index = int(index_finger_tip.y * h)

            # Almacenar coordenadas del dedo índice

            index_fingers.append((x_index, y_index))

            # También puedes dibujar un círculo más grande en el dedo índice para destacarlo

            cv2.circle(frame, (x_index, y_index), 8, (0, 255, 0), -1)

  

    # Dibujar línea entre los dedos índices si hay exactamente 2 manos detectadas

    if len(index_fingers) == 2:

        # Obtener coordenadas de ambos dedos índices

        x1, y1 = index_fingers[0]

        x2, y2 = index_fingers[1]

        # Dibujar línea entre los dedos índices

        cv2.line(frame, (x1, y1), (x2, y2), (0, 0, 255), 3)

        # Calcular y mostrar distancia entre los dedos

        distance = math.sqrt((x2 - x1)**2 + (y2 - y1)**2)

        cv2.putText(frame, f"Distancia: {int(distance)}px",

                   (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 255, 255), 2)

```

