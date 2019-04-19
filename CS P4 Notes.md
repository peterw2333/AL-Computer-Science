## 4.1.1 Abstractions

### Abstraction

Abstraction is filtering out unnecessary informations, leaving out only necessary and/or important information. 

For example, the metro system can be represented as a graph with vertices representing stations and edges representing lines. The actual geographical positions of the stations can be left out as they are not important.

### Decomposition

The breaking down of complex task into simpler tasks. 

It is the idea behind the divide-and-conquer algorithms, such as binary search and quicksort.

### Data modeling

Data modeling is the process of creating a data model for the data to be stored in a Database. 

A data model is a conceptual representation of

- Data objects
- The associations between different data objects
- The rules.

### Pattern Recognition

Looking for common solutions in different problems, in order to complete task in a more efficient and effective way.

### Algorithm Design

Developing step-by-step instructions to solve a problem

## 4.1.2 Algorithms

### Binary Search

**Binary search** can only be carried out on **sorted arrays**.

```pseudocode
DECLARE MyArray: ARRAY [1:100] OF INTEGER
DECLARE LBound: INTEGER
DECLARE UBound: INTEGER
DECLARE MiddleIndex: INTEGER
DECLARE Flag: BOOLEAN
DECLARE Target: INTEGER
DECLARE TargetIndex: INTEGER

INPUT Target
LBound <- 1
UBound <- 100
Flag <- FALSE

WHILE Flag = FALSE
	MiddleIndex <- INT((LBound + UBound)/2)
	IF MyArray[MiddleIndex] = Target THEN
		Flag <- TRUE
		TargetIndex <- MiddleIndex
	ELSE IF Myarray[MiddleIndex] < Target THEN
		LBound <- MiddleIndex + 1
	ELSE
		UBound <- MiddleIndex - 1
	END IF
END WHILE
```

The maximum number of comparisons using binary search on a sorted array of size $n$ is $\lceil\log_2{n}\rceil+1$.



### Insertion Sort

```pseudocode
DECLARE MyArray: ARRAY[0:99] OF INTEGER
DECLARE Pointer: INTEGER
DECLARE Position: INTEGER
DECLARE temp: INTEGER

// Version 1: Swap
FOR Pointer <- 1 TO 99
	Position <- Pointer
	WHILE Position > 0 AND MyArray[Position - 1] > MyArray[Position]
		temp <- MyArray[Position]
		MyArray[Position] <- MyArray[Position - 1]
		MyArray[Position - 1] <- temp
		Position <- Position - 1
	END WHILE
END FOR

// Version 2: Move & Insert
FOR Pointer <- 1 TO 99
	Position <- Pointer
	temp <- MyArray[Position]
	WHILE Position > 0 AND MyArray[Position - 1] > temp
		MyArray[Position] <- MyArray[Position - 1]
		Position <- Position - 1
	END WHILE
	MyArray[Position] <- temp
END FOR
```



### Efficient Bubble Sort

```
DECLARE MyArray: [0:99] OF INTEGER
DECLARE Flag: BOOLEAN
DECLARE temp: INTEGER
DECLARE i: INTEGER
DECLARE j: INTEGER

i <- 1

REPEAT
	Flag <- TRUE
	FOR j <- 0 TO 99 - i
		IF MyArray[j] > MyArray[j + 1] THEN
			Flag <- FALSE
			temp <- MyArray[j]
			MyArray[j] <- MyArray[j + 1]
			MyArray[j + 1] <- temp
		END IF
	END FOR
	i <- i + 1
UNTIL Flag = TRUE
```

#### Insertion Sort vs Bubble Sort

Insertion sort is an adaptive sort, therefore useful on partially sorted arrays.

Insertion sort have the same order of time complexity ($O(n^2)​$) as bubble sort, but generally performs fasters as it requires less swaps (one swaps = 3 writes), so preferable on large arrays.

Bubble sort needs to swap through the whole unsorted part of the array, while insertion sort only need to swap until the correct position. Also, the move-and-insert approach reduces the 3 operation of swapping down to 1, therefore insertion sort is more efficient.

 

## 4.1.3 Abstract Data Types (ADT)

### Stack

Data can only be added and removed in one end.

**Last In First Out (LIFO).** 

When the stack is full, we say that it is in **overflow** state.

When the stack is empty, we say that it is in **underflow** state.

`pop()` is for removal of the upmost item.

`push()` is for adding an item to the top of the stack.



#### Applications

- Reversing words: pushing the word in character by character, and pop out character by character in reverse order

- Recursion: push the latest instance of the function into the stack until base case. Then pop them and execute one by one

- Interrupt Handling: If a new interrupt is formed when the handling of an old one is not completed, the previous one is pushed into a stack and handled after the handling of new one is finished

- Conversion from infix to postfix notation (Reverse Polish Notation, RPN)

- Evaluation of an RPN expression



#### Implementation

```pseudocode
TYPE Stack
	DECLARE top: INTEGER
	DECLARE a: ARRAY[0:99] OF INTEGER
END TYPE

// Initialisation
PROCEDURE initStack(st: Stack)
	st.top <- -1
END PROCEDURE

// Adding element
PROCEDURE push(st: Stack, x: INTEGER)
	IF st.top >= 99 THEN
		OUTPUT "Overflow"
	ELSE
		st.top <- st.top + 1
		st.a[st.top] <- x
	END IF
END PROCEDURE

// Removing Element
FUNCTION pop(st: Stack) RETURNS INTEGER
	DECLARE temp: INTEGER
	IF st.pop <0 THEN
		OUTPUT "Underflow"
	ELSE
		temp <- st.a[st.top]
		st.top <- st.top - 1
		RETURN temp
	END IF
END FUNCTION
```



## Queue

#### Implementation

(Circular Queue)

```
TYPE Queue
	DECLARE head: INTEGER
	DECLARE tail: INTEGER
	DECLARE a: ARRAY[0:99] OF INTEGER
	DECLARE count: INTEGER
ENDTYPE

PROCEDURE init(qu: Queue)
	qu.head <- 0
	qu.tail <- 0
	qu.count <- 0
ENDPROCEDURE

PROCEDURE enQueue(x: INTEGER, qu: Queue)
	IF qu.count = 100 THEN
		OUTPUT "Queue is full."
	ELSE
		qu.count <- qu.count + 1
		IF qu.tail = 100 THEN
			qu.tail <- 0
			qu.a[qu.tail] <- x
		ELSE
			qu.a[qu.tail] <- x
			qu.tail <- qu.tail + 1
		ENDIF
	ENDIF
ENDPROCEDURE 

PROCEDURE deQueue(qu: Queue)
	IF qu.count = 0 THEN
		OUTPUT "Queue is empty."
	ELSE
		qu.count <- qu.count - 1
		IF qu.head = 99 THEN
			qu.head <- 0
		ELSE
			qu.head <- qu.head + 1
		ENDIF
	ENDIF
ENDPROCEDURE
```



## Linked List

A Linked List consists of a start pointer and a list of connected nodes.

Each node consists of two parts: A pointer to next node, and its data.

The StartPointer is a pointer which points to the first item of the list.

CIE always use an array of nodes to store the linked list.

Here is an initialised empty linked list:

StartPointer <- 0

| Array Index | Data | Pointer   |
| ----------- | ---- | --------- |
| 0           | ""   | 1         |
| 1           | ""   | 2         |
| 2           | ""   | 3         |
| 3           | ""   | 4         |
| 4           | ""   | 5         |
| 5           | ""   | 6         |
| 6           | ""   | NULL (-1) |

### Create a new linked list:

```pseudocode
// NullPointer should be set to -1 if using array element with index 0 
CONSTANT NullPointer = 0
// Declare record type to store data and pointer
TYPE ListNode
    DECLARE Data: STRING
    DECLARE Pointer: INTEGER 
ENDTYPE
DECLARE StartPointer : INTEGER 
DECLARE FreeListPtr : INTEGER 
DECLARE List[l : 7] OF ListNode
PROCEDURE InitialiseList 
    StartPointer <- NullPointer // set start pointer
    FreeListPtr <- 1 // set starting position of free list
    FOR Index <- 1 TO 6 // link all nodes to make free list
        List[Index].Pointer <- Index + 1
    ENDFOR
    List[7].Pointer <- NullPointer // last node of free list 
ENDPROCEDURE
```

### Inserting a new node into an ordered linked list:

```pseudocode
PROCEDURE InsertNode(Newitem: ListNode)
    IF FreeListPtr <> NullPointer THEN 
        // there is space in the array
        // take node from free list and store data item 
        NewNodePtr <- FreeListPtr
        List[NewNodePtr].Data <- Newitem
        FreeListPtr <- List[FreeListPtr].Pointer
        // find insertion point
        ThisNodePtr <- StartPointer // start at beginning of list
        WHILE ThisNodePtr <> NullPointer AND List[ThisNodePtr].Data < Newitem 
            // while not end of list
            PreviousNodePtr <- ThisNodePtr
            // remember this node 
            // follow the pointer to the next node
            ThisNodePtr <- List[ThisNodePtr].Pointer 
        ENDWHILE
        IF PreviousNodePtr = StartPointer THEN
            // insert new node at start of list
            List[NewNodePtr].Pointer <- StartPointer
            StartPointer <- NewNodePtr
        ELSE // insert new node between previous node and this node
            List[NewNodePtr].Pointer <- List[PreviousNodePtr].Pointer
            List[PreviousNodePtr].Pointer <- NewNodePtr
        ENDIF
    ENDIF
ENDPROCEDURE
```

### Find an element in an ordered linked list:

```pseudocode
FUNCTION FindNode() RETURNS INTEGER
    CurrentNodePtr <- StartPointer // start at beginning of list
    WHILE CurrentNodePtr <> NullPointer // not end of list
    AND List[CurrentNodePtr].Data <> Dataitem // item not found 
    // follow the pointer to the next node
        CurrentNodePtr <- List[CurrentNodePtr].Pointer
    ENDWHILE
    RETURN CurrentNodePtr // returns NullPointer if item not found 
ENDFUNCTION
```

### Delete a node from an ordered linked list:

````pseudocode
PROCEDURE DeleteNode (DataItem: STRING)
    ThisNodePtr <- StartPointer // start at beginning of list 
    WHILE ThisNodePtr <> NullPointer // while not end of list
    AND List[ThisNodePtr].Data <> Dataitem // and item not found 
        PreviousNodePtr <- ThisNodePtr // remember this node
        // follow the pointer to the next node 
        ThisNodePtr <- List[ThisNodePtr].Pointer
    ENDWHILE
    IF ThisNodePtr <> NullPointer THEN // node exists in list
        IF ThisNodePtr = StartPointer THEN // first node to be deleted
        	StartPointer <- List[StartPointer].Pointer 
        ELSE
        	List[PreviousNodePtr] <- List[ThisNodePtr].Pointer 
        ENDIF
    List[ThisNodePtr].Pointer <- FreeListPtr
    FreeListPtr <- ThisNodePtr 
    ENDIF
ENDPROCEDURE
````

### Output all nodes stored in the linked list

```pseudocode
PROCEDURE OutputAllNodes
	CurrentNodePtr <- StartPointer // start at beginning of list 
	WHILE CurrentNodePtr <> NullPointer // while not end of list
		OUTPUT List[CurrentNodePtr].Data
		// follow the pointer to the next node 
		CurrentNodePtr <- List[CurrentNodePtr].Pointer
	ENDWHILE 
ENDPROCEDURE
```



## Binary (search) Tree

A binary tree:

- have at most 2 children for each parent
- Exist a unique route from one node to another



Right node > Parent node > Left node

The first node is called **root**.

A node is called **leaf** if it has no children.

**Height** is the number of layers of the tree.

A tree is **balanced** if its layers = $\log_2n$, where $n$ is the number of nodes of the tree.

When a tree is not balanced, its time complexity is no longer logarithmic.



|      | Sorted Array | Ordered Linked List | Binary Tree |
| ---- | ------------ | ------------------- | ----------- |
| Add  | O(n)         | O(n)                | O(log n)    |
| Find | O(log n)     | O(n)                | O(log n)    |

*Deleting a node from a binary tree is not required in A Level Computer Science syllabus.*



### Pseudocode:

```pseudocode
TYPE Node
	LeftPointer : INTEGER
	RightPointer : INTEGER
	Data : STRING
ENDTYPE

DECLARE Tree : ARRAY[0 : 9] OF Node
DECLARE FreePointer : INTEGER
DECLARE RootPointer : INTEGER

PROCEDURE CreateTree()
	DECLARE Index : INTEGER
	RootPointer ← -1
	FreePointer ← 0
	FOR Index ← 0 TO 9 // link nodes
		Tree[Index].LeftPointer ← Index + 1
		Tree[Index].RightPointer ← -1 
	ENDFOR
	Tree[9].LeftPointer ← -1 
ENDPROCEDURE

PROCEDURE AddToTree(ByValue NewDataItem : STRING)
	// if no free node report an error
	IF FreePointer = -1
		THEN
   			ERROR("No free space left")
	ELSE // add new data item to first node in the free list 
		NewNodePointer ← FreePointer 
		Tree[NewNodePointer].Data ← NewDataItem 
		// adjust free pointer
		FreePointer ← Tree[FreePointer].LeftPointer 
		// clear left pointer
		Tree[NewNodePointer].LeftPointer ← -1
		// is tree currently empty ?
		IF RootPointer = -1
			THEN // make new node the root node
				RootPointer ← NewNodePointer
		ELSE // find position where new node is to be added
			Index ← RootPointer
			CALL FindInsertionPoint(NewDataItem, Index, Direction)
			IF Direction = "Left"
   				THEN   // add new node on left
					Tree[Index].LeftPointer ← NewNodePointer 
				ELSE // add new node on right
					Tree[Index].RightPointer ← NewNodePointer 
			ENDIF
		ENDIF
	ENDIF
ENDPROCEDURE

PROCEDURE TraverseTree(Pointer: INTEGER)
// 前序遍历
	IF Pointer <> NULL
   		THEN
   			TraverseTree(Tree[Pointer].LeftPointer)
   			OUTPUT Tree[Pointer]
   			TraverseTree(Tree[Pointer].RightPointer)
	ENDIF
ENDPROCEDURE

```

## Hash Table

The main idea behind hashing is the calculation of memory address to store an item using its value.

When two different data have the same memory address, **collision** happens. Collision needs to be reduced  as much as possible. But collisions cannot be completely prevented.

#### Three ways to handle collisions:

- chaining: create a linked list for collisions with start pointer at the hashed address 
- using overflow areas: all collisions are stored in a separate overflow area, known as 'closed hashing' 
- using neighbouring slots: perform a linear search from the hashed address to find an empty slot, known as 'open hashing'. 

### Inserting a record into a hash table

```pseudocode
PROCEDURE Insert (NewRecord: Record)
    Index <- Hash(NewRecord.Key) 
    WHILE HashTable[Index] NOT empty
        Index <- Index + 1 // go to next slot
        IF Index > Max THEN // beyond table boundary? 
        // wrap around to beginning of table 
        	Index <- 1
        ENDIF 
    ENDWHILE
    HashTable[Index] <- NewRecord 
ENDPROCEDURE
```

### Find a record in a hash table

```pseudocode
FUNCTION FindRecord(SearchKey: STRING) RETURNS Record
	Index <- Hash (SearchKey)
    WHILE (HashTable[Index].Key <> SearchKey) AND (HashTable[Index] NOT empty)
        Index <- Index + 1 // go to next slot
        IF Index > Max THEN // beyond table boundary?
        	// wrap around to beginning of table 
        	Index <- 0
        ENDIF 
    ENDWHILE
    IF HashTable[Index) NOT empty THEN // if record found
    	RETURN HashTable[Index] // return the record 
    ENDIF
ENDFUNCTION
```

## Dictionary

Dictionary is a collection of key-value pairs.

In pseudocode, a dictionary can be implemented as an array of records, where each record consists of a key and a value.

```pseudocode
TYPE Entry
	DECLARE Key: STRING
	DECLARE Value: STRING
ENDTYPE
DECLARE Dictionary: ARRAY[0:999] OF Entry
```

```pseudocode
// Initialisation
FOR index <- 0 TO 999:
	Dictionary[index].Key = ""
	Dictionary[index].Value = ""
ENDFOR

// Adding a new key-value pair
PROCEDURE AddNewPair(NewKey: STRING, NewValue: STRING)
    index <- 0 
    IF Dictionary[999].Key <> "" THEN
    	OUTPUT "The dictionary is full!"
        index <- 1000
    ENDIF
    WHILE index <= 999
        IF Dictionary[index].Key = "" AND Dictionary[index].Value = "" THEN
            Dictionary[index].Key <- NewKey
            Dictionary[index].Value <- NewValue
            index <- 1000
        ENDIF
        index <- index + 1
    ENDWHILE
ENDPROCEDURE

FUNCTION FindValue(ThisKey: STRING) RETURNS STRING
	index <- 0
	WHILE index <= 999
		IF Dictionary[index].Key = ThisKey THEN
			RETURN Dictionary[index].Value
		ENDIF
		index <- index + 1
	ENDWHILE
	RETURN "Not Found!"
ENDFUNCTION
```



In python, there is a built-in type dictionary, so we can use it directly.

```python
EnglishFrench = {}
EnglishFrench["book"] = "livre"  adding a key-value pair into the dictionary

print(EnglishFrench["book"])  accessing a key-value pair in the dictionary

 alternative method of setting up a dictionary
ComputingTerms = {"Boolean" : "can be TRUE or FALSE", "Bit" "0 or 1"}
```



# 4.1.4 Recursion

A **recursive** procedure means that the procedure is defined in terms of itself.

The procedure must contain a **base case** and a **general case**.

**Base case**: An explicit solution of the recursive function

**General case**: a definition of a recursive function in terms of itself

The general case should be able to be reduced to the base case for the procedure to end.

In a programming language, a recursive function/procedure contains a call of itself inside its definition.



### Benefits

- Recursive solution is usually the easiest to write
- More elegant and use less code than iterative solution

### Drawbacks

- Repeated recursive calls can carry large overheads in terms of memory usage and processor time. 
- For example, the procedure call countDownFrom(100) will require 100 stack frames before it completes.

### Implementation

Recursive subroutines can only be executed if the compiler produces object code that uses a **stack** to push return addresses and local variables when calling a subroutine repeatedly.

- Before procedure call is executed current state of the registers / local variables is saved onto the stack
- When returning from a procedure call the registers/local variables are re-instated



 4.2 Algorithm Design Methods

# 4.2.1 Decision Tables

A **decision table** is a precise way of modeling logic. 

Each possible combination of conditions is considered in turn and what action is required.

A decision table consists of four quadrants:

| Condition | Condition Alternatives |
| --------- | ---------------------- |
| Actions   | Action entries         |

An example of a decision table:

| Conditions | >= 90 marks | Y    | Y    | N    | N    |
| ---------- | ----------- | ---- | ---- | ---- | ---- |
|            | < 20 marks  | Y    | N    | Y    | N    |
| Actions    | Distinction |      | X    |      |      |
|            | Pass        |      |      |      | X    |
|            | Fail        |      |      | X    |      |

Y = yes, N = no, X means that the action is to be performed.

Note that a mark cannot be >=90 and <20 at the same time. Therefore that column is unnecessary.

## Simplifying a Decision Table

A decision tables can be simplified if an action is independent of whether a condition is fulfiled.

For Example:

| Conditions | Order Value over $50 | Y    | Y    | Y    | Y    | N    | N    | N    | N    |
| ---------- | -------------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|            | Small Package        | Y    | Y    | N    | N    | Y    | Y    | N    | N    |
|            | Promotion Code       | Y    | N    | Y    | N    | Y    | N    | Y    | N    |
| Action     | Free delivery        | X    |      |      |      |      |      |      |      |
|            | $1 charge            |      | X    | X    |      |      |      |      |      |
|            | $5 charge            |      |      |      | X    | X    | X    | X    | X    |

Note that if order value is not over $50, the action is always ​charging 5 dollars. Therefore the last 4 columns can be combined into one:

| Conditions | Order Value over $50 | Y    | Y    | Y    | Y    | N    |
| ---------- | -------------------- | ---- | ---- | ---- | ---- | ---- |
|            | Small Package        | Y    | Y    | N    | N    | -    |
|            | Promotion Code       | Y    | N    | Y    | N    | -    |
| Action     | Free delivery        | X    |      |      |      |      |
|            | $1 charge            |      | X    | X    |      |      |
|            | $5 charge            |      |      |      | X    | X    |

# 4.2.2 Jackson Structure Programming (JSP)

JSP is used to present the data and program structure of a program. 

It uses tree structure, with the root - main program at the top, with each node representing an action or a data item.

There are elementary components, which have no part, and composite components

### Three types of composite components:

 - Selection, represented as an circle (o) on the upper-right corner. Only one of them is selected.
 - Iteration, represented as a asterisk (*)  on the upper-right corner. It has two or more parts.
 - A sequence has two or more components (shown as having two or more children).

### Example:

An order form and its corresponding JSP structure and data diagrams:

![Order Form](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.2/Order Form.png)

JSP Structure Diagram:

![JSP Data](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.2/JSP Data.png)

JSP Data Diagram:

![JSP Structure](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.2/JSP Structure.png)

# 4.2.3 State-Transition Diagrams

A computer can be seen as a **finite state machine**(FSM), which information can be presented in a **state-transition table**.

**Finite state machine:** a machine that consists of a fixed set of possible states with a set of
inputs that change the state and a set of possible outputs

**State-transition table:** a table that gives information about the states of an FSM

An example of a state-transition table:

|       |      | Current State |      |
| ----- | ---- | ------------- | ---- |
|       |      | S1            | S2   |
| Input | a    | S1            | S1   |
|       | b    | S2            | S2   |

A **State-transition diagram** can be used to describe the behaviour of a FSM.

If an FSM has a **final state** (halting state), it is shown by a double-circled state.

![std](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.2/std.png)

If an input causes an output, it is shown by an vertical bar separating from its corresponding input.

For example, if when input is **a** and state is **s1**, output is **e**, then it is shown by **a|e**.

Always remember to draw a **start** to indicate the starting state! (shown in the image)

# 4.3 Further Programming

## 4.3.1 Programming Paradigms

**Programming paradigms** are a way to classify programming languages based on their features. 

### Low Level Programming

The features of low-level programming languages give us the ability to **manipulate the contents of memory addresses and registers directly** and exploit the architecture of a given processor.

Different types of processors use different programming languages because they support different instruction sets.

### Imperative (Procedural) Programming

**Procedural Programming** is based upon the concept of **procedure calls**, in which statements are structured into procedures (functions, subroutines).

### Declarative Programming

**Declarative programming** is a programming paradigm that expresses the logic of a computation without describing its control flow.

### Object-Oriented Programming (OOP)

**Object-oriented programming (OOP)** is a programming paradigm based on the concept of "objects", which can contain data, in the form of **fields** (attributes), and code, in the form of **procedures** (methods).

**Encapsulation:** combining data and subroutines into a class

**Class:** A **template** for creating objects that shares a common behaviour and common structure.

In CIE Exams, all attributes need to be **private**, therefore they all need a pair of **set** and **get** methods. All methods are public.

**Attributes:** the data items of a class

**Methods:** the subroutines of a class

**Object:** an instance of a class

#### Advantages of OOP over procedural languages 

- The attributes can only be manipulated using methods provided by the class definition, so the attributes are protected from accidental changes.
- Classes provided in module libraries are thoroughly tested, so less likely to introduce bugs.

Each class needs a **constructor:** a special type of method that is called to create a new object and initialise its attributes.

<Attribute 1>

<Attribute 2>

A constructor in python looks like this:

```python
def __init__():
	pass
```

The attributes and methods of a class can be demonstrated in a class diagram:

| <Class Name>  |
| ------------- |
| <Attribute 1> |
| <Attribute 2> |
| ……            |
| Constructor() |
| <Method 1>    |
| <Method 2>    |
| …...          |

The data types of attributes and the parameter taken by the methods are not required.

Class definition in python:

```python
class Shape:

    def __init__(self, color = "green", filled = True):  initialsing the attributes
        self.__color = color
        self.__filled = filled

    def GetColor(self):
        return self.__color

    def SetColor(self, color):
        self.__color = color

    def GetFilled(self):
        return self.__filled

    def SetFilled(self, filled):
        self.__filled = filled

    def ToString(self):
        if self.__filled:
            return "A shape with color of" + self.__color + "and filled"
        else:
            return "A shape with color of" + self.__color + "and not filled"

class Circle(Shape):  inheritance

    def __init__(self, color, filled, radius = 1.0):
        Shape.__init__(self, color, filled)
        self.__radius = radius

    def GetRadius(self):
        return self.__radius

    def SetRadius(self, radius):
        self.__radius = radius

    def CalcArea(self):
        return 3.14 * self.__radius * self.__radius

    def CalcPerimeter(self):
        return 2 * 3.14 * self.__radius

    def ToString(self):
        return "A circle with radius =" + str(self.__radius) + ", which is a subclass of" + Shape.ToString(self)

class Rectangle(Shape):  inheritance

    def __init__(self, color, filled, length, width):
        Shape.__init__(self, color, filled)
        self.__length = length
        self.__width = width

    def GetLength(self):
        return self.__length

    def SetLength(self, length):
        self.__length = length

    def GetWidth(self):
        return self.__width

    def SetWidth(self, width):
        self.__width = width

    def CalcArea(self): 
		 polymorphism, this function have the same name but is different from the one in the class Circle.
        return self.__width * self.__length

    def CalcPerimeter(self):
        return 2 * (self.__length + self.__width)

    def ToString(self):
        return "A rectangle with width =" + str(self.__width) + "and length =" + str(self.__length) + ", which is a subclass of" + Shape.ToString(self)

```

### Inheritance

**Inheritance:** all attributes and methods of the base class are copied to the subclass

The inheritance relationship between classes can be represented in a inheritance diagram.

![Inheritance Diagram](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.3/Inheritance Diagram.png)

In this diagram, **Book** and **CD** are both subclasses of the class **LibraryItem**.

**Abstract class:** a base class that is never used to create objects directly.

In this case, the class **LibraryItem** is an abstract class.

In the previous example, the class **Shape** is an abstract class.

### Polymorphism

**Polymorphism:** the method behaves differently for different classes in the hierarchy

In the previous example, the `CalculateArea()` method behaves differently because the way to calculate the area of a circle and a rectangle are different.

### Containment

**Containment:** a relationship in which one class has a component that is of another class type

![Containment Class Diagram](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.3/Containment Class Diagram.png)

```python
class Course:
    def __init__ (self, t, m):  sets up a new course 
        self.CourseTitle = t
        self.MaxStudents = m
        self.__NumberOfLessons = 0
        self.__CourseLesson = []
        self.__CourseAssessment = Assessment
	def AddLesson(self, t, d, r):
        self.NumberOfLessons = self.NumberOfLessons + 1
        self.CourseLesson.append(Lesson(t, d, r)) 
         Containment: the component __CourseLesson contains an object of the class Lesson.
```

## 4.3.2 File Processing

This is a definition of a record data type:

```pseudocode
TYPE CarRecord
    DECLARE VehicleID: STRING
    DECLARE Registration: STRING
    DECLARE DateOfRegistration: DATE
    DECLARE EngineSize: INTEGER
    DECLARE PurchasePrice: CURRENCY
ENDTYPE
```

In python, there is no built-in record structure. However, we can implement it using class.

```python
class CarRecord():
	def __init__(self):
        self.VehicleID = ""
        self.Registration = ""
        self.DateOfRegistration = None
        self.EngineSize = 0
        self.PurchasePrice = 0.0
```

### File Processing

#### File Processing in Pseudocode

```pseudocode
OPENFILE <filename> FOR RANDOM // Opening a random file
PUTRECORD <filename>, <identifier> // Writing in a random file
GETRECORD <filename>, <identifier> // Reading a random file
SEEK <filename>, <address> // Move the pointer to an address
EOF(<filename>) // Test for end of file

// Saving contents of array
OPENFILE "CarFile" FOR WRITE 
FOR i <- 1 TO MaxRecords
	PUTRECORD "CarFile", Car[i] 
ENDFOR
CLOSEFILE "CarFile"

// Restoring contents of array
OPENFILE "CarFile" FOR READ 
FOR i <- 1 TO MaxRecords
	GETRECORD "CarFile", Car[i] 
ENDFOR
CLOSEFILE "CarFile"

// Saving a record
OPENFILE "CarFile " FOR RANDOM 
Address <- Hash(ThisCar.VehicleID) 
SEEK "CarFile", Address
PUTRECORD "CarFile", ThisCar 
CLOSEFILE "CarFile"

// Retrieving a record
OPENFILE "CarFile" FOR RANDOM 
Address <- Hash(ThisCar.VehicleID) 
SEEK "CarFile", Address
GETRECORD "CarFile", ThisCar 
CLOSEFILE "CarFile"
```

#### File Processing in Python

```python
import pickle  this library is required for python binary file processing

MyFile = open(filename, option)  options: rb = binary read, wb = binary write, rb+ = binary read and write

pickle.dump(obj, MyFile)  obj is the data that needs to be written into the file.

pickle.load(MyFile)  reading from file

MyFile.seek(n)  Go to the nth byte of the file

MyFile.close()  closing file
```

```python
 Sequential File Processing
import pickle  this library is required to create binary files
ThisCar = CarRecord()
Car = [ThisCar for i in range(100)]

CarFile = open('Cars.DAT', 'wb')  open file for binary write 

for i in range(100):  loop for each array element
    pickle.dump(Car[i], CarFile)  write a whole record to the binary file 
    
CarFile.close()  close file

CarFile = open('Cars.DAT','rb')  open file for binary read

Car = []  start with empty list 
while True:  check for end of file
	Car.append(pickle.load(CarFile))
    
CarFile.close()
```

```python
 Random File Processing
import pickle  this library is required to create binary files 
ThisCar = CarRecord()

CarFile = open('Cars.DAT','rb+')  open file for binary read and write
Address = hash(ThisCar.VehicleID) 
CarFile.seek(Address)
pickle.dump(ThisCar, CarFile)  write record to the binary file

CarFile.close()  close file

CarFile = open('Cars.DAT','rb')  open file for binary read
Address = hash(VehicleID) 
CarFile.seek(Address)
ThisCar = pickle.load(CarFile)  load record from file 

CarFile.close()
```



## 4.3.3 Exception Handling

Runtime errors are called exceptions. 

They occur for many reasons, such as division by zero, array index out of bound, file not exist, etc.

Exception is better handled than just let the program crash.

Pseudocode:

```
TRY
	<statementsA>
EXCEPT
	<statementsB>
ENDTRY
```

Any run-time error that occurs during the execution of `<statementsA>` is caught and handled by executing  `<statementsB>`.

Python:

```python
try:
	x = int(x)
    print(x)
except NameError:
	print("variable x is not defined")
except TypeError:  multiple except blocks can be used, each handling a different exception
    print("variable x is not an integer")
else:  execute if no error is raised
    print("Nothing went wrong")
finally:  execute regardless of error or not
    pass
```



## 4.3.4 Use of development tools/programming environments

An **Integrated Development Environment (IDE)** is a software program that features for program editing, translation from high level to low level language, and testing of program code.

### Features of IDE:

- Syntax checking (on entry
- Structure blocks (e.g. IF structure and loops begin/end highlighted) 
- General prettyprint features
- Automatic indentation
- Highlights any undeclared variables
- Highlights any unassigned variables
- Commenting out/in of blocks of code
- Visual collapsing / highlighting of blocks of code
- Single stepping
- Breakpoints
- Variable/expressions report window

### Interpreter vs Compiler:

#### Interpreter:

- Easier de-bugging 
- The interpreter stops when error encountered 
- error can be corrected in real time 
- The interpreter translates a statement then executes it immediately 
- Parts of the program can be tested, without all the program code being available. 

#### Compiler:

- Once translated the compiler software is not needed to run the program 
- Compiled code should execute faster 
- Compiler produces an executable file 
- The executable file produced by a compiler can be distributed without users having sight of the source code // source code is kept secure // users are unable to make changes to the program 
- Cross-compilation is possible 

### Features of Debuggers:

- **Breakpoint**: set a breakpoint in the program code, and executing will pause at this point.
- **Stepping**: 
  - Stepping allows one statement to be executed at a time, the program execution pauses after each statement 
  - Often used from a set breakpoint
  - Can use variable watch at each step
  - Stepping over to skip statements
- **Variable watch:**
  - Variable watch allows tester to see the current contents of a variable
    // Used to see how variable contents change when stepping through program 
  - Tester chooses variables to watch (because there may be too many variables)

# 4.4 Software Development

## 4.4.1 Software development resources

**Program generator:** a computer program that can be used to create other computer programs

**Program library:** a collection of pre-compiled routines or modules that a program can use



## 4.4.2 Testing

### Why errors occur:

- The programmer has made a coding mistake. 
- The requirement specification was not drawn up correctly. 
- The software designer has made a design error. 
- The user interface is poorly designed and the user makes mistakes. 
- Computer hardware experiences failure. 

### Testing Methods:

**Integration testing:** individually tested modules are joined into one program and tested to ensure the modules interact correctly 

**Alpha testing:** testing of software in-house by dedicated testers

**Acceptance testing:** testing of software by customers before sign-off

**Beta testing:** testing of software by a limited number of chosen users before general release



### Test Plans and Test Data

#### Outline Test Plan

- flow of control: does the user get appropriate choices and does the chosen option go to the correct module? 
- validation of input: has all data been entered into the system correctly?  
- do loops and decisions perform correctly? 
- is data saved into the correct files? 
- does the system produce the correct results?

#### Test Data

There are three types of test data:

**Normal (valid)** data, **abnormal (erroneous)** data, and **boundary(extreme)** data.

The boundary data needs to include both data just inside the boundary and data just outside the boundary.



## 4.4.3 Project Management

Development of a large program requires a team. A team usually include:

- Program designers
- Software testers
- Document writers

If new hardware is involved, there will also be:

- Engineers
- Installers



### Program Evaluation and Review Technique (PERT) Chart

**Deliverable:** the result of an activity, such as a document or a report

**Milestone:** a scheduled event signifying the completion or submission of a deliverable

![Breakdown of Project](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.4/Breakdown of Project.jpeg)

![PERT Chart](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.4/PERT Chart.png)

The second image is an example of a PERT chart, which visualises the first image.

**Milestones** are shown as numbered nodes.

**Arrows** indicate dependence: when A -> B, A must be completed in order to start B.

**Dashed Arrows** indicate **dummy activity**: ctivities that must be completed in sequence but don't require resources or completion time.



**Critical path:** the longest possible continuous pathway from Start to Finish 

In this case, the critical path is 1->2->3->5->6->7->8->10->11.



### Gantt Chart

A Gantt chart is a horizontal bar chart developed by Henry Gantt. 

It is a graphical representation of a project schedule and helps to plan specific activities in a project. 

![Gantt Chart](/Users/peter/Library/Mobile Documents/com~apple~CloudDocs/学习/Notes/CS/Images/P4/4.4/Gantt Chart.png)

- The horizontal axis represents **time**. 
- Individual activities are shown as **horizontal bars**, one activity per row.
- Activities can overlap. In this case, module testing can start before all program code are written.
- Some activities can only start when other is finished. In this case, integration testing can only start when all modules are tested. This shows **dependence** and may be shown with an downward arrow connecting the end of the first activity and the beginning of the second.

# Special Notes

`file.read` reads and returns the whole file as a single string.

`file.readline` reads and returns the current line. 

`file.readlines` reads the whole file and returns an array of strings, each string contains the content of a line.



```
FUNCTION Divisor(x, y)
	IF y = 0
		THEN
			RETURN x
		ELSE
			x <- x MOD y
			RETURN Divisor(y, x)
	ENDIF
ENDFUNCTION
```

The purpose of line 1 is <u>terminating</u> the function, not just base case.



Initialising an array in **python** with 100 empty strings:

```python
MyList = ["" for i in range(100)]

```



By value:
 – a local copy of the data is used
 – leaving the variable in the main program unaffected 

By reference:
 – the address of the memory location of the data to be used is passed
 – so value changes in procedure are also reflected in main program

The constructor of subclass should call the constructor of base class in its definition.

For example:

```python
class Shape:

    def __init__(self, color = "green", filled = True):
        self.__color = color
        self.__filled = filled
        
class Circle(Shape):

    def __init__(self, color, filled, radius = 1.0):
        Shape.__init__(self, color, filled)
        self.__radius = radius
```

