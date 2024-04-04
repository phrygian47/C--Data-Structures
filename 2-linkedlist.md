# What is a Linked List?

A Linked list is linear data structure, meaning items within the structure are ordered sequentially, or linearly. Each element of the linked list is attacked to the previous element and the next element. A linked list keeps track of these elements using pointers in the following fashion:

![photo](./images/Singly-Linked-List1.png)

You can see that each element is attached to the next using a "next" pointer that points to that element. This is called a "Singly Linked List". More advanced applications of the data structure also include a previous pointer usually named "prev", that points to the element before it. This type of linked list is called a "Doubly Linked List". Most linked lists also have a class attribute aptly named "data", this represents the data that you're storing, go figure. This attribute is also how you will access the data in your programming, for example we may see something like this:

```C#
    var item = myLinkedList.Data;
```

Linked lists are one of the most used and sought after data structures when it comes to dynamic data as the list will easily grow and shrink to handle the data. Now that we are familiar with what a linked list is, how is one constructed?

## Nodes

A linked list and its elements are constructed using nodes. In a singly linked list the node has two fields, it has a data field which stores the data, and a pointer field that points to the location of the next node in the list. When a linked list is at its end the node will then point to NULL which is useful for finding the end of a linked list. The following the code for constructing a singly linked list node; however, note that C# has its own C# class if you so choose to use it.

```C#
internal class Node {  
    internal int data;  
    internal Node next;  
    public Node(int d) {  
        data = d;  
        next = null;  
    }  
} 
```

## Common Linked List Operations

We can create a linked list in C# by simply intializing one like any other structure or variable.

```C#
    LinkedList<type> my_list = new LinkedList<type>(); // type would be replaced with desired data type such as int, string, etc.
```

To add to a linked list there are 3 options, insert_head(value), insert_tail(value), and insert(node, value). insert_head inserts the data before the top, or the head of the linked list, insert_tail similarly inserts the data the end or the tail of the list, and insert takes a node and inserts the data after that node. These three operations can be used in C# using the following:

```C#
    LinkedList<string> myList = new LinkedList<string>;
    myList.AddFirst("Fus");     // This inserts the data before the head of a LL.
    myList.AddLast("Dah");      // This inserts the data at the end of the LL.
    myList.AddAfter("Fus", "Ro")// This inserts the data after the node containing "fus"

    foreach(string str in myList){
        Console.Write(str + " "); // Fus Ro Dah
    }
```

We can also remove from a linked list with the following common operations: remove_head(), remove_tail(), and remove(node). These operation removes the first item, last item, and item containing "node" respectfully. They can be accessed in C# with:
```C#
    myList.RemoveFirst();   // LL now contains "Ro" and "Dah"
    myList.RemoveLast();    // LL now contains "Dah"
    myList.Remove("Dah");    // LL is now empty
```

Other operations of a linked list include size() and empty(). These operations return the size of the list, and a boolean representing if the list is empty. These are accessed in C# with:

```C#
    var length = myList.Count;  // length = 0
    if (myList.Count == 0){     // returns true
        Console.Writeline("The List is Empty");
    }
```

A linked list looks similar in how it operates toa dynamic array, however a linked list is much more efficient in the long run. The following table shows the effciency of these common operations and why they have that efficiency.

| Operation             | Efficiency                               |
|-----------------------|------------------------------------------|
| AddFirst(value)       | O(1) only adjusting pointers             |
| AddLast(value)        | O(1) only adjusting pointers             |
| AddAfter(node, value) | O(n) loop to find node                   |
| RemoveFist()          | O(1) only adjusting pointers             |
| RemoveLast()          | O(1) only adjusting pointers             |
| Remove(node)          | O(n) loop to find node                   |
| Count                 | O(1) size is maintained with LL class    |
| Count == 0            | O(1) only comparison is needed no loops. |

## Basic Code Example

Your biggest dream is to be the owner of a popular hot dog stand in New York city. However you are unsure how to handle the traffic of multiple oders. As orders are placed you are given their name. Write a program to order your customer's orders by name in the order they are received, and use this list to determine the next order to process. For this example as a customer enters the line we are given an input of their name. Let's say we see 3 people in line, we need to add all of their names into our list, and make sure we can retrieve them in order:

```C#
    int n = 0;
    Console.WriteLine("How many people are in line? ");
    n = int.Parse(Console.ReadLine());

```

Now that we know how many orders we are completing let us create our Linked List with the following Syntax
```C#
    LinkedList<String> orderLine = new LinkedList<String>();
```

We've created our list, now let us add to our list the order of people in which they arrive.
```C#
    for (int i = 0 ; i < n ; ++){
        var name = "";
        Console.WriteLine("What is the name for order number" + i + 1 + "?");
        name = Console.ReadLine();
        orderLine.AddLast(name);
    }
```

Now that our list is complete, we can display the order in which we need to complete orders, we can do this most easily with a foreach loop.

```C#
    foreach (var person in orderLine){
        Console.WriteLine("Order up for " + person + "!")
        Console.WriteLine("Are you ready for the next order? (press any key to continue) ")     // Buffer for chef to control when the next order is displayed.
        Console.ReadLine();
    }
    Console.WriteLine("All orders complete!");

```

An example of this code being run is found here:
```
    How many people are in line? 
    > 3
    What is the name for order number 1?
    > Robert
    What is the name for order number 2?
    > Ana
    What is the name for order number 3?
    > Josh
    Order up for Robert!
    Are you ready for the next order? (press any key to continue) 
    > y
    Order up for Ana!
    Are you ready for the next order? (press any key to continue)
    > y
    Order up for Josh!
    All orders complete!
```

Now you're one step closer to achieving your dream of being a greasy hotdog stand owner. 

## Car Trouble

You just bought an old car that you are planning to restore, as you inspect the car you find there are a number of issues with the car all with varying priorities of "high", "medium" or "low". Create a program that adds these issues into a linked list as you discover them, and make sure to order by priority. Then print out the order of issues to show the order in which things need to be done. 

Execution of the code can be seen here.
```
    What needs to be fixed?
    > Brakes
    What is the priority? (1: high, 2: medium, 3: low)
    > 1
    Add another issue? (y/n)
    > y
    What needs to be fixed?
    > Blinker
    What is the priority? (1: low, 2: medium, 3: high)
    > 13
    Add another issue? (y/n)
    > n
    Do repairs in this order: 
   Brakes 
   Blinker
```

Once you are done you can review the solution [here.](code_solutions.md#car-troubles-solution)
