Flyweight
=========

Real world example
> Did you ever have fresh tea from some stall? They often make more than one cup that you demanded and save the rest for any other customer so to save the resources e.g. gas etc. Flyweight pattern is all about that i.e. sharing.

In plain words
> It is used to minimize memory usage or computational expenses by sharing as much as possible with similar objects.

Wikipedia says
> In computer programming, flyweight is a software design pattern. A flyweight is an object that minimizes memory use by sharing as much data as possible with other similar objects; it is a way to use objects in large numbers when a simple repeated representation would use an unacceptable amount of memory.

**Programmatic example**

Translating our tea example from above. First of all we have tea types and tea maker

```java
package com.prady00.dp.structural.flyweight;
// Anything that will be cached is flyweight.
// Types of tea here will be flyweights.
class KarakTea
{
}

```
```java

// Acts as a factory and saves the tea
package com.prady00.dp.structural.flyweight;

import java.util.ArrayList;
import java.util.List;

// Acts as a factory and saves the tea
class TeaMaker
{
    protected List<KarakTea> availableTea = new ArrayList<KarakTea>();

    public void make(String preference)
    {
        
    }
}
```

Then we have the `TeaShop` which takes orders and serves them

```java
package com.prady00.dp.structural.flyweight;

import java.util.ArrayList;
import java.util.List;

class TeaShop
{
    protected List<String> orders = new ArrayList<>();
    protected TeaMaker teaMaker;

    public TeaShop(TeaMaker teaMaker)
    {
        this.teaMaker = teaMaker;
    }

    public void takeOrder(String teaType, int table)
    {
        this.orders.add(teaType + "at table " + table);
    }

    public void serve()
    {
        boolean String;
		for (String order : this.orders) {
            System.out.println(order);
        }
    }
}
```
And it can be used as below

```java
package com.prady00.dp.structural.flyweight;

public class FlyweightRunner {

	public static void main(String[] args) {
		TeaMaker teaMaker = new TeaMaker();
		TeaShop shop = new TeaShop(teaMaker);

		shop.takeOrder("less sugar", 1);
		shop.takeOrder("more milk", 2);
		shop.takeOrder("without sugar", 5);

		shop.serve();
		// Serving tea to table# 1
		// Serving tea to table# 2
		// Serving tea to table# 5

	}

}

```
