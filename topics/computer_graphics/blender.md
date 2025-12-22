# Blender fundamentals

<br>![computer graphics image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/computer_graphics.jpg)

## Table of Contents
+ [Basics](#basics)
+ [Editing](#editing)
+ [Materials](#materials)
+ [Modifiers](#modifiers)
+ [Sculpting](#sculpting)
+ [Donut tutorial basics](#donut-tutorial-basics)
+ [Links](#links)


## Basics

**Blender** is a free, open-source, multiplatform 3D computer graphics software tool set. It's used for creating animated films, visual effects, art, 3D-printed models, motion graphics, interactive 3D applications, and virtual reality.

A **mesh** is made of a single **vertex** (singular) or many **vertices** (plural). An **edge** is made of two vertices joined by a line. A **face** is made of 4 vertices forming a square.

- **View movement**:
  - **Orbit**: `MMB` (middle mouse button).
  - **Zoom**: `scroll` (discrete) or use the magnifying glass icon (continuous).
  - **Pan view**: `Shift MMB`
  - **Look through camera**: Use camera icon. Take photo with `F12` (Render/Render image).

- **Basic windows**:
  - **Viewport**: Scene showing 3D objects.
  - **Scene objects menu**: List of objects in the scene.
  - **Properties menu**: Different properties (some are general, some are selection dependent).
  
- **Workspace**: Setup with different types of windows for working on a specific type of task. There're some preconfigured workspaces (layout, modelling, sculpting, UV editing, texture paint, shading, animation, rendering, compositing, geometry nodes, scripting), but you can custom or create new ones.

- **Viewport shading** (`Z`): Type of rendering used in the viewport. Change it using the top right icons.
  - Wireframe
  - Solid
  - Material
  - Rendered

- **Object Interaction mode**: `tab` (switch between object and edit mode), `Ctrl tab` (choose mode), or change it in the top left drop-down list. Modes:
  - Object
  - Edit
  - Sculpt
  - Vertex paint
  - Weight paint
  - Texture paint

- **Properties menu**: Basic properties:
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
    - **Move**: `G`. Move along axis with `G + MMB` or `G + X/Y/Z` (or `G + hold MMB`).
    - **Rotate**: `R`. Rotate along axis with `R + MMB` or `G + X/Y/Z`.
    - **Scale**: `S`. Scale along axis with `S + MMB` or `S + X/Y/Z`.
    - **Move camera**: Like any other object (default), or like the view (select camera object > object properties > camera to view)
	- **Cancel any move/rotation/scaling**: `Alt G/R/S`
	
- **Edition**:
  - **Add object**: `shift + A`. Right after creation, you have temporary options available.
  - **Delete**: `x` or `supr`.
  - **Duplicate** (`Shift D`): Duplicate object (immediately). Keep it in its original place with `esc` or `RMB`. Cancel duplication with `Ctrl Z`.
  - **Proportional editing** (`O` or top icon): Set mode (`O`), select vertices, grab them (`G`), set influence radius (scroll), and move the vertices.
  - **Shade flat/smooth**: `RMB` on object and select shading type.
  - **Snap** (`shift tab` or top icon): When moving vertices, they follow a surface.
  - **Extrude** (`E`): Add new vertices out of existing ones.
  - **Translate along a plane**: With comma (`,`) select orientation `normal`. Then move with `G X/Y/Z`.
  - **Join meshes**: Select them in Object mode > `Ctrl J`
  - **Detach face** (`Y`)
  
- **Others**:
  - **Object properties**: `N`
  - **F3**: Search.
  - **Remove window**: RMB on divider > `Join areas` > Select area to remove
  - **Toggle X-ray**: `Alt Z`
  - **Select linked vertices**: Select vertex and `Ctrl L`
  - **Select edge chain**: `Alt` + select edge.
    - **Add next edge chain to selection**: `Select/More` or `Select/Less` (numpad alternative: `Ctrl +` or `Ctrl -`).
  - **Hide part of your mesh**: Select vertices > `H` (to unhide: `Alt H`).
  - **Link two objects**: Select both > `Ctrl P` > `Object (Keep transform)` (last selection is parent)
  - **Face culling**: `Viewport shading > backface culling` (not activated by default).
  - **Full screen**: `Ctrl Alt Space`
  - **Create new object from selected vertices**: `P` > `Selection`
  
**Edit mode tools**:

Keep LMB on a tool icon to show different variants. Right after applying a tool, you have temporary options available. The tools are:

- **Annotate**: Make annotations on the active data. Variants: Normal, Line, Polygon, Eraser.
- **Measure**: Measure distance and angles.
- **Add cube**: Add cube on top of a surface.
- **Extrude** (`E`):
  - __Region__: Extrude freely or along an axis.
  - __Manifold__: Extrude, dissolves edges whose faces form a flat surface and intersect new edges.
  - __Along normals__: Extrude region together along local normals.
  - __Individual__: Extrude each individual face separately along local normals.
  - __To cursor__: Duplicate and extrude selected vertices, edges or faces towards the mouse cursor.
- **Insert faces** (`I`): Insert new faces into selected faces.
- **Bevel** (`Ctrl B`): Cut into selected items at an angle to create bevel or chamfer.
- **Loop cut** (`Ctrl R`):
  - __Loop cut__: Cut mesh loop and slide it.
  - __Offset edge loop cut__: Offset edge loop slide.
- **Knife** (`K`):
  - __Knife__: Cut new topology.
  - __Bisect__: Cut geometry along a plane (click-drag to define plane).
- **Poly build**: 
- **Spin**:
  - __Spin__: Extrude selected vertices in a circle around the cursor in indicated viewport.
  - __Spin duplicates__: Extrude selected vertices in a circle around the cursor in indicated viewport.
- **Smooth**:
  - __Smooth__: Flatten angles of selected vertices.
  - __Randomize__: Randomize vertices.
- **Slide**:
  - __Edge__: Slide an edge loop along a mesh.
  - __Vertex__: Slide a vertex along a mesh.
- **Shrink/Fatten**:
  - __Shrink/Fatten__: Shrink/Fatten selected vertices along normals.
  - __Push/Pull__: Push/pull selected items.
- **Shear**:
  - __Shear__: Shear selected items along the given axis.
  - __To sphere__: Move selected items outward in a spherical shape around geometric center.
- **Rip**:
  - __Region__: Rip polygons and move the result.
  - __Edge__: Extend vertices and move the result.



- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
- ****: 
  
## Materials
  
**Material** properties (Properties menu > Texture >  `new`): This menu is a simplified version of the Shader editor (both are linked).
  - Surface: `Base color`, `Roughness`, `Normal`…
    - Options: `Image texture` (load from file)…
  
**Shader editor** (in shading workspace ): Use nodes to create a shader (like a PBR shader)
  - **Add node**: `shift + A` (or select input point from a node > drag > select type of node)
  - Specify the type of texture (`sRGB`, `Non-color`…). Normal maps also need an intermediate node (`normal map`).

**Texture paint** (workspace):
  - Painting a texture requires creating an image, and saving it once finished.
  - Default objects already have UV wrapping done.




## Modifiers

**Modifiers** add a procedural operation/effect to the active object. Main options: `Apply modifier` (applies changes to mesh).

Note: if your object disappears after applying a modifier, deselect `Properties/Viewport/GPU subdivision`.

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
  - __**Subdivision surface**__: Split faces into smaller parts, giving smoother appearance. If GPU doesn't support this, deselect `Edit/Preferences/Viewport/GPU subdivision`.
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
  - __**Shrinkwrap**__: Project the shape onto another object.
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


## Sculpting

Sculpting is done in the **Sculpting mode**. Sculpt options are applied before modifiers are applied. Thus, sometimes you may want to `Apply modifier` so the model has enough geometry for sculpting. Basic controls are:

- Adjust brush size: `F`
- Adjust strength: `Shift F`
- Prevent tool from reaching opposite side of the mesh: Brush > `Front face only`
- Mask options: Mask
  - `Clear mask`
  - `Smooth mask`
  - Invert mask: `Ctrl I`

**Tools**:

- Inflate (`I`)
- Grab (`G`)
- Mask (`M`): Paint areas you don't want to be affected by a subsequent tool.
- Mesh filter: Applies a uniform filter to the entire mesh (except masked areas).
- Smooth (`S`) 


## Donut tutorial basics

1. Start with a **torus** primitive (`shift + A`) for the donut.
2. Apply smooth shading and **subdivision surface** modifier.
3. Deform it with **proportional editing** (`O`).
4. Use **edge selection** (`Alt` + select edge) to select the middle edge and slightly scale it down (`S`).
5. Create ice: duplicate donut, delete vertices in the lower half, apply **solidify** modifier.
6. Edit ice borders:
  - Snap (snap individual elements to `face project`)
  - Increment geometry (`Apply modifier`) so the ice snaps well.
  - Select some geometry and hide it (`H`) so proportional editing don't mess up our geometry.
  - Proportional editing.
7. Add detail to ice:
  - Add **subdivision surface** modifier.
  - Transform borders from U to C shape: **Solidify** modifier > Edge data > Increase `Crease inner`.
  - Add drops: Extrude (`E`)
8. Fix snapping errors using **Shrinkwrap** and `Apply modifier`.
9. Add thickness to ice borders and drops:
  - `Apply modifier` solidify (we need the geometry)
  - `Apply modifier` subdivision surface (we need more geometry)
  - Sculpt tools used:
    - **Inflate** for drops
    - **Grab** for making drop tails thinner
    - **Mask** for masking the borders we want to inflate (
	- **Mesh filter** for inflating the whole mesh (except mask)
    - **Smooth** for removing artifacts
10. Create counter: `Shift A` > `Plane`
11. Parent both objects (`Ctrl P`) and put then on the counter.
12. Set **materials** (in Shading workspace or Properties menu): Configure `Base color`, `roughness`, and `normals`. Load texture files.
13. **Texture paint** workspace: Paint the middle of the donut.



## Links

- [Blender 4.0 Beginner donut tutorial](https://www.youtube.com/playlist?list=PLjEaoINr3zgEPv5y--4MKpciLaoQYZB1Z)
- [Blender shortcuts](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/computer_graphics/blender_shortcuts.pdf)