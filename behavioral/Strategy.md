Strategy
--------

Real world example
> Consider the example of sorting, we implemented bubble sort but the data started to grow and bubble sort started getting very slow. In order to tackle this we implemented Quick sort. But now although the quick sort algorithm was doing better for large datasets, it was very slow for smaller datasets. In order to handle this we implemented a strategy where for small datasets, bubble sort will be used and for larger, quick sort.

In plain words
> Strategy pattern allows you to switch the algorithm or strategy based upon the situation.

Wikipedia says
> In computer programming, the strategy pattern (also known as the policy pattern) is a behavioural software design pattern that enables an algorithm's behavior to be selected at runtime.

**Programmatic example**

Translating our example from above. First of all we have our strategy interface and different strategy implementations

```java
package com.prady00.dp.behavioral.strategy;
interface SortStrategy
{
    public String[] sort(String[] dataset);
}
```

```java
package com.prady00.dp.behavioral.strategy;

class BubbleSortStrategy implements SortStrategy
{
    public String[] sort(String[] dataset)
    {
        System.out.println("Sorting using bubble sort");
        
        // Do sorting
        return dataset;
    }
}
```


```java
package com.prady00.dp.behavioral.strategy;

class QuickSortStrategy implements SortStrategy
{
    public String[] sort(String[] dataset)
    {
        System.out.println("Sorting using quick sort");

        // Do sorting
        return dataset;
    }
}
```

And then we have our client that is going to use any strategy
```java
package com.prady00.dp.behavioral.strategy;
class Sorter
{
    public SortStrategy sorter;

    public Sorter(SortStrategy sorter)
    {
        this.sorter = sorter;
    }

    public String[] sort(String[] dataset)
    {
        return this.sorter.sort(dataset);
    }
}
```
And it can be used as
```java
package com.prady00.dp.behavioral.strategy;

public class StrategyRunner {

	public static void main(String[] args) {
		String[] dataset = {"1", "5", "4", "3", "2", "8"};

		Sorter sorter = new Sorter(new BubbleSortStrategy());
		sorter.sort(dataset); // Output : Sorting using bubble sort

		Sorter sorter2 = new Sorter(new QuickSortStrategy());
		sorter2.sort(dataset); // Output : Sorting using quick sort
	}

}

```
