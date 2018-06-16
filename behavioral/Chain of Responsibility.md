Chain of Responsibility
==========================

Real world example
> For example, you have three payment methods (`A`, `B` and `C`) setup in your account; each having a different amount in it. `A` has 100 USD, `B` has 300 USD and `C` having 1000 USD and the preference for payments is chosen as `A` then `B` then `C`. You try to purchase something that is worth 210 USD. Using Chain of Responsibility, first of all account `A` will be checked if it can make the purchase, if yes purchase will be made and the chain will be broken. If not, request will move forward to account `B` checking for amount if yes chain will be broken otherwise the request will keep forwarding till it finds the suitable handler. Here `A`, `B` and `C` are links of the chain and the whole phenomenon is Chain of Responsibility.

In plain words
> It helps building a chain of objects. Request enters from one end and keeps going from object to object till it finds the suitable handler.

Wikipedia says
> In object-oriented design, the chain-of-responsibility pattern is a design pattern consisting of a source of command objects and a series of processing objects. Each processing object contains logic that defines the types of command objects that it can handle; the rest are passed to the next processing object in the chain.

**Programmatic Example**

Translating our account example above. First of all we have a base account having the logic for chaining the accounts together and some accounts

```java
package com.prady00.dp.behavioral.cor;
abstract class Account
{
    protected Account successor;
    public Double balance;
    
    public Account(Double balance)
    {
        this.balance = balance;
    }

    public void setNext(Account account)
    {
        this.successor = account;
    }

    public void pay(Double amountToPay)
    {
        if (this.canPay(amountToPay)) {
        	System.out.println("Paid " + amountToPay + " using " + getClass().getName());
        } else if (this.successor.balance > 0) {
        	System.out.println("Cannot pay using " + getClass().getName() + " Proceeding .. " );
            this.successor.pay(amountToPay);
        } else {
        	System.out.println("None of the accounts have enough balance");
        }
    }

    public boolean canPay(Double amount)
    {
        int comparision = Double.compare(this.balance , amount);
        if(comparision > 0){
        	return true;
        }
        return false;
    }
}
```

```java
package com.prady00.dp.behavioral.cor;
class Bank extends Account
{
	public Double balance;

    public Bank(Double balance)
    {
    	super(balance);
        this.balance = balance;
    }
}
```

```java
package com.prady00.dp.behavioral.cor;
class Bitcoin extends Account
{
	public Double balance;

    public Bitcoin(Double balance)
    {
    	super(balance);
        this.balance = balance;
    }
}
```

```java
package com.prady00.dp.behavioral.cor;
class Paypal extends Account
{
    protected Double balance;

    public Paypal(Double balance)
    {
    	super(balance);
        this.balance = balance;
    }
}
```

Now let's prepare the chain using the links defined above (i.e. Bank, Paypal, Bitcoin)

```java
package com.prady00.dp.behavioral.cor;

public class ChainOfResponsibilityRunner {

	public static void main(String[] args) {
		
		// Let's prepare a chain like below
		// bank->paypal->bitcoin
		//
		// First priority bank
		// If bank can't pay then paypal
		// If paypal can't pay then bit coin

		Bank bank 		= new Bank(100.00); 	// Bank with balance 100
		Paypal paypal 	= new Paypal(200.00); 	// Paypal with balance 200
		Bitcoin bitcoin = new Bitcoin(300.00); 	// Bitcoin with balance 300

		bank.setNext(paypal);
		paypal.setNext(bitcoin);

		// Let's try to pay using the first priority i.e. bank
		bank.pay(259.00);

		// Output will be
		// ==============
		// Cannot pay using com.prady00.dp.behavioral.cor.Bank Proceeding .. 
		// Cannot pay using com.prady00.dp.behavioral.cor.Paypal Proceeding .. 
		// Paid 259.0 using com.prady00.dp.behavioral.cor.Bitcoin

	}
}
```
