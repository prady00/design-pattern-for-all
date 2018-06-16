Template Method
---------------

Real world example
> Suppose we are getting some house built. The steps for building might look like
> - Prepare the base of house
> - Build the walls
> - Add roof
> - Add other floors

> The order of these steps could never be changed i.e. you can't build the roof before building the walls etc but each of the steps could be modified for example walls can be made of wood or polyester or stone.

In plain words
> Template method defines the skeleton of how a certain algorithm could be performed, but defers the implementation of those steps to the children classes.

Wikipedia says
> In software engineering, the template method pattern is a behavioral design pattern that defines the program skeleton of an algorithm in an operation, deferring some steps to subclasses. It lets one redefine certain steps of an algorithm without changing the algorithm's structure.

**Programmatic Example**

Imagine we have a build tool that helps us test, lint, build, generate build reports (i.e. code coverage reports, linting report etc) and deploy our app on the test server.

First of all we have our base class that specifies the skeleton for the build algorithm
```java
package com.prady00.dp.behavioral.template;
abstract class Builder
{
    // Template method
    final public void build()
    {
        this.test();
        this.lint();
        this.assemble();
        this.deploy();
    }

    abstract public void test();
    abstract public void lint();
    abstract public void assemble();
    abstract public void deploy();
}
```

Then we can have our implementations

```java
package com.prady00.dp.behavioral.template;
class AndroidBuilder extends Builder
{
    public void test()
    {
        System.out.println("Running android tests");
    }

    public void lint()
    {
        System.out.println("Linting the android code");
    }

    public void assemble()
    {
        System.out.println("Assembling the android build");
    }

    public void deploy()
    {
        System.out.println("Deploying android build to server");
    }
}
```

```java
package com.prady00.dp.behavioral.template;
class IosBuilder extends Builder
{
    public void test()
    {
        System.out.println("Running ios tests");
    }

    public void lint()
    {
        System.out.println("Linting the ios code"); ;
    }

    public void assemble()
    {
        System.out.println("Assembling the ios build");
    }

    public void deploy()
    {
        System.out.println("Deploying ios build to server");
    }
}
```
And then it can be used as

```java
package com.prady00.dp.behavioral.template;

public class TemplateMethodRunner {

	public static void main(String[] args) {
		Builder androidBuilder = new AndroidBuilder();
		androidBuilder.build();

		// Output:
		// Running android tests
		// Linting the android code
		// Assembling the android build
		// Deploying android build to server

		Builder iosBuilder = new IosBuilder();
		iosBuilder.build();

		// Output:
		// Running ios tests
		// Linting the ios code
		// Assembling the ios build
		// Deploying ios build to server
	}

}

```
