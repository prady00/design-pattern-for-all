Bridge
=======
Real world example
> Consider you have a website with different pages and you are supposed to allow the user to change the theme. What would you do? Create multiple copies of each of the pages for each of the themes or would you just create separate theme and load theme based on the user's preferences? Bridge pattern allows you to do the second i.e.

![With and without the bridge pattern](https://cloud.githubusercontent.com/assets/11269635/23065293/33b7aea0-f515-11e6-983f-98823c9845ee.png)

In Plain Words
> Bridge pattern is about preferring composition over inheritance. Implementation details are pushed from a hierarchy to another object with a separate hierarchy.

Wikipedia says
> The bridge pattern is a design pattern used in software engineering that is meant to "decouple an abstraction from its implementation so that the two can vary independently"

**Programmatic Example**

Translating our WebPage example from above. Here we have the `WebPage` hierarchy

```java
package com.prady00.dp.structural.bridge;
interface WebPage
{
    public String getContent();
}
```

```java
package com.prady00.dp.structural.bridge;
class About implements WebPage
{
   
	protected Theme theme;

    public About(Theme theme)
    {
        this.theme = theme;
    }

    public String getContent()
    {
        return "About page in " + this.theme.getColor();
    }
}
```

```java
package com.prady00.dp.structural.bridge;
class Careers implements WebPage
{
    protected Theme theme;

    public Careers(Theme theme)
    {
        this.theme = theme;
    }

    public String getContent()
    {
        return "Careers page in " + this.theme.getColor();
    }
}
```
And the separate theme hierarchy
```java

interface Theme
{
    public function getColor();
}

```

```java
package com.prady00.dp.structural.bridge;

interface Theme
{
    public String getColor();
}
```

```java
package com.prady00.dp.structural.bridge;

class LightTheme implements Theme
{
    public String getColor()
    {
        return "Off white";
    }
}

```

```java
package com.prady00.dp.structural.bridge;
class AquaTheme implements Theme
{
    public String getColor()
    {
        return "Light blue";
    }
}
```
And both the hierarchies
```java
package com.prady00.dp.structural.bridge;

public class BridgeRunner {

	public static void main(String[] args) {
		Theme darkTheme = new DarkTheme();

		WebPage about = new About(darkTheme);
		WebPage careers = new Careers(darkTheme);

		System.out.println(about.getContent());// "About page in Dark Black";
		System.out.println(careers.getContent());// "Careers page in Dark Black";

	}

}

```