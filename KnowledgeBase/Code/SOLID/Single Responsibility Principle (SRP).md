![[SRP.png]]

As the name suggests, the Single Responsibility principle states **2 key principles**.
1. Your class or method should have only **one reason to change**.
2. Your class or method should have only **one responsibility to take care of**.
---
So what does that mean actually? While you design your logic in either class or method, you should not be writing all kinds of responsibilities in one place. This will make your code quite complex and unmanageable. It will also be difficult to adjust new changes later as there are high chances it will affect the other functionality and you will end up testing all the functionalities even though it is a smaller change. Let’s take the example below.

![[Class_invoice.png]]
``` c#
public class Invoice  
{  
    public void AddInvoice()  
    {   
        // your logic  
    }  
  
    public void DeleteInvoice()  
	{   
        // your logic  
    }  
  
    public void GenerateReport()  
	{   
        // your logic  
    }  
  
    public void EmailReport()  
	{   
        // your logic  
    }  
}
```

The class Invoice consists of 4 different methods - AddInvoice(), DeleteInvoice(), GenerateReport(), EmailReport(). As the single responsibility principle says, your class or method should have only one responsibility and only one reason to change, now let’s find out whether the above example satisfies the conditions. If we take a look at the methods, each has a single responsibility. For e.g. The AddInvoice() method is only responsible for adding an invoice to the system, DeleteInvoice() method is only responsible for deleting invoices,s and likewise for GenerateReport() and EmailReport() methods. We can say that methods do satisfy the single responsibility principle. But if you take a look at Invoice class, it is now taking care of multiple responsibilities which are not satisfying the single responsibility principle. So in order to satisfy the single responsibility principle for class Invoice, we will divide the methods into different classes where one class will take care of only one responsibility.

![[Separation to classes for SRP.png]]

We are going to club methods AddInvoice() and DeleteInvoice() into single class Invoice as they do a similar kind of functionality. Whereas we will be creating separate classes Report and Email for methods GenerateReport() and EmailReport() respectively as they are completely independent and have different functionality.

![[Divided class for SRP.png]]

``` c#
public class Invoice  
{  
    public void AddInvoice()  
    {  
	    // your logic  
    }  
  
    public void DeleteInvoice()  
    {  
	    // your logic  
    }  
}  
  
public class Report  
{  
  
    public void GenerateReport()  
    {  
	    // your logic  
    }  
}  
  
public class Email  
{  
    public void EmailReport()  
    {  
	    // your logic  
    }  
}
```

That’s it! Now each class is responsible to take care of only one responsibility and only one reason to change. The code is now ever smaller and manageable for each functionality and you won’t be required to test the complete functionality of each class if the change is happening for any one of the classes.

### Conclusion

With the above example, we have now understood how to refactor the code and achieve the single responsibility principle. With the help of the single responsibility principle, it helps us to:
1. Reduce the complexity of the program
2. It's easier to maintain the code.
   
[Reference](https://www.geeksforgeeks.org/system-design/single-responsibility-in-solid-design-principle/)
[[SOLID]]
