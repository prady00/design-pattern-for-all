Memento
========

Real world example
> Take the example of calculator (i.e. originator), where whenever you perform some calculation the last calculation is saved in memory (i.e. memento) so that you can get back to it and maybe get it restored using some action buttons (i.e. caretaker).

In plain words
> Memento pattern is about capturing and storing the current state of an object in a manner that it can be restored later on in a smooth manner.

Wikipedia says
> The memento pattern is a software design pattern that provides the ability to restore an object to its previous state (undo via rollback).

Usually useful when you need to provide some sort of undo functionality.

**Programmatic Example**

Lets take an example of text editor which keeps saving the state from time to time and that you can restore if you want.

First of all we have our memento object that will be able to hold the editor state

```java
package com.prady00.dp.behavioral.memento;
class EditorMemento
{
    protected String content;

    public EditorMemento(String content)
    {
        this.content = content;
    }

    public String getContent()
    {
        return this.content;
    }
}
```

Then we have our editor i.e. originator that is going to use memento object

```java
package com.prady00.dp.behavioral.memento;

// Originator
class Editor
{
    protected String content = "";

    public void type(String words)
    {
        this.content = this.content + " " + words;
    }

    public String getContent()
    {
        return this.content;
    }

    public EditorMemento save()
    {
        return new EditorMemento(this.content);
    }

    public void restore(EditorMemento memento)
    {
        this.content = memento.getContent();
    }
}
```

And then it can be used as

```java
package com.prady00.dp.behavioral.memento;

public class MementoRunner {

	public static void main(String[] args) {
		
		Editor editor = new Editor();

		// Type some stuff
		editor.type("This is the first sentence.");
		editor.type("This is second.");

		// Save the state to restore to : This is the first sentence. This is second.
		EditorMemento saved = editor.save();

		// Type some more
		editor.type("And this is third.");
		
		editor.save();
		
		System.out.println(editor.getContent());
		
		System.out.println("Restoring");

		// Restoring to last saved state
		editor.restore(saved);
		
		System.out.println(editor.getContent()); // This is the first sentence. This is second.

	}

}

```
