Command
==========================

Real world example
> A generic example would be you ordering food at a restaurant. You (i.e. `Client`) ask the waiter (i.e. `Invoker`) to bring some food (i.e. `Command`) and waiter simply forwards the request to Chef (i.e. `Receiver`) who has the knowledge of what and how to cook.
> Another example would be you (i.e. `Client`) switching on (i.e. `Command`) the television (i.e. `Receiver`) using a remote control (`Invoker`).

In plain words
> Allows you to encapsulate actions in objects. The key idea behind this pattern is to provide the means to decouple client from receiver.

Wikipedia says
> In object-oriented programming, the command pattern is a behavioral design pattern in which an object is used to encapsulate all information needed to perform an action or trigger an event at a later time. This information includes the method name, the object that owns the method and values for the method parameters.

**Programmatic Example**

First of all we have the receiver that has the implementation of every action that could be performed
```java
package com.prady00.dp.behavioral.command;
// Receiver
class Bulb
{
    public void turnOn()
    {
        System.out.println("Bulb has been lit");
    }

    public void turnOff()
    {
        System.out.println("Darkness!");
    }
}
```
then we have an interface that each of the commands are going to implement and then we have a set of commands
```java
package com.prady00.dp.behavioral.command;
interface Command
{
    public void execute();
    public void undo();
    public void redo();
}
```

```java
package com.prady00.dp.behavioral.command;
// Command
class TurnOn implements Command
{
    protected Bulb bulb;

    public TurnOn(Bulb bulb)
    {
        this.bulb = bulb;
    }

    public void execute()
    {
        this.bulb.turnOn();
    }

    public void undo()
    {
        this.bulb.turnOff();
    }

    public void redo()
    {
        this.execute();
    }
}
```

```java
package com.prady00.dp.behavioral.command;
class TurnOff implements Command
{
    protected Bulb bulb;

    public TurnOff(Bulb bulb)
    {
        this.bulb = bulb;
    }

    public void execute()
    {
        this.bulb.turnOff();
    }

    public void undo()
    {
        this.bulb.turnOn();
    }

    public void redo()
    {
        this.execute();
    }
}
```
Then we have an `Invoker` with whom the client will interact to process any commands
```java
package com.prady00.dp.behavioral.command;
// Invoker
class RemoteControl
{
    public void submit(Command command)
    {
        command.execute();
    }
}
```
Finally let's see how we can use it in our client
```java
package com.prady00.dp.behavioral.command;

public class Client {

	public static void main(String[] args) {
		Bulb bulb = new Bulb();

		TurnOn turnOn = new TurnOn(bulb);
		TurnOff turnOff = new TurnOff(bulb);

		RemoteControl remote = new RemoteControl();
		remote.submit(turnOn); // Bulb has been lit!
		remote.submit(turnOff); // Darkness!

	}

}
```

Command pattern can also be used to implement a transaction based system. Where you keep maintaining the history of commands as soon as you execute them. If the final command is successfully executed, all good otherwise just iterate through the history and keep executing the `undo` on all the executed commands.
