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

    }
}
```

This code does absolutely nothing, but it does give us a starting point for our code.
