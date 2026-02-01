GameObjects are the **base objects** of Unity. To be more specific, there exists a **class** called **GameObject**, which contains members and methods that apply to everything in a project, including characters, props, sceneries, etc. 

 A GameObject acts as a container for functional [components](component) that determine how the GameObject looks and behaves.
 
Any script that derives from [MonoBehaviour](MonoBehaviour%20Class) can be added to a GameObject as a component.

## Class Architecture

The GameObject class is implemented in C++, in Unity's game engine, and its full architecture is unavailable. You can see the documentation for its methods on Unity's documentation page. 

It also inherits from an actual C# class called [Object](Object%20Class.md). 