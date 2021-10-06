# Creating and Manipulating Strings

A string is basically a sequence of characters.

```
String name = "Fluffy";
String name = new String("Fluffy");
```

Both give you a reference variable of type name pointing to the String object "Fluffy", which is in the *String Pool*.

## Concatenation

Placing one String before the other String and combining them together is called string
concatenation. Rules when concatenating:

1. If both operands are numeric, + means numeric addition.
2. If either operand is a String, + means concatenation.
3. The expression is evaluated left to right.

## Immutability

Once a String object is created, it is not allowed to change. It cannot be made larger or
smaller, and you cannot change one of the characters inside it. Mutable is another word for changeable. Immutable is the opposite—an object that can’t be changed once it’s created.

## The String Pool

The string pool, also known as the intern pool, is a location in the Java virtual machine (JVM) that collects all strings. The string pool contains literal values that appear in your program. For example, “name” is a literal and therefore goes into the string pool. myObject.toString() is a string but not a literal, so it does not go into the string pool. Strings not in the string pool are garbage collected just like any other object.

## Important String Methods

### - length()
Returns the length of the string.

### - charAt()
Returns the char at given index.

### - substring()
Returns the string from given index until either the end of the string or until (NOT included) the given ending index.

### - toLowerCase() and toUpperCase()
Returns the string in lower- or upercase.

### - equals() and equalsIgnoreCase()
Returns boolean whether two strings have equal content case sensitive, unless case is ignored.

### startsWith() and endsWith()
Returns whether String starts or ends with given char.

### contains()
Returns whether given value is inside the String. Case sensitive.

### replace()
Replace searches for given value and replaces it for the given new value.

### trim()
Removes the white spaces in front and at the back of a String.

# Using the StringBuilder Class
When building a string, sometimes we need to change a String at several positions rapidly. This is very inefficient. Luckily, Java has a solution. The StringBuilder class creates a String without storing all those interim String values. Unlike the String class, StringBuilder is not immutable. It can then later be set to a String, if need be.

## Mutability and Chaining

When chaining some String-methods, it keeps on returning new Strings. Chaining StringBuilder objects doesn’t work this way. Instead, the StringBuilder changes its own state and returns a reference to itself! 
```
4: StringBuilder a = new StringBuilder("abc");
5: StringBuilder b = a.append("de");
6: b = b.append("f").append("g");
7: System.out.println("a=" + a);
8: System.out.println("b=" + b);
```

There is only one StringBuilder here, so both `a` and `b` are now `abcdefg`.

## Creating a StringBuilder

There are three ways to construct a StringBuilder:
```
StringBuilder sb1 = new StringBuilder();
StringBuilder sb2 = new StringBuilder("animal");
StringBuilder sb3 = new StringBuilder(10); // Reserves a certain number of slots for characters.
```

## Important StringBuilder Methods

### - chartAt(), indexOf(), length(), substring()
These four methods work exactly the same as on the String class.

### - append()
Most used method on the StringBuilder. It simply adds to the current StringBuilder.

### - insert()
This method adds characters to the StringBuilder at the request index and returns a reference to the StringBuilder itself.

### - delete()
delete() removes characters from the sequence and returns the reference to the StringBuilder.

### - deleteCharAt()
Does what it implies. It deletes character at the given index

### - reverse()
Reverses the order of the characters in the StringBuilder and a reference to itself.

### - toString()
Converts the StringBuilder to a String.

## StringBuilder versus StringBuffer
StringBuilder and StringBuffer do literally the same thing. StringBuffer is old.

# Understanding Equality

We learned how to use the `==` to compare numbers or to check if two object references are refering to the same object.

```
String x = "Hello World";
String y = "Hello World";
System.out.println(x == y); // true
```
Remember that Strings are immutable and literals are pooled. The JVM created only one literal in memory. x and y both point to the same location in memory; therefore, the statement outputs true.

```
String x = "Hello World";
String z = " Hello World".trim();
System.out.println(x == z); // false
```

Although x and z happen to evaluate to the same string, one is computed at `runtime`. Since it isn’t the same at compile-time, a new String object is created.

```
String x = new String("Hello World");
String y = "Hello World";
System.out.println(x == y); // false
```

Since you have specifically requested a different String object, the pooled value isn’t shared.

The `LESSON:` don't use the `==`-operator on Strings, or Objects in general.

# Understanding Java Arrays
An array is an area of memory on the heap with space for a designated number of elements. An array is an ordered list, it can contain duplicates.

## Creating an Array of Primitives
`int[] numbers = new int[3];`.

This creates: `[0, 0, 0]`. An array with integers, with a default value of `0` (see chapter 1) with the length of 3.

`int[] numers2 = new int[] {42, 55, 99};`

This creates : `[42, 55, 99];`. It is commonly written as following:

`int[] numbers2 = {42. 55, 99};`.

**IMPORTANT:**
All of these are correct!!

```
int[] numAnimals;
int [] numAnimals2;
int numAnimals3[];
int numAnimals4 [];
```

`int ids[], types;`

This creates an integer array and an integer!

## Creating an Array with Reference Variables

We can call equals() on an array because an array is an object. It can return true because of reference equality. The equals() method on arrays does `not` look at the elements of the array. Remember, this would work even on an int[] too. int is a primitive; int[] is an object.

The array does not allocate space for the String
objects. Instead, it allocates space for a reference to where the objects are really stored.

## Using an Array

Accessing an element in the array is simple: 

```
int[] numbers = {1, 2, 3};
int number = numbers[2]; // will select "3"
```

Be careful with accessing indexes which are out of bounds.

## Sorting

Almost any type of array can be sorted. Use the `sort()` method.

## Searching

We can search through an array, **but only if the array is already sorted.** The exam creators will not expect you to know what incorrect values come
out. As soon as you see the array isn’t sorted, look for an answer choice about unpredictable output.

## Varargs

