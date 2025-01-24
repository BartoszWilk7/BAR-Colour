OpenGL 3D Scene Renderer
This project is a 3D scene renderer written in C++ using OpenGL and the Windows API. It demonstrates how to draw 3D primitives, apply colors, handle user input for rotation, and implement basic shading and blending.

Features
Interactive 3D Scene: Rotate the scene using arrow keys.
3D Axes: Displays X, Y, and Z axes for spatial orientation.
Colored Bars: Two bars with gradient coloring using gamma correction.
3D Cubes: A cube rendered with multicolored faces, demonstrating flat and smooth shading.
Blending and Transparency: Basic blending is implemented to enhance the visual appearance.
Code Overview
1. Main Components
The code is structured into the following key components:

Window Setup: Initializes a Win32 window for OpenGL rendering.
OpenGL Context: Sets up an OpenGL rendering context.
Drawing Functions: Renders 3D primitives and gradients in the scene.
Input Handling: Responds to arrow keys to rotate the 3D scene.
2. Key Functions
1. DrawScene
This function is the core rendering function. It draws the 3D scene, including the axes, colored bars, and cube.


void DrawScene(GLfloat xRot, GLfloat yRot)
Parameters:
xRot: Rotation angle around the X-axis.
yRot: Rotation angle around the Y-axis.
Description:
Clears the screen and depth buffer.
Applies rotations to the scene.
Draws 3D axes as lines.
Draws two gradient-colored bars using GL_QUAD_STRIP.
Renders a cube with each face having a unique color.
2. SetMyPixelFormat
This function sets up the pixel format for the OpenGL rendering context.


void SetMyPixelFormat(HDC hdc)
Description:
Configures the color depth (cColorBits) and depth buffer (cDepthBits).
Enables double-buffering for smooth rendering.
3. ResizeWindow
Handles resizing of the window and adjusts the viewport and projection accordingly.


void ResizeWindow(int width, int height)
Description:
Ensures the viewport matches the new window size.
Sets up an orthographic projection using glOrtho.
Enables depth testing for proper 3D rendering.
4. WndProc
The main window procedure handles messages from the operating system.


LRESULT CALLBACK WndProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam)
Key Features:
Handles keyboard input for rotating the scene.
Resizes the viewport on window resize.
Calls DrawScene to render the 3D objects on the screen.
5. WinMain
The entry point of the program.


int APIENTRY WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPTSTR lpCmdLine, int nCmdShow)
Description:
Registers the window class.
Creates the main application window.
Enters the message loop to handle user input and rendering.
3. How the Scene is Rendered
Axes
Drawn as three white lines along the X, Y, and Z axes to help orient the viewer in 3D space:


glBegin(GL_LINES);
glColor3f(1, 1, 1);
glVertex3f(10, 0, 0); glVertex3f(-10, 0, 0); // X-axis
glVertex3f(0, 10, 0); glVertex3f(0, -10, 0); // Y-axis
glVertex3f(0, 0, 10); glVertex3f(0, 0, -10); // Z-axis
glEnd();
Gradient Bars
Two horizontal bars with gradient coloring are drawn using GL_QUAD_STRIP. Gamma correction is applied to the second bar.


glBegin(GL_QUAD_STRIP);
for (i = 0; i <= 10; i++) {
    glColor3f(pow(0.4 * (GLfloat)i, gamma), pow(0.4 * (GLfloat)i, gamma), 0); // Gamma correction
    glVertex3f(-5 + (GLfloat)i, -7, 6); glVertex3f(-5 + (GLfloat)i, -4, 6);
}
glEnd();
Cube
A cube is drawn with each face having a unique color. It demonstrates the use of GL_QUADS for creating a solid 3D object:


glBegin(GL_QUADS);
glColor3f(1, 0, 0); glVertex3f(3, -3, -3); // Red face
glColor3f(0, 1, 0); glVertex3f(-3, 3, -3); // Green face
// Other faces follow similarly
glEnd();
How to Use
Prerequisites
Windows OS
A C++ compiler that supports OpenGL (e.g., MinGW, MSVC)
OpenGL and GLUT libraries
Build Instructions
Clone this repository:
git clone https://github.com/yourusername/opengl-3d-scene-renderer.git
cd opengl-3d-scene-renderer
Compile the code using your preferred compiler. For example:

bash
g++ -o scene_renderer main.cpp -lopengl32 -lglu32
Run the executable:

bash
./scene_renderer
Controls
Arrow Keys: Rotate the 3D scene around X and Y axes.
