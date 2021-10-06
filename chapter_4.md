# Designing Methods`

```
public final void nap(int minutes) throws InterruptedException {
    somerandomstuffhere
}
```

This is called a method declaration, which specifi es all the information needed to call
the method. Breaking it down:

- `public`: **access modifier**. Not required.
- `final`: **Optional specifier**. Not required.
- `void`: **Return type**. Required.
- `nap`: **Method name**. Required.
- `int minutes`: **parameters**. Required, but can be empty.
- `throws`: **Optional exception list**. Not required.
- `somerandomstuffhere`: **method body**. Required, but can be empty.

Let us deep dive into these!

## Access Modifiers.

Java has four access modifiers.

1. public -> this method can be called from any class.
2. private -> this method can be called from within the same class.
3. protected -> this method can be called from classes in the same package or from subclasses (more on subclasses in chapter 5).
4. Default (Package Private) Access -> this method can only be called by classes within the same package. You `never` write this out. This is active by simply omiting the access modifier.

Access modifier must be specified `before` the return type. Otherwise it won't compile.

## Optional Specifiers

There are a number of optional specifi ers, but most of them aren’t on the exam. Optional
specifi ers come from the following list. Unlike with access modifi ers, you can have multiple
specifi ers in the same method (although not all combinations are legal). When this happens,
you can specify them in any order.

- `static`: Covered later in this chapter. Used for class methods.
- `abstract`: Covered in Chapter 5. Used when not providing a method body.
- `final`: Covered in Chapter 5. Used when a method is not allowed to be overridden by a subclass.
- `synchronized`: On the OCP but not the OCA exam.
- `native`: Not on the OCA or OCP exam. Used when interacting with code written in another language such as C++.
- `strictfp`: Not on the OCA or OCP exam. Used for making fl oating-point calculations portable.

Optional Specifiers must be specified `after` the access modifier and `before` the return type.

## Return Type

The return type might be an
actual Java type such as String or int. If there is no return type, the void keyword is used.

When checking return types, you also have to look inside the method body. Methods
with a return type other than void are required to have a return statement inside the
method body. This return statement must include the primitive or object to be returned.
Methods that have a return type of void are permitted to have a return statement with no
value returned or omit the return statement entirely.

## Method Name

Method names follow the same rules as we practiced with variable names in Chapter 1,
“Java Building Blocks.” To review, an identifi er may only contain letters, numbers, $, or \_.
Also, the fi rst character is not allowed to be a number, and reserved words are not allowed.
By convention, methods begin with a lowercase letter but are not required to.

## Parameter List

Although the parameter list is required, it doesn’t have to contain any parameters. If you do have multiple parameters, you separate them with a comma.

## Optional Exception List

In Java, code can indicate that something went wrong by throwing an exception. You can list as many types of exceptions as you want in this clause separated by commas.

`public void twoExceptions() throws IllegalArgumentException, InterruptedException { }`

## Method Body

The final part of a method declaration is the method body (except for abstract methods and interfaces). A method body is simply a code block. It has braces that contain zero or more Java statements.

# Working with Varargs

As you saw in the previous chapter, a method may use a vararg parameter (variable argument) as if it is an array. It is a little different than an array, though. A vararg parameter
must be the last element in a method’s parameter list. This implies you are only allowed to
have one vararg parameter per method.

```
public void walk1(int... nums) { }
public void walk2(int start, int... nums) { }
public void walk3(int... nums, int start) { } // DOES NOT COMPILE
public void walk4(int... start, int... nums) { } // DOES NOT COMPILE
```

# Applying Access Modifiers

## Private Access

Private access is easy. Only code in the same class can call private methods or access private fields.

## Default (Package Private) Access

This allows classes in the `same package` to access her members. When there is no access modifier, Java uses the default, which is package private access. This means that the member is “available" to classes in the same package.

## Protected Access

Protected access allows everything that default (package private) access allows and more. The protected access modifi er adds the ability to access members of a parent class. Subclasses can use protected access modifiers.

Any attempts to access protected members when it is `NOT` done from a `subclass` or `in the same package`, it is restricted!

`IMPORTANT:`

Even when a subclass `extends` a class, it still cannot access the original class directly when it is created in the same class. Confusing! Just keep this in mind:

```
1: package pond.swan;
2: import pond.shore.Bird; // in different package than Bird
3: public class Swan extends Bird { // but subclass of bird
4: public void swim() {
5: floatInWater(); // package access to superclass
6: System.out.println(text); // package access to superclass
7: }
8: public void helpOtherSwanSwim() {
9: Swan other = new Swan();
10: other.floatInWater(); // package access to superclass
11: System.out.println(other.text);// package access to superclass
12: }
13: public void helpOtherBirdSwim() {
14: Bird other = new Bird();
15: other.floatInWater(); // DOES NOT COMPILE
16: System.out.println(other.text); // DOES NOT COMPILE
17: }
18: }
```

We are in the `Swan` class here and we are instantiating a `Bird` in the `helpOtherBirdSwim()` method. We do not have direct access to `Bird`, so we aren't able to use its members, `unless` we create a `Swan`.

This is arguably one of the most confusing points on the exam.
Looking at it a different way, the protected rules apply under two scenarios:

- A member is used without referring to a variable. This is the case on lines 5 and 6. In
  this case, we are taking advantage of inheritance and protected access is allowed.
- A member is used through a variable. This is the case on lines 10, 11, 15, and 16.
  In this case, the rules for the reference type of the variable are what matter. If it is a
  subclass, protected access is allowed. This works for references to the same class or a
  subclass.

## Public Access

Protected access was a tough concept. Luckily, the last type of access modifi er is easy: public
means anyone can access the member from anywhere.

| Can access | If that member is private? | If that member has default package private access? | if that member is protected ? | if that member is public? |

| Can access                                                    | If that member is private? | If that member has default package private access? | If that member is protected ? | if that member is public? |
| ------------------------------------------------------------- | :------------------------- | :------------------------------------------------- | :---------------------------- | :------------------------ |
| Member in the same class                                      | Yes                        | Yes                                                | Yes                           | Yes                       |
| Member in another class in same package                       | No                         | Yes                                                | Yes                           | Yes                       |
| Member in a superclass in a different package                 | No                         | No                                                 | Yes                           | Yes                       |
| Method/field in a non-superclass class in a different package | No                         | No                                                 | No                            | Yes                       |

## Designing Static Methods and Fields

Except for the main() method, we've been looking at instance methods. Static methods don't require an instance of the class. They are shared among all users of the class. You can think of statics as being a member of the single class object that exist independently of any instances of tha class.
