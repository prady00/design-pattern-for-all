Decorator
=========

Real world example

> Imagine you run a car service shop offering multiple services. Now how do you calculate the bill to be charged? You pick one service and dynamically keep adding to it the prices for the provided services till you get the final cost. Here each type of service is a decorator.

In plain words
> Decorator pattern lets you dynamically change the behavior of an object at run time by wrapping them in an object of a decorator class.

Wikipedia says
> In object-oriented programming, the decorator pattern is a design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. The decorator pattern is often useful for adhering to the Single Responsibility Principle, as it allows functionality to be divided between classes with unique areas of concern.

**Programmatic Example**

Lets take coffee for example. First of all we have a simple coffee implementing the coffee interface

```java
package com.prady00.dp.structural.decorator;
interface Coffee
{
    public int getCost();
    public String getDescription();
}

```
```java
package com.prady00.dp.structural.decorator;
class SimpleCoffee implements Coffee
{
    public int getCost()
    {
        return 10;
    }

    public String getDescription()
    {
        return "Simple coffee";
    }
}
```
We want to make the code extensible to allow options to modify it if required. Lets make some add-ons (decorators)
```java
package com.prady00.dp.structural.decorator;
class MilkCoffee implements Coffee
{
    protected Coffee coffee;

    public MilkCoffee(Coffee coffee)
    {
        this.coffee = coffee;
    }

    public int getCost()
    {
        return this.coffee.getCost() + 2;
    }

    public String getDescription()
    {
        return this.coffee.getDescription() + ", milk";
    }
}

```
```java
package com.prady00.dp.structural.decorator;
class WhipCoffee implements Coffee
{
    protected Coffee coffee;

    public WhipCoffee(Coffee coffee)
    {
        this.coffee = coffee;
    }

    public int getCost()
    {
        return this.coffee.getCost() + 5;
    }

    public String getDescription()
    {
        return this.coffee.getDescription() + ", whip";
    }
}
```

Lets make a coffee now

```java
package com.prady00.dp.structural.decorator;

public class DecoratorRunner {

	public static void main(String[] args) {
		Coffee someCoffee = new SimpleCoffee();
		System.out.println(someCoffee.getCost()); // 10
		System.out.println(someCoffee.getDescription()); // Simple Coffee

		someCoffee = new MilkCoffee(someCoffee);
		System.out.println(someCoffee.getCost()); // 12
		System.out.println(someCoffee.getDescription()); // Simple Coffee, milk

		someCoffee = new WhipCoffee(someCoffee);
		System.out.println(someCoffee.getCost()); // 17
		System.out.println(someCoffee.getDescription()); // Simple Coffee, milk, whip
	}

}


```