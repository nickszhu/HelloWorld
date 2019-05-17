# 3D Game Tutorial

### Unity UI

- Project Window: list all the *assets*
- Console Window
- Hierarchy Window
- Scene View
- Game Window
- Inspector Window

### Basic Control:
`F` : focus on a selected object

`Left click` : select

`Middle click` : drag

`Right click` : rotate

### Prefabs
Prefabs are a special type of Asset that represent a GameObject or collection of GameObjects with components that are already set up.  They’re like a blueprint which you can use to easily make instances of the same thing. Each instance of a Prefab is linked to the Prefab Asset, so changing the Asset will change all versions of the Prefab in all Scenes.

### Animators
Animator Controllers contain a *state machine* which determines what animation the Animator component should be setting for its hierarchy at any given time. You can add animations and animation transitions into Controllers.

### Rigidbody
To make your charactor react to physics, use Rigidbody component to represent it is rigid. Restrict movement and rotations of the charactor in xyz directions.

### Collider
Colliders define the shape of an object for the purpose of physical collisions, allowing your character to hit things and be hit. 

### Scripts
- add a Script Component
- drag the scripts you wrote to component in Inspector Window

### Environment
- Directional lights
- Global Illumination Lightmapping
- NavMesh: an invisible shape over the ground that defines an area within which selected GameObjects can move.  

### Cinemachine
- One or more ‘virtual’ cameras are created in a Scene.
- These virtual cameras are managed by a component called the Cinemachine Brain.
- The Cinemachine Brain is attached to the same GameObject as a Camera component — by default this will be the Main Camera GameObject.
- The Cinemachine Brain manages all of the virtual cameras and decides which virtual camera (or combination of virtual cameras) the actual camera should follow.

### Post-Processing Effects
post-processing effects are grouped together and used on different areas of the game world. This means that when the camera is in a particular area, its designated set of processes are applied to the image.
