Mediator
========

Real world example
> A general example would be when you talk to someone on your mobile phone, there is a network provider sitting between you and them and your conversation goes through it instead of being directly sent. In this case network provider is mediator.

In plain words
> Mediator pattern adds a third party object (called mediator) to control the interaction between two objects (called colleagues). It helps reduce the coupling between the classes communicating with each other. Because now they don't need to have the knowledge of each other's implementation.

Wikipedia says
> In software engineering, the mediator pattern defines an object that encapsulates how a set of objects interact. This pattern is considered to be a behavioral pattern due to the way it can alter the program's running behavior.

**Programmatic Example**

Here is the simplest example of a chat room (i.e. mediator) with users (i.e. colleagues) sending messages to each other.

First of all, we have the mediator i.e. the chat room

```java
package com.prady00.dp.behavioral.mediator;
interface ChatRoomMediator 
{
    public void showMessage(User user, String message);
}
```

```java
package com.prady00.dp.behavioral.mediator;

import java.util.Date;

// Mediator
class ChatRoom implements ChatRoomMediator
{
    public void showMessage(User user, String message)
    {
        Date time = new Date();
        String sender = user.getName();
        System.out.println(time + "[" + sender + "]:" + message);
    }
}
```

Then we have our users i.e. colleagues
```java
package com.prady00.dp.behavioral.mediator;
class User {
    protected String name;
    protected ChatRoomMediator chatMediator;

    public User(String name, ChatRoomMediator chatMediator) {
        this.name = name;
        this.chatMediator = chatMediator;
    }
    
    
    public void send(String message) {
        this.chatMediator.showMessage(this, message);
    }


	public String getName() {
		return this.name;
	}
}
```
And the usage
```java
package com.prady00.dp.behavioral.mediator;

public class MediatorRunner {

	public static void main(String[] args) {
		ChatRoomMediator mediator = new ChatRoom();

		User john = new User("John Doe", mediator);
		User jane = new User("Jane Doe", mediator);

		john.send("Hi there!");
		jane.send("Hey!");

		// Output will be
		// Thu May 31 14:56:15 IST 2018[John Doe]:Hi there!
		// Thu May 31 14:56:15 IST 2018[Jane Doe]:Hey!

	}

}
```