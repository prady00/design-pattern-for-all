Iterator
========

Real world example
> An old radio set will be a good example of iterator, where user could start at some channel and then use next or previous buttons to go through the respective channels. Or take an example of MP3 player or a TV set where you could press the next and previous buttons to go through the consecutive channels or in other words they all provide an interface to iterate through the respective channels, songs or radio stations.  

In plain words
> It presents a way to access the elements of an object without exposing the underlying presentation.

Wikipedia says
> In object-oriented programming, the iterator pattern is a design pattern in which an iterator is used to traverse a container and access the container's elements. The iterator pattern decouples algorithms from containers; in some cases, algorithms are necessarily container-specific and thus cannot be decoupled.

**Programmatic example**

Translating our radio stations example from above. First of all we have `RadioStation`

```java
package com.prady00.dp.behavioral.iterator;
class RadioStation
{
    protected double frequency;

    public  RadioStation(Double frequency)
    {
        this.frequency = frequency;
    }

    public double getFrequency()
    {
        return this.frequency;
    }

	@Override
	public String toString() {
		return "RadioStation [frequency=" + frequency + "]";
	}
    
}
```
Then we have our iterator

```java
package com.prady00.dp.behavioral.iterator;

import java.util.Arrays;
import java.util.Iterator;

class StationList implements Iterator<RadioStation> {

	int iterator = 0;

	protected RadioStation[] radiostationArray = new RadioStation[5];

	@Override
	public boolean hasNext() {
		try {
			if (radiostationArray[iterator] instanceof RadioStation) {
				return true;
			}
		} catch (Exception e) {
			return false;
		}
		return false;
	}

	@Override
	public RadioStation next() {
		return radiostationArray[iterator++];
	}

	public void addStations() {
		Arrays.asList(0, 1, 2, 3, 4)
				.stream()
				.forEach(
						element -> {
							radiostationArray[element] = new RadioStation(Math
									.random() * Math.random());
						});
	}

}
```
And then it can be used as
```java
package com.prady00.dp.behavioral.iterator;

public class IteratorRunner {

	public static void main(String[] args) {
		
		StationList stationList = new StationList();

		stationList.addStations();
		
		while(stationList.hasNext()){
			System.out.println(stationList.next());
		}
		
	}

}
```
