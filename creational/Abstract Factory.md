Abstract Factory
================

Real world example
> Extending our door example from Simple Factory. Based on your needs you might get a wooden door from a wooden door shop, iron door from an iron shop or a PVC door from the relevant shop. Plus you might need a guy with different kind of specialities to fit the door, for example a carpenter for wooden door, welder for iron door etc. As you can see there is a dependency between the doors now, wooden door needs carpenter, iron door needs a welder etc.

In plain words
> A factory of factories; a factory that groups the individual but related/dependent factories together without specifying their concrete classes.

Wikipedia says
> The abstract factory pattern provides a way to encapsulate a group of individual factories that have a common theme without specifying their concrete classes

**Programmatic Example**

Translating the door example above. First of all we have our `Door` interface and some implementation for it

```java
package com.prady00.dp.creational.abstractFactory;
interface Door
{
    public void getDescription();
}
```

```java
package com.prady00.dp.creational.abstractFactory;
class WoodenDoor implements Door
{
    public void getDescription()
    {
        System.out.println("I am a wooden door");
    }
}
```
```java
package com.prady00.dp.creational.abstractFactory;
class IronDoor implements Door
{
    public void getDescription()
    {
        System.out.println("I am an iron door");
    }
}
```
Then we have some fitting experts for each door type

```java
package com.prady00.dp.creational.abstractFactory;
interface DoorFittingExpert
{
    public void getDescription();
}
```

```java
package com.prady00.dp.creational.abstractFactory;
class Welder implements DoorFittingExpert
{
    public void getDescription()
    {
        System.out.println("I can only fit iron doors");
    }
}
```

```java
package com.prady00.dp.creational.abstractFactory;
class Carpenter implements DoorFittingExpert
{
    public void  getDescription()
    {
        System.out.println("I can only fit wooden doors");
    }
}
```

Now we have our abstract factory that would let us make family of related objects i.e. wooden door factory would create a wooden door and wooden door fitting expert and iron door factory would create an iron door and iron door fitting expert
```java
package com.prady00.dp.creational.abstractFactory;
interface DoorFactory
{
    public Door makeDoor();
    public DoorFittingExpert makeFittingExpert();
}
```

Wooden factory to return carpenter and wooden door

```java
package com.prady00.dp.creational.abstractFactory;
class WoodenDoorFactory implements DoorFactory
{
    public WoodenDoor makeDoor()
    {
        return new WoodenDoor();
    }

    public Carpenter makeFittingExpert()
    {
        return new Carpenter();
    }
}
```

Iron door factory to get iron door and the relevant fitting expert

```java
package com.prady00.dp.creational.abstractFactory;
class IronDoorFactory implements DoorFactory
{
    public IronDoor makeDoor()
    {
        return new IronDoor();
    }

    public Welder makeFittingExpert()
    {
        return new Welder();
    }
}
```
And then it can be used as
```java
package com.prady00.dp.creational.abstractFactory;

public class AbstractFactoryRunner {

	public static void main(String[] args) {
		
		WoodenDoorFactory woodenFactory = new WoodenDoorFactory();

		Door door = woodenFactory.makeDoor();
		DoorFittingExpert expert = woodenFactory.makeFittingExpert();

		door.getDescription();  // Output: I am a wooden door
		expert.getDescription(); // Output: I can only fit wooden doors

	}

}
```

As you can see the wooden door factory has encapsulated the `carpenter` and the `wooden door` also iron door factory has encapsulated the `iron door` and `welder`. And thus it had helped us make sure that for each of the created door, we do not get a wrong fitting expert.   

**When to use?**

When there are interrelated dependencies with not-that-simple creation logic involved
