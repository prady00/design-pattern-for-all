
Prototype
=============


Real world example
> Remember dolly? The sheep that was cloned! Lets not get into the details but the key point here is that it is all about cloning

In plain words
> Create object based on an existing object through cloning.

Wikipedia says
> The prototype pattern is a creational design pattern in software development. It is used when the type of objects to create is determined by a prototypical instance, which is cloned to produce new objects.

In short, it allows you to create a copy of an existing object and modify it to your needs, instead of going through the trouble of creating an object from scratch and setting it up.

**Programmatic Example**

In Java, it can be easily done using `Clonable`

```php
package com.prady00.dp.creational.prototype;
class Sheep implements Cloneable
{
    protected String name;
    protected String category;

    public Sheep(String name, String category)
    {
        this.name = name;
        this.category = category;
    }

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return this.name;
    }

    public void setCategory(String category)
    {
        this.category = category;
    }

    public String getCategory()
    {
        return this.category;
    }
    
    @Override
	public Object clone() throws CloneNotSupportedException{
			return new Sheep(this.name, this.category);
	}

	@Override
	public String toString() {
		return "Sheep [name=" + name + ", category=" + category + "]";
	}
    
}
```
Then it can be cloned like below
```java
package com.prady00.dp.creational.prototype;

public class PrototypeRunner {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		Sheep originalSheep = new Sheep("Dolly", "Mountain");
		
		Sheep clonedSheep = null; 
		
		try {
			clonedSheep = (Sheep) originalSheep.clone();
		} catch (CloneNotSupportedException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		System.out.println(originalSheep);
		System.out.println(clonedSheep);

	}

}
```

**When to use?**

When an object is required that is similar to existing object or when the creation would be expensive as compared to cloning.
