Factory Method
==============

Real world example
> Consider the case of a hiring manager. It is impossible for one person to interview for each of the positions. Based on the job opening, she has to decide and delegate the interview steps to different people.

In plain words
> It provides a way to delegate the instantiation logic to child classes.

Wikipedia says
> In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.

 **Programmatic Example**

Taking our hiring manager example above. First of all we have an interviewer interface and some implementations for it

```java
package com.prady00.dp.creational.factorymethod;
interface Interviewer
{
    public void askQuestions();
}
```

```java
package com.prady00.dp.creational.factorymethod;
class Developer implements Interviewer
{
    public void askQuestions()
    {
        System.out.println("Asking about design patterns!");
    }
}
```
```java
package com.prady00.dp.creational.factorymethod;
class CommunityExecutive implements Interviewer
{
    public void askQuestions()
    {
        System.out.println("Asking about community building"); 
    }
}
```

Now let us create our `HiringManager`

```java
package com.prady00.dp.creational.factorymethod;
abstract class HiringManager
{

    // Factory method
    abstract protected Interviewer makeInterviewer();

    public void takeInterview()
    {
        Interviewer interviewer = this.makeInterviewer();
        interviewer.askQuestions();
    }
}

```
Now any child can extend it and provide the required interviewer
```java
package com.prady00.dp.creational.factorymethod;
class DevelopmentManager extends HiringManager
{
    protected Interviewer makeInterviewer()
    {
        return new Developer();
    }
}
```

```java
package com.prady00.dp.creational.factorymethod;
class MarketingManager extends HiringManager
{
    protected Interviewer makeInterviewer() 
    {
        return new CommunityExecutive();
    }
}
```
and then it can be used as

```java
package com.prady00.dp.creational.factorymethod;

public class FactoryMethodRunner {

	public static void main(String[] args) {
		
		DevelopmentManager devManager = new DevelopmentManager();
		devManager.takeInterview(); // Output: Asking about design patterns

		MarketingManager marketingManager = new MarketingManager();
		marketingManager.takeInterview(); // Output: Asking about community building.

	}

}
```

**When to use?**

Useful when there is some generic processing in a class but the required sub-class is dynamically decided at runtime. Or putting it in other words, when the client doesn't know what exact sub-class it might need.
