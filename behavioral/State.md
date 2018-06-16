State
-----
Real world example
> Imagine you are using some drawing application, you choose the paint brush to draw. Now the brush changes its behavior based on the selected color i.e. if you have chosen red color it will draw in red, if blue then it will be in blue etc.  

In plain words
> It lets you change the behavior of a class when the state changes.

Wikipedia says
> The state pattern is a behavioral software design pattern that implements a state machine in an object-oriented way. With the state pattern, a state machine is implemented by implementing each individual state as a derived class of the state pattern interface, and implementing state transitions by invoking methods defined by the pattern's superclass.
> The state pattern can be interpreted as a strategy pattern which is able to switch the current strategy through invocations of methods defined in the pattern's interface.

**Programmatic example**

Let's take an example of text editor, it lets you change the state of text that is typed i.e. if you have selected bold, it starts writing in bold, if italic then in italics etc.

First of all we have our state interface and some state implementations

```java
package com.prady00.dp.behavioral.state;
interface WritingState
{
    public void write(String words);
}
```
```java
package com.prady00.dp.behavioral.state;
class UpperCase implements WritingState
{
    public void write(String words)
    {
        System.out.println(words.toUpperCase());
    }
}
```

```java
package com.prady00.dp.behavioral.state;
class LowerCase implements WritingState
{
    public void write(String words)
    {
        System.out.println(words.toLowerCase()); ;
    }
}
```

```java
package com.prady00.dp.behavioral.state;
class DefaultText implements WritingState
{
    public void write(String words)
    {
        System.out.println(words);
    }
}
```

Then we have our editor
```java
package com.prady00.dp.behavioral.state;
class TextEditor
{
    private WritingState state;

    public TextEditor(WritingState state)
    {
        this.state = state;
    }

    public void setState(WritingState state)
    {
        this.state = state;
    }

    public void type(String words)
    {
        this.state.write(words);
    }
}
```
And then it can be used as
```java
package com.prady00.dp.behavioral.state;

public class StateRunner {

	public static void main(String[] args) {
		
		TextEditor editor = new TextEditor(new DefaultText());

		editor.type("First line");

		editor.setState(new UpperCase());

		editor.type("Second line");
		editor.type("Third line");

		editor.setState(new LowerCase());

		editor.type("Fourth line");
		editor.type("Fifth line");

	}

}

```
