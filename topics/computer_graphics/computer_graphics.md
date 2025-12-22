# Computer graphics fundamentals

<br>![computer graphics image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/computer_graphics.jpg)

## Table of Contents
+ [References](#references)
+ [Basics](#basics)
  + [Definitions](#definitions)
  + [Graphics pipeline](#graphics-pipeline)
  + [Coordinate systems and transformations](#coordinates-systems-and-transformations)
  + [Vertex data](#vertex-data)
  + [GLSL](#glsl)
  + [Depth testing](#depth-testing)
+ [Textures](#textures)
+ [Algebra](#algebra)
+ [Camera](#camera)
+ [Lighting](#lighting)
  + [Basics](#basics)
  + [Normals](#normals)
  + [Phong lighting model](#phong-lighting-model)
  + [Blinn-Phong lighting model](#blinn-phong-lighting-model)
  + [Materials](#materials)
  + [Light casters](#light-casters)
  + [Gamma correction](#gamma-correction)
  + [Shadow](#shadow)
  + [Normal/Bump mapping](#normal/bump-mapping)
  + [Parallax mapping](#parallax-mapping)
  + [HDR](#hdr)
  + [Bloom](#bloom)
  + [Deferred shading](#deferred-shading)
  + [SSAO](#ssao)
+ [Model loading](#model-loading)
+ [Advanced topics](#advanced-topics)
+ [Vulkan](#vulkan)
+ [ECS architecture](#ecs-architecture)


## References

- [vulkan-tutorial](https://vulkan-tutorial.com/)
- [learnopengl](https://learnopengl.com/)
- [OpenGL-tutorial](http://www.opengl-tutorial.org/)
- [GLSL built-in variables](https://www.khronos.org/opengl/wiki/Built-in_Variable_(GLSL))


## Basics

### Definitions

- **Vertex** (plural: vertices): Collection of data (vertex attributes) needed for rendering a 3D point (position, color, normal, UVs, tangent/bitangent, skinning weights, bone indices…). A collection of vertices form a **vertex buffer**. There's a __maximum number of vertex attributes__ that we can declare, which is limited by hardware.

- **Index**: Integer referring to a specific vertex in a vertex buffer. A collection of indices form an **index buffer**. The index buffer says which vertices form which triangle. Instead of duplicating vertices for every triangle, we store them once and use indices to connect them.

- **Mesh**: Structured collection of vertices connected into primitives (points, lines, triangles, quads, polygons) that define the shape and surface of a 3D object. It's made of **vertices**, **edges** (straight lines connecting pairs of vertices), and **faces/polygons** (closed set of edges, usually triangles or quads).

- **Frustum**: Truncated 3D pyramid-shaped volume that represents what the camera can see. Its tip is at the camera, but the **near plane** (closest distance the camera can see) and **far plane** (farthest distance the camera can see) cut off the tip and far end of the pyramid respectively.

- **Library**: Collection of resources that can be used during software development to implement a computer program. Some useful libraries for computer graphics are:
  - **GLM**: Header-only mathematics library for graphics software. Designed based on the GLSL (shading language).
  - **GLFW**: Can create and manage windows and contexts, and handle user input from mouse, keyboard, and joystick.

### Graphics pipeline

Generally, an 3D object is defined by a **vertex buffer** and an **index buffer**, which are used to build primitives (points, lines, triangles…). Its 3D points are usually in **model space** (**model coords**) (local to the object). Both buffers are loaded into the GPU.

On the CPU we build the transformation matrices: **Model (M)**, **View (V)**, **Proyection (P)**, **Normal (N)**. Then, we pass them to the shaders (via uniform buffers, push constants, or descriptor sets). We will use them in the vertex shader to transform vertex coords from model space to clip space.

Typical **graphics pipeline**:

- **Vertex shader (VS)**

Runs once per vertex. Its main purpose is to transform 3D coords into different 3D coords (model coords to clip coords) and to do some basic processing on the vertex attributes. **Input**: Single vertex in model coords and any additional data (such as transformation matrices `M`, `V`, `P`, `N`). **Output**: Vertex position in clip coords (transformed using transformation matrices: `P·V·M·inPos`) (output value should be assigned to `gl_Position`). Transformation process: Model → World → View → Clip coords.

- **Tessellation** (optional)

This phase allows to subdivide coarse geometry into finer geometry, on the fly. It "refines" surfaces. Three stages:

  - TCS (Tessellation Control Shader): Runs per patch (group of vertices defined by patch size). Output: tessellation levels and per-vertex data for tessellation.
  - TPG (Tessellation Primitive Generator): Fixed-function. Subdivides the patch into new vertices according to tessellation levels.
  - TES (Tessellation Evaluation Shader): Runs per generated vertex. Input: baycentric location on tessellated patch. Output: per-vertex data including `gl_Position` in clip space.

- **Geometry shader (GS)** (optional)

The **input** is the collection of vertices that form a primitive. It allows to create, destroy, or modify whole primities on the fly. It can generate other shapes by emitting new vertices to form new/other primitives. It "amplifies/filters" primitives. Example: a second triangle out of the given shape.

- **Primitive assembly**

It takes as **input** the collection of the vertices from the vertex shader that form a **primitive** (point, line, triangle), and assembles all the points in the primitive shape given.

- **Clipping / Frustum culling**

GPU tests each primitive against the clip volume (4D cube, frustum) (in Vulkan: `-w ≤ x ≤ w`, `-w ≤ y ≤ w`, `0 ≤ z ≤ w`). Primitives outside the clip volume are discarded, those partially outside get clipped (new vertices are generated at the intersections with the frustum boundaries).

- **Perspective divide / Homogenization**

GPU transforms clip coords to NDCs (Normalized Device Coords) by dividing each component by `w` (`(x/w,y/w,z/w)`). NDCs are within range [-1.0, 1.0] on X and Y, but within [0, 1] on Z (in OpenGL Z is within [-1, 1]). Any coordinates outside this range won't be visible in the screen.

- **Viewport transform**

GPU maps NDCs to **pixel/window/screen/framebuffer coords** using the viewport dimensions and depth range (that you defined in `VkViewport`). Value X is mapped to range [0, width], and Y to [0, height]. Depth values go into the depth buffer. Depth value is within [0, 1] by default, but this is configurable.

- **Rasterization stage**

It maps the resulting primitives to the corresponding pixels on the final screen, resulting in **fragments** (potential pixels containing all data required to calculate the final pixel color, such as lights, shadows, light color…) for the fragment shader to use. Then, **clipping** is performed (all fragments outside your view are discarded).

- **Fragment shader (FS)**

It runs once per fragment, and works in pixel coords. Here we calculate the final color of a pixel (RGBA). Usually, all the advanced effects occur here.

- **Depth test + Alpha test + Blending**

Checks the corresponding **depth** and **stencil** value of the fragment and uses those to check if the resulting fragment is in front or behind other objects and should be discarded accordingly. Also checks for **alpha values** (they define the opacity of an object), and **blends** the objects accordingly.

Most often we only have to work with vertex and fragment shaders. We are required to define at least them because there're no default vertex/fragment shaders on the GPU. Geometry shader is optional, usually left to its default shader. Others: tessellation stage and transform feeback loop.

### Coordinate systems and transformations

#### Transformations:

[Model → World → View → Clip] → NDC → Screen

1. **(Model)**
2. [Model mat] → **(World)**
3. [View mat] → **(View)**
4. [Projection mat] → **(Clip)**
5. <Perspective divide> → **(NDC)** (automatic)
6. <Viewport transform> → **(Screen)** (automatic)

![Transformations](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_8.png)

#### In the pipeline

- __Model__ starts in **model coords**.
- __Vertex shader__: Model coords are transformed to **clip coords** (model → world → view → clip) using transformation matrices M, V, P. Clip coords are `(x,y,z,w)`.
- __Tessellation shader__
- __Geometry shader__
- __Primitive assembly__
- __Clipping__: Primitives are tested against the clip volume. Those outside are discarded, those partially outside get clipped. Test in Vulkan: `-w ≤ x ≤ w`, `-w ≤ y ≤ w`, `0 ≤ z ≤ w`.
- __Perspective divide / Homogenization__: Clip coords are transformed to **NDCs** by dividing each vertex by `w` (`(x/w,y/w,z/w)`). In Vulkan, NDCs are within range [-1.0, 1.0] on XY, but within [0, 1] on Z. Any coordinates outside this range won't be visible in the screen.
- __Viewport transform__: NDCs are transformed to **pixel coords**. Value X is mapped to range [0, width] and Y to [0, height]. Depth value go to depth buffer. Depth value is within [0, 1] by default, but this is configurable.
- __Rasterization__: It maps primitives to **fragments** (potential pixels).
- __Fragment shader__: Works in pixel coords. Computes final color of the fragment.
- __Depth test + Alpha test + Blending__: Get the final color of a pixel.

#### Coordinates systems

- **Model/Local/Object** (`x,y,z`): Origin in the object (usually centered at `(0,0,0)`).
- **World** (`x,y,z`): Origin in the world, where objects are placed.
- **View/Eye/Camera** (`x,y,z`): Origin in the camera. Looking direction is -Z axis in Vulkan. 
- **Clip** (`x,y,z,w`): The camera's view frustum is stretched in a way every visible point is within [-w, w] for XY, and [0, w] for Z. It's not viewable, but it's convenient for clipping (W defines the view frustum, a truncated piramid) and perspective divide (W is the divisor). XY are scaled relative to the view frustum (based on FOV and aspect ratio), Z is nonlinearly remapped to fit into the near/far clip range, and W carries the perspective scaling. W comes from depth and is different per vertex (in orthographic projections it's constant: W=1).
- **NDCs** (`x,y,z`): Values XY are within [-1, 1], and Z within [0, 1] in Vulkan. It's like a unit cube centered on the screen that contains all the visible scene.
- **Pixel** (`x,y`, `z`): Real screen positions and depth. Depth is within [0, 1] by default.

![coordinates](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_1.png)

#### Transformation matrices

Used for transforming vertex coords. The user generates a few transformation matrices. Some matrices are combinations of other matrices. To combine matrices, multiply them in reverse order. 

- **MVP matrix (MVP)**: Transforms model coords to clip coords (`MVP · modelPos`). Combination of M, V, and P (`P·V·M`).
  - **Model matrix (M)**: Transforms model coords to world coords (world space) (`M · modelPos`). Combination of T, R, and S (`T·R·S`).
    - **Translation matrix (T)**
	- **Rotation matrix (R)**
	- **Scaling matrix (S)**
  - **View matrix (V)**: Transforms world coords to view coords (camera space) (`V · worldPos`).
  - **Projection matrix (P)**: Transforms view coords to clip coords (`P · viewPos`). Two types of projections: **Perspective** and **Orthographic**. (More info below).
- **Normal matrix (N)**: Transforms normals from model coords to world/view coords. Used when M applies non-uniform scaling. (More info below).

**Projections**: Two types:

- **Orthographic**: Size independent of distance. Defines by a cube-like frustum box. It has W=1, so perspective divison has no effect.
- **Perspective**: Far objects appear smaller. Defines a pyramide-like frustum.

**Normal matrix** (`vec3`) ((M<sup>-1</sup>)<sup>T</sup>): If your model matrix has **non-uniform scaling** (different scale factors on x, y, z), applying it to the normals will distort them by making them no longer perpendicular to the surface, breaking lighting calculations. Normal transformation is done with a different matrix, the normal matrix (transpose of the inverse of M). Two approaches:

- (M<sup>-1</sup>)<sup>T</sup> → If you want normals in **world space**.
- ((M·V)<sup>-1</sup>)<sup>T</sup> → If you want normals in **view space**.

**Passing matrices** to the vertex shader (approaches):

- __Pass MVP and N__. This is simple and faster (less work per vertex on the GPU), but you lose access to individual M, V, or P inside the shader. Used for simple transformations. Not recommended if you need world-space or view-space positions/normals for lighting, reflections, shadows, etc.
- __Pass M, V, P, N separately__ (more common). Slightly more math per vertex and more uniform data passed to the shader. Used for advanced shading (lighting, reflections, shadows, normal transformation, post-processing…) that require world-space or view-space positions/normals.

**Matrix changes**: Matrices are usually passed to the shaders each frame, since they change a lot. They change when:

- __Model__: The object's state changes.
- __View__: The camera moves.
- __Projection__ (not frequent): Projection changes.
- __Normal__ (rarely necessary): Necessary for normals only when non-uniform scaling is applied.

To draw the same object in different places we can draw it many times in the render loop, but sending a different Model matrix each time to the vertex shader.

### Vertex data

To send vertex data to the vertex shader you need to reserve some memory on the GPU for it, configure how the API should interpret the memory, and specify how to send the data. Vertex data can be sent all at once, there's no need to send it one vertex at a time. Sending data to GPU is relatively slow, so we should try to send as much data as possible at once. We can also send **indices** (they specify at which order to draw the vertices) to avoid repeating (overlapping) vertices.

![vertex buffer](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_2.png)

### GLSL

**Shader**: Little programs that rest on the GPU, and just transform inputs to outputs. Shaders are extremely pipelined; they cannot communicate with each other, except via input and output. If we need data from outside the shader, we have to pass data around via vertex attributes, uniforms, samplers, or get it from the built-in variables. Shaders receive some input, operate on it, and produce an output. Most common shaders:

- **Vertex shader**: Runs per vertex.
  - Input: Vertex attributes, UBOs…
  - Output:
    - Clip-space coordinates
	- Any output for the fragment shader

- **Fragment shader**: Runs per fragment.
  - Input: UBOs, textures, input from vertex shader…
  - Output: One or more fragment colors (the render pipeline determines the number of outputs).

**Shader program**: Final linked version of multiple shaders combined (links the outputs of each shader to the inputs of the next).

**GLSL**: C-like language used to write shaders, which is later translated to **SPIR-V**. It contains features for vector/matrix manipulation. It supports different **types** (`int`, `float`, `double`, `uint`, `bool`, `vec`, `mat`). It includes some built-in [**variables**](https://www.khronos.org/opengl/wiki/Built-in_Variable_(GLSL)) and [**functions**](https://www.khronos.org/opengl/wiki/Built-in_Function_(GLSL)).

**Vectors** may be a 1, 2, 3, or 4 component container for any basic type (`vecn`, `bvecn`, `ivecn`, `uvecn`, `dvecn`). They can be accessed in different ways (`xyzw`, `rgba`, `stpq`). They allow **swizzling** (flexible way of selecting components). We can pass vectors as arguments to vector constructor calls.

**Uniforms** is a way to pass data from CPU to GPU's shaders. Uniforms are global (i.e., each uniform variable is unique pershader program object, and can be accessed/defined from any shader at any stage). Uniforms keep their values until they're either reset or updated. If you declare a uniform that isn't used anywhere in your GLSL code, the compiler will remove the variable from the compiled version.

**Fragment interpolation** (in the fragment shader): Given the fragment shader's input variables (vertex colors), the rasterizer will assign a color to each fragment based on the position of the fragment in the triangles shape.

**Built-in functions**:

- `clamp()`: Clamps its first argument between a range.
- `max()`: Returns the greater of 2 values.
- `length()`: Calculate the length of a vector.

**Built-in variables**: 

- Vertex shader:

  - `gl_Position` (output) (vec4, floats): Clip-space output position vector. Setting this is required for rendering anything.
  - `gl_PointSize` (output) (vec2, floats): Used to set the size of point primitives (width and height in pixels).
  - `gl_VertexID` (input) (integer): In indexed rendering, it holds the current index of the vertex; otherwise, it holds the number of currently processed vertex since the start of the render call (example: calling `glDrawArrays(GL_TRIANGLES, 2, 4)` makes vertex shader run 4 times, with `gl_VertexID = 2, 3, 4, 5`).
  - `gl_InstanceIndex` (input): Id of the current instance of the object, starting from 0.It's incremented for each instance being rendered starting from 0.
  - `gl_InstanceID` (input): Like `gl_InstanceIndex`, but it incorporates the `firstInstance` offset (`gl_InstanceID = gl_InstanceID + firstInstance`).
  
- Fragment shader:

  - `gl_FragCoord` (input): Pixel coords of the fragment. It depends upon the number of pixel specified for the window (like 800x600). The `z` is its depth value (range [0, 1]). Example: This could be used for splitting the screen to compare visual output of different fragment calculations.
  - `gl_FrontFacing` (input) (bool): This tell whether the fragment is part of a front-facing (true) or back-facing (false) face. Useless if face-culling is enabled.
  - `gl_FragDepth` (output): Set fragment's depth value (range [0, 1]). If not set, it takes the value of `gl_FragCoord.z`. Disadvantage: Early depth testing (EDT) is disabled as soon as we write to this variable because the API couldn't know its value without running the fragment shader. However, it's possible to mediate between both sides by redeclaring this variable at the top of the fragment shader with a depth condition (`any`, `greater`, `less`, `unchanged`). A `greater` or `smaller` condition tells the API that you only write values larger or smaller than the fragment's depth value, so it can do EDT when the buffer value is on the other direction.
  
```
#version 420 core
out vec4 FragColor
layout (depth_greater) out float gl_FragDepth;  // feature only available from OpenGL 4.2

void main()
{
  fragColor = vec4(1.0);
  gl_FragDepth = gl_FragColor.z + 0.1;
}
```

**Interface blocks**:

- **GLSL struct**: C-like struct containing shader variables. Mostly used for organizing input, output, and uniforms.

- **Interface block**: It looks like a `struct` declaration, but is declared using `in` or `out` keyword. It allows us to group together the shader variables that we declare as input or output. This helps organize our shader's inputs/outputs, and it's useful to group it into arrays. The block name (`VS_OUT`) should be the same in both shaders so they're matched together.

```
// Vertex shader:

out VS_OUT
{
  vec2 texCoords;
} vs_out;

void main()
{
  gl_Position = proj * view * model * vec4(aPos, 1.0);
  vs_out.texCoords = aTexCoords;
}
```

```
// Fragment shader:

in VS_OUT
{
  vec2 texCoords;
} fs_in;

void main()
{
  fragColor = texture(tex, fs_in.texCoords);
}
```

### Depth testing

**Depth buffer / z-buffer**: Buffer (like the color buffer) that stores information per fragment, and has the same width and height as the color buffer. The API stores depth values as 16, 24, or 32 bit floats (usually 24) in the range [0, 1]. It's used to prevent rendering triangles that are behind other triangles.

**Depth test**: When enabled, the API tests the fragment's depth (`gl_FragCoord.z`) against the content of the depth buffer. If the depth test is passed, the fragment is rendered and the depth buffer is updated with the new depth value. Otherwise, the fragment is discarded. The test is done in screen space (`gl_FragCoord`), after the fragment shader (and the stencil test) has run. When not enabled, all fragments are drawn in front of the fragments that were drawn before (similarly to always pass the depth test). We can visualize the depth buffer if we output the value `gl_FragCoord.z` (fragment's depth value) as a color.

**Early depth test (EDT)**: Hardware feature supported by most GPUs that allows depth test to run before fragment shader runs, so we can prematurely discard some fragments (running fragment shader is expensive). Enable it in Vulkan by adding `layout(early_fragment_test) in;` to the fragment shader. EDT is not possible if the fragment shader writes to its depth value since, in this case, the API cannot know the depth value beforehand.

When applying depth test, you should clear depth buffer before each frame. Otherwise, you're using depth values from last frame (unless this is a desired behavior).

OpenGL allows to modify the comparison operators used for depth test with `glDepthFunc()`. By default, it's `GL_LESS` (discards fragment if its depth value ≥ depth buffer's value).

In **view space**, the depth values can be any value between the projection-frustum's near and far plane. The near and far values are those we provided to the projection matrix to set the visible frustum (0 for close plane, 1 for far plane). There're different ways of **transforming** view space depth to range [0, 1].

- __Linear transformation__ (almost never used):

FA<sub>depth</sub> = (z - near) / (far - near)

- __Non- linear transformation__ (typically used due to projection properties). We get enormous precision when z is small, and much less when z is far away. It's proportional to 1/z, which means that z-values between 1 and 2 result in depth values between 1 and 0.5 (50% of the [0, 1] range), and between 50 and 100 account for the 2%.

FA<sub>depth</sub> = ((1/z) - (1/near)) / ((1/far) - (1/near))

![depth values graph](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_3.png)

Depth values are linear in view-space but, after applying the projection matrix, they're not linear in clip-space. The non-linear equation to transform z-values from view to clip space is embedded within the projection matrix.

**Reverse fragment's depth values** from non-linear to linear (pixel space → clip space):

1. Re-transform depth values from range [0, 1] to NDCs in range [-1, 1].
2. Reverse the non-linear equation as done in the projection matrix and apply this inversed equation to the resulting depth value. This equation is derived from the projection matrix for non-linearizing depth values, returning depth values between `near` and `far` ([more about projection matrix](http://www.songho.ca/opengl/gl_projectionmatrix.html)).
3. Linearized depth values range from `near` to `far`, so most of its values will be about 1.0 and displayed completely white. Divide this value by `far` to convert it to range [0, 1], which works better for visualization purposes.

```
float linearizeDepth(float depth)
{
  float ndc_z = depth * 2.0 - 1.0;
  return (2.0 * near * far) / (far + near - ndc_z * (far -near));
}

void main()
{
  float depth = linearizeDepth(gl_FragCood.z) / far;
  fragColor = vec4(vec3(depth), 1.0);
}
```

**Z-fighting**: Visual artifact that may occur when two planes are so closely aligned to each other that the depth buffer doesn't have enough precision to figure out which one is in front of the other, so they continually switch order. This is more noticeable when objects are further away because depth buffer has less precision at larger z-values. This cannot be completely prevented, but some trick may help:

- __Never place objects too close to each other__ in a way that some of their triangles closely overlap. Create a small offset between them.
- __Set near plane as far as possible__. Since precision is extremely large when close to the near plane, this produces significantly greater precision over the entire frustum range, but may cause clipping of near objects.
- __Use higher precision depth buffer__, at the cost of some performance. Most depth buffers have 24 bits precision, but most GPUs support 32 bits.


## Textures

**Textures** are images (1D, 2D, or 3D) used to add detail to an object. They can also be used to store a large collection of arbitrary data to send to the shaders).

To map a texture to a triangle, each vertex should have a **texture coordinate** associated (range [0, 1]) that specifies what part of the texture image to sample from. We passes these coordinates to the vertex shader (as vertex attributes), which then passes them to the fragment shader, which interpolates the texture coordinates for each fragment (**fragment interpolation**).

![depth values graph](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_4.png)

**Sampling**: Retrieving the texture color using texture coordinates. We've to tell the API how to sample our textures, that is, how to map a coordinate to a texture pixel (**texel**). Some options are:

- **Nearest neighbor / Point filtering**: Selects the texel whose center is closest to the coordinate.
- **(Bi)linear filtering**: Interpolated value from the neighboring texels, depending on the coordinate.
- etc.

**Mipmaps**: Collection of texture images where each subsequent texture is twice as small compared to the previous one. Far away objects may only produce a few fragments, but a high resolution texture may produce some artifacts and use a lot of memory. Mipmaps solve this. After a certain distance threshold from the viewer, the API will use a different mipmap texture. Mipmaps are primarily used for when textures get downscaled. While switching between mipmap levels during rendering , the API may show some artifacts (sharp edges between two mipmap layers). Like texture filtering, we can filter between mipmap levels using nearest or linear filtering for switching between mipmap levels. There're 2 things to filter: how to sample a mipmap texture and how to switch between mipmap levels. Options:

- How a mipmap is sampled:
  - `NEAREST`: Nearest-neighbor texel.
  - `LINEAR`: Bilinear interpolation of 4 nearest texels.
- What mipmap is chosen:
  - `NEAREST_MIPMAP`: Choose the closest mipmap level.
  - `LINEAR_MIPMAP`: Linear interpolation between two adjacent mipmap levels.
  
Some available options are:
  - Nearest sampling & nearest mipmap
  - Linear sampling & nearest mipmap
  - Nearest sampling & linear mipmap
  - Linear sampling & linear mipmap

**stb_image.h** ([link](https://github.com/nothings/stb/blob/master/stb_image.h)): Single-header image-loading library that supports several popular file formats and does the hard work for us. Process:

- Add it to your project and include this:

```
#define STB_IMAGE_IMPLEMENTATION
#include "stb_image.h"
```

The `STB_IMAGE_IMPLEMENTATION` preprocessor modifies the header file such that it only contains the relevant definition source code, effectively turning the header file into a `.cpp` file.

- Load image:

```
int width, height, numChannels;
stbi_set_flip_vertically_on_load(true);   // Optional: flip the y-axis during loading
unsigned char *imageData = stbi_load("container.jpg", &width, &height, &numChannels, 0);
```

- Generate texture and mipmaps

- Free the image (`stbi_image_free(imageData)`)

**Mix colors**: Operations with color can be done in the fragment shader. Some options:

- Mix colors directly (like the resulting texture color and the vertex colors) by multiplying them (`fragColor = texture(ourTexture, TexCoord) * vec4(ourColor, 1.0);`). 
- Mix colors by linearly interpolating them based on a ratio using the GLSL built-in function `mix(color1, color2, ratio)`.


## Algebra

### Vectors

**Vectors** are Nx1 matrices. They have **direction** (xyz), **magnitude**, and **dimension** (1D, 2D, 3D…). They can describe a direction or a position. Operations:

- **Scalar**:   x + (a, b, c) = (a+x, b+x, c+x)
- **Negation**:   -(a, b, c) = (-a, -b, -c)
- **Addition/Subtraction**:   (a, b, c) - (x, y, z) = (a-x, b-y, c-z)
- **Length**:   √(a<sup>2</sup> + b<sup>2</sup> + c<sup>2</sup>)   (Pythagoras theorem)
- **Unit vector**: Vector of length 1. Useful for working with directions. Compute the unit vector of any vector (**normalization**) by dividing each component by its length.
- **Multiplication** (two types):
  - **Dot product (A · B = scalar)**: Multiplication of A's magnitude by the magnitude of the projection of B over the line defined by A (alternative: length_A · length_B · cosθ). If the vectors go in opposite directions, the result is negative. It's commutative (A·B = B·A). 
  - **Cross product (A x B = vector)**: Vector orthogonal to both according to the right-hand rule. It length is equal to the area of the parallelogram formed by the original 2 vectors. It's not commutative (AxB ≠ BxA).
  
![Matrix addition and subtraction](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_5.png)

### Matrices

**Matrices** are rectangular arrays of elements indexed by `(i, j)` (rows, columns). Operations:

- **Addition/Subtraction** (A + B): Done on a per-element basis, for matrices of same dimensions.
- **Scalar-matrix product** (s · A): Multiply each element by the scalar.
- **Matrix-matrix product** (A · B): Dimensions matter (A(i,j) · B(j,i) = C(i,i)). Non-commutative (A·B ≠ B·A).
- **Matrix-vector product**: A transformation can be placed inside a matrix (usually 4x4) and, by multiplying it with a vector, transform the vector ((4,4)·(4,1) = (4,1)).
  - **Identity matrix**: Produces a vector identical to the former one.
  - **Scaling**: Applies one scale factor to each axis.
  - **Translation**: Add another vector to the original to get a new vector with different position.
  - **Rotation**: Different ways of rotating a vector:
    - **Rotation matrix**: Specify an angle and rotation axis (X, Y, or Z unit axis). To rotate around an arbitrary axis, combine 3 rotation matrices. Beware of Gimbal lock problem.
	- **Arbitrary rotation matrix**: Rotate around an arbitrary unit axis. Gimbal lock problem is harder to get.
	- **Quaternions** (recommended): Prevents Gimbal lock, is safer, and easier to compute.

The **`w` component** (homogenous coordinate) of a vector tells whether it denotes a **position (1)** or a **direction (0)**. Positions can be translated, but directions are not.

**Combining matrices** can be done using matrix-matrix multiplication. This way we combine multiple transformation matrices in a single matrix. It's advised to first do scaling, then rotations, then translations (`translation · rotation · scaling`), which requires multiplying matrices in reverse order.

![Transformation matrices](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_6.png)

### GLM

**GLM** ([link](https://glm.g-truc.net/0.9.9/index.html)) is a header-only library for computer graphics mathematics.

```
#include <glm/glm.hpp>
#include <glm/gtc/matrix_transform.hpp>
#include <glm/gtc/type_ptr.hpp>

glm::vec3 nullMatrix;   // null matrix (all elements are 0)
glm::vec3 identity(1);   // identity matrix
```

Get the transformation matrices with:

- Translation:

```
glm::mat4 mvp = glm::translate(vec1, glm::vec3(1,1,0));
```

- Rotation:

```
mvp = glm::rotate(mvp, glm::radians(90), glm::vec3(0,0,1));
mvp = glm::rotate(mvp, glm::radians(10), glm::vec3(0,1,0));
mvp = glm::rotate(mvp, glm::radians(20), glm::vec3(1,0,0));
```

- Scaling:

```
mvp = glm::scale(mvp, glm::vec3(2, 2, 2));
```

Column-major ordering is the default matrix layout in GLM, so no need to transpose it.

Pass the tranformation matrix (`mvp`) to the shaders through a uniform, and multiply it with the vertex you want to transform. Doing this in the vertex shader saves us the effor of re-defining the vertex data and sending it again.

- **Model matrix (M)**: Transforms model coords to world coords. Get it by combining Scaling, Rotation, and Translation matrices in reverse order of transformation.

```
glm::mat4 mm(1.f);
mm = glm::translate(mm, translation);
mm = glm::rotate(mm, rotationZ, glm::vec3(0,0,1));
mm = glm::rotate(mm, rotationY, glm::vec3(0,1,0));
mm = glm::rotate(mm, rotationZ, glm::vec3(1,0,0));
mm = glm::scale(mm, scale);
return mm;
```

- **View matrix (V)**: Transforms world coords to camera coords. Used to move the camera. It moves the entire scene around inversed to where we want the camera to move, making it look like we're moving the camera.

```
glm::lookAt(camPos, lookDir, up);
```

- **Projection matrix (P)**: Transforms camera coords to clip coords. Two types:

  - **Orthographic** projection: It defines a cube-like frustum box that defines the clipping space. No perspective is applied.
  
```
glm::ortho(left, right, bottom, top, near, far);
```

  - **Perspective** projection: Perspective makes far object appear smaller.
  
```
glm::perspective(fov, aspectRatio, near, far);   // aspectRatio = viewportWidth/viewportHeight
```

![Projections](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_7.png)


## Camera

A camera is simulated by moving all objects in the scene in reverse direction. The view matrix transforms all the world coords into view coords, which are relative to the camera's position and direction. A camera is defined with these variables:

- **Camera position** (P) in world space.
- **Looking direction** (D) (backwards, out of the screen).
- **Right vector** (R) (`glm::normalize(glm::cross(camDir, up))`).
- **Up vector** (U) (`glm::cross(right, camDir)`).

These 4 elements define a coordinate system with the camera at its center. With them you can create a matrix with those 3 axes and the translation vector, and transform any vector to that particular coordinate space by multiplying it with this matrix. This is what `glm::lookAt()` matrix does.

![lookAt function](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_9.png)

Since we want to rotate and translate the world in the opposite direction of where we want the camera to move, the rotation (left matrix) is transposed, and the translation (right matrix) is inverted. Using this `glm::lookAt` matrix as our **view matrix** we can transform all world coords to view space.

**Moving camera**: Just update the camera variables when pressing some keys. To make it run at the same speed on any hardware, keep track of the time it took to render the last frame and balance the speed accordingly.

**Looking around**: Given some **Euler angles (pitch, roll, yaw)**, which represent any rotation in 3D, we can convert them into a new 3D direction vector.

![Rotations](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_10.png)

**Example**: Non-roll camera.

- Direction vector:

```
glm::vec3 dir;
```

- Considering the **yaw** angle counter-clockwise starting from x-axis:

```
dir.x = cos(yaw);   // angles in radians
dir.y = sin(yaw);
```

- Considering the **pitch** angle counter-clockwise, we see that x and y are influence by yaw:

```
dir.x = cos(yaw) · cos(pitch);
dir.y = sin(yaw) · cos(pitch);
dir.z = sin(pitch);
```

- Example: If we set `yaw = -90`, the camera will point to negative z.

![Angles](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_11.png)

**Direction change**: The yaw and pitch values are obtained from mouse/controller/joystick movement: horizontal move affects yaw, vertical move affects pitch. We have to save last frame's mouse horizontal and vertical positions, and calculate how much they changed in the current frame (offset).

- Tell GLFW to hide the cursor and capture it (put cursor in the center of the window when the application has focus):

```
glfwSetInputMode(window, GLFW_CURSOR, GLFW_CURSOR_DISABLED);
```

- Tell GLFW to listen to mouse movement events by creating a **callback function** (it will be called each time the mouse moves) with this prototype, and register it with GLFW:

```
void mouse_callback(GLFWwindow * window, double xpos, double ypos);
glfwSetCursorPosCallback(window, mouse_callback);
```

- Add mouse offset to camera's yaw and pitch:

```
yaw += xoffset;
pitch += yoffset;
// <<< compute dir
camFront = glm::normalize(dir);
```

**Zoom**: When the FOV becomes smaller, the scene's projected space gets smaller, which gives the illusion of zooming in (the scene is projected over the same NDC). We can use a callback function for mouse scrolling.

```
glfwSetScrollCallback(window, scroll_callback);   //register the callback function
```


## Lighting

### Basics

In real life, the color of an object is the mixture of colors that it doesn’t absorbe. Actually, an object’s color is the amount of each color component it reflects from a light source. If we multiply the light source’s color with an object’s color value, the resulting color would be the reflected color of the object. Digitally (in the shader), we represent colors with RGB components in the range [0, 1].

Some **lighting shading models** are:

- **Phong shading**: Phong lighting model applied in the fragment shader.
- **Gouraud shading**: Phong lighting model applied in the vertex shader. Less quality but more efficiency.
- **Blinn-Phong**: Phong lighting, but with a more realistic specular component.

**Normal vector**: Unit vector perpendicular to the vertex surface. Used for computing diffuse and specular lighting. Each vertex can have a normal. Usually, we use the surrounding vertices to figure out a vertex normal. The API interpolates vertices' normals to compute fragments' normals.

Lighting calculation is often done in view space (not world space) because there we already know viewer's position (0,0,0). This requries to transform all relevant vectors with the view matrix as well (don't forget to cahgne the normal matrix too).

Lighting calculations are usually done in the **fragment shader**. We pass vertex world position from vertex shader to fragment shader. In the fragment shader we get the fragment's world position interpolated from the 3 vertices of the triangle (primitive). In lighting calculations we usually care only about directions, not magnitudes, so ensure that all relevant vectors end up as unit vectors (simplifies calculations) by normalizing them.

### Normals

Normals are mainly used for lighting. Normal vectors (`vec3`) are passed from vertex shader to fragment shader (interpolated).

**Transformation** to world space is not necessary (they're just directions, not positions), except when rotations or non-uniform scaling is applied. Translations have no effect over normals (they don't have an homogeneous coordinate `w`).

- **Multiplying normal vectors with a model matrix (M)** requires removing the translation part (take the upper-left 3x3 matrix of M by casting it to `vec3`), or setting the `w` component to 0 and multiply with the 4x4 matrix.
- If M performs **non-uniform scaling**, vertices would be changed in such a way that the normal vector is not perpendiular to the surface anymore (only normal's magnitude changes, not its directions). This distorts the lighting. This is fixed by using a different model matrix specifically tailored for normal vectors (**normal matrix**).
- Normals usually require **normalization**, since they have been interpolated from the vertex shader (their magnitud changed), and M might have applied scaling.

![Normal distortion](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_15.png)

**Normal matrix (N)**: Transpose of the inverse of the upper-left 3x3 part of the module matrix ([link](http://www.lighthouse3d.com/tutorials/glsl-12-tutorial/the-normal-matrix/)). It's a 3x3 model matrix (or model-view) without translation that is modified in such a way that it keeps normal vectors facing the correct direction when non-uniform scaling is applied. It's recommended to compute N in the CPU and send it to the shader (inverting matrices is expensive for shaders).

```
Normal = mat3(transpose(inverse(model))) * aNormal;
```

### Phong lighting model

This model consists of 3 lightings:

- **Ambient**: Objects are almost never completely dark, so we give them ambient lighting constant.
- **Diffuse**: The more a part of an object faces a light source, the brighter it becomes.
- **Specular**: Bright spot of light that appears on shiny objects. It's more inclined to the color of the light than the color of the object.

After computing these lightings, we **combine** them (add up) and multiply with the object color: `vec3 result = (ambient + diffuse + specular) * objectColor`

![Light components](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_12.png)

#### Ambient lighting

Light usually doesn’t come from a single light source, but from many sources scattered all around us, including reflections in other surfaces. There are “global illumination algorithms”, but they are too expensive. Instead, we use a **global** ambient lightning. Main parameters:

- Light's ambient strength
- Material's albedo (object's color/texture)

```
vec3 ambient = lightAmbient * lightColor * objectColor;
```

#### Diffuse lighting

It gives more brightness the closer the fragment’s **normal** is aligned to the **light ray** (unit vector from fragment to light source). The smaller the **incidence angle** (`dot(normal, lightRay)`), the more brightness (maximum brightness when light ray is perpendicular to the surface). Main parameters:

- Light's diffuse
- Material's albedo

```
float diff = max(dot(normal, -lightDir), 0);
vec3 diffuse = lightDiffuse * diff * objectColor;
```

If the angle between 2 vectors is > 90º, the dot product becomes negative. Since color cannot be negative, we use **max()** (GLSL function that returns the highest of 2 parameters) to avoid that.

![Incidence angle](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_13.png)

#### Specular lighting

It reflects the lightsource in the surface. Similar to diffuse lighting, but also based on the view directions.

- Light's specularity
- Material's specularity [0, 1]
- Material's roughness/shininess [0, inf.]

Calculation steps:

- Get **reflection vector** (reflect(-lightDir, normal)`):
- Get **view vector** (`normalize(camPos, -fragPos)`): 
- Get **specularity intensity** (`pow(max(dot(viewDir, reflectDir), 0), roughness)`).
- Result: `vec3 specular = material_specularity * specular_intensity * lightColor`

![Angle](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_14.png)

### Blinn-Phong lighting model

Phong lighting is efficient, but its specular reflections break down un certain conditions:

- __Diffuse__ component: If the angle between normal and light source > 90º, diffuse = 0.
- __Specular__ component: If the angle between camera and reflection > 90º, the dot product becomes negative, resulting in specularity = 0, which is not realistic (specially with low roughness exponents).

Blinn-Phong fixes the specular component using a **halfway vector** (unit vector halfway between view and light directions). The closer it aligns with the surface's normal vector, the higher the specular contribution.

```
vec3 lightDir = normalize(lightPos - fragPos);
vec3 viewDir = normalize(viewPos - fragPos);
vec3 halfwayDir = normalize(lightDir + viewDir);
float spec = pow(max(dot(normal, halfwayDir), 0), shininess);
vec3 specular = lightColor * spec;
```

Blinn-Phong usually requires between 2 and 4 times the Phong roughness exponent to get similar visuals.

### Materials

The properties of a **light** can be represented with a set of values in a struct in the fragment shader. This makes it easy to change light colors over time (example: using `sin(time * x)`).

- Position
- Ambient (low intensity)
- Diffuse (exact color of the light)
- Specular (full intensity)

The properties of a **material** can be represented with a set of values, or maps. Some of them are:

- Albedo/Diffuse
- Roughness / Shininess / Smoothness / Gloss
- Specularity / Metalness: Specifies what parts are shiny and its intensity.
- Height / Displacement / Bump
- Ambient occlusion
- Normal

Using some tools (Gimp, Photoshop…) it's easy to transform a diffuse texture to a specular image by cutting out some parts, transforming it to black and white, and increasing brightness/contrast.

### Light casters

**Light caster**: Light source that casts light upon objects. Types:

- **Directional**: Parallel rays (sun).
- **Point**: Light source with a given position (light bulb).
- **Spot**: Light source that shoots light rays in a specific direction (flashlight).

#### Directional light

Light source modelled to be infinitely far away. The rays are parallel and have the same direction. Represented by a light **direction** vector (not a position vector). 

Some people pass all vectors as `vec4`. This let us check the `w` component (`w=1`: position, `w=2`: direction) and adjust the calculations based on that (use direction or position of light during light calculations).

#### Point light

Light source with a given position that illuminates in all directions, where light rays fade out (reduce intensity) over distance (attenuation). Represented by a **position** and an **attenuation** value. Light's intensity can be attenuated using a:

- **Linear** equation (looks fake)
- **Quadratic** equation (more realistic):   F<sub>att</sub> = 1.0 / (K<sub>c</sub> + K<sub>l</sub> · d + K<sub>q</sub> · d<sup>2</sup>)

  - **d**: Distance form fragment to light source.
  - **K<sub>c</sub>**: Constant. Usually kept at 1.0. It makes sure denominator ≥ 1 (otherwise, intensity will boost).
  - **K<sub>l</sub>**: Multiplied by **d** (linear intensity reduction).
  - **K<sub>q</sub>**: Multiplied by **d<sup>2</sup>** (quadratic intensity reduction).

The light will diminish mostly linearly until the distance becomes large enough for the quadratic term to surpass the linear term and the light intensity will decrease a lot faster.

![Attenuation](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_16.png)

Choosing the right values for these 3 terms depend on many factors: environment, lighting distance, type of light, etc. Check usual values [here](http://wiki.ogre3d.org/tiki-index.php?page=-Point+Light+Attenuation).

```
float distance = length(light.pos - fragPos);
float attenuation = 1.0 / (light.constant + light.linear * dist + light.quadratic * dist * dist);
ambient *= attenuation;
diffuse *= attenuation;
specular *= attenuation;
```

#### Spot light

Light source that only shoots light rays in a specific direction. Represented by a **position**, a **direction**, and a **cutoff angle**. It also uses attenuation. For each fragment we check whether it's in the spotlight's cone and, if so, we lit the fragment accordingly.

![Spot light](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_17.png)

- `lightDir`: Direction from fragment to light source.
- `spotDir`: Direction the spotlight is aiming at.
- `phi` (ϕ): Cutoff angle. Everything outside is not lit.
- `thetha` (θ): Angle between `lightDir` and `spotDir`.

We just need to calculate the **dot product** (returns the cosine of the angle between 2 unit vectors) between `lightDir` and `spotDir`, and compare this with the cosine of the cutof angle ϕ (computing the inverse of the cosine is expensive).

**Smooth edges**: We get them by simulating an **inner (ϕ)** and **outer (γ)** cone. We define another cosine value for the outer cone. If the fragment is between the inner and the outer cone it should calculate an intensity value between 0 and 1. Intensity is 1 inside the inner cone, but it's 0 outside the outer cone. Intensity is calculated with **I = (θ - γ) / (ϕ - γ)**. If we `clamp` values properly, we don't need an `if-else` in the fragment shader. We can simply multiply the light components with the calculated intensity:

```
float theta = dot(lightDir, normalize(-light.dir));
float epsilon = light.innerCutOff - light.outerCutoff;
float intensity = clamp((theta - light.outerCutoff) / epsilon, 0, 1);
diffuse *= intensity;
specular *= intensity;
```

#### Multiple lights

A single color vector represents the fragment's output color. For each light, the light's contribution to the fragment is added to this output color vector. Example:

```
out vec4 fragColor;

void main()
{
  vec3 output = vec3(0);
  output += computeDirectionalLight(…);
  for(int i = 0; i < n; i++)
    output += computePointLight(…);
  output += computeSpotLight(…);
  fragColor = vec4(output, 1);
}
```

### Gamma correction

Human eyes are more susceptible to changes in dark colors. Therefore, what we consider a linear range of brightnesses is not physically correct. Given brightness A, what we consider the double of A (perceived brightness) is different than what it really is (physical brightness).

![Brightness scale](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_18.png)

Since the top line looks correct for the human eye, monitors use a power relationship (~2.2, depending on the monitor) for displaying output colors so the linear brightness colors are mapped to the non-linear ones (`finalColor.rgb = pow(color.rgb, vec3(2.2))`).

When rendering graphics, the color and brightness options we configure are based on what we perceive from the monitor. Thus, all options are actually non-linear brightness/color options. However, the monitor transforms our colors, distorting them.

![Gamma table](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_19.png)

The dotted line represents color values in linear space. The solid line is how monitors display colors. The colors we render are darkened by the monitor (except 0 and 1). The dashed line is how we should correct our colors to compensate for the monitor's transformation.

Example: In the fragment shader we output color (0.5,0,0), but the monitor displays (0.5,0,0)<sup>2.2</sup> = (0.218,0,0). If we want to double (0.5,0,0) and get (1,0,0), the monitor will show (1,0,0), which is almost 5 times more brightness than (0.218,0,0).

**Gamma correction** solves this. In the fragment shader, multiply the final output color by the inverse of the monitor's gamma (`pow(color.rgb, vec3(1/2.2))`) (dashed line) before displaying to the monitor. This makes colors brighter before monitor darkens them, balancing them out. We work with colors in linear space but, before rendering them, we apply inverse monitor's gamma(`1/2.2`), and then the monitors applies gamma (`2.2`), which results in colors rendered in non-linear space.

Instead of applying gamma correction in each shader of each rendered object, it can be applied only once in a quad in a post-processing stage.

**Color spaces**:

- **RGB**: Linear color space (no gamma applied).
- **sRGB**: The color space as a result of gamma 2.2.

**Textures**:

Monitors display colors with gamma applied. All pictures you create or edit are in sRGB, not RGB (because picking colors is based on what artists see on the monitor). When we don’t apply gamma correction to our fragments, textures are displayed exactly as they are because they were in sRGB, the same space they were worked in. However, now that we display everything in linear space, the texture colors will be off. They are too bright since gamma correction is applied twice: at fragment shader and at image creation (when we create an image based on what we see on the monitor, we are gamma correcting the color values so they look good on the monitor).

This is solved by transforming the sRGB textures to linear space before doing any calculations on their color values (`vec3 diffuseColor = pow(texture(diffuse, UBcoords).rgb, vec3(2.2))`). But be careful, not all textures are in sRGB. Textures for coloring objects (diffuse maps…) are almost always in sRGB, but textures for retrieving lighting parameters (specular maps, normal maps…) are almost always in linear space (so don't transform them to linear).

**Attenuation**:

In the real physical world, lighting attenuates closely inversely proportional to the squared distance from a light source (`float attenuation = 1 / (dist * dist)`). However, this attenuations is usually too strong, giving a small radius that doesn't look phusically right. Thus, other attenuation functions are used that give more control, or the linear equivalent (`1 / dist`).

- __Without gamma correction__, the __linear__ attenuation gives more plausible results than the quadratic variant. 
- __With gamma correction__, the linear attenuation looks too weak and the __quadratic__ one gives better results.

Without gamma correction, we don't visualize our scene in linear space, so we choose the attenuation functions that look best on our monitor, but aren't physically correct. Example: squared attenuations becomes (1 / dist<sup>2</sup>)<sup>2.2</sup>, which creates larger attenuation. But linear attenuation becomes (1 / dist)<sup>2.2</sup>, which resembles its physical equivalent more.

The more advanced attenuations function we use still ahs its place in gamma corrected scenes as it gives more control over attenuation, but requires different parameters in a gamma corrected scene.

**Conclusion**:

- Gamma correct final color (preferably, at post-processing)
- Transform textures (only those for coloring) to linear space (RGB)
- Modify attenuation parameters

Automatic gamma correction after each fragment shader run can be enabled in OpenGL with `glEnable(GL_FRAMEBUFFER_SRGB)`. In Vulkan you can set swapchain format as `VkSurfaceFormat::colorSpace = VK_COLOR_SPACE_SRGB_NONLINEAR_KHR` (more info [here](https://stackoverflow.com/questions/12524623/what-are-the-practical-differences-when-working-with-colors-in-a-linear-vs-a-no) and [here](https://stackoverflow.com/questions/66401081/vulkan-swapchain-format-unorm-vs-srgb)).

GPU vendors assume that when you’re storing an 8-bit intensity in a texture or framebuffer, it’s sRGB, and when you’re processing colors, it’s linear. Usually, each framebuffer and texture has an “sRGB flag” you can turn on to enable automatic conversion when reading and writing. When read in the shader, it is converted from sRGB to RGB. When output, it is converted from RGB back to sRGB. Thus, you don’t need to explicitly do sRGB conversion or gamma correction at all. However, non-coloring textures (normal, specular, roughness…) are RGB by default, so you will need to apply sRGB transformation when read to counter the automatic RGB transformation.

### Shadows

<<<

### Normal/Bump mapping

**Normal types:**

- **Vertex normal**: Normal of a vertex (vertex attribute).
- **Surface normal**: Fragment normal obtained by interpolating various vertex normals. Alternatively: Single normal used by all the fragments of a triangle.
- **Map/Sampled normal**: Fragment normal obtained from a normal map using UV coords (vertex attribute).

Instead of only using **per-surface normals**, we can additionally use **per-fragment normals** (map normals). This makes lighting think that the surface has more detail. We can store these normals in a 2D texture (normal map), where the XYZ components are stored as RGB values. The normal range is [-1,1], but color range is [0,1], so we need to transform normal's range during read and write operations:

- Store them onto a 2D texture: `vec3 rgb_normal = normal * 0.5 + 0.5`
- Read them in the fragment shader: `normal = normalize(normal * 2 - 1` (we transform them back)

**Tangent space**: Map normals are expressed in tangent space, where normals always point roughly in the positive Z direction. This coordinate space is a local coordinate system defined at each vertex, and interpolated for each fragment. It's local to the surface of a triangle (kind of the local space of the normal maps' vectors). 

- **X (T) (tangent)**: Aligned with the surface texture positive U-axis (depends upon the triangle's surface and texture orientation).
- **Y (B) (bitangent)**: Aligned with the positive surface texture positive V-axis (depends upon the triangle's surface and texture orientation).
- **Z (N) (surface normal)**: Aligned with the surface normal.

We use a **map normal** on a plane that has its own **surface normal**, so lighting won't look correct unless we compute the correct normals for our fragments. We need to do all the lighting in the same coordinate space.

If we express the unit axes of one coordinate system A in terms of another B and arrange them in a matrix, that matrix can convert vectors from A into B.

**TBN matrix**: It allows to transform normal vectors from tangent space to a different coordinate space (world or view coordinates) (or viceversa if we use its inverse), orienting them along the final mapped surface's direction. TBN matrix is made of 3 perpendicular vectors (Tangent, Bitangent, Normal) that are aligned along the normal map surface (right, up, forward). We already know the up vector (surface's normal). We can calculate tangents and bitangents from the triangle's vertices and its texture coords (since texture coords are in the same space as tangent vectors).

![Tangent space](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/cg_20.png)

For simple plain surfaces (wall, water…) we can get a single tangent space for the entire surface and use it for each vertex (see above). But for irregular surfaces (terrain, mountains…) we have to get the tangent space of each vertex. 

```
// Vertex shader (irregular terrain)
vec3 tangent = normalize(cross(vec3(0,1,0), normal));
vec3 bitangent = normalize(cross(normal, tangent));
outTBN = transpose(mat3(tangent, bitangent, normal));
```

There're 2 ways we can use a TBN matrix for normal mapping (we explain the second one):

- Take the **TBN matrix** (`mat3(tangent, bitangent, normal)`) that transforms any vector from tangent to world space, pass it to the __fragment shader__, and use it to transform the sampled normal from tangent space to world space. Now the sampled normal is in the same space as the other lighting variables.
- Take the **inverse of the TBN matrix** (`transpose(mat3(tangent, bitangent, normal))`) (transpose of orthogonal matrix == its inverse; and transpose is cheaper than inverse) that transforms any vector from world space to tangent space, and use it in the __vertex shader__ to transform not the normal, but the other relevant lighting variables to tangent space, and pass them to the fragment shader. Now the other lighting variables are in the same space as the sampled normal. Steps:

  1. Once we have the tangent (or the bitangent) vector, we pass it to the vertex shader as a vertex attribute.
  2. In the vertex shader we transform the TBN vectors to the coordinate system we'd like to work in (world-space) and create the TBN matrix.
  3. If we want to be really precise, we would multiply the TBN vectors with the normal matrix as we only care about the orientation of the vectors.
  4. Then we get the inverse of TBN matrix (it transforms any vector from world-space to tangent-space), use it to transform the relevant lighting variables to tangent space (`vertexPos`, `camPos`, `lightPos`/`lightDir`), and pass them to the fragment shader.
  5. In the fragment shader we use these variables to calculate lighting in tangent space (sampled normal vector is already in tangent space). Since Y coordinate is inverted in Vulkan, normal maps must be reflected in the Y axis.
  
```
// Vertex shader
// ...
layout(location = 2) in vec3 aNormal;
layout(location = 3) in vec3 aTangent;

void main()
{
  vec3 N = normalize(vec3(modelMat * vec4(aNormal, 0)));
  vec3 T = normalize(vec3(modelMat * vec4(aTangent, 0)));
  vec3 B = cross(N, T);
  mat3 TBN = transpose(mat3(T,B,N));
  outTangentLightPos = TBN * lightPos;   // for point & spot light
  outTangentLightDir = TBN * lightDir;   // for directional light
  outTangentViewPos  = TBN * viewPos;
  outTangentFragPos  = TBN * vec3(modelMat * vec4(aPos, 1));
}
```

```
// Fragment shader

vec3 normal = texture(normalMap, texCoords).rgb;
normal = normalize(normal * 2.f - 1.f);   // transform to range [-1, 1]
```

By convention, images (jpeg, png…) are almost always in sRGB color space (non-linear). With Paint you can check the sRGB color coordinates. When passing a sRGB image to the shader as texture, it will automatically transform the texture to RGB (linear) (if you told Vulkan to do so) because it's easier for making operations with colors. Later, when the shader outputs the result, the color is automatically transformed back to sRGB. Therefore, the data about the normals that you get in the shader (RGB) is different than the original image (sRGB), so we have 2 options ([link](https://stackoverflow.com/questions/73608823/colors-in-range-0-255-doesnt-correspond-to-colors-in-range-0-1/73617701#73617701)):

- Transform the data to sRGB in the shader in order to get the correct data.
- Ise images in RGB color space (tell Vulkan about this).

**Computing Tangents for a mesh**:

If your mesh only has positions, normals, and UVs, you need to compute tangents (and bitangents) yourself.

- **Compute tangent** (and bitangent) per triangle from the vertices positions (`p0, p1, p2`) and UV coords (`uv0, uv1, uv2`).

```
glm::vec3 edge1 = p1 - p0;
glm::vec3 edge2 = p2 - p0
glm::vec2 deltaUV1 = uv1 - uv0;
glm::vec2 deltaUV2 = uv2 - uv0;
float f = 1.f / (deltaUV1.x * deltaUV2.y - deltaUV2.x * deltaUB1.y);

glm::vec3 tangent;
tangent.x = f * (deltaUV2.y * edge1.x - deltaUV1.y * edge2.x);
tangent.y = f * (deltaUV2.y * edge1.y - deltaUV1.y * edge2.y);
tangent.z = f * (deltaUV2.y * edge1.z - deltaUV1.y * edge2.z);

glm::vec3 bitangent;
bitangent.x = f * (-deltaUV2.x * edge1.x + deltaUV1.x * edge2.x);
bitangent.y = f * (-deltaUV2.x * edge1.y + deltaUV1.x * edge2.y);
bitangent.z = f * (-deltaUV2.x * edge1.z + deltaUV1.x * edge2.z);
```

- **Accumulate per vertex**: Add this tangent (and bitangent) to each vertex in the triangle. Repeat for each triangle. At the end, normalize.

- **Orthogonalize against normal**: Tangent space should be orthogonal, so make a Gram-Schmidt orthogonalization against the normal.

```
tangent = glm::normalize(tangent - normal * glm::dot(normal, tangent));   // This ensures `tangent` is perpendicular to `normal`
```

- **Store handedness** (optional): Bitangent can be reconstructed in the shader.

```
vec3 bitangent = cross(N, T) * handedness
```

Where `handedness` is a `+1` or `-1` scalar stored in `tangent.w`. It's useful when UVs are mirrored. It's determined by:

```
float handedness = (glm::dot(glm::cross(normal, tangent), bitangent) < 0.f) ? -1.f : 1.f;
```

<<<

**Synthesis_**

- Normal maps are stored as RGB textures. Color range is [0, 1], but normal range is [-1, 1], so a transformation is needed for reading and writing operations.
- Tangent space (T,B,N): 


**Notes (normal mapping):**

- Normal maps are directions relative to the orientation of the texture. The TBN matrix is aligned to the texture.
- Mesh's vertices sometimes store a tangent (left to right orientation of the UVs), a vertex normal, and a bitangent/binormal. Mesh tangents are based on the UVs.
- Normal map is aligned with the tangent plane.
- Process:
  - Compute TBN matrix (tangent plane) → Transform variables from world to tangent space (required for normal maps).
  - Triplanar projections of albedo, specular, roughness, and normal map. World coordinate system determines projection.
  - Normal map is projected onto the tangent plane in the same way, but its sub-normals must be aligned with the tangent plane (first, fix normal values if projection is inverted, according to the TBN used).
  
More about normal mapping:

- [OpenGL tutorial](http://www.opengl-tutorial.org/intermediate-tutorials/tutorial-13-normal-mapping/)
- [TBN matrix normal mapping](https://www.youtube.com/watch?v=0QhR7WSoF78)
- [Normal mapping for a triplanar shader](https://bgolus.medium.com/normal-mapping-for-a-triplanar-shader-10bf39dca05a)

### Parallax mapping

<<<

### HDR

<<<

### Bloom

<<<

### Deferred shading

<<<

### SSAO

<<<

-------------------------------------






Face culling



Model matrix for Normals: Normals are passed to fragment shader in world coordinates, so they have to be multiplied by the model matrix (MM) first (this MM should not include the translation part, so we just take the upper-left 3x3 part). However, non-uniform scaling can distort normals, so we have to create a specific MM especially tailored for normal vectors: mat3(transpose(inverse(model))) * aNormal.









## Model loading

### OBJ files

Models are usually designed with **3D modeling tools** (Blender, 3DS Max, Maya…) and then exported to model files. We want to parse them and extract the data. Some **model formats** are:

- **Wavefront.obj**: Model data + minor material information (color, diffuse/specular maps…). Easy to parse. Check Wavefront's wiki to see its structure.
- **Collada file format**: XML-based. Extremely extensive (models + lights + materials + animation data + cameras + complete scene information + etc.).

**Main elements** in an OBJ file:

- **Vertices** (`v`): Vertex position (`v 1.0 2.0 -1.0`). It's 3D (`x y z`) or 4D (`x y z w`).
- **Texture UVs** (`vt`): Texture coordinate (`vt 0.1 0.2`). It's 2D (`u v`) or 3D (`u v w`).
- **Vertex normals** (`vn`): Normal vector (`vn 0.0 0.0 1.0`).
- **Faces** (`f`): Triangle, quad, or polygon. Indices for `v`, `vt` and `vn`. Indices are 1-based (start form 1, not 0). Negative indices count from the end.
- Structure: Faces can be separated into objects and groups.
  - **Object** (`o`): Object name (`o ObjectName`).
  - **Group** (`g`): Group name (`g GroupName`).
- Materials:
  - **Materials file** (`mtllib`): References an external material file (`mtllib file.mtl`) with shading information (colors, textures…).
  - **Material used** (`usemtl`): Material used (`usemtl MaterialName`).

Typical structure:

```
mtllib cube.mtl
o Cube
v -1.0 -1.0 1.0
v  1.0 -1.0 1.0
v  1.0  1.0 1.0
v -1.0  1.0 1.0
vn 0.0 0.0 1.0
vt 0.0 0.0
vt 1.0 0.0
vt 1.0 1.0
vt 0.0 1.0
s 1
usemtl white
f 1/1/1 2/2/1 3/3/1 4/4/1
```

Note: `s 1`, `s 2`, etc. means "smoothing group X" is active. Faces share normals if they belong to the same smoothing group. Flat shading (no smoothing) is denoted by `s off`.

### Assimp

There're different libraries for importing model files such as:

- **tiny_obj_loader** ([link](https://github.com/tinyobjloader/tinyobjloader)): Tiny library for loading wavefront.obj files.
- **Assimp** (Open Asset Import Library): Library able to import and export dozens of model file formats. It loads all the model's data into its own generalized data structure (`aiScene`), from where we can retrieve the data, which abstracts us from the file format.

Assimp **data structure**:

- **Scene** (`aiScene`): All data from the imported object is loaded into this. It contains:
  - All **meshes** (`aiMesh`). Each one contains: `mName`, `mVertices`,  `mNormals`, `mTextureCoords`, `mMaterialIndex`, `mColor`, `mTangent`, `mBitangent`…
  - All **materials** (`mMaterials`). Each one contains textures and properties.
  - **More** (`mName`, `mCameras`, `mLights`, `mTextures`, `mSkeletons`…).
  - Root **node** of a tree (`aiNode`). Each node contains:
    - Indices to meshes stored in the scene object
    - Children nodes
  
![Assimp structure](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/resources/assimp_structure.png)

Each node represents an object or group, and contains one or more meshes (geometry chunks with a single material). Data can be read by traversing all nodes and reading the data they contain.








## Advanced topics

## Vulkan

## ECS architecture



Instance rendering:

To render multiple instances of the same mesh, you want to make a single draw call for the mesh, and then pass to the shader the data (like model matrix) for each instance. There are different ways of passing this instance data:

- **Push constants**: Small, fast uniform blocks (≤ 128 bytes) updated per draw. Useful for very small per-object data.

```
layout(push_constant) uniform Push {
    mat4 model;
} pushData;
```

```
vkCmdPushConstants(cmdBuffer, pipelineLayout, VK_SHADER_STAGE_VERTEX_BIT, 0, sizeof(PushData), &pushData);
```

- **Single UBO**: Binding containing one descriptor containing an array of structs with per-instance data. Useful for moderate scene sizes.

```
layout(std140, binding = 0) uniform ObjectUBO {
    mat4 model[NUM_OBJECTS];
} ubo;

void main() {
    gl_Position = projection * view * ubo.model[gl_InstanceIndex] * vec4(inPos, 1.0);
}
```

- **Array of UBOs**: Binding containing multiple UBOs (descriptors). Not efficient or scalable (too descriptor overhead). Rarely used. There's a max number of descriptors per set (usually in the thousands).

```
layout(std140, binding = 0) uniform ubObj {
    mat4 model;					// mat4
    mat4 normalMatrix;			// mat3
} ubo[0];

void main() {
	gl_Position = proj * view * ubo[i].model * vec4(pos, 1.0);
}
```

- **SSBOs (Storage Buffer Objects)**: Large arrays of structs, accessible by index. Useful for many instances (hundreds or hundred of thousands) and GPU-driven rendering (compute shaders, indirect draws…). Shareable with other shaders. Most modern and flexible approach.

```
layout(std430, binding = 1) buffer ObjectBuffer {
    mat4 model[];
} objectData;

void main() {
    gl_Position = projection * view * objectData.model[gl_InstanceIndex] * vec4(inPos, 1.0);
}
```

- **Instance buffer**: Buffer that stores per-instance data. Useful for a few thousand instances. Fastest possible access. Limited number of vertex attributes (typically 16-32 per stage).

```
layout(location = 0) in vec3 inPosition; // from vertex buffer
layout(location = 1) in mat4 inModel;    // from instance buffer
layout(location = 5) in vec4 inColor;    // from instance buffer (next attribute)

void main() {
    gl_Position = projection * view * inModel * vec4(inPosition, 1.0);
}
```

```
vkCmdBindVertexBuffers(cmdBuffer, 0, 2, vertexBuffers, offsets);
```

UBOs and SSBOs differences:

- UBOs: Small, read-only, and fast. Applies `std140`. Limit: typically 16-64 KB per block (`maxUniformBufferRange`).
- SSBOs: Large, flexible, and read/write. Applies `std430`. Limit: typically 1GB+ (`maxStorageBufferRange`).

Many modern engines use either SSBOs or a hybrid strategy (SSBOs & Instance buffer).

In the CPU, `alignas(16)` ensures proper alignment of structs for `std430` layout.

```
struct alignas(16) InstanceData {
    glm::mat4 model;
    glm::mat4 normalMatrix;
};
```




Alignment:

**Alignment**: A data type aligned to X-bytes means that the data starts at memory addresses that are multiples of X bytes.

**Memory layout of shader interface blocks**: Defined by the API. It specifies the alignment requirements for each element. Some layouts are:

- `std140` (for UBO)
- `std430` (for SSBO)

**`std140` memory layout**

Buffers passed to the shader must be aligned to 16 bytes. Thus, apply `alignas(16)` to the entire struct or to its first member.

Each member type also has specific alignment rules:

- `float` → 4 bytes.
- `vec2` → 8 bytes.
- `vec3`/`vec4` → 16 bytes.
- `mat4` → 16 bytes per column.
- Struct → Aligned to largest member. Size multiple of 16.
- Arrays → Each element aligned to 16 bytes.

C++ code:

```
struct alignas(16) Example {   // not needed if 1st element is aligned
    alignas(16) glm::mat4 model;   // not needed if the struct is aligned
    alignas(16) glm::vec3 color;
    alignas(4) float intensity;   // last element doesn't need to be aligned
	alignas(8) glm::vec2 uv;
	float pad[4];  // not needed, unless the struct is an element of an array
};
```

GLSL code:

```
layout(set = 0, binding = 1) uniform Example {
    mat4 model;
    vec3 color;
	float intensity;
	vec2 uv;
	float pad[4];
} example;
```

Descriptor total size must be a multiple of 16 bytes. Otherwise, GPU might misread the following descriptors or elements in arrays.

**`std430` memory layout**

Data can be packed more tightly. Data must be aligned to the natural alignment of each type. No 16-bytes rounding rules, unless required by members or arrays.

**Vulkan descriptor size**

When creating the buffer, if it contains multiple descriptors (UBOs or SSBOs), their size (`VkBufferCreateInfo::size`) must satisfy the minimum alignment for that buffer type, except for the last one:

- UBO → `VkPhysicalDeviceLimits::minUniformBufferOffsetAlignment`
- SSBO → `VkPhysicalDeviceLimits::minStorageBufferOffsetAlignment`