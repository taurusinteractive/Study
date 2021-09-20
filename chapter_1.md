# Understanding the Java Class Structure.

Classes are building blocks. Using classes requires you to create an `_object_` in most cases.

An object is a runtime `instance` of a class in memory. All the various objects of all the different classes represent the `state` of your program.

## Fields and Methods

Fava classes have two primary elements:

- `Methods`
- `Fields`

Together they are called the `members` of the class.

### Methods

Methods are often called functions or procedures in other programming languages. These add functionality to the class.

### Fields

Fields are often called variables in other programming languages. These hold the state of the program. Methods (can) use the fields to operate on.

#### Simple class example:

```
public class Animal {
    String: name;

    public String getName() {
        return name;
    }

    public void setName(String newName) {
        name = newName;
    }
}
```

Java calls a word with special meaning a _keyword_. The `public` keyword in the example means the class can be used elsewhere. The `class` simply means you are defining a class. `Animal` is the name given to the class.

The `name` variable is an example of a class field. It holds the state of the name of the animal in this case.

The function `getName()` represents a method of the class. In this case, the method is publically accessable from elsewhere. The `String` is the return type, meaning it will return a string to the method using this method. The function `setName()` is not returning anything, hence the `void` keyword. It also uses a `_parameter_`, which needs to be supplied by the calling method. As specified, this parameter needs to be a type string.

The full declaration of a method is called a `_method signature_`.

## Comments

Commonly used in code is the _comment_. Commands are not executable code, which means they can be placed anywhere. There are three types of comments.

- `single line comment`:

```
// comment until end of the line
```

- `Multiple line comment`:

```
/* Multiple line
 * comment
 */
```

Often we use an asterisk (\*) at the beginning of the lines in between, but we don't have to.

- `Javadoc comment`:

```
/**
 * Javadoc multiple line comment
 * @author Jeanne and Scott
 */
```

Similar to multiline, but this one starts with `/**`. This special syntax tells the Javadoc tool to pay attention to this comment.

## Classes vs Files.

Most classes are defined in their own `\*_.java file_`. It is usually public, so all the code can call it.

**Attention:**
Java does not require that the class be public. This would be just fine!

```
class Animal {
    private String name;
}
```

It is even possible to put two classes in the same file. If you do so, only `ONE` of the classes is `ALLOWED` to be public!

If you have a public class, this class name `MUST` match with the file name.

## Writing a _main()_ Method

A Java program begins execution with its main() _method_. A `main() _method_` is the gateway between the startup of a Java process and the beginning of the programmers code. It is managed by the `Java Virtual Machine`, abbreviated as `JVM`. The JVM uses the computer system to allocate memory and CPU, accesses files etc.

The main() method hooks our code into that process and runs through the code and shuts down once the code was run. The most basic example:

```
public class Zoo {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

This code does absolutely nothing, but it does give us a starting point for our code.

The only reason we need a class structure, and thus a main() method, is because the Java language requires it. To compile Java code, the file must have the extension _.java_. The name of the file must match the name of the class. The result is a file of `bytecode` by the same name, but with a `.class` filename extension. Bycode consists of instructions that t he JVM knows how to execute.

Let us go through the words in the main() method's signature.

- public

The keyword public is what's called an `_access modifier_`. It declares this method's level of exposure to potential callers in the program. More about the access modifier in Chapter 4 (@TODO: add link).

- static

They keyword `_static_` binds a method to its class so it can `ONLY` be called by the class name.

**Attention**:

If a main() method isn't present in the class we name with the .java executable (in other words, the 'main' file which starts our program), the process will throw an error and terminate. It will also throw an error if the main function is `NOT` static.

- void

The keyword _void_ represents the `return type`. A method that returns no data (void), returns control to the caller silently. Other return types will actually return some form of data to the caller.

- main(String[] args)

The parameter list of the main method is represented as an array _java.lang.String_ Objects. In practice, you can write: either of these:

`String[] args`

`String args[]`

`String... args`

The variables _args_ hint that this list contains values that were read in (arguments) when the JVM started. The name _args_ can be replaced by anything.

# Understanding Package Declarations and Imports

Java has thousands of built-in classes, organized in `_packages_`, which are logocal groupings for classes. If you want to use a certain class, you firstly import the package, rather than the specific class (at first). Then, once the package was defined, you can point to the specific class.

```
public class ImportExample {
    public static void main(String[] args) {
        Random r = new Random();
        System.out.println(r.nextInt(10));
    }
}
```

Without importing the class, the Java compiler will not compile, since it has no idea where `Random` is coming from. We fix this by putting this on top of the file:

`import java.util.Random`.

The compiler first looks at the word `java`, which means it came from the JDK in this case. It can start with something else, which then means it is likely coming from elsewhere.

Then, Java will look for _child packages_, in this case `util`. Be aware that these package names can be named as the developer likes, so something like `com.mypackage.this.is.valid.package.naming` is perfectly fine!

## Wildcards

Classes in the same package can be imported together, using a wildcard. The wildcard is written with an asterisk. Example:

`import java.util.*`

This allows the developer to use all the Classes inside the `java.util` package. Not that this `ONLY` imports **classes**! It will `NOT` import child packages, fields or methods. However, there is the so called "**static import**", which also imports other types. More on that in chapter 4.

Using specific imports and wildcard imports achieve exactly the same. The compiler will take care of the imports and thus using wildcards will not slow down your application.

## Redundant Imports

There is one special package we will never have to import: `java.lang`, which is _always_ imported. You can still manually import it, but you don't have to.

Another case would be importing a class which is inside the same `package` as the class importing it. Java automatically looks in the current package already for other classes.

Say we need the `Paths` class and the `Files` class from the `nio` package. We can import these two ways.

Using a wildcard:

```
import java.nio.file.*
```

Using explicit imports:

```
import java.nio.file.Files;
import java.nio.file.Paths;
```

Examples of imports that will NOT work:

`import java.nio.*;`
This does not work because `file` is a package, not a class.

`import java.nio.*.*;`
This doesn't work, because you can only use one wildcard and it MUST be at the end.

`import java.nio.file.Paths.*;`
This doesn't work, because you can only import classes, not methods inside classes.

## Naming Conflicts

We use packages because then we can `reuse` class names, without them interfering with each other.

In the wild, there are many overlapping class names. One example is the `Date` class which is located in both `java.util` and `java.sql`. But what if we need classes out both of these packages? Then a explicitly imported classes takes precedence over imports with a wildcard.

```
import java.util.Date;
import java.sql.*;
```

In this example we can make use of all the classes in `java.jql`, but the `Date` one, because we explicitly told Java we are using the one from `java.util`. If you **really** need to use both `Date` methods inside one class, then you can do this:

```
import java.util.Date;

public class Conflicts {
    Date date;
    java.sql.Data sqlDate;
}
```

You can directly point to the package / classname when initializing a variable.

## Creating a New Package

When we do not define a _package_ ourselves, it is considered to be in the **default package**. You can tell something is in the default package when there is no package name.

A package can be created by making a new directory. For example
`C:/temp/packagea;`

```
package packagea;

public class ClassA {
}
```

`C:/temp/packageb;`

```
package packageb;
import packagea.ClassA;

public class ClassB {
    public static void main(String[] args) {
        ClassA a;
    }
}
```

In the example above, we have two packages. Package b contains the `starter method` for the application called `main()`. The class imports `ClassA` from the package `packagea` and instantiates an `Object` using the ClassA class.

## Code Formatting on the Exam

On the exam we don't worry about imports, unless they are specifically printed. If they are not printer, we must assume they are correct. The same goes for when the `main()` method is missing.

# Creating Objects

Programs can only do usefull things if we create new objects. An object is an _instance_ of a class.

## Constructors

To create an instance of a class, you must write `new` before it. For example:

`Random r = new Random();`

First we declare the _type_ we will be creating, then we give it a name. Java can then store a reference to the object. Then we write `new Random()` to actually **create** the object.

`Random()` looks like a method, because of the parentheses. However, it is called a **_constructor_**. which is a special type of method. A constructor creates a new object.

Defining a constructor is done within a class like this:

```
public class Car {
    public Car() {
        // inside the constructor
    }
}
```

Two key points to note about the contructor.

- The **_name_** must match the class name.
- The constructor must NOT have a return type.

Any methods with the same name as the class, but with a return type are treated like regular methods.

The purpose of a constructor is to initialize fields, although you can put any code in the constructor.

A constructor can take in parameters, which you can use to set the fields. It is also possible to have multiple constructors, which can take more or less parameters.

If you do not define a constructor, there is one supplied by Java under the hood.

## Reading and Writing Object Fields

It can be possible to read and write instance variables directly from the caller. For example:

```
public class Vehicle {
    int numberWheels;

    public static void main(String[] args) {
        Vehicle car = new Vehicle();
        car.numberWheels = 4;

        System.out.println(car.numberWheels);
    }
}
```

Here we write the amount of wheels to four, once we created the object and place a reference as `car` to it in memory. Then we read it by accessing its property and print it.

A field can also be initalized with a value. It's really simple:

```
public class Vehicle {
    int numberWheels = 4;

    public static void main(String[] args) {
        // your code here
    }
}
```

## Instance Initializer Blocks

It is important to know what a `code block` is. A block can be recognized by the braces `{}`. Code inside these braces is executed as a whole. It is possible to define variables which are only ever instantiated during the execution of a block.

When a code block is _outside_ of a method, it is called an `instance initializer`. In chapter 5 we'll learn how to use a static initializer.

## Order of Initialization

When fields are being initialized in multiple places, it is important to remember in what order the initialization process is executed. In general, this is the order:

- Fields and instance initializer blocks are run in the order in which they appear in the file.
- The constructor runs after all fields and instance initializer blocks have run.

In this example, the `number` variable changes from `3` to `4`, to `5` in the constructor, before it is being printed in the `main() method`.

```
public class Egg {
    public Egg() {
        number = 5;
    }

    public static void main(String[] args) {
        Egg egg = new Egg();
        System.out.println(egg.number);
    }

    private int number = 3;
    {number = 4; }
}
```

# Distinguishing Between Object References and Primitives

Java applications contain two types of data: primitive types and reference types.

## Primitive Types

Java has eight built-in data types, which are the _`primitive types`_. In essence, these represent the building blocks for Java objects. All Java objects are basically a complex collection of these built-in types, even though it does not look like it on the surface. An overview:

| Keyword | Type                        | Example |
| ------- | :-------------------------- | :------ |
| boolean | true or false               | true    |
| byte    | 8-bit integral value        | 123     |
| short   | 16-bit integral value       | 123     |
| int     | 32-bit integral value       | 123     |
| long    | 64-bit integral value       | 123     |
| float   | 32-bit floating-point value | 123.45f |
| double  | 64-bit floating-point value | 123.456 |
| char    | 32-bit Unicode value        | 'a'     |

Key points:

- float and double are used for floating-point (decimal) values.
- A float requires the letter f following the number
- byte, short, int and long are used for numbers without decimal points.
- Each numeric type uses twice as many bits as the smaller similar type.

Calculating the maximum and minimum number of a type is easy. You 2 $^x$ where x is the amount of bits. Then you divide the outcome by two and retract 1 on the positive side. The division by two, is because Java also supports a negative number. A byte is 8 bits. That means 2 $^8$ = 256. Divide this by two and you'll end up with 128. So this would mean it can hold a number from -128 to 127.

When there is a number in the code, it is called a _literal_. Java assumes it is an `int`, unless stated otherwise.

An other way to specify a number is to change the `base`. Java allows you to specify digits in other formats:

- octal (digits 0-7) which uses the number 0 as a prefix. Example: 017
- hexadecimal (digits 0-9 and letters A-F), which uses the number 0 followed by x or X as a prefix. Example: 0xFF.
- binary (digits 0-1) which uses the number 0 followed by b or B as prefix. Example: 0b10.

It is possible to add underscores in a number since Java 7. This is merely to make the number more readable.
Example:

`int million1 = 1000000;`

`int million2 = 1_000_000;`

Underscores can only be added in the middle of a number. So not at the start, end or just before or after a break for decimal numbers.

## Reference Types

A _reference type_ refers to an object (which is an instance of a class). Unlike primitive types, reference types do not hold their values in memory where the variable is allocated. Instead, they "point" to an object by storing the memory address where the object is located. This is also known as a `pointer`. Java does not allow you to know where the physical address in memory is. You can only use the reference to refer to the object.

Declaring and initializing reference types is very similar to primitive types:

`java.util.Data today;`

`String greeting;`

A value can be assigned in two ways:

- A reference can be assigned to another object of the same type.
- A reference can be assigned to a `new object` using the new keyword.

In the examples above, we can use the `today` variable name as a reference. We can assign a `new Date()` as a value, or assign an existing `Data object`. We can then access its properties through `today`, but never directly in memory.

## Key Differences

- Reference types can be assigned `null`, which means they are not referring to any object. Primitive types will result in a compiling error if `null` is assigned.

- Reference types can be used to call methods when they do not point to `null`. Primitives do not have these methods declared on them.

- Primitive types have lowecase type names. Classes come with an uppercase. We should maintain this convention.

# Declaring and Initializing Variables

A _`variable`_ is a name for a piece of memory that stores data. When declaring a variable, you need to state the variable type along with giving it a name (e.g. `int number`).

We can initialize the variable when we declare it, but also after we declare it.

`int number;`

`number = 10; //give it value after we declare it.`

`int number2 = 12; // give value at the same time of declaring it`

## Declaring Multiple Variables

It's possible to declare multiple variables in one go, as long as they have the same type. For example:

`String string1, string2, string3;`

It is also possible to directly assign a value when you declare multiple variables, but you don't have to for all of them.

`String string1 = "I am Groot", string2, string3;`

In this example `string1` is declared AND has a value. `string2` and `string3` have been declared, but have not been initialized.

## Identifier

Java has precise rules about identifier names. These rules are applied to all isntances where we are free to name something. Variables, methods, classes and fields.

- The name must begin with a letter or the symbol `$` or `_`
- Subsequent characters may also be numbers
- You cannot use the same name as a Java `reserved word`.

Reserved words:

- abstract
- assert
- boolean
- break
- byte
- case
- catch
- char
- class
- const\*
- continue
- default
- do
- double
- else
- enum
- extends
- false
- final
- finally
- float
- for
- goto\*
- if
- implements
- import
- instanceof
- int
- interface
- long
- native
- new
- null
- package
- private
- protected
- public
- return
- short
- static
- strictfp
- super
- switch
- synchronized
- this
- throw
- throws
- transient
- true
- try
- void
- volatile
- while

Keywords with an `*` are not being used.

# Understanding Default Initialization of Variables

Before using a variable, it needs a value. Some types of variables get this value set automatically, while others do not.

## Local Variables

A `local variable` is a variable defined within a method. Local variables MUST be initialized before being used. They do not have a default value and contain garbage data until initialized. Trying to use an uninitialized local variable will result in a compiling error.

## Instance and Class Variables

Variables that are not local variables are known as _instance variables_ or _class variables_. Instance variables are the same as fields. Class variables share their value with all objects made of that class! Simply said:

`Animal cat = new Animal();`

`Animal dog = new Animal();`

```
public class Animal () {
    static int numberOfAnimals = 2;
}
```

Both `cat` and `dog` have a `numberOfAnimals` of two. If we change this inside `dog`, it automatically changes in `cat` as well. We can recognize `class variables` because they have the `static` keyword in their declaration.

Both instance and class variables do NOT have to be initialized. They will be given a default value if we do not assign them a value. The table below shows the default values for variable types.

| Variable type                           | Default Initialization value   |
| --------------------------------------- | :----------------------------- |
| boolean                                 | false                          |
| byte, short, int, long                  | 0 (in the type's bit-length)   |
| float, double                           | 0.0 (in the type's bit-length) |
| char                                    | '\u0000' (NUL)                 |
| All object references (everything else) | null                           |

# Understanding Variable Scope
