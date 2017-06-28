# .NET-Performance-Tips and Guidelines
The term performance generally refers to the execution speed of a program. You can sometimes increase execution speed by following certain basic rules in your source code.

## Boxing and Unboxing
It is best to avoid using value types in situations where they must be boxed a high number of times, for example in non-generic collections classes such as System.Collections.ArrayList. You can avoid boxing of value types by using generic collections such as System.Collections.Generic.List<T>. Boxing and unboxing are computationally expensive processes. When a value type is boxed, an entirely new object must be created. This can take up to 20 times longer than a simple reference assignment. When unboxing, the casting process can take four times as long as an assignment.

## Strings
When you concatenate a large number of string variables, for example in a tight loop, use System.Text.StringBuilder instead of the C# + operator or the Visual Basic Concatenation Operators. 

When declaring Empty string use string.Empty instead of "".

## Destructors
Empty destructors should not be used. When a class contains a destructor, an entry is created in the Finalize queue. When the destructor is called, the garbage collector is invoked to process the queue. If the destructor is empty, this simply results in a loss of performance.

## Save expensive call results in a variable
If you are calling an expensive function and using its result multiple times, save that result in a variable rather than having to call the function multiple times.

````
// bad
if (reallySlowSearchForIndex("abc") >= 0) {
    remove(reallySlowSearchForIndex("abc"));
}

// good
int index = reallySlowSearchForIndex("abc");
if (index >= 0) {
    remove(index);
}
````
