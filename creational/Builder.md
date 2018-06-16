Builder
=======

Real world example
> Imagine you are at Hardee's and you order a specific deal, lets say, "Big Hardee" and they hand it over to you without *any questions*; this is the example of simple factory. But there are cases when the creation logic might involve more steps. For example you want a customized Subway deal, you have several options in how your burger is made e.g what bread do you want? what types of sauces would you like? What cheese would you want? etc. In such cases builder pattern comes to the rescue.

In plain words
> Allows you to create different flavors of an object while avoiding constructor pollution. Useful when there could be several flavors of an object. Or when there are a lot of steps involved in creation of an object.

Wikipedia says
> The builder pattern is an object creation software design pattern with the intentions of finding a solution to the telescoping constructor anti-pattern.

**Programmatic Example**

The sane alternative is to use the builder pattern. First of all we have our burger that we want to make

```java
package com.prady00.dp.creational.builder;
class Burger
{
    protected int size;

    protected boolean cheese = false;
    protected boolean pepperoni = false;
    protected boolean lettuce = false;
    protected boolean tomato = false;

    public Burger(BurgerBuilder builder)
    {
        this.size = builder.size;
        this.cheese = builder.cheese;
        this.pepperoni = builder.pepperoni;
        this.lettuce = builder.lettuce;
        this.tomato = builder.tomato;
    }
}
```

And then we have the builder

```java
package com.prady00.dp.creational.builder;
class BurgerBuilder
{
    public int size;

    public boolean cheese = false;
    public boolean pepperoni = false;
    public boolean lettuce = false;
    public boolean tomato = false;

    public BurgerBuilder(int size)
    {
        this.size = size;
    }

    public BurgerBuilder addPepperoni()
    {
        this.pepperoni = true;
        return this;
    }

    public BurgerBuilder addLettuce()
    {
        this.lettuce = true;
        return this;
    }

    public BurgerBuilder addCheese()
    {
        this.cheese = true;
        return this;
    }

    public BurgerBuilder addTomato()
    {
        this.tomato = true;
        return this;
    }

    public Burger build()
    {
        return new Burger(this);
    }
}
```
And then it can be used as:

```java
package com.prady00.dp.creational.builder;

public class BuilderRunner {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Burger burger = (new BurgerBuilder(14))
                .addPepperoni()
                .addLettuce()
                .addTomato()
                .build();

	}

}
```

**When to use?**

When there could be several flavors of an object and to avoid the constructor telescoping. The key difference from the factory pattern is that; factory pattern is to be used when the creation is a one step process while builder pattern is to be used when the creation is a multi step process.
