# Blender fundamentals

<br>![computer graphics image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/computer_graphics.jpg)

## Table of Contents
+ [Basics](#basics)
+ [Editing](#editing)
+ [Modifiers](#modifiers)
+ [Modelling](#modelling)
+ [Donut tutorial basics](#donut-tutorial-basics)
+ [Links](#links)


## Basics

**Blender** is a free, open-source, multiplatform 3D computer graphics software tool set. It's used for creating animated films, visual effects, art, 3D-printed models, motion graphics, interactive 3D applications, and virtual reality.

- **View movement**:
  - **Orbit**: `MMB` (middle mouse button).
  - **Zoom**: `scroll` (discrete) or use the magnifying glass icon (continuous).
  - **Pan view**: `Shift + MMB`
  - **Look through camera**: Use camera icon. Take photo with `F12` (Render/Render image).

A **mesh** is made of a single **vertex** (singular) or many **vertices** (plural). An **edge** is made of two vertices joined by a line. A **face** is made of 4 vertices forming a square.

- **Basic windows**:
  - Viewport: Scene showing 3D objects.
  - Scene objects menu: List of objects in the scene.
  - Properties menu: Different properties (some are general, some are selection dependent).

- **Viewport shading**: Type of rendering used in the viewport(wireframe, solid, material, rendered). Change it using the top right icons.

- **Object Interaction mode**: Change it in the top left drop-down list, or using `tab` (switch between object and edit mode). Modes: object, edit, sculpt, vertex paint, weight paint, texture paint.

- **Basic properties** (properties menu):
  - **Tool**: Active tool and workspace settings
  - **Render**
  - **Output**
  - **View layer**
  - **Scene**
  - **World**
  - **Collection**
  - **Object properties**
  - **Object modifiers**
  - **Object constraints**
  - **Object data**
  - **Object material**
  - **Object texture**
  - **Particles**
  - **Physics**


## Editing

- **Object movement**: Confirm with `RMB`. Cancel with `LMB` or `esc`.
    - **Move**: `G`. Move along axis with `G + MMB` or `G + X/Y/Z`.
    - **Rotate**: `R`. Rotate along axis with `R + MMB` or `G + X/Y/Z`.
    - **Scale**: `S`. Scale along axis with `S + MMB` or `S + X/Y/Z`.
    - **Move camera**: Like any other object (default), or like the view (select camera object > object properties > camera to view)

- **Object properties**: `N`
- **Shade flat/smooth**: `RMB` on object and select shading type.

- **Delete**: `x` or `supr`.
- **Add**: `shift + A`
- **Duplicate** (`Shift + D`): Duplicate object. Keep it in its original place with `esc` or `RMB`. Cancel duplication with  
- **Proportional editing** (`O` or top icon): Set mode (`O`), select vertices, grab them (`G`), set influence radius (scroll), and move the vertices.
- **Edge select** (`Alt` + select edge): Select all vertices along an edge.
- **Toggle X-ray**: `Alt + Z`

## Modifiers

**Modifiers** add a procedural operation/effect to the active object.

Note: if your object disappears after applying a modifier, deselect Properties/Viewport/GPU subdivision.

- **Edit**:
  - **Data transfer**: Transfer several types of data (vertex groups, UV maps, vertex colors, custom normals) from one mesh to another.
  - **Mesh cache**: Deform the mesh using an external frame-by-frame vertex transform cache.
  - **Mesh sequence cache**: Deform the mesh or curve using an external mesh-cache in Alembic format.
  - **Normal edit**: Modify the direction of the surface normals.
  - **Weighted normal**: Modify the direction of the surface normals using a weighting method.
  - **UV project**: Project the UV map coordinates from the negative Z axis of another object.
  - **UV warp**: Transform the UV map using the differences between two objects.
  - **Vertex weight edit**: Modify of the weights of a vertex group.
  - **Vertex weight mix**: Mix the weights of two vertex groups.
  - **Vertex weight proximity**: Set the vertex group weights based on the distance to another target object.
- **Generate**: 
  - **Array**: Create copies of the shape with offsets.
  - **Bevel**: Generate sloped corners by adding geometry to the mesh's edges or vertices.
  - **Boolean**: Use another shape to cut, combine or perform a different operation.
  - **Build**: Cause the faces of the mesh object to appear or disappear one after the other over time.
  - **Decimate**: Reduce the geometry density.
  - **Edge split**: Split away joined faces at the edges.
  - **Mask**: Dynamically hide vertices based on a vertex group or armature.
  - **Mirror**: Mirror along the local X, Y, and/or Z axes, over the object origin.
  - **Multiresolution**: Subdivide the mesh in a way that allows editing the higher subdivision levels.
  - **Remesh**: Generate new mesh topology based on the current shape.
  - **Screw**: Lathe around an axis, treating the input mesh as a profile.
  - **Skin**: Create a solid shape from vertices and meshes, using the vertex radius to define the thickness.
  - __**Solidify**__: Make the surface thick.
  - __**Subdivision surface**__: Split the faces into smaller parts, giving it a smoother appearance. If your GPU doesn't support this, deselect Edit/Preferences/Viewport/GPU subdivision.
  - **Triangulate**: Convert all polygons to triangles.
  - **Volume to mesh*: -
  - **Weld**: Find groups of vertices closer than dist and merge them together.
  - **Wireframe**: Convert faces into thickened edges.
- **Deform**:
  - **Armature**: Deform the shape using an armature object.
  - **Cast**: Ship the shape towards a predefined primitive.
  - **Curve**: Bend the mesh using a curve object.
  - **Displace**: Offset vertices based on a texture.
  - **Hook**: Deform specific points using another object.
  - **Laplacian deform**: Deform based a series of anchor points.
  - **Lattice**: Deform using the shape of a lattice object.
  - **Mesh deform**: Deform using a different mesh, which acts as a deformation cage.
  - **Shrinkwrap**: Project the shape onto another object.
  - **Simple deform**: Deform the shape by twisting, bending, tapering, or stretching.
  - **Smooth**: Smooth the mesh by flattening the edges between adjacent faces.
  - **Smooth corrective**: Smooth the mesh while still preserving the volume.
  - **Smooth laplacian**: Reduce the noise on a mesh surface with minimal changes to its shape.
  - **Surface deform**: Transfer motion from another mesh.
  - **Warp**: Warp parts of a mesh to a new location in a very flexible way thanks to two specified objects.
  - **Wave**: Adds a ripple-like motion to an objects geometry.
- **Physics**:
  - **Cloth**: -
  - **Collision**: -
  - **Dynamic paint**: -
  - **Explode**: Break apart the mesh faces and let them follow particles.
  - **Fluid**: -
  - **Ocean**: Generate a moving ocean surface.
  - **Particle instance**: -
  - **Particle system**: Spawn particles from the shape.
  - **Soft body**: -
- **Hair** curves:
  - **Deformation**: blend, frizz, roll, rotate, shrinkwrap, smooth, straighten, trim, noise.
  - **Generation**: generate, duplicate, interpolate.
  - **Guides**: braid, clump, curl.
  - **Utility**: attach hair curves to surface, redistribute curve points, restore curve segment length.
  - **Write**: set hair curve profile.
- **Geometry nodes**: -


## Modelling


## Donut tutorial basics

1. Start with a **torus** primitive (`shift + A`) for the donut.
2. Apply smooth shading and **subdivision surface** modifier.
2. Deform it with **proportional editing** (`O`).
3. Use **edge selection** (`Alt` + select edge) to select the middle edge and slightly scale it down (`S`).
4. Create ice: duplicate donut, delete vertices in the lower half, apply **solidify** modifier.
5. 
6. 



## Links

- [Blender 4.0 Beginner donut tutorial](https://www.youtube.com/playlist?list=PLjEaoINr3zgEPv5y--4MKpciLaoQYZB1Z)
- [Blender shortcuts](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/blender_shortcuts.pdf)