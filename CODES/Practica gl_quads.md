En esta practica creo una esfera con opengl.glu 
El código crea y dibuja una esfera tridimensional que gira y cambia de colores continuamente

Para que la esfera cambie de colores se calcula el color de cada vértice basándose en sus coordenadas espaciales usando la fórmula glColor3f((x + 1) / 2, (y + 1) / 2, (z + 1) / 2) donde x, y y z son las coordenadas de cada punto de la esfera esto convierte las coordenadas que van de -1 a 1 a valores entre 0 y 1 creando un gradiente de color que depende de la posición de cada vértice en la esfera la esfera gira constantemente con glRotatef actualizando angulo_rotacion en cada cuadro lo que hace que los colores parezcan moverse y cambiar ya que las coordenadas de los vértices cambian su posición relativa en el espacio y por tanto su color asignado
``` PYTHON
from OpenGL.GL import *
from OpenGL.GLU import *
from OpenGL.GLUT import *

import math

import sys

  

# Variables globales

angulo_rotacion = 0
def esfera_quad(radio=1.0, segmentos_lat=20, segmentos_long=20):

    """

    Crea una esfera usando GL_QUADS

    """

    glBegin(GL_QUADS)

    for i in range(segmentos_lat):

        for j in range(segmentos_long):

            # Calcular los 4 vértices del cuadrilátero

            for k in range(4):

                if k == 0:  # Vértice superior izquierdo

                    theta = i * math.pi / segmentos_lat

                    phi = j * 2 * math.pi / segmentos_long

                elif k == 1:  # Vértice superior derecho

                    theta = i * math.pi / segmentos_lat

                    phi = (j + 1) * 2 * math.pi / segmentos_long

                elif k == 2:  # Vértice inferior derecho

                    theta = (i + 1) * math.pi / segmentos_lat

                    phi = (j + 1) * 2 * math.pi / segmentos_long

                else:  # Vértice inferior izquierdo

                    theta = (i + 1) * math.pi / segmentos_lat

                    phi = j * 2 * math.pi / segmentos_long

                # Convertir coordenadas esféricas a cartesianas

                x = radio * math.sin(theta) * math.cos(phi)

                y = radio * math.cos(theta)

                z = radio * math.sin(theta) * math.sin(phi)

                # Asignar color basado en la posición

                glColor3f((x + 1) / 2, (y + 1) / 2, (z + 1) / 2)

                glVertex3f(x, y, z)

    glEnd()

  

def dibujar():

    global angulo_rotacion

    # Limpiar buffers

    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)

    glLoadIdentity()

    # Posicionar cámara

    gluLookAt(0, 0, 5,    # posición de la cámara

              0, 0, 0,    # punto al que mira

              0, 1, 0)    # vector arriba

    # Rotar la esfera

    glRotatef(angulo_rotacion, 1, 1, 0.5)

    angulo_rotacion += 1

    # Dibujar esfera

    esfera_quad(radio=1.0, segmentos_lat=25, segmentos_long=25)

    # Intercambiar buffers

    glutSwapBuffers()

  

def redimensionar(ancho, alto):

    # Configurar viewport

    glViewport(0, 0, ancho, alto)

    # Configurar proyección

    glMatrixMode(GL_PROJECTION)

    glLoadIdentity()

    gluPerspective(45, ancho/alto, 0.1, 50.0)

    # Volver al modo de vista de modelo

    glMatrixMode(GL_MODELVIEW)

  

def teclado(tecla, x, y):

    # Salir con ESC o 'q'

    if tecla == b'\x1b' or tecla == b'q':  # ESC o Q

        sys.exit()

  

def inicializar():

    # Configurar fondo

    glClearColor(0.1, 0.1, 0.1, 1.0)  # Gris oscuro

    # Habilitar depth testing

    glEnable(GL_DEPTH_TEST)

    # Configurar suavizado

    glEnable(GL_LINE_SMOOTH)

    glEnable(GL_POLYGON_SMOOTH)

    glHint(GL_LINE_SMOOTH_HINT, GL_NICEST)

    glHint(GL_POLYGON_SMOOTH_HINT, GL_NICEST)

  

def timer(valor):

    # Forzar redibujado

    glutPostRedisplay()

    glutTimerFunc(16, timer, 0)  # ~60 FPS

  

def main():

    # Inicializar GLUT

    glutInit(sys.argv)

    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH)

    glutInitWindowSize(800, 600)

    glutInitWindowPosition(100, 100)

    glutCreateWindow(b"Esfera con GL_QUADS - Sin Pygame")

    # Configurar callbacks

    inicializar()

    glutDisplayFunc(dibujar)

    glutReshapeFunc(redimensionar)

    glutKeyboardFunc(teclado)

    glutTimerFunc(0, timer, 0)

    # Entrar al loop principal

    print("Controles:")

    print("- ESC o Q: Salir")

    print("- La esfera rota automáticamente")

    glutMainLoop()

  

if __name__ == "__main__":

    main()
``` 
*El código usa OpenGL para renderizar la esfera calculando sus vértices con coordenadas esféricas segmentos_lat y segmentos_long determinan la suavidad de la esfera y se configura un bucle de animación con timer que redibuja la escena aproximadamente 60 veces por segundo creando la animación fluida de rotación y cambio de colores*