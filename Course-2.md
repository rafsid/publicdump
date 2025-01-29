Learn OpenUSD: Working With Prims and Default Schemas
Learning Objectives
Skip to main content



Welcome to Learn OpenUSD: Foundations. This multi-course curriculum serves as an entry point to your journey learning OpenUSD, and is focused on teaching foundational terminology, Python best practices, and introducing concepts that are important to OpenUSD workflows.
This is the second course in our Learn OpenUSD: Foundations series. This course, Working With Prims and Default Schemas, is designed to help us become proficient in working with prims, the essential building blocks of OpenUSD, and is perfect for both beginners and those looking to enhance their OpenUSD skills.
In this course, we will:
* Define prims. Start with the basics by learning how to define various types of prims, setting the stages for our 3D creations. Understand the role and significance of different prim types within a scene.
* Retrieve prims by path. Gain the ability to locate and retrieve prims using their specific paths, enabling precise control and manipulation of scene elements.
* Validate prims. Ensure the integrity of our 3D scenes by learning how to check if prims are valid. This step is crucial for maintaining a well-structured and error-free scene.
* Set a default prim. Discover how to designate a default prim for USD files, simplifying the management and navigation of complex scenes.
* Understand USD API vs. schema-based API. Explore the differences between using the USD API and the schema-based API, and understand when and why to use each approach for optimal results.
This course is designed for both beginners and those with some experience in 3D graphics and OpenUSD, providing you with the knowledge and skills to effectively use OpenUSD in your projects. We encourage you to actively participate in the activities and quizzes to enhance your learning experience.


Working With Prims and Default Schemas




We will use a Jupyter notebook to conduct activities at various points throughout this course. We recommend you launch the experience now (it may take a moment to load), and we’ll let you know when it’s time to come back to it. 
If at any point during the course you need to relaunch the notebook, come back to this page to do so. In the meantime, let’s move on to the first module: Defining a Prim Without a Schema.
￼

This Lab
0 : 39 : 50
 / 
3 : 00 : 00
Course
3 : 43 : 51
 / 
12 : 00 : 00

LAUNCH

STOP TASK
Course loading. It will take about 5 minutes to load.
Once loaded, a countdown clock will be displayed showing how much longer the server will be active for. Please download any files you wish to keep before the countdown is over as the server files will be deleted. Downloading can be done by right-clicking a file name in the file explorer on the left side of the Jupyter UI.



Overview: Defining a Prim Without a Schema

In this module, Defining a Prim Without a Schema, we will explore the concept of defining a prim without using a schema in OpenUSD. This module focuses on understanding the role of specifiers in USD. In this module, we will:
* Identify the different types of specifiers and their roles in USD.
* Explain how specifiers influence the composition and traversal of prims in a scene.
* Demonstrate how to define and modify prims using Python, without relying on schemas.
Continue on to the first lesson on specifiers. 


Lecture: What Are Specifiers?
Skip to main content




Specifiers in OpenUSD convey the intent for how a prim or a primSpec should be interpreted in the composed scene. The specifier will be one of three things: Def, Over or Class.
How Does It Work?
￼
Def, which is short for define, defines the prim in the current layer. Def indicates a prim exists, is present on the stage and available for processing. 
The resolved specifier of a prim – essentially, which specifier wins when the composition is completed – determines which traversals (like rendering) will visit that prim. Default traversals will only visit defined (def), non-abstract prims. Abstract prims are those that resolve to the class specifiers. Over, the weakest specifier, will resolve to either a def or class specifier.
￼
Over, which is short for override, holds overrides for opinions that already exist in the composed scene on another layer. The over will not translate back to the original prim, and is what enables non-destructive editing workflows, such as changing a property of a prim, like its color, in another layer.   

￼
Class prims are essentially a blueprint. They contain opinions that are meant to be inherited, making it useful when you’re creating base prims from which other prims can inherit properties or opinions. 
It’s worth noting that class prims are intended as the target of an inherit or specialize composition arc – a concept we’ll review in a future module. 
Prims that resolve to class specifiers will also be present and composed on a stage, but won’t be visited by default traversals, meaning it will be ignored by traversals such as the rendering API, Hydra.
Working With Python
￼
Below is an example of how we can get or set a prim's specifier using Python. First, we're defining a new prim called "Box" with the type Cube. The def specifier indicates that box is fully described as a Cube prim in the stage, with a size property set to 4. 
The over specifier modifies the size property without redefining it entirely; in this case, size is overriden to have a value of 10. This change only applies to this specific instance; it does not redefine the prim at the root level. 
Lastly, we're defining a new prim as a class called "_box". This can be used as  a reusable template in the USD scene. 

#Get a prim’s specifier
prim.GetSpecifier()

#Set a prim’s specifier
prim.SetSpecifier(specifier)

def Cube “Box” {
    double size = 4
}

over “Box” {
    double size = 10
}

class “_box” {
    double size = 4
}
Key Takeaways
Again, every prim will have a specifier. To have a prim present on the stage and available for processing you would define (def) that prim. You can use override specifiers, (over), to hold opinions that will be applied to prims in another layer and leverage non-destructive editing workflows, while class specifiers (class) can be leveraged to set up a set of opinions and properties to be inherited or specializes by others.



Activity: Defining a Prim Without a Schema
Skip to main content


Switch over to the Jupyter notebook environment and complete the following activities:
* Activity 1: Creating a USD File 
* Activity 2: Defining a Prim Without a Schema.
Return to the course when complete. 
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.
Open Jupyter Notebook



Review: Defining a Prim Without a Schema
Skip to main content



In this module, we explored the concept of defining a prim without a schema. We:
* Identified the three types of specifiers. We discussed Def, Over, and Class—and their significance in USD.
* Explained how these specifiers affect the composition and traversal of prims. Def is the strongest and Over allows for non-destructive modifications.
* Demonstrated the use of Python to define and modify prims. We showcased how to apply specifiers effectively to define and modify prims without schemas.
Next, we will explore how to get, validate, and set prims at a path in USD.

Quiz
3 points possible (graded)
What are the three types of specifiers in OpenUSD, and what is their significance?

Def, Over, Class

Def, Override, Class

Define, Over, Class

Define, Override, Blueprint
unanswered
Which specifier allows for non-destructive editing by holding overrides for opinions that already exist in the composed scene?

Def

Over

Class

Define
unanswered
In OpenUSD, what is the purpose of using a class specifier?

To define a prim as a complete entity

To override existing properties

To serve as a blueprint for inheritance

To delete a prim
unanswered
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.


Overview: Getting, Validating and Setting Prims at Path
Skip to main content



This module, Getting, Validating and Setting Prims at a Path, explores working with paths in OpenUSD for navigating and manipulating scene hierarchies. In this module, we will...
* Describe the structure and purpose of paths in OpenUSD.
* Utilize the pxr.Sdf.Path class to manage path data for prims and properties.
* Apply Python functions to retrieve, validate, and set prims using their paths.

First, let’s talk about what a path is. Continue to the first lecture: What Is a Path?


Lecture: What Is a Path?
Skip to main content



In OpenUSD, a path is a type that represents the location of a prim within a scene hierarchy. Its string representation consists of a sequence of prim names separated by forward slashes (/), similar to file paths in a directory structure. The stage root, which serves as the starting point for the hierarchy, is represented by a forward slash ("/").
For example, the path /World/Geometry/Box represents a prim named Box that is a child of a prim named Geometry, which is a child of the root prim named World.
How Does It Work?
Paths in OpenUSD are handled through the pxr.Sdf.Path class to encode path data including prims, properties (both attributes and relationships), and variants. 
Prims are indicated by a slash separator, which indicates the namespace Child (ex: "/geo/box")
Period separators after an identifier is used to introduce a property (ex:
"/geo/box.weight")
Variants are indicated by curly brackets, like this: "/geo/box{size=large}")
They are used to:
1. Uniquely identify prims and properties. Each prim and property in a scene has a unique path that distinguishes it from other prims and properties. 
2. Navigate the scene hierarchy. Paths allow you to traverse the scene hierarchy via the USD stage and access specific prims.
3. Specify locations for authoring. When creating or modifying prims, paths are used to specify where the prims should be placed in the hierarchy on the USD stage.
4. Query and filter prims. Paths can be used to filter and select specific prims based on their location in the hierarchy using Sdf.PathExpression.
Working With Python
￼
Here are a few Python functions relevant to paths in OpenUSD.

# Import the Sdf class 
from pxr import Sdf 

# Return the path of a Usd.Prim as an Sdf.Path object
Usd.Prim.GetPath() 

# Retrieve a Usd.Prim at the specified path from the Stage
Usd.Stage.GetPrimAtPath()
Key Takeaways
Using Sdf.Path objects in OpenUSD provides a way to uniquely identify and locate objects (prims) within our scene hierarchy. We will use paths for authoring, querying, and navigating USD data effectively. 


Activity: Getting, Validating and Setting Prims at Path
Level 2 headings may be created by course providers in the future.

Skip to main content


Now, let's switch over to the Jupyter notebook environment and complete Activity 3: Getting, Validating and Setting Prims at a Path, then we'll return to the course.
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.
Open Jupyter Notebook



Lecture: What Is a Default Prim?

￼
In this lesson, we’ll explore the concept of default prims in Universal Scene Description. Default prims are essential for scene management, especially when dealing with complex hierarchies and references. By the end of this lesson, we’ll understand what default prims are, why they are important, and how to set them using Python.
How Does It Work?
A default prim in OpenUSD is a top-level prim, or primitive, that is part of the scene’s metadata and serves as the primary entry point or root for a stage. Think of it as the “control point” in the scene, which helps other parts of the system know where to start or what to focus on. 
It is best practice to set a default prim in our stages. This is crucial for tools and applications that read USD files, as it guides them to the primary content; for some it may even be considered invalid if the default prim is not specified for the stage. usdchecker checks for a default prim and reports an error if it is not set on a stage. A default prim is also particularly useful when the stage’s root layer is referenced in other stages (such as a reference or payload), as it eliminates the need for consumers to specify a target prim manually.
Let’s look at this example. Let's assume we have a USD file named simple_scene.usda with the following content:

#usda 1.0
(
    defaultPrim = "Car"
)

def Xform "Car" {
    def Mesh "Body" {
        double3[] points = [(0, 0, 0), (2, 0, 0), (2, 1, 0), (0, 1, 0)]
        int[] faceVertexCounts = [4]
        int[] faceVertexIndices = [0, 1, 2, 3]
    }
}

def Xform "Building" {
    def Mesh "Structure" {
        double3[] points = [(0, 0, 0), (5, 0, 0), (5, 10, 0), (0, 10, 0)]
        int[] faceVertexCounts = [4]
        int[] faceVertexIndices = [0, 1, 2, 3]
    }
}
The defaultPrim metadata is set to Car, indicating that Car is the main entry point of this USD file. When we bring this .usda in as a reference or payload the Car will show up visually in the stage. If we set the defaultPrim to Building then the Building will show up in the stage when referenced. If no defaultPrim is set then when the above .usda is brought in as a payload or reference it will resolve as an empty layer and output a warning message in the log.
Working With Python
￼
The default prim is set using the SetDefaultPrim() method on a USD stage. This method accepts any Usd.Prim, but the prim must be a top-level prim on the stage. Here’s a simple example:

from pxr import Usd, UsdGeom, Sdf

# Create a new USD stage
stage = Usd.Stage.CreateInMemory()

# Define a top-level Xform prim
default_prim = UsdGeom.Xform.Define(stage, Sdf.Path("/World")).GetPrim()

# Set the Xform prim as the default prim
stage.SetDefaultPrim(default_prim)

# Export the stage to a string to verify
usda = stage.GetRootLayer().ExportToString()
print(usda)

# Check that the expected default prim was set
assert stage.GetDefaultPrim() == default_prim
Key Takeaways
In summary, default prims are the top-level prims that serve as the main entry point for a USD stage. Setting a default prim is a best practice when our stage’s root layer might be composed into another stage, whether as a reference, payload, or specialize.
By utilizing default prims, we can create more organized and manageable USD stages. 


Activity: Setting a Default Prim
Skip to main content


Let's wrap up this module with another hands-on activity. Switch over to the Jupyter notebook environment and complete Activity 4: Setting a Default Prim, then we'll return to the course.
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.
Open Jupyter Notebook


Review: Creating an OpenUSD Stage

Now we have a better understanding of paths in OpenUSD. In this module, we…
* Described how paths are structured in USD. We talked about how paths are used to define a prim’s location namespace, and the role of paths in identifying and navigating scene elements.
* Utilized the pxr.Sdf.Path class to manage path data. This allows for precise control over scene hierarchies.
* Applied Python functions to retrieve, validate, and set prims. We explored the function IsValid() to verify that a prim is valid, and GetPrimAtPath() to retrieve prims.
Next, we’ll get into default schemas and their importance in Universal Scene Description.

Quiz
3 points possible (graded)
What is the function of paths in USD?

To store data attributes

To represent the location of a prim within a scene hierarchy

To define the type of a prim

To override prim properties
unanswered
Which Python class is used to manage path data for prims and properties in USD?

pxr.Usd.Stage

pxr.Sdf.Path

pxr.Usd.Prim

pxr.UsdGeom.Xform
unanswered
What method would you use to check if a prim retrieved by path is valid?

IsValid()

CheckValid()

Validate()

IsPathValid()
unanswered
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.


Overview: Understanding Default Schemas
Skip to main content



In this module, we will explore the concept of schemas in OpenUSD, focusing on how they define and govern the behavior of prims. We will…
* Explain the role of schemas in providing structure and interoperability in OpenUSD.
* Differentiate between IsA schemas and API schemas, and their respective uses.
* Implement schema-related operations using Python to enhance USD scene management.
Let’s get started with our first lesson, What Are Schemas?


Lecture: What Are Schemas?
Skip to main content



￼
Schemas give meaning to objects (prims) in OpenUSD, i.e., “What is this object? What capabilities does it have?”. Schemas define the data models and optional API for encoding and interchanging 3D and non-3D concepts through OpenUSD. 
In the next couple lessons on schemas, we'll explore the different types of schemas, their characteristics, and how they enable the creation of sophisticated virtual worlds and digital twins.
What Are Schemas?

Schemas serve as blueprints that author and retrieve data, like attributes and  relationships that govern behaviors of objects in a USD scene. They provide a consistent and extensible way to define and interpret data, ensuring data interoperability between different software tools and applications. 
Each prim in a scene is an object that implicitly contains the properties and fallback values of the typed schema that’s telling the prim what it is. For example, the radius attribute for the UsdGeomSphere schema is defined as double radius = 1 meaning that all sphere prims have a radius represented by a double-precision floating point number with a value of 1 by default.
Schemas are primarily data models with documented rules on how the data should be interpreted. While schemas define the structure and rules, they do not necessarily include the implementation of behaviors. For example, the UsdPhysics schema does not come with a physics engine. Developers should understand that schemas often expose methods to facilitate interactions with the defined structure and may provide behaviors in the schema API, but this is not a requirement.
There is a trend toward codeless schemas for easier distribution, suggesting that schemas might become more lightweight, focusing on data modeling rather than behavior implementation.
Actual behavior enforcement can be managed by other subsystems within the runtime ecosystem. This allows for flexibility and performance optimization based on different use cases.
Working With Python
￼
In Python, we can work with schemas using the following methods:

# Retrieve the schema info for a registered schema
Usd.SchemaRegistry.FindSchemaInfo()

# Retrieve the schema typeName
Usd.SchemaRegistry.GetSchemaTypeName()
These methods allow us to interact with and manipulate schemas programmatically, enabling us to create, modify, and validate USD assets based on predefined rules and conventions.
Key Takeaways
Schemas in OpenUSD serve as templates for defining prims.
It's worth noting there are actually two distinct types of schemas: IsA and API schemas, which we'll cover in the next lesson.


Lecture: What Are IsA Schemas and API Schemas?



There are two types of schemas used with OpenUSD: IsA schemas and API schemas. Let’s talk about IsA schemas first.
IsA Schemas
IsA schemas, also known as Typed schemas or Prim schemas, essentially tell a prim what it is. Because of this, each prim can only subscribe to one IsA schema at a time.
We use the typeName metadata to assign an IsA schema to a prim.  
IsA schemas are derived from the core class UsdTyped, the base class for all typed schemas, which is why we hear IsA schemas referred to as “typed” schemas. 
These schemas can either be concrete (instantiable) or abstract (non-concrete, serve as base classes). We refer to a schema as concrete when the schema can be instantiated as prims in the USD scene, as we see with UsdGeomMesh and UsdGeomScope. Concrete schemas provide both a name and a typeName in the schema definition.
Meanwhile, abstract, or non-concrete schemas, provide a name but no typeName in the schema definition. This enables them to serve as a base class for related sets of concrete schemas, the way UsdGeomPointBased serves as a base class for geometric objects that contain points, like meshes (UsdGeomMesh), or basis curves (UsdGeomBasisCurves).
Let’s look at a couple of the common default schemas that will come up as we are learning about OpenUSD. 


UsdGeom
￼
UsdGeom defines schemas for representing geometric objects, such as meshes, cameras, and curves as mentioned above. It also includes schemas for transformations, visibility, and other common properties. 

# Import related classes
from pxr import UsdGeom

# Define a sphere in the stage
sphere = UsdGeom.Sphere.Define(stage, "/World/Sphere")
	
# Get and Set the radius attribute of the sphere
sphere.GetRadiusAttr().Set(10)


UsdLux
￼
UsdLux defines schemas for representing light sources in a scene. It includes schemas such as sphere lights, disk lights, and distant lights, which were discussed in the lesson on USD lights. 
Examples include UsdLuxDiskLight, UsdLuxRectLight, and UsdLuxSphereLight.
# Import related classes
from pxr import UsdLux

# Define a disk light in the stage
disk_light = UsdLux.DiskLight.Define(stage, "/World/Lights/DiskLight")
	
# Get all Attribute names that are apart of the DiskLight schema
dl_attribute_names = disk_light.GetSchemaAttributeNames()
	
# Get and Set the intensity attribute of the disk light prim
disk_light.GetIntensityAttr().Set(1000)
API Schemas
In addition to IsA schemas, we have API schemas. API schemas are similar to IsA schemas except it does not specify a typeName. Since it does not have a typeName they are considered to be non-concrete. 
API schemas are typically named with the suffix “API” in their C++ or Python class name, such as UsdShadeConnectableAPI. Properties that belong to an API schema are namespaced with the schemas base name and camelCased. For example, UsdPhysics.RigidBodyAPI.CreateVelocityAttr() will create an attribute named physics:velocity.
API schemas can be classified as non-applied or applied schemas, and single-apply or multiple-apply, where single-apply API schemas are applied to only a single instance of a prim, and multiple-apply API schemas can be applied multiple times to the same prim with different instance names. 
Unlike IsA schemas, API schemas do not assign a typeName to a prim. Instead, are list-edited in the apiSchemas metadata and queryable via the HasAPI method. API schemas are assigned to already-typed prims to annotate them with additional properties that govern behaviors. 
The following is a key example of an API Schemas.
UsdPhysics
￼
UsdPhysics adds physics properties to any UsdGeomXformable object for simulation such as rigid body dynamics.

# Import related classes
from pxr import UsdPhysics

# Apply a UsdPhysics Rigidbody API on the cube prim
cube_rb_api = UsdPhysics.RigidBodyAPI.Apply(cube.GetPrim())
	
# Get the Kinematic Enabled Attribute 
cube_rb_api.GetKinematicEnabledAttr()
	
# Create a linear velocity attribute of value 5
cube_rb_api.CreateVelocityAttr(5)
This example shows how API schemas can be applied to prims to add specific properties that govern behaviors, such as adding rigid body capabilities to an object hierarchy. 
Key Takeaways
API schemas work alongside IsA schemas to provide a flexible and extensible system for building complex scenes in OpenUSD. 
Schemas are a complex topic, but when leveraged correctly, they can simplify development of USD scenes. We’ll cover schemas again, including custom schemas, in future lessons.


Activity: Adding Prims With Default Schemas
Skip to main content


Let's complete a few final lessons for this course focusing on default schemas. Switch over to the Jupyter notebook environment and complete the following activities, then return to the course.
* Activity 5: UsdGeom and Xform
* Activity 6: Scope and Cube
* Activity 7: UsdShade and Material
* Activity 8: UsdLux and Distant Light
If you don't already have it open, you can find the Jupyter notebook in the Using the Jupyter Notebook section of this course.
Open Jupyter Notebook


Review: Understanding Default Schemas
Skip to main content



In this module, we gained insights into default schemas in Universal Scene Description. To recap, we:
* Explained the role of schemas in OpenUSD. We talked about how schemas serve as blueprints for defining prims, ensuring data consistency and interoperability.
* Differentiated between the two schema classes. We reviewed IsA schemas (typed schemas) and API schemas, and discussed their distinct roles in scene management.
* Implemented Python operations to interact with schemas. We experimented with various default schemas, enhancing our ability to manage and manipulate USD scenes effectively.
With this knowledge, we are now equipped with a basic understanding of how schemas can create sophisticated and well-structured OpenUSD scenes. Quiz yourself on this module's content in the section below.

Quiz
3 points possible (graded)
What is the primary function of schemas in USD?

To store scene metadata

To define and govern the behavior of prims

To manage scene hierarchies

To override prim properties
unanswered
Which type of schema in USD is known as a Typed schema?

API schema

IsA schema

Override schema

Define schema
unanswered
How do API schemas differ from IsA schemas in USD?

API schemas can be applied multiple times to the same prim

IsA schemas are non-concrete

API schemas assign a typeName to a prim

IsA schemas provide additional properties without a typeName
unanswered
Submit
Some problems have options such as save, reset, hints, or show answer. These options follow the Submit button.



Review: Working With Prims and Default Schemas
Skip to main content


We've reached the end of this course, Working With Prims and Default Schemas. In this course, we:
* Defined prims. We started with the basics by learning how to define various types of prims, setting the stage for our 3D creations. Now, we understand the role and significance of different prim types within a scene.
* Retrieved prims by path. We gained the ability to locate and retrieve prims using their specific paths, enabling precise control and manipulation of scene elements.
* Validated prims. We ensured the integrity of our 3D scenes by learning how to check if prims are valid. This step is crucial for maintaining a well-structured and error-free scene.
* Set a default prim. We discovered how to designate a default prim for USD files, simplifying the management and navigation of complex scenes.
* Differentiated between USD API and schema-based API. We explored the differences between using the USD API and the schema-based API, and now understand when and why to use each approach for optimal results.

Congratulations! By finishing this module, we’ve completed this course, Working With Prims and Default Schemas. Continue your Learn OpenUSD: Foundations series learning journey with the next course in this series, Using Attributes, where we’ll revisit the concept of USD attributes in more depth.



