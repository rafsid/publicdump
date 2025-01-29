 



Welcome to Learn OpenUSD: Foundations. This multi-course curriculum serves as an entry point to your journey learning OpenUSD, and is focused on teaching foundational terminology, Python best practices, and introducing concepts that are important to OpenUSD workflows. 
In this course, Learning About Stages, Prims and Attributes, we will: 
* Create and manipulate USD files. Learn how to set up our own USD files from scratch, setting the foundation for your 3D scenes.
* Define primitives. Get hands-on experience with defining various types of prims, the building blocks of USD, and understand their roles in a 3D environment.
* Establish scene hierarchies. Discover how to organize and structure 3D elements effectively, creating a coherent and manageable scene hierarchy.
* Light up scenes. Add dynamic lighting to scenes, bringing them to life and enhancing their visual appeal.
* Manage attributes and metadata. Delve into the details of attributes and metadata, learning how to set, get, and manipulate these essential elements.
* Traverse and inspect USD files. Develop skills to traverse through USD files, inspecting and understanding the intricate details of our scenes.
* Verify prims' existence. Learn techniques to check for the existence of specific prims, ensuring the integrity and completeness of our 3D scenes.
This course is designed for both beginners and those with some experience in 3D graphics and OpenUSD, providing you with the knowledge and skills to effectively use OpenUSD in your projects. We encourage you to actively participate in the activities and quizzes to enhance your learning experience.


Overview: Creating an OpenUSD Stage
Let's get started with the first module in this course! In this module, Creating an OpenUSD Stage, we will:
* Define the role of stages in 3D scene description.
* Explain the components of Hydra within OpenUSD.
* Identify the characteristics and use cases of USD, USDC, USDA and USDZ file formats. 
* Implement practical examples to manipulate 3D scenes programmatically with Python. 
Continue to the first lecture: What is a Stage?


 



Welcome to this lesson on OpenUSD stages, a core element in 3D scene description. Understanding OpenUSD stages enables collaboration across various applications and datasets by allowing us to aggregate our data in one place. 
At its core, an OpenUSD Stage presents the scenegraph, which dictates what is in our scene. It is the hierarchy of objects, called prims. These prims can be anything from geometry, to materials, to lights and other organizational elements. This scene is commonly stored in a data structure of connected nodes, which is why we refer to it as the scenegraph. 

How Does It Work?
Think of it as a scene, a shot or a scenario we may open up in a DCC. A stage could be made up entirely with just one USD file (like a robot), or it could be a USD file that includes many more USD files (like a factory with many robots). The stage is the composed result of the file or files that may contribute to a scenegraph.
Composition is the result of the algorithm for how all of the USD files (or layers, in USD parlance, as USD content need not be file-backed) should be assembled and combined. We’ll look at composition more closely later on.

￼
In the example above, we have a stage, which contains USD assets in the scenegraph, like Car.usd, Environment.usd, Lighting.usd and Cameras.usd. This organization is useful for aggregating data for architectural workflows, factory planning and manufacturing, visual effects in filmmaking – anywhere where multiple assets need to be combined and integrated seamlessly.
Each one of these USD assets can also be opened independently of the current stage. In this case, if we opened Car.usd, it would have its own stage that would be composed of Simulation.usd and Geometry.usd.
When we leverage OpenUSD stages properly, we can enable:
* Modularity: Stages enable the modification of individual elements without altering the original files (“non-destructive” editing), fostering a flexible workflow upon modular scene elements.
* Scalability: Stages can manage large datasets efficiently (e.g., via payloads, which we’ll learn more about when we dive deeper into composition).
Working With Python
Creating a USD stage is the first step to generating a new USD scenegraph. In Python, we can use the functions: 
# Create a new, empty USD stage where 3D scenes are assembled
Usd.Stage.CreateNew()
  
# Open an existing USD file as a stage
Usd.Stage.Open()
  
# Saves all layers in a USD stage
Usd.Stage.Save()
Key Takeaways
An OpenUSD stage is the key to managing and interacting with 3D scenes using USD. The stage enables non-destructive editing, layering, and referencing, making it ideal for complex projects involving multiple collaborators. Leveraging OpenUSD stages properly can significantly enhance the efficiency and quality of 3D content production.
In the next lesson, we'll be talking about the rendering architecture within OpenUSD that lets us visualize our stages. 


 


In this lesson, we'll explore Hydra, a powerful rendering architecture within OpenUSD. Understanding Hydra enables efficient and flexible rendering of complex 3D scenes.

Hydra is a rendering architecture within OpenUSD that provides a high-performance, scalable, and extensible solution for rendering large 3D scenes. It serves as a bridge between the scene description data, such as USD, and the rendering backend, such as OpenGL or DirectX. 
The open and extensible nature of Hydra means it supports many different renderers, like Arnold and Renderman, and OpenUSD's included HdStorm renderer offers a simple way for developers to visualize data out of the box. 
Hydra has three main parts:
* A scene delegate, which provides the scene information
* The render index, which keeps track of changes and manages the scene
* The render delegate, which uses the render index and scene delegate to visualize scene information to create the final image.
How Does It Work?
Hydra operates on one or more scene delegates, which is a hierarchical representation of the scene data. It processes the scene delegates into an abstract renderable scene, which render delegates can use to generate rendering instructions tailored for the specific rendering backend. This approach decouples the scene data from the rendering backend, allowing for flexibility and extensibility.
Hydra supports various render delegate plugins, enabling developers to create custom rendering backends or extend existing ones. OpenUSD ships with HdStorm, the real-time OpenGL/Metal/Vulkan render delegate leveraged by usdview and many other tools. It also ships with HdTiny and HdEmbree, which can be used as examples of how to implement render delegates. 

Key Takeaways
Understanding Hydra enables efficient and flexible rendering of complex 3D scenes. Now, we know that:
* Hydra is a rendering architecture within OpenUSD that bridges scene data and rendering backends.
* It operates on a scene delegate and enables render delegate plugins to generate rendering instructions for specific backends.
* Hydra supports various rendering backends and techniques, including rasterization and ray tracing.
* It provides extensibility through plugins and custom rendering backends.
With its support for various rendering techniques, extensibility, and decoupling of scene data from rendering backends, Hydra empowers users to create work in large scenes. We encourage you to explore Hydra further and leverage its capabilities in your OpenUSD projects.


 



In this lesson, we'll explore the core OpenUSD file formats – USD, USDA, USDC and USDZ. All the formats are used by OpenUSD for storing and exchanging 3D scene data of various types, including meshes, cameras, lights, and shaders.

What is USDA?
USDA (.usda) are ASCII text files that encode scene descriptions in a format that can easily be read and edited. It is a native file format used by OpenUSD to store and exchange 3D scene data. It is human-readable, which makes USDA particularly useful for tasks that involve manual editing or inspection of scene data. This makes USDA optimal for small files, such as a stage that is referencing external content. 
What is USDC?
The Crate Binary Format, or USDC (.usdc), is a compressed binary file format used by OpenUSD to store and exchange 3D scene data. It is designed to minimize load time and provide a more efficient representation of the scene data compared to the human-readable ASCII format (USDA).
The Crate Binary Format uses various compression techniques to reduce the file size and improve loading performance. It also employs memory mapping for faster file access and loading times. The structure of the file is organized in a way that allows for efficient parsing and retrieval of the scene data. USDC is extremely efficient for numerically-heavy data, like geometry.
What is USD?
A USD (.usd) file can be either ASCII or binary – the advantage of which is that we can change the underlying format at any point without breaking references. Using USD is also beneficial for debugging, because an asset that is in binary can easily be changed to ASCII to take a look at what might be causing the issue. As we learn more about USD, we may decide to separate heavier data from more light weight data. When doing so, consider using .usdc and .usda explicitly to avoid obfuscation and create large .usda files unintentionally.
What is USDZ?
Let’s also touch on USDZ (.usdz). USDZ is an atomic, uncompressed, zipped archive so that we can deliver all of the necessary assets together. We would not use USDZ if we are still making edits to the asset, but it is a great way to package and ship our asset when it is complete. For example, a mesh with its texture files can be delivered as one archive. It’s generally intended as read-only and is optimal for XR experiences. More on USDZ will be covered in future lessons.
Each USD file format can be created through Python bindings in the OpenUSD library. When creating a new stage we can pass in a string to represent a file name that ends in .usdc, .usd, .usda, or .usdz.
For this course, we will primarily be using USDA files because they are readable, but as we work more with OpenUSD, we may choose to use USDC or USD instead. We may also choose to use some other 3D format backed by an SdfFileFormatPlugin if we prefer to keep our source data as is and still leverage all of OpenUSD for scene manipulation and rendering.
Key Takeaways
Now, we should have a better understanding of the various OpenUSD file formats and the purpose each one serves. 
    * There are four native formats: USD, USDA, USDC and USDZ and they are used by OpenUSD for storing and exchanging 3D scene data.
    * All OpenUSD file formats are hierarchical and extensible based on layers and composition, which supports non-destructive editing, collaboration, and interoperability between different software tools.
    * Any other 3D file format can be loaded into OpenUSD Stages through plugins. It’s worth noting that any data provider can implement file format plugins to natively speak USD – even .usdc, .usd, .usda, and .usdz are file format plugins.
    * Developers can interact with USD files using Python bindings.

Top of step 1
The top bar within your course allows you to easily jump to different sections and shows you what’s coming up.
Okay

Bottom of step 1


Activity: Creating a USD File
We've just completed the first three lessons in this course. Now, let's switch over to the Jupyter notebook environment and complete Activity 1: Creating a USD File, then we'll return to the course.
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.




 


As we finish this module, we should have a foundational understanding of OpenUSD stages and their significance in 3D scene description. Here's a recap of what we covered: 
* Defined OpenUSD stages. We explored the concept of stages as hierarchical scenegraphs that organize various scene elements, such as geometry, materials, and lights, into a cohesive structure. This modular approach allows for efficient data management and non-destructive editing, enabling flexibility and scalability in complex projects.
* Discussed Hydra rendering architecture. We introduced Hydra, a powerful rendering architecture within OpenUSD that decouples scene data from rendering backends. This flexibility supports various rendering techniques and enables efficient visualization of complex scenes.
* Explored OpenUSD file formats. We discussed the different file formats used in OpenUSD, including USDA, USDC, USD, and USDZ, each serving specific purposes in storing and exchanging 3D scene data.
* Experimented with Python. We learned how to create, open, and save USD stages using Python functions. This hands-on experience is crucial for programmatically managing 3D scenes and integrating them into larger workflows.
In the next module, Creating a Prim, we'll introduce the concept of primitives in Universal Scene Description.
Quiz
4/4 points (graded)
What is an OpenUSD stage, and what role does it play in 3D scene description?

A stage is a rendering engine for 3D scenes.

A stage is a hierarchical scenegraph that organizes objects called prims.

A stage is a file format for storing 3D models.

A stage is a tool for editing textures.
correct
Answer
Correct:Correct. An OpenUSD stage is a hierarchical scenegraph that organizes objects called prims, which can include geometry, materials, and lights. It allows for modular and scalable management of 3D scenes.
Which Python function would you use to create a new USD stage?

Usd.Stage.CreateNew()

Usd.Stage.New()

Usd.Stage.Open()

Usd.Stage.Save()
correct
Answer
Correct:Correct. The function Usd.Stage.CreateNew() is used to create a new USD stage.
USDA files are binary files that provide efficient data storage for large datasets.

True

False
correct
Answer
Correct:USDA files are human-readable ASCII text files, making them ideal for manual editing and inspection of scene data.
What are the differences between the USD, USDA, USDC, and USDZ file formats?

USD is ASCII or binary; USDA is human-readable; USDC is binary; USDZ is an uncompressed archive.

USD is a text format; USDA is binary; USDC is ASCII; USDZ is a compressed archive.

USD and USDZ are for text files; USDA and USDC are for binary files.
correct
Answer
Correct:USD can be either ASCII or binary; USDA is a human-readable ASCII format; USDC is a compressed binary format for efficient data representation; USDZ is an uncompressed archive for packaging complete assets.
Show answer
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.

Overview: Creating a Prim
Welcome to the module on Creating a Prim. In this module, we will:
* Identify the role of prims, including what a prim is and its role within the OpenUSD ecosystem.
* Review the various prim attributes and types of data that a prim can encapsulate, such as geometry, materials, and transformations.
Continue on to learn about prims! 

 



Primitives, or prims for short, are the building blocks of any OpenUSD scene, making understanding them essential for anyone working with 3D content creation and manipulation in the OpenUSD ecosystem. 

A prim is the core component within the USD framework. Think of a prim as a container that holds various types of data, attributes, and relationships which define an object or entity within a scene. A prim can be a type of imageable or non-imageable entity, such as a mesh, a material, or a light or an xform. Prims are organized in a hierarchical structure, creating a scenegraph that represents the relationships and transformations between objects in the scene. 
Each prim has a unique identifier known as a path, which helps in locating it within the scene graph. For example, a prim’s path might be /World/BuildingA/Geometry/building_geo, indicating that it is a child of the Geometry prim, which itself is a child of the BuildingA prim, and so on.
How Does It Work?
Prims can have various types of attributes associated with them, such as position, rotation, scale, material information, animation data, and more. These properties define the attributes and relationships of the objects they represent. 
A key feature of USD prims is their ability to encapsulate data, allowing them to be shared, referenced, and instanced across different scenes and files. This promotes efficient data management, modularity, and collaborative workflows. Typical use cases include defining models, cameras, lights, or even groups of other prims. The ability to efficiently manage and manipulate these prims non-destructively is what makes USD so powerful in various industries where complex scenes are the norm. 
Working With Python
In Python, working with prims involves several methods using the USD Python API:


# Generic USD API command. Used to define a new prim on a stage at a specified path, and optionally the type of prim.
stage.DefinePrim(path, prim_type)

# Specific to UsdGeom schema. Used to define a new prim on a USD stage at a specified path of type Xform. 
UsdGeom.Xform.Define(stage, path)
	
# Retrieves the children of a prim. Useful for navigating through the scenegraph.
prim.GetChildren()
	
# Returns the type of the prim, helping identify what kind of data the prim contains.
prim.GetTypeName()

# Returns all properties of the prim.
prim.GetProperties()
Key Takeaways
In this lesson, we covered what a prim is in the context of OpenUSD, its characteristics, and its role in building and managing 3D scenes. We also looked at how prims facilitate data encapsulation and sharing, which are critical for complex 3D project workflows. Understanding prims is foundational as we start working with OpenUSD.
Let's create our first prim in the next activity. 


Activity: Defining a Cube in the Stage

Congratulations, we've made it to the second activity. Switch over to the Jupyter notebook environment and complete Activity 2: Defining a Cube in the Stage, then return to the course.
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.



Review: Creating a Prim
In this module, we introduced the concept of prims within the OpenUSD framework. Here's a recap of what we covered:
* Identified the role of prims. Prims are essential components in OpenUSD, acting as containers that define objects and their relationships within a scene.
* Explored types of prim data. We explored how prims contain various types of data and attributes, including geometry, material and transformations among others. 
This knowledge sets the stage for more advanced topics in OpenUSD, where you will further explore the manipulation and rendering of complex 3D scenes. In the next module, Creating a Hierarchy, we'll explore ways to organize and add structure to prims in the stage.  
Quiz
2/2 points (graded)
In the context of OpenUSD, what is a prim?

A rendering engine for 3D scenes.

A core component that acts as a container for data and attributes in a scene.

A file format for storing 3D models.
correct
Which of the following qualify as prims in OpenUSD? Select all that apply.

Mesh

Material

Light

Xform
correct
Show answer
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.

Overview: Creating a Hierarchy
In this module, we’ll explore how to organize our stage and prims by creating a hierarchy, focusing on the concepts of scope and xform prims in OpenUSD. In this module, we will:
* Define what a scope is in the concept of OpenUSD.
* Identify the primary function of an xform prim.
* Recall basic Python functions used to define scope and xform prims in a USD scene. 
Let’s begin! 



Understanding scopes is important as they help in organizing and managing complexity in large-scale 3D scenes. 
In OpenUSD, a scope is a special type of prim that is used primarily as a grouping mechanism in the scenegraph. It does not represent any geometry or renderable content itself but acts as a container for organizing other prims. Think of scope as an empty folder on your computer where you organize files; similarly, scope helps in structuring and organizing prims within a USD scene.

How Does It Work?
Scope prims are used to create a logical grouping of related prims, which can be particularly useful in complex scenes with numerous elements. For example, a scope might be used to group all prims related to materials, animation, or geometry. A key feature of scopes is that they cannot be transformed, which promotes their usage as lightweight organizational containers. All transformable child prims (such as geometry prims or xforms) will be evaluated correctly from within the scope prim and down the hierarchy. This organization aids in simplifying scene management, making it easier for teams to navigate, modify, and render scenes. It also enhances performance by enabling more efficient data management and updates within the scene graph.
Working With Python
When working with scope in USD using Python, a couple functions are particularly useful:

# Used to define a new scope at a specified path on a given stage
UsdGeom.Scope.Define(stage, path)

# This command is generic, but it's useful to confirm that a prim's type is a scope, ensuring correct usage in scripts
prim.IsA(UsdGeom.Scope)
Key Takeaways
Scope prims in OpenUSD play a crucial role in the organization and management of complex 3D scenes. Its primary function is to serve as a container for other prims, helping maintain clarity and structure in large projects.
Next, we'll talk about another way to organize prims: the xform. 

 




In Universal Scene Description, xforms play a key role in defining the spatial transformations of objects in a scene.
In OpenUSD, an xform is a type of prim that stores transformation data, such as translation, rotation, and scaling, which apply to its child prims. This makes xforms a powerful tool for grouping and manipulating the spatial arrangement of objects in a 3D scene. Xform stands for 'transform', reflecting its role in transforming the space in which its children reside.

How Does It Work?
Xform prims allow for hierarchical transformations, meaning that transformations applied to a parent xform affect all of its child prims. This is essential in complex scenes where multiple objects need to move or scale relative to the parent. Typical use cases include animating characters or robotic arms, where different parts are children of an xform prim, or arranging furniture in architectural visualization, where all items in a room might be scaled or rotated together.
Working With Python
Working with xform in USD via Python involves several functions:

# Used to define a new Xform prim at a specified path on a given stage
UsdGeom.Xform.Define(stage, path)

# Retrieves the order of transformation operations, which is crucial for understanding how multiple transformations are combined. Different orders can yield different results, so understanding XformOpOrder is important. 
xform.GetXformOpOrderAttr()
	
# Adds a new transform operation to the xform prim, such as translation or rotation, with specified value   
xform.AddXformOp(opType, value)
Key Takeaways
Now, we've explored what xform prims are and how they function within the USD framework. We've seen how xform prims are essential for defining and managing spatial transformations in a scene, making them indispensable for any 3D content creation workflow.
Let's experiment with the concept of container prims, like scope and xform, in our next activity. 


Activity: Creating a Hierarchy

Now, we're ready to move onto Activity 3: Creating a Hierarchy. Switch over to the Jupyter notebook environment and come back to the course when complete.
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.


Top of step 1
The top bar within your course allows you to easily jump to different sections and shows you what’s coming up.
Okay

Bottom of step 1


Review: Creating a Hierarchy

 



In this module, we explored the use of scope and xform prims within OpenUSD to create a hierarchy. In this module, we:
* Defined scopes. We discussed how scopes serve as containers to organize other prims without applying transformations.
* Identified key functions of xforms. We reviewed how like scopes, xforms can serve as container prims while applying spatial transformations to their child prims.
* Implemented basic Python functions. We leveraged basic Python functions used to define scope and xform prims in a USD scene. 
This hierarchical organization is essential for managing complex 3D scenes. Now that we understand a little bit about how to organize our USD scenes, let’s move on to the next module. 

Quiz
3/3 points (graded)
A scope prim in OpenUSD can be used to apply transformations to its child prims.

True

False
correct
Answer
Correct:A scope prim can serve as a container for child prims, but cannot apply transformations.
What is the primary function of an xform prim in OpenUSD?

To render geometry

To store transformation data such as translation, rotation and scaling

To act as a non-transformable container
correct
Which Python function is used to define a new scope prim in a USD stage?

UsdGeom.Xform.Define(stage, path)

UsdGeom.Cube.Define(stage, path)

UsdGeom.Scope.Define(stage, path)
correct
Show answer
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.

Lecture: What Are Commonly Used USD Modules?
 



In this lesson, we're talking about a few commonly used USD modules that are a great place to start for OpenUSD development. The USD code repository is made up of four core packages: base, usd, imaging, and usdImaging. To author and read USD data, you only need the base and usd packages. We will focus on modules found in these two packages.

USD’s API consists of many modules with varying purposes including: authoring, reading, and composing USD data, imaging composed scenes, defining plugin interfaces for extending USD’s capabilities, and more.
How Does It Work
When authoring or querying USD data, you will almost always use a few common USD modules such as Usd, Sdf, and Gf along with some schema modules. Schemas are grouped into schema domains and each domain has its own module. The schema modules you use will depend on the type of scene description you’re working with. For example, UsdGeom for geometry data, UsdShade for materials and shaders, and UsdPhysics for physics scene description. 
Working With Python
The schema modules are covered more in depth in relevant videos for each domain. Let’s have a closer look at a few of the other common USD modules: Usd, Sdf, and Gf. In Python, you can import these modules from the pxr namespace:
# Import Usd, Sdf, and Gf libraries from Pixar
from pxr import Usd, Sdf, Gf

Usd is the core client-facing module for authoring, composing and reading USD. It provides an interface for creating or opening a Stage and generic interfaces for interacting with prims, properties, metadata, and composition arcs. 
Sdf (scene description foundation) provides the foundations for serializing scene description to a reference text-based file format and implements scene description layers, (SdfLayer) which stores part of the scene description. Most notably, you will commonly see this module used for managing prim and property paths and creating USD layers.
Gf is the graphics foundation and contains the foundation classes and functions that contribute graphics, like Linear Algebra, Basic Mathematical Operations and Basic Geometry. This module contains classes for 3D data types that you will use for getting and setting particular USD attributes.
Key Takeaways
Now, you should be more familiar with the commonly used  USD modules for OpenUSD development to start exploring the OpenUSD API on your own. You can find the full set of core packages and modules available to you on OpenUSD.org.

 
Lecture: What Are USD Lights?
In this lesson, we'll explore lights in OpenUSD, schemas belonging to the UsdLux domain. Understanding lights in OpenUSD allows for accurate and realistic lighting in 3D scenes.

USDLux includes a set of light types and light-related schemas. It provides a standardized way to represent various types of lights, such as:
* Directional lights (UsdLuxDistantLight)
* Area lights, including
    * Cylinder lights (UsdLuxCylinderLight)
    * Rectangular area lights (UsdLuxRectLight)
    * Disk lights (UsdLuxDiskLight)
    * Sphere lights (UsdLuxSphereLight)
* Dome lights (UsdLuxDomeLight)
* Portal lights (UsdLuxPortalLight)
How Does It Work?
Start by defining light prims within a USD scene. These light primitives consist of scene description for specific light types (e.g., UsdLuxDistantLight for directional lights) and contain attributes that provide comprehensive control over the light's properties, such as intensity, color, and falloff. These light primitives allow for accurate lighting calculations during rendering. 
Working With Python
Here are a few relevant Python commands for working with USD lights:

# Import the UsdLux module
from pxr import UsdLux
	
# Create a sphere light primitive
UsdLux.SphereLight.Define(stage, '/path/to/light')

# Set the intensity of a light primitive
light_prim.GetIntensityAttr().Set(500)
UsdLux has API schemas that allow you to add light behavior to prims in your scene, so you can also add light properties to meshes and volumes.

Key Takeaways
OpenUSD provides a standardized way to represent various types of lights in a USD scene to ensure consistent light behavior across different applications and renderers. They support different properties and attributes, and advanced features like light filters, IES profiles and linking. Renderers can utilize USD’s lights and materials for accurate lighting calculations.
By understanding how to define and control lights within OpenUSD, developers and 3D practitioners can achieve realistic lighting, enhance visual quality, and unlock new possibilities in their projects.

Activity: Lighting a Stage
 


Now that we understand a little bit about lights in OpenUSD, let's switch over to the Jupyter notebook environment and complete Activity 4: Lighting a Stage. Return to the course when you're ready to continue.
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.
Open Jupyter Notebook



Overview: Lighting a Stage
 



In this module, we explored the basics of lighting in OpenUSD. Here's a recap of what we accomplished:
* Introduced the commonly used USD modules. We covered the foundational USD modules like Usd, Sdf and Gf, which are essential for creating, reading and composing USD data.
* Identified lights in the UsdLux domain. We learned about various light types and how to define and control these lights in a USD scene. 
* Leveraged Python functions for lighting. We imported USD modules like UsdLux, and added lights from the UsdLux module to our stage with various Python functions. 
By understanding these concepts, we can now think about implementing realistic lighting in our 3D projects using OpenUSD. Test your knowledge with the quiz before continuing on to the next module!
Quiz
3/3 points (graded)
The Usd module is primarily used for defining light properties in USD scenes.

True

False
correct
Answer
Correct:The Usd module is used for authoring, composing, and reading USD, not specifically for defining light properties.
Which of the following is NOT a type of light available in the UsdLux domain?

UsdLuxDistantLight

UsdLuxCylinderLight

UsdLuxSpotLight

UsdLuxSphereLight
correct
Answer
Correct:SpotLight is not mentioned in the provided UsdLux light types.
The UsdGeom module is used for defining 3D graphics-related prims and property schemas.

True

False
correct
Answer
Correct:UsdGeom is used for defining 3D graphics-related prims and property schemas.
Show answer
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.


Overview: Defining Attributes
 



Welcome to the fifth module in the Learning About Stages, Prims and Attributes course. This module, Defining Attributes, focuses on the concept of properties (including attributes and relationships) within the OpenUSD framework. 
In this module, we will:
* Identify the two types of OpenUSD properties. 
* Describe the function of attributes and relationships in OpenUSD. 
* Recognize the role of primvars and XformCommonAPI in reference to attributes. 
* Leverage some basic Python functions for attribute manipulation.
Continue on to the first lecture.

Lecture: What Are Attributes?
 



USD attributes are one of the two types of USD properties, the other being relationships. Properties are used to describe the characteristics of objects, or "prims," within a USD scene. 
Attributes store data values that define the appearance, behavior, or other properties of a prim. 
Relationships, on the other hand, establish connections between prims, enabling hierarchical structures and data sharing.
For this lesson, we'll concentrate on attributes.

Attributes are the most common type of property that you'll work with when creating scenes. An attribute can have one specific data type, such as a number, text, or a vector. Each attribute can have a default value, and it can also have different values at different points in time, called timeSamples.
How Does It Work?
Attributes are name-value pairs (often referred to as key-value pairs) that store data associated with a prim. 
Any given attribute has a single, defined data type associated with it. Each attribute is defined with the type of data that it can hold. A single attribute can represent various types of properties, such as the vertices of a piece of geometry, the diffuse color of a material, or the mass of an object. These are typically defined through the Sdf library.
Some common examples of attributes include:
* Visibility - Controls the visibility of a prim in the scene.
* Display color - Specifies the display color applied to a geometric prim.
* Extent - Defines the boundaries of a geometric prim. 
Attributes can be authored and stored within USD layers, which are files that describe different aspects of a scene. When a USD stage is composed, the attribute values from various layers are combined according to specific composition rules, allowing for flexible scene assembly.
Attributes can be animated by providing multiple key-framed values over time. OpenUSD's timeSampling model ensures efficient storage and interpretation of animated data.
Working With Python
To work with attributes in OpenUSD, we will generally use schema-specific APIs. Each schema-specific API has a function to grab its own attributes. Review the following examples to learn more. 

# Get the radius value of sphere_prim that is of type UsdGeom.Sphere
sphere_prim.GetRadiusAttr().Get()

# Set the double-sided property of the prim
sphere_prim.GetDoubleSidedAttr().Set(True)

While there’s also a dedicated UsdAttribute API, in general, it's preferred to use the schema-specific methods, if they exist, as they are more clear and less brittle. You can learn more about how to work with each specific schema on OpenUSD’s documentation.
Key Takeaways
In summary, 
* Attributes are values with a name and data type that define the properties of prims in a USD scene. 
* Attributes are the primary means of storing data in USD. 
* Each attribute has a single, defined data type.
* Attributes are authored and stored within USD layers, enabling efficient scene composition.
* Attributes can be animated by providing key-framed values over time.
* They can be queried, modified and animated using the USD API.
Understanding attributes is essential for creating rich and detailed 3D scenes, enabling efficient collaboration and interoperability across various tools and pipelines.
In the next lesson, let's talk about the other USD property: relationships.


Lecture: What Are Relationships?
 



In the previous lesson, we introduced the concept of USD properties, which are used to describe the characteristics of prims in USD scenes. As mentioned, there are two types of USD properties: attributes and relationships. This lesson will discuss relationships. 
Relationships establish connections between prims, acting as pointers or links between objects in the scene hierarchy. A relationship allows a prim to target or reference other prims, attributes, or even other relationships. This establishes dependencies between scenegraph objects.

How Does It Work?
Relationships store path values that point to other scene elements. When you query a relationship's targets, OpenUSD performs path translations to map the authored target paths to the corresponding objects in the composed scene prims.
Relationships are robust against path translations, a key advantage over hard-coded paths. If a target prim's path changes due to editing or referencing, the relationship automatically remaps to the new location.
Relationships can have multiple targets, making them useful for grouping or collecting objects together. For example, a material relationship might target all geometry prims that should use that material.
Note that a relationship is an alternative type of property to an attribute. Unlike an attribute, it has no data type. It is a way of declaring, at creation time, that the only use for a property is to record linkage information. Conceptually, it is like an attribute whose data type is a "link". This means you can not use a relationship to connect two already-existing attributes - for that, you can use attribute connections.
Working With Python
Here are a few Python commands to familiarize yourself as you work with relationships. These can be useful as you establish connections between different scene elements, like materials and geometry.

# Get the target paths of a relationship
UsdRelationship.GetTargets()

# Set the target paths for a relationship
UsdRelationship.SetTargets()

# Add a new target path to a relationship
UsdRelationship.AddTarget()

# Remove a target path from a relationship
UsdRelationship.RemoveTarget()
Key Takeaways
Relationships enable robust encoding of dependencies and associations between scene elements, such as:
* Binding geometry to materials
* Grouping prims into collections
* Establishing connections in shading networks
* Modeling hierarchical relationships (e.g. parent-child)

Using relationships instead of hard paths enhances:
* Non-destructive editing workflows
* Referencing and asset reuse across tools
* Collaborative workflows across teams

Relationships are a way to link scene elements while enabling non-destructive editing and cross-tool collaboration. They enhance the flexibility and scalability of OpenUSD-based pipelines.




Lecture: What Are Primvars?
 



Primvars enable efficient management and manipulation of hierarchical object data in complex 3D scenes. Continue on with this lesson to learn more.



Short for primitive variables, primvars are special attributes that contain extra features. They address the following problems in computer graphics:
* The need to "bind" user data on geometric primitives that becomes available to shaders during rendering.
* The need to specify a set of values associated with vertices or faces of a primitive that will interpolate across the primitive's surface under subdivision or shading.
* The need to inherit attributes down namespace to allow sparse authoring of shareable data.
Some examples include, texture coordinates, vertex colors, or custom metadata, allowing for interpolating data on individual objects.
Primvars are essential for various tasks, including:
* Storing UVs for texture mapping
* Defining vertex colors for per-Vertex shading
* Deformation and animation
How Does It Work?
Primvars are defined within the scene description and can be accessed and modified using OpenUSD APIs. Each primvar can store different types of data, such as scalar values, vectors, or arrays.
Working With Python
Developers working with OpenUSD can interact with primvars using the Python API. 

# Constructs a UsdGeomPrimvarsAPI on UsdPrim prim
primvar_api = UsdGeom.PrimvarsAPI(prim)

# Creates a new primvar called displayColor of type Color3f[]
primvar_api.CreatePrimvar('displayColor', Sdf.ValueTypeNames.Color3fArray)

# Gets the displayColor primvar
primvar = primvar_api.GetPrimvar('displayColor')

# Sets displayColor values
primvar.Set([Gf.Vec3f(0.0, 1.0, 0.0)])

# Gets displayColor values
values = primvar.Get()
Key Takeaways
The ability to store and manipulate hierarchical object data using primvars is a powerful feature that enables advanced 3D workflows and facilitates interoperability between different tools and applications. By leveraging primvars effectively, we’ll be able to efficiently manage and manipulate per-object data in complex 3D scenes, enabling advanced workflows and facilitating interoperability between different tools and applications. 

Activity: Adding Attributes to a Prim
 


We just learned about the different types of OpenUSD properties: attributes and relationships, and we talked about primvars which are special attributes that can contain extra features. Now, let's learn how to add attributes to a prim with the next activity. Switch over to the Jupyter notebook environment and complete Activity 5: Adding Attributes to a Prim.
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.
Open Jupyter Notebook


Activity: Getting the Value of a Current Attribute

 


Let's keep going with the next activity, Activity 6: Getting the Value of a Current Attribute. We'll wrap up this module with one more lecture when we return. 
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.
Open Jupyter Notebook


Lecture: What Is XformCommonAPI?

 



XformCommonAPI is a component of the OpenUSD framework. Today, we're diving into this API to understand its utility in the 3D content creation pipeline.
This API facilitates the authoring and retrieval of a common set of operations with a single translation, rotation, scale and pivot that is generally compatible with import and export into many tools. It's designed to simplify the interchange of these transformations.

How Does It Work?
The API provides methods to get and set these transformations at specific times – for instance, it allows the retrieval of transformation vectors at any given frame or TimeCode, ensuring precise control over the simulation process.
There’s another way to author and retrieve translations – through the UsdGeomXformable function. Xformable prims support arbitrary sequences of transformations, which gives power users a lot of flexibility. A user could place two rotations on a “Planet” prim, allowing them to control revolution and rotation around two different pivots on the same prim. This is powerful, but complicates simple queries like “What is the position of an object at time 101.0?” 
Working With Python
Below is an example of how to work with the XformCommonAPI in a USD environment.
from pxr import Usd, UsdGeom

# Create a stage and define a prim path
stage = Usd.Stage.CreateNew('example.usda')
prim = UsdGeom.Xform.Define(stage,'/ExamplePrim')

# Check if the XformCommonAPI is compatible with the prim using the bool operator 
if not (xform_api := UsdGeom.XformCommonAPI(prim)):
    raise Exception("Prim not compatible with XformCommonAPI")

# Set transformations
xform_api.SetTranslate((10.0, 20.0, 30.0))
xform_api.SetRotate((45.0, 0.0, 90.0), UsdGeom.XformCommonAPI.RotationOrderXYZ)
xform_api.SetScale((2.0, 2.0, 2.0))
These commands demonstrate how to apply translations, rotations, and scaling to a 3D object using the XformCommonAPI. We can get a transformation matrix from the xformable prim that works with any xformOp order using the GetLocalTransformation method.
Key Takeaways
The XformCommonAPI provides the preferred way for authoring and retrieving a standard set of component transformations, including scale, rotation, scale-rotate pivot and translation.
The goal of the API is to enhance, reconfigure or adapt each structure without changing the entire system. This approach allows for flexibility and customization by focusing on the individual parts rather than the whole. This is done by limiting the set of allowed basic operations and by specifying the order in which they are applied. 

Review: Defining Attributes

 



In this module, we explored the critical role of attributes in OpenUSD and their significance in scene composition. Here's what we achieved:
* Identified the two types of OpenUSD properties. We introduced the concepts of attributes and relationships. 
* Described the function of attributes and relationships in OpenUSD. Attributes store data values that define the properties of a prim, while relationships establish connections between prims.
* Recognized the role of primvars and XformCommonAPI. We talked about primvars, which are a special type of attribute key for graphics, and XformCommonAPI which is one way to author transformation properties.  
* Utilized basic Python functions for attribute manipulation. We learned how to identify attributes associated with a prim, and how to modify attributes through Python. 
Test your knowledge with the following quiz, then continue on to the final module in this course.
Quiz
6/6 points (graded)
Attributes in USD are used to define the relationships between different prims.

True

False
correct
Answer
Correct:Attributes store data values that define the appearance, behavior, or other properties of a prim. They are one of two types of USD properties; the other being relationships.
What is a primary function of attributes in a USD scene?

To store data values that define the appearance and behavior of a prim

To create hierarchical structures

To establish connections between different scenes

To manage user permissions
correct
Which of the following is NOT a common example of an attribute?

Visibility

Display color

Relationship

Extent
correct
Answer
Correct:Common examples of attributes include visibility, display color and the extents, or boundaries of a geometric prim. Relationships are not a type of attribute.
What is the primary purpose of primvars in OpenUSD?

To establish connections between prims

To store and manage hierarchical object data

To define the overall scene structure

To control animation timing
correct
Answer
Correct:Primvars enable efficient management and manipulation of hierarchical object data in complex 3D scenes.
What is the main advantage of using relationships instead of hard-coded paths in USD?

They are faster to process.

They require less memory.

They are robust against path translations.

They allow for larger scene files.
correct
Answer
Correct:Relationships store path values that point to other scene elements and are robust against path translations, a key advantage over hard-coded paths. If a target prim's path changes due to editing or referencing, the relationship automatically remaps to the new location.
What Python command is used to set the display color attribute of a prim to red?

cube_color_attr.Set([1.0, 0.0, 0.0])

cube_color_attr.Set((1.0, 0.0, 0.0))

cube_color_attr.Set(255, 0, 0)

cube_color_attr.Set("red")
correct
Show answer
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.

Overview: Traversing a Stage
 



In this module, we will explore stage traversal in OpenUSD. We will:
* Define stage traversal. We’ll understand what stage traversal is and its importance in navigating the scenegraph.
* Identify the methods of stage traversal. We’ll learn about various traversal modes and predicates used for filtering.
* Recognize basic Python functions for stage traversal. We’ll familiarize ourselves with key Python functions used in stage traversal. 
Let’s begin.


Lecture: What Is Stage Traversal?
 



Stage traversal helps us navigate and manipulate the scenegraph more efficiently. So, what is stage traversal? It's the process of traversing the scenegraph of a stage. This allows us to iterate over the scenegraph, accessing and manipulating the prims and their relationships within the scene. Stage traversal is for tasks such as querying or editing the scene data, and it's a fundamental concept in OpenUSD.

How Does It Work?
When we open a layer in a stage, we can traverse the scenegraph using various methods. We can iterate through child prims, access parent prims, and traverse the hierarchy to find specific prims of interest. This process is facilitated by the stage object, which provides an interface to load, edit, and save USD data. 
Traversing stages works via the Usd.PrimRange class. There are other methods that use Usd.PrimRange as a base class, such as stage.Traverse.
There are two traversal modes:
* Default: Iterate over child prims
* PreAndPostVisit: Iterate over the hierarchy and visit each prim twice, once when first encountering it, and then again when "exiting" the child hierarchy.
There are also predicates which can be used for pre-filtering the result:
* Usd.PrimIsActive: Usd.Prim.IsActive() - If the active metadata is True
* Usd.PrimIsLoaded: Usd.Prim.IsLoaded() - If the (ancestor) payload is loaded
* Usd.PrimIsModel: Usd.Prim.IsModel() - If the kind is a sub kind of Kind.Tokens.model
* Usd.PrimIsGroup: Usd.Prim.IsGroup() - If the kind is Kind.Tokens.group
* Usd.PrimIsAbstract: Usd.Prim.IsAbstract() - If the prim specifier is Sdf.SpecifierClass
* Usd.PrimIsDefined: Usd.Prim.IsDefined() - If the prim specifier is Sdf.SpecifierDef

Working With Python
When writing code related to stage traversal, here are a few relevant Python functions we should know:

# Open a USD file and create a Stage object
stage = Usd.Stage.Open('car.usda')

# Traverses the stage of prims that are active
stage.Traverse()

# Define a predicate to filter prims that are active and loaded
predicate = Usd.PrimIsActive & Usd.PrimIsLoaded

# Traverse starting from the given prim and based on the predicate for filtering the traversal
Usd.PrimRange(prim, predicate=predicate)
Key Takeaways
In summary, stage traversal enables navigation and manipulation of the scenegraph. It's essential for tasks such as querying the scene data and has numerous applications across various industries. Let's experiment with stage traversal in our next activity. 


Activity: Traversing a Stage


Switch over to the Jupyter notebook environment and complete Activity 7: Traversing a Stage and the bonus activity, Does the Prim Exist? Return to the course when complete.
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.
Open Jupyter Notebook



Review: Traversing a Stage

 



With that, we’ve completed this module on stage traversal. In this module we...
* Defined stage traversal. We learned that stage traversal is the process of traversing the scenegraph of a stage, allowing us to iterate over the scenegraph and access prims within a scene.
* We identified various methods of stage traversal. We discovered two traversal modes: default (iterating over child prims) and PreAndPostVisit (iterating over the hierarchy and visiting each prim twice). We also learned about predicates for pre-filtering results, such as Usd.PrimIsActive and Usd.PrimIsLoaded. 
* We recognized basic Python functions for stage traversal. We became familiar with key functions like stage.Traverse() to traverse active prims, and Usd.PrimRange() for more specific traversal. 
Test your knowledge of stage traversal with the following quiz.
Quiz
3/3 points (graded)
What is the primary purpose of stage traversal in OpenUSD?

To create new prims

To navigate and manipulate the scenegraph

To render 3D scenes

To compress USD files
correct
Which of the following is NOT a traversal mode in OpenUSD?

Default

PreAndPostVisit

DepthFirst

Both a and b are valid traversal modes
correct
The Usd.PrimIsActive predicate filters prims based on whether their active metadata is True.

True

False
correct
Show answer
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.


Review: Learning About Stages, Prims and Attributes

In this course, Learning About Stages, Prims and Attributes, we: 
* Created and manipulate USD files. We learned how to set up our own USD files from scratch, setting the foundation for your 3D scenes.
* Defined primitives. We experimented with defining various types of prims, the building blocks of USD, and understand their roles in a 3D environment.
* Established scene hierarchies. We discovered how to organize and structure 3D elements effectively, creating a coherent and manageable scene hierarchy.
* Lit up scenes. We added dynamic lighting to scenes, bringing them to life and enhancing their visual appeal.
* Managed attributes and metadata. We dove into the details of attributes and metadata, and learned how to set, get, and manipulate these essential elements.
* Traversed and inspect USD files. We developed skills to traverse through USD files, inspecting and understanding the intricate details of our scenes.
* Verified prims' existence. We learned techniques to check for the existence of specific prims, ensuring the integrity and completeness of our 3D scenes.
Congratulations! You've completed this course, Learning About Stages, Prims and Attributes. This course is just the beginning of the Learn OpenUSD: Foundations series. Continue your learning journey with the next course in this series, Working With Prims and Default Schemas, where we’ll discuss what it means to create a prim without a schema and review pre-built, default schemas in OpenUSD.

