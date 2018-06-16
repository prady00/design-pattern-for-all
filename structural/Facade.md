Facade
======

Real world example
> How do you turn on the computer? "Hit the power button" you say! That is what you believe because you are using a simple interface that computer provides on the outside, internally it has to do a lot of stuff to make it happen. This simple interface to the complex subsystem is a facade.

In plain words
> Facade pattern provides a simplified interface to a complex subsystem.

Wikipedia says
> A facade is an object that provides a simplified interface to a larger body of code, such as a class library.

**Programmatic Example**

Taking our computer example from above. Here we have the computer class

```java
package com.prady00.dp.structural.facade;
class Computer
{
    public void getElectricShock()
    {
        System.out.println("Ouch!");
    }

    public void makeSound()
    {
        System.out.println("Beep beep!");
    }

    public void showLoadingScreen()
    {
        System.out.println("Loading..");
    }

    public void bam()
    {
        System.out.println("Ready to be used!");
    }

    public void closeEverything()
    {
        System.out.println("Bup bup bup buzzzz!");
    }

    public void sooth()
    {
        System.out.println("Zzzzz");
    }

    public void pullCurrent()
    {
        System.out.println("Haaah!");
    }
}
```
Here we have the facade
```java
package com.prady00.dp.structural.facade;
class ComputerFacade
{
    protected Computer computer;

    public ComputerFacade(Computer computer)
    {
        this.computer = computer;
    }

    public void turnOn()
    {
        this.computer.getElectricShock();
        this.computer.makeSound();
        this.computer.showLoadingScreen();
        this.computer.bam();
    }

    public void turnOff()
    {
        this.computer.closeEverything();
        this.computer.pullCurrent();
        this.computer.sooth();
    }
}
```
Now to use the facade
```java
package com.prady00.dp.structural.facade;

public class FacadeRunner {

	public static void main(String[] args) {
		ComputerFacade computer = new ComputerFacade(new Computer());
		computer.turnOn(); // Ouch! Beep beep! Loading.. Ready to be used!
		computer.turnOff(); // Bup bup buzzz! Haah! Zzzzz

	}

}
```
