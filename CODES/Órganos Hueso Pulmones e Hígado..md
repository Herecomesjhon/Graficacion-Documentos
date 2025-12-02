El programa mostrará una ventana con tres figuras 3D (ojo, hueso y riñón) que rotan continuamente con iluminación básica.

El código implementa un sistema de visualización tridimensional que renderiza modelos anatómicos estilizados en tiempo real utilizando tecnologías clásicas de gráficos por computadora.

El programa emplea OpenGL como núcleo gráfico utilizando su pipeline de renderizado fijo con funciones de modo inmediato como glBegin y glVertex para definir geometrías básicas La capa GLU.

``` PYTHON
import glfw

from OpenGL.GL import *

from OpenGL.GLU import *

import math

  

rotation = 0.0

quad = None  # Declarar globalmente

  

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

  

def init_quadric():

    global quad

    quad = gluNewQuadric()

    if quad is None:

        print("Error: No se pudo crear el quadric object")

    else:

        gluQuadricNormals(quad, GLU_SMOOTH)

        gluQuadricTexture(quad, GL_TRUE)

  

def draw_eye():

    """Dibuja dos esferas simples"""

    glPushMatrix()

    # Primera esfera (roja) a la izquierda

    glColor3f(0.85, 0.67, 0.65)  # Rojo

    glPushMatrix()

    glTranslatef(0.7, 0, 0)

    draw_sphere(0.54, 30, 30)

    glPopMatrix()

  

    glColor3f(1, 1, 1)  # Blanco

    glPushMatrix()

    glTranslatef(0.56, 0, 0)

    draw_sphere(0.6, 30, 30)

    glPopMatrix()

    # Segunda esfera (azul) a la derecha

    glColor3f(0.84, 0.85, 0.92)  # Azul

    glPushMatrix()

    glTranslatef(0.49, 0, 0)

    draw_sphere(0.55, 30, 30)

    glPopMatrix()

  

    glColor3f(0, 0, 0)  # Negro

    glPushMatrix()

    glTranslatef(0.3, 0, 0)

    draw_sphere(0.4, 30, 30)

    glPopMatrix()

  

    glPopMatrix()

  

def draw_hueso():

    global quad  # Importante: usar el quadric global

    if quad is None:

        print("Error: quad no inicializado")

        return

    glPushMatrix()

    glColor3f(1.0, 0.95, 0.85)  # color hueso o blanco pero bonito

    glPushMatrix()

    glRotatef(-90, 1, 0, 0)

    glTranslatef(0, 0, -1)

    gluCylinder(quad, 0.2, 0.2, 2.0, 30, 30)  # Usa el objeto quad

    glPopMatrix()

  

    glPushMatrix()

    glTranslatef(0, -1.0, 0.2)

    draw_sphere(0.3, 30, 30)

    glPopMatrix()

  

    glPushMatrix()

    glTranslatef(0, -1.0, -0.2)

    draw_sphere(0.3, 30, 30)

    glPopMatrix()

  

    glPushMatrix()

    glTranslatef(0, 1.0, 0.2)

    draw_sphere(0.35, 30, 30)

    glPopMatrix()

  

    glPushMatrix()

    glTranslatef(0, 1.0, -0.2)

    draw_sphere(0.35, 30, 30)

    glPopMatrix()

    glPopMatrix()

  

def draw_riñon():

    glPushMatrix()

    glColor3f(0.65, 0.20, 0.22)

    glPushMatrix()

    glTranslatef(0, 1, 0.2)

    draw_sphere(0.3, 30, 30)

    glPopMatrix()

  

    glPushMatrix()

    glTranslatef(0, 0.65, -0.2)

    draw_sphere(0.35, 30, 30)

    glPopMatrix()

  

    glPushMatrix()

    glTranslatef(0, 0.35, -0.2)

    draw_sphere(0.35, 30, 30)

    glPopMatrix()

  

    glPushMatrix()

    glTranslatef(0, 0, 0.2)

    draw_sphere(0.3, 30, 30)

    glPopMatrix()

    glPopMatrix()

  

def setup_lighting():

    glEnable(GL_LIGHTING)

    glEnable(GL_LIGHT0)

    glEnable(GL_DEPTH_TEST)

    glEnable(GL_COLOR_MATERIAL)

    glColorMaterial(GL_FRONT_AND_BACK, GL_AMBIENT_AND_DIFFUSE)

    light_position = [1.0, 1.0, 1.0, 0.0]  # Cambié a 0.0 (direccional)

    light_diffuse = [1.0, 1.0, 1.0, 1.0]

    light_ambient = [0.2, 0.2, 0.2, 1.0]

    glLightfv(GL_LIGHT0, GL_POSITION, light_position)

    glLightfv(GL_LIGHT0, GL_DIFFUSE, light_diffuse)

    glLightfv(GL_LIGHT0, GL_AMBIENT, light_ambient)

    glEnable(GL_NORMALIZE)

  

def main():

    global rotation, quad

    if not glfw.init():

        print("Error al inicializar GLFW")

        return

  

    window = glfw.create_window(800, 600, "Dos Esferas Simples", None, None)

    if not window:

        glfw.terminate()

        print("Error al crear ventana")

        return

  

    glfw.make_context_current(window)

    glfw.swap_interval(1)  # VSync

  

    glClearColor(0.54, 0.72, 0.84, 1.0)

    setup_lighting()

    init_quadric()

  

    while not glfw.window_should_close(window):

        width, height = glfw.get_framebuffer_size(window)

        glViewport(0, 0, width, height)

        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)

        # Configurar proyección

        glMatrixMode(GL_PROJECTION)

        glLoadIdentity()

        aspect = width / height if height > 0 else 1.0

        gluPerspective(45, aspect, 0.1, 100.0)

        # Configurar vista

        glMatrixMode(GL_MODELVIEW)

        glLoadIdentity()

        gluLookAt(0, 0, 5, 0, 0, 0, 0, 1, 0)

        # Rotar la escena

        glPushMatrix()

        rotation += 0.5

        glRotatef(rotation, 0, 1, 0)

        # Dibujar objetos

        draw_eye()

        glPushMatrix()

        glTranslatef(2, 0, 0)

        draw_hueso()

        glPopMatrix()

  

        glPushMatrix()

        glTranslatef(-3, -0.5, 0)

        draw_riñon()

        glPopMatrix()

        glPopMatrix()

  

        glfw.swap_buffers(window)

        glfw.poll_events()

  

    if quad:

        gluDeleteQuadric(quad)

    glfw.terminate()

  

if __name__ == "__main__":

    main()
```
