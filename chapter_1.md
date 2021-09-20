# Understanding the Java Class Structure.

Classes are building blocks. Using classes requires you to create an <span style="color: #1eced4">_object_</span> in most cases.

An object is a runtime <span style="color: #1eced4">instance</span> of a class in memory. All the various objects of all the different classes represent the <span style="color: #1eced4">state</span> of your program.

## Fields and Methods

Fava classes have two primary elements:

- <span style="color: #1eced4">Methods</span>
- <span style="color: #1eced4">Fields</span>

Together they are called the <span style="color: #1eced4">members</span> of the class.

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

Java calls a word with special meaning a _keyword_. The <span style="color: #1eced4">public</span> keyword in the example means the class can be used elsewhere. The <span style="color: #1eced4">class</span> simply means you are defining a class. <span style="color: #1eced4">Animal</span> is the name given to the class.

The <span style="color: #1eced4">name</span> variable is an example of a class field. It holds the state of the name of the animal in this case.

The function <span style="color: #1eced4">getName()</span> represents a method of the class. In this case, the method is publically accessable from elsewhere. The <span style="color: #1eced4">String</span> is the return type, meaning it will return a string to the method using this method. The function <span style="color: #1eced4">setName()</span> is not returning anything, hence the <span style="color: #1eced4">void</span> keyword. It also uses a <span style="color: #1eced4">_parameter_</span>, which needs to be supplied by the calling method. As specified, this parameter needs to be a type string.

The full declaration of a method is called a <span style="color: #1eced4">_method signature_</span>.

## Comments

Commonly used in code is the _comment_. Commands are not executable code, which means they can be placed anywhere. There are three types of comments.

- <span style="color: #1eced4">single line comment</span>:

```
// comment until end of the line
```

- <span style="color: #1eced4">Multiple line comment</span>:

```
/* Multiple line
 * comment
 */
```

Often we use an asterisk (\*) at the beginning of the lines in between, but we don't have to.

- <span style="color: #1eced4">Javadoc comment</span>:

```
/**
 * Javadoc multiple line comment
 * @author Jeanne and Scott
 */
```

Similar to multiline, but this one starts with `/**`. This special syntax tells the Javadoc tool to pay attention to this comment.

## Classes vs Files.

Most classes are defined in their own <span style="color: #1eced4">\*_.java file_</span>. It is usually public, so all the code can call it.

**Attention:**
Java does not require that the class be public. This would be just fine!

```
class Animal {
    private String name;
}
```

It is even possible to put two classes in the same file. If you do so, only <span style="color: #1eced4">ONE</span> of the classes is <span style="color: #1eced4">ALLOWED</span> to be public!

If you have a public class, this class name <span style="color: #1eced4">MUST</span> match with the file name.

## Writing a _main()_ Method

A Java program begins execution with its main() _method_. A <span style="color: #1eced4">main() _method_</span> is the gateway between the startup of a Java process and the beginning of the programmers code. It is managed by the <span style="color: #1eced4">Java Virtual Machine</span>, abbreviated as <span style="color: #1eced4">JVM</span>. The JVM uses the computer system to allocate memory and CPU, accesses files etc.

The main() method hooks our code into that process and runs through the code and shuts down once the code was run. The most basic example:

```
public class Zoo {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

This code does absolutely nothing, but it does give us a starting point for our code.

The only reason we need a class structure, and thus a main() method, is because the Java language requires it. To compile Java code, the file must have the extension _.java_. The name of the file must match the name of the class. The result is a file of <span style="color: #1eced4">bytecode</span> by the same name, but with a <span style="color: #1eced4">.class</span> filename extension. Bycode consists of instructions that t he JVM knows how to execute.

Let us go through the words in the main() method's signature.

- public

The keyword public is what's called an <span style="color: #1eced4">_access modifier_</span>. It declares this method's level of exposure to potential callers in the program. More about the access modifier in Chapter 4 (@TODO: add link).

- static

They keyword <span style="color: #1eced4">_static_</span> binds a method to its class so it can <span style="color: #1eced4">ONLY</span> be called by the class name.

**Attention**:

If a main() method isn't present in the class we name with the .java executable (in other words, the 'main' file which starts our program), the process will throw an error and terminate. It will also throw an error if the main function is <span style="color: #1eced4">NOT</span> static.

- void

The keyword _void_ represents the <span style="color: #1eced4">return type</span>. A method that returns no data (void), returns control to the caller silently. Other return types will actually return some form of data to the caller.

- main(String[] args)

The parameter list of the main method is represented as an array _java.lang.String_ Objects. In practice, you can write: either of these:

`String[] args`

`String args[]`

`String... args`

The variables _args_ hint that this list contains values that were read in (arguments) when the JVM started. The name _args_ can be replaced by anything.

# Understanding Package Declarations and Imports

Java has thousands of built-in classes, organized in <span style="color: #1eced4">_packages_</span>, which are logocal groupings for classes. If you want to use a certain class, you firstly import the package, rather than the specific class (at first). Then, once the package was defined, you can point to the specific class.

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

This allows the developer to use all the Classes inside the `java.util` package. Not that this <span style="color: #1eced4">ONLY</span> imports **classes**! It will <span style="color: #1eced4">NOT</span> import child packages, fields or methods. However, there is the so called "**static import**", which also imports other types. More on that in chapter 4.

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

We use packages because then we can <span style="color: #1eced4">reuse</span> class names, without them interfering with each other.

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
