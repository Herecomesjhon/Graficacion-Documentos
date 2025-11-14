``` PYTHON
import glfw

from OpenGL.GL import *

from OpenGL.GLU import *

import math

  

rotation = 0.0

  

def draw_sphere(radius, slices=30, stacks=30):

    """Dibuja una esfera usando primitivas OpenGL (sin GLUT)"""

    for i in range(stacks):

        lat1 = math.pi * (-0.5 + i / stacks)

        lat2 = math.pi * (-0.5 + (i + 1) / stacks)

        glBegin(GL_QUAD_STRIP)

        for j in range(slices + 1):

            lng = 2 * math.pi * j / slices

            x1 = math.cos(lat1) * math.cos(lng)

            y1 = math.sin(lat1)

            z1 = math.cos(lat1) * math.sin(lng)

            x2 = math.cos(lat2) * math.cos(lng)

            y2 = math.sin(lat2)

            z2 = math.cos(lat2) * math.sin(lng)

            glNormal3f(x1, y1, z1)

            glVertex3f(x1 * radius, y1 * radius, z1 * radius)

            glNormal3f(x2, y2, z2)

            glVertex3f(x2 * radius, y2 * radius, z2 * radius)

        glEnd()

  

def draw_eye(x_offset=0):

    """Dibuja un ojo con offset en X para posicionarlo"""

    glPushMatrix()

    glTranslatef(x_offset, 0, 0)  # Mover todo el ojo a la posición deseada

    # Primera esfera (color piel)

    glColor3f(0.85, 0.67, 0.65)

    glPushMatrix()

    glTranslatef(0.5, 0, 0)

    draw_sphere(0.54, 30, 30)

    glPopMatrix()

  

    # Esfera blanca

    glColor3f(1, 1, 1)

    glPushMatrix()

    glTranslatef(0.36, 0, 0)

    draw_sphere(0.6, 30, 30)

    glPopMatrix()

    # Iris

    glColor3f(0.84, 0.85, 0.92)

    glPushMatrix()

    glTranslatef(0.29, 0, 0)

    draw_sphere(0.55, 30, 30)

    glPopMatrix()

  

    # Pupila

    glColor3f(0, 0, 0)

    glPushMatrix()

    glTranslatef(0.1, 0, 0)

    draw_sphere(0.4, 30, 30)

    glPopMatrix()

  

    glPopMatrix()

  

def setup_lighting():

    """Configura iluminación básica"""

    glEnable(GL_LIGHTING)

    glEnable(GL_LIGHT0)

    glEnable(GL_DEPTH_TEST)

    glEnable(GL_COLOR_MATERIAL)

    light_position = [1.0, 1.0, 1.0, 0.2]

    glLightfv(GL_LIGHT0, GL_POSITION, light_position)

  

def main():

    global rotation

    if not glfw.init():

        return

  

    window = glfw.create_window(800, 600, "Dos Ojos Rotando", None, None)

    if not window:

        glfw.terminate()

        return

  

    glfw.make_context_current(window)

  

    glClearColor(0.54, 0.72, 0.84, 1.0)

    setup_lighting()

  

    while not glfw.window_should_close(window):

        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)

        glMatrixMode(GL_PROJECTION)

        glLoadIdentity()

        gluPerspective(45, 800/600, 0.1, 100.0)

        glMatrixMode(GL_MODELVIEW)

        glLoadIdentity()

        glTranslatef(0, 0, -5)

        # Rotar la escena

        rotation += 0.5

        glRotatef(rotation, 0, 1, 0)

        # Dibujar dos ojos - uno a cada lado

        draw_eye(-1.5)  # Ojo izquierdo

        draw_eye(1.5)   # Ojo derecho

        glfw.swap_buffers(window)

        glfw.poll_events()

  

    glfw.terminate()

  

if __name__ == "__main__":

    main()
``` 