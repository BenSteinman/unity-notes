Properties in C# are syntax sugar for classes that allowed for controlled access to data. They allow for safety checks when setting data, and they are used in a field-like syntax instead of a function call.

## Example

```
class User
{
    private string name; //field
    public string Name //property
    {
        get{ return name; } //get method
        set{ name = value; } //set method
    }
}
```

```
class Program
{
    static void Main()
    {
        User user = new User(); 
        user.Name = "Alice"; // calls the setter
        string userName = user.Name; // calls the getter

    }
}
```

