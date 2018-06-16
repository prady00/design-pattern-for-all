Visitor
-------
Real world example
> Consider someone visiting Dubai. They just need a way (i.e. visa) to enter Dubai. After arrival, they can come and visit any place in Dubai on their own without having to ask for permission or to do some leg work in order to visit any place here; just let them know of a place and they can visit it. Visitor pattern lets you do just that, it helps you add places to visit so that they can visit as much as they can without having to do any legwork.

In plain words
> Visitor pattern lets you add further operations to objects without having to modify them.

Wikipedia says
> In object-oriented programming and software engineering, the visitor design pattern is a way of separating an algorithm from an object structure on which it operates. A practical result of this separation is the ability to add new operations to existing object structures without modifying those structures. It is one way to follow the open/closed principle.

**Programmatic example**

Let's take an example of a zoo simulation where we have several different kinds of animals and we have to make them Sound. Let's translate this using visitor pattern

```java
package com.prady00.dp.behavioral.visitor;
// Visitee
interface Animal
{
    public void accept(AnimalOperation operation);
}
```

```java
package com.prady00.dp.behavioral.visitor;
// Visitor
interface AnimalOperation
{
    public void visitMonkey(Monkey monkey);
    public void visitLion(Lion lion);
    public void visitDolphin(Dolphin dolphin);
}
```
Then we have our implementations for the animals
```java
package com.prady00.dp.behavioral.visitor;
class Monkey implements Animal
{
    public void shout()
    {
        System.out.println("Ooh oo aa aa!");
    }

    public void accept(AnimalOperation operation)
    {
        operation.visitMonkey(this);
    }
}
```

```java
package com.prady00.dp.behavioral.visitor;
class Lion implements Animal
{
    public void roar()
    {
        System.out.println("Roaaar!");
    }

    public void accept(AnimalOperation operation)
    {
        operation.visitLion(this);
    }
}
```

```java
package com.prady00.dp.behavioral.visitor;
class Dolphin implements Animal
{
    public void speak()
    {
        System.out.println("Tuut tuttu tuutt!");
    }

    public void accept(AnimalOperation operation)
    {
        operation.visitDolphin(this);
    }
}
```
Let's implement our visitor
```java
package com.prady00.dp.behavioral.visitor;
class Speak implements AnimalOperation
{
    public void visitMonkey(Monkey monkey)
    {
        monkey.shout();
    }

    public void visitLion(Lion lion)
    {
        lion.roar();
    }

    public void visitDolphin(Dolphin dolphin)
    {
        dolphin.speak();
    }
}
```

And then it can be used as
```java
package com.prady00.dp.behavioral.visitor;

public class VisitorRunner {

	public static void main(String[] args) {
		Animal monkey = new Monkey();
		Animal lion = new Lion();
		Animal dolphin = new Dolphin();

		Speak speak = new Speak();

		monkey.accept(speak);    // Ooh oo aa aa!    
		lion.accept(speak);      // Roaaar!
		dolphin.accept(speak);   // Tuut tutt tuutt!

	}

}

```
