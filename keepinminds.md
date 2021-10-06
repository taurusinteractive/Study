```
class Game{
  public void play() throws Exception{
    System.out.println("Playing...");
  }
}

public class Soccer extends Game{
   public void play(){
      System.out.println("Playing Soccer...");
   }
   public static void main(String[] args){
       Game g = new Soccer();
       g.play();
   }
}
```

Will not compile, because `g.play()` is trying to acccess the `play()` in `class Game`, which can throw an exception. Methods that can throw an exception, must be wrapped in a try catch.

---

- A class is `uninstantiable` if the class is declared `abstract`.
- If a method has been declared as `abstract`, it cannot provide an `implementation` (i.e. it cannot have a method body ) and the `class` containing that method `must be declared abstract`).
- If a `method` is `not declared abstract`, it `must provide a method body` (the class can be abstract but not necessarily so).
- If `any method in a class is declared abstract`, then the `whole class must be declared abstract`.
- A `class can` still `be` made `abstract` even `if it has no abstract method`.

---

A method is said to be `overloaded` when the other method's `name is same and parameters` ( either the `number or` their `order`) are `different`. A different return type does not matter!

---

`append() method does not exist in String class`. It exits only in StringBuffer and StringBuilder.

---

You `need a boolean in an 'if' condition`.

---

`Casting a base class to a subclass` as in : b = (B) a; is also called as `narrowing` (as you are trying to narrow the base class object to a more specific class object) and `needs explicit cast`.

`Casting a sub class to a base class` as in: A a = b; is also called as `widening` and does `not need any casting`.

---

`& and | do not short circuit the expression`.

`&& and || do not evaluate the rest of the expression if the result of the whole expression can be known by just evaluating the left operand`

---

`All arrays are initialized to contain the default values of their type`.

This means, int[] iA = new int[10]; will contain 10 integers with a value of 0.

Object[] oA = new Object[10]; will contain 10 object references pointing to null.

boolean[] bA = new boolean[10] will contain 10 booleans of value false.

---

A `try` / `catch` block with a `finally`, can never ever be written with `finally` as NOT the last statement.

---

A `try` / `catch` can be used on methods, even if those do not throw an `Exception`. The try catch is redundant, but will compile.

---

`static method` cannot be overridden by a non-static method and `vice versa`
