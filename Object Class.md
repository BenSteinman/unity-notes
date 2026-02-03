The object class is the **base class** which *all subclasses inherit from* in Unity. Don't derive from or instantiate this class directly. Instead, use the appropriate subclass such as [[GameObject]], [MonoBehaviour](MonoBehaviour%20Class), or [ScriptableObject](ScriptableObject%20Class.md).

Any public variable you make that derives from `UnityEngine.Object` is shown in the Inspector as a drop target, allowing you to set the value from the GUI.

### Example

```
using UnityEngine;

public class ObjectTest : MonoBehaviour
{
    public GameObject myObject1234;
}
```

Dragging this script onto an object in the scene allows you to select **My Object 1234** from the inspector.

![[Pasted image 20260202221350.png]]

### Generic Objects

Some APIs in Unity don't care if it's a GameObject, Material, Texture, or any other Unity asset. They just need some object Unity knows about. Because these APIs are designed to work with any object, they use `.Object` in their signature

For example:
```
Object[] textures = Resources.LoadAll("Textures", typeof(Texture2D));
```

This line of code assigns all 2d textures in the Assets/Resources/**Textures** directory to an array of type **Object**. While each element in this array is actually of type **Texture2D**, they are stored in the generic **Object** array. In fact, trying to use an array of **Texture2D** to hold your textures would not compile, since `Resources.LoadAll` returns an **Object** type.

This code would not compile:
```
Texture2D[] textures = Resources.LoadAll("Textures", typeof(Texture2D));
```
Unity does not allow you to implicitly convert type **Object** to **Texture2D**.

### Native vs Managed Objects

Managed Objects are objects that inherit from the .Object class which you instantiate. They, like all objects are managed by C# garbage collector, but this is not why they are called Managed Objects. The derive the name because they are implemented as wrapper layers which manage access to native resources, not just garbage collection. 

Native Objects are objects that are managed entirely by the Unity engine. They contain the actual data. When you instantiate an object of or inheriting from the `.Object` class, a counterpart native object is linked to the managed object you created. The big data does not live in the managed object but the native object.
## Class Architecture

The object class, and any class that inherits from it, is mainly a wrapper for a C++ class implemented under the hood. For example, this is a function from the Texture2D C# class: 
```
    public TextureFormat format // property declaration
    {
        [NativeName("GetTextureFormat")] // attribute, links to native C++
        get
        {
            IntPtr intPtr = MarshalledUnityObject.MarshalNotNull(this);
            if (intPtr == (IntPtr)0) // check if ptr is null
            {
                ThrowHelper.ThrowNullReferenceException(this); 
            }

            return get_format_Injected(intPtr); // call c++ code & return
        }
    }
```

This code is a [[property]] that gets the texture format of a Texture2D object.
### Properties

```
hideFlags
name
```
### Public Methods

```
GetInstanceId
ToString
```