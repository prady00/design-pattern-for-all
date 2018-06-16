Observer
--------
Real world example
> A good example would be the job seekers where they subscribe to some job posting site and they are notified whenever there is a matching job opportunity.   

In plain words
> Defines a dependency between objects so that whenever an object changes its state, all its dependents are notified.

Wikipedia says
> The observer pattern is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.

**Programmatic example**

Translating our example from above. First of all we have job seekers that need to be notified for a job posting
```java
package com.prady00.dp.behavioral.observor;
class JobPost
{
    private String title;

    public JobPost(String title)
    {
        this.title = title;
    }

    public String getTitle()
    {
        return this.title;
    }
}
```

```java
package com.prady00.dp.behavioral.observor;
class JobSeeker
{
    private String name;

    public JobSeeker(String name)
    {
        this.name = name;
    }

    public void onJobPosted(JobPost jobPost)
    {
        // Do something with the job posting
    	System.out.println("Hi " + this.name + "! New job posted: "+ jobPost.getTitle());
    }
}
```
Then we have our job postings to which the job seekers will subscribe
```java 
package com.prady00.dp.behavioral.observor;

import java.util.ArrayList;
import java.util.List;

class EmploymentAgency
{
    private List<JobSeeker> observers = new ArrayList<>();

    protected void notify(JobPost jobPost)
    {
        for(JobSeeker jobSeeker :  observers) {
            jobSeeker.onJobPosted(jobPost);
        }
    }

    public void attach(JobSeeker observer)
    {
        observers.add(observer);
    }

    public void addJob(JobPost jobPost)
    {
        this.notify(jobPost);
    }
}
```
Then it can be used as
```java
package com.prady00.dp.behavioral.observor;

public class ObservorRunner {

	public static void main(String[] args) {
		// Create subscribers
		JobSeeker pradeep = new JobSeeker("pradeep kumar");
		JobSeeker gaurav = new JobSeeker("gaurav varshney");

		// Create publisher and attach subscribers
		EmploymentAgency employmentAgency = new EmploymentAgency();
		employmentAgency.attach(pradeep);
		employmentAgency.attach(gaurav);

		// Add a new job and see if subscribers get notified
		employmentAgency.addJob(new JobPost("Software Engineer"));

		// Output
		// Hi pradeep kumar! New job posted: Software Engineer
		// Hi gaurav varshney! New job posted: Software Engineer
	}

}

```