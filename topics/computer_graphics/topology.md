# Topology

<br>![computer graphics image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/computer_graphics.jpg)

## Table of Contents

+ [Basics](#basics)



## Basics

**Topology**: It's the way edges (and by extension, faces) of a 3D model are connected together. Topology is important for:

- Good animation deformation. 
- Optimization (it can save rendering time and resources).
- Model accuracy (like overly sharped models caused by **pinching** topology).
- Good UVs split.

**Terms:**

- **Vertex**: Point in 3D space.
- **Edge**: Two vertices connected together.
- **Triangle**: Three-sided face.
- **Quad**: Four-sided face.
- **Ngons**: Face with more than four sides. This should be avoided whenever possible since it can cause problems when the model is deformed.
- **N-pole**: Vertex connected to only three edges. Density is higher around it.
- **E-pole**: Vertex connected to more than four edges. Density is lower around it.
- **Mesh resolution/density**: The bigger the subdivision in the mesh, the higher its resolution/density. A model can have fluctuating densities throughout the model. You should find a balance, but it's not always possible.

If possible, you usually want to keep triangles, ngons, and poles on flat surfaces since they don't create many issues there.

A flat face is a **plantar face**; otherwise, it's a **non-plantar face** (in Blender, you can switch triangulation of a non-plantar face with `Ctrl F` > `Face data/Flip quad tessellation`). Each face has a **normal** (useful for lighting).

**Edge flow**: Edges in a model usually have a flow. An edge flow wrapped around your model creates a loop. Generally, edge flows are the best way to control a mesh. 
**Poles** are often used to redirect the edge flow. Usually, e-poles are created unintentionally, but you will want to use n-poles more often because they're usually more useful. Poles act similar to the triangle and ngon.

**Reduction**: Going from a higher number edge loop to a lower one. This is done using n-poles.









---------------------------------------

We want quad topology, specially for areas that will undergo strong deformation (like elbows).

Our topology should follow possible deformation (like topology around the mouth that simulates the orientation of muscle fibers) or the object's flow (like topology of a car's tyre/wheel that requires circular details).

In sculpting, quads are preferred for consistent details and resolution.

For sharp edges, consider adding more edges around the area that you want sharp.



Using a specular material can help spot mistakes more easily.

## References

- PzThree (2024) [_**Blender - Topology fundamentals**_](https://youtu.be/MD1QmdqXRfc?list=PLXPDJgqHHibegfwbeBP8-1znNtGkqqd59). YouTube.