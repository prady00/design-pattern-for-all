Composite
=========

Real world example
> Every organization is composed of employees. Each of the employees has the same features i.e. has a salary, has some responsibilities, may or may not report to someone, may or may not have some subordinates etc.

In plain words
> Composite pattern lets clients treat the individual objects in a uniform manner.

Wikipedia says
> In software engineering, the composite pattern is a partitioning design pattern. The composite pattern describes that a group of objects is to be treated in the same way as a single instance of an object. The intent of a composite is to "compose" objects into tree structures to represent part-whole hierarchies. Implementing the composite pattern lets clients treat individual objects and compositions uniformly.

**Programmatic Example**

Taking our employees example from above. Here we have different employee types

```java
package com.prady00.dp.structural.composite;

import java.math.BigDecimal;

interface Employee
{
    public String getName();
    public void setSalary(BigDecimal $salary);
    public BigDecimal getSalary();
 
}

```

```java
package com.prady00.dp.structural.composite;

import java.math.BigDecimal;

class Developer implements Employee
{
    protected BigDecimal salary;
    protected String name;
   
    public Developer(String name, BigDecimal salary)
    {
        this.name = name;
        this.salary = salary;
    }

    public String getName()
    {
        return this.name;
    }

    public void setSalary(BigDecimal salary)
    {
        this.salary = salary;
    }

    public BigDecimal getSalary()
    {
        return this.salary;
    }
}

```

```java
package com.prady00.dp.structural.composite;

import java.math.BigDecimal;

class Designer implements Employee
{
    protected BigDecimal salary;
    protected String name;

    public Designer(String name, BigDecimal salary)
    {
        this.name = name;
        this.salary = salary;
    }

    public String getName()
    {
        return this.name;
    }

    public void setSalary(BigDecimal salary)
    {
        this.salary = salary;
    }

    public BigDecimal getSalary()
    {
        return this.salary;
    }
}
```

Then we have an organization which consists of several different types of employees

```java
package com.prady00.dp.structural.composite;

import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.List;

class Organization
{
    protected List<Employee> employees = new ArrayList<Employee>();

    public void addEmployee(Employee employee)
    {
        this.employees.add(employee);
    }

    public BigDecimal getNetSalaries()
    {
    	BigDecimal netSalary = new BigDecimal(0);

        for(Employee employee: employees) {
            netSalary = netSalary.add(employee.getSalary());
        }

        return netSalary;
    }
}
```

And then it can be used as

```java
package com.prady00.dp.structural.composite;

import java.math.BigDecimal;

public class CompositeRunner {

	public static void main(String[] args) {
		// Prepare the employees
		Employee john = new Developer("John Doe", new BigDecimal(12000));
		Employee jane = new Designer("Jane Doe", new BigDecimal(15000));

		// Add them to organization
		Organization organization = new Organization();
		organization.addEmployee(john);
		organization.addEmployee(jane);

		System.out.println("Net salaries: " + organization.getNetSalaries());  // Net Salaries: 27000

	}

}

```