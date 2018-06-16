Proxy
=====
Real world example
> Have you ever used an access card to go through a door? There are multiple options to open that door i.e. it can be opened either using access card or by pressing a button that bypasses the security. The door's main functionality is to open but there is a proxy added on top of it to add some functionality. Let me better explain it using the code example below.

In plain words
> Using the proxy pattern, a class represents the functionality of another class.

Wikipedia says
> A proxy, in its most general form, is a class functioning as an interface to something else. A proxy is a wrapper or agent object that is being called by the client to access the real serving object behind the scenes. Use of the proxy can simply be forwarding to the real object, or can provide additional logic. In the proxy extra functionality can be provided, for example caching when operations on the real object are resource intensive, or checking preconditions before operations on the real object are invoked.

**Programmatic Example**

Taking our security door example from above. Firstly we have the door interface and an implementation of door

```java
package com.prady00.dp.structural.proxy;
interface Door
{
    public void open();
    public void close();
}
```
```java
package com.prady00.dp.structural.proxy;

class LabDoor implements Door
{
    public void open()
    {
        System.out.println("Opening lab door");
    }

    public void close()
    {
        System.out.println("Closing the lab door");
    }
}
```
Then we have a proxy to secure any doors that we want
```java
package com.prady00.dp.structural.proxy;
class SecuredDoor
{
    protected Door door;

	public SecuredDoor(Door door)
    {
        this.door = door;
    }

    public void open(String password)
    {
        if (this.authenticate(password)) {
            this.door.open();
        } else {
            System.out.println("Big no! It ain't possible.");
        }
    }

    public boolean authenticate(String password)
    {
        return password.equals("ecr@t");
    }

    public void close()
    {
        this.door.close();
    }
}
```
And here is how it can be used
```java
package com.prady00.dp.structural.proxy;

public class ProxyRunner {

	public static void main(String[] args) {
		SecuredDoor door = new SecuredDoor(new LabDoor());
		
		door.open("invalid"); // Big no! It ain't possible.

		door.open("ecr@t"); // Opening lab door
		door.close(); // Closing lab door

	}

}

```
