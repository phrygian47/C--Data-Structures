# Solution for the Workout Problem

For this solution we create a stack and simply base what is pushed to the stack first and then check that element to determine what the following workouts will be. This can be done more efficiently with only 3 if else statement, but for our purposes we will be a little more inefficient to utilize the stack more.
```C#
    var workoutStack = new Stack(); // Initialize new stack to contain workouts
    var workouts = ["Push", "Pull", "Legs"];
    /* First workout of the week can be any as there 
    is nothing currently in the stack*/
    int choice = 0;
    Console.WriteLine("Choose your first workout: 0 = Push, 1 = Pull, 2 = Legs":)
    choice = Console.ReadLine();
    Console.WriteLine("The first workout is" + workouts[choice]);
    workoutStack.Push(workouts[choice]);

    // Now for the second workout we need to check the last workout
    var lastWorkout = workoutStack.Pop();
    if (lastWorkout == workouts[0]){
        workoutStack.Push(workouts[1]);
        var nextWorkout = workouts[1];
        Console.Writeline("Today's workout is: " + nextWorkout);
    } else if (lastWorkout == workouts[1]){
        workoutStack.Push(workouts[2]);
        var nextWorkout = workouts[2];
        Console.Writeline("Today's workout is: " + nextWorkout);
    } else if (lastWorkout == workouts[2]){
        workoutStack.Push(workouts[0]);
        var nextWorkout = workouts[0];
        Console.Writeline("Today's workout is: " + nextWorkout);
    }
    // For the final workout we check the last workout using the stack again.
    var lastWorkout = workoutStack.Pop();
    if (lastWorkout == workouts[0]){
        workoutStack.Push(workouts[1]);
        var finalWorkout = workouts[1];
        Console.Writeline("The final workout is: " + nextWorkout);
    } else if (lastWorkout == workouts[1]){
        workoutStack.Push(workouts[2]);
        var finalWorkout = workouts[2];
        Console.Writeline("The final workout is: " + nextWorkout);
    } else if (lastWorkout == workouts[2]){
        workoutStack.Push(workouts[0]);
        var finalWorkout = workouts[0];
        Console.Writeline("the Final workout is: " + nextWorkout);
    }

```

# Car Troubles Solution

For this solution we will not be using the implement C# class of Linked Lists as we are using a priority attribute in our LinkedList class. You absolutely can solve this using the C# class by perhaps creating a class for the issue and inserting objects into a Linked List, this is simply how I chose to solve this issue. This LinkedList PriorityQueue class can be found on the [GeeksForGeeks website](https://www.geeksforgeeks.org/priority-queue-using-linked-list/), it has just been slightly modified to fit our purposes here.

```C#
 class PriorityQueue
{
// Node
    public class Node{
        public string data;
        // Lower values indicate
        // higher priority
        public int priority;
        public Node next;
    }

    public static Node node = new Node();

// Function to Create A New Node
    public static Node newNode(string d, int p){
        Node temp = new Node();
        temp.data = d;
        temp.priority = p;
        temp.next = null;

        return temp;
    }

// Removes the element with the
// highest priority from the list
    public static Node pop(Node head){
        Node temp = head;
        (head) = (head).next;
        return head;
    }

// Function to push according to priority
    public static Node push(Node head, string d, int p){
        Node start = (head);

        // Create new Node
        Node temp = newNode(d, p);

        /* Special Case: The head of list
        has lesser priority than new node.
        So insert new node before head node
        and change head node.*/
        if ((head).priority > p)
        {

            // Insert New Node before head
            temp.next = head;
            (head) = temp;
        }
        else
        {

            // Traverse the list and find a
            // position to insert new node
            while (start.next != null &&
                   start.next.priority < p)
            {
                start = start.next;
            }

            // Either at the ends of the list
            // or at required position
            temp.next = start.next;
            start.next = temp;
        }
        return head;
    }

    public override string ToString(){
        return "<Issues>{" + string.Join(", ", this) + "}";
    }

    public static void Main(string[] args){
        // Create a Priority Queue
        string issue;
        int priority;
        string done;
        Console.WriteLine("What needs to be fixed?" );
        issue = Console.ReadLine();       // Get issue name
        Console.WriteLine("What is the priority? (1: high, 2: medium, 3: low");
        priority = int.Parse(Console.ReadLine()); // Get issue priority
        Node issues = newNode(issue, priority);
        Console.WriteLine("Add another issue? (y/n)");
        done = Console.ReadLine().ToLower();
        while (done == "y");{
            Console.WriteLine("What needs to be fixed?" );
            issue = Console.ReadLine();       // Get issue name
            Console.WriteLine("What is the priority? (1: high, 2: medium, 3: low");
            priority = int.Parse(Console.ReadLine()); // Get issue priority
            issues = push(issues, issue, priority);
            Console.WriteLine("Add another issue? (y/n)");
            done = Console.ReadLine().ToLower();
        }
        // Print out issues in order
        Console.WriteLine("Do repairs in this order: ")
        foreach (var issue in issues){
            Console.WriteLine(issue.data);
        }
    }
}

```

# Balanced Binary Tree
For this problem we are given an unbalanced BST that we must balance. To do this we will not use rotation but simply create a new tree. We do this by adding all nodes to a list using recursion, and doing it in order. Keep in mind we are using many functions that are defined int the BST.md file, for the sake of brevity I will not include the entire class here.

```C#
    public void BSTtoList(Node root, List<Node> nodes){
        // Base case
        if (root == null){
            return;
        }
        // By adding the left first before adding the right we order the list
        // smallest to greatest
        BSTtoList(root.left, nodes)
        nodes.Add(root);
        storeBSTNodes(root.right, nodes)
    }
    public void buildBalancedTree(int[] nodes, int start, int end){
        // Base case
        if (start > end){
            return;
        }
        var mid = (start + end) / 2;
        Node node = nodes[mid];
        node.left = buildBalancedTree(nodes, start, mid-1, bst);
        node.right = buildBalancedTree(nodes, mid+1, end, bst);
    }
    public static void Main(){
        tree.Insert(10);    // this is creating our unbalanced tree
        tree.Insert(9);
        tree.Insert(8);
        tree.Insert(7);
        tree.Insert(6);
        tree.Insert(5);

        List<Node> nodes = new List<Node>();
        BSTtoList(root, nodes);

        int n = nodes.Count;
        buildBalancedTree(nodes, 0, n-1);
    }
```