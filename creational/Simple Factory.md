
Simple Factory
==================
Real world example
> Consider, you are building a house and you need doors. It would be a mess if every time you need a door, you put on your carpenter clothes and start making a door in your house. Instead you get it made from a factory.

In plain words
> Simple factory simply generates an instance for client without exposing any instantiation logic to the client

Wikipedia says
> In object-oriented programming (OOP), a factory is an object for creating other objects – formally a factory is a function or method that returns objects of a varying prototype or class from some method call, which is assumed to be "new".

**Programmatic Example**

First of all we have a door interface and the implementation
```java
package com.prady00.dp.creational.simpleFactory;
interface Door
{
    public float getWidth();
    public float getHeight();
}
```

```java
package com.prady00.dp.creational.simpleFactory;
class WoodenDoor implements Door
{
    protected float width;
    protected float height;

    public WoodenDoor(float width, float height)
    {
        this.width = width;
        this.height = height;
    }

    public float getWidth()
    {
        return this.width;
    }

    public float getHeight()
    {
        return this.height;
    }
}
```
Then we have our door factory that makes the door and returns it
```java
package com.prady00.dp.creational.simpleFactory;
class DoorFactory
{
    public static Door makeDoor(float width, float height)
    {
        return new WoodenDoor(width, height);
    }
}
```
And then it can be used as
```java
package com.prady00.dp.creational.simpleFactory;

public class SimpleFactoryRunner {

	public static void main(String[] args) {
		Door door = DoorFactory.makeDoor(100, 200);
	}

}

```

**When to Use?**

When creating an object is not just a few assignments and involves some logic, it makes sense to put it in a dedicated factory instead of repeating the same code everywhere.
