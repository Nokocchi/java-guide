# Java guide

An introduction to Java, assuming some familiarity with basic python. 

- [Java guide](#java-guide)
  * [Part 1: Some initial definitions](#part-1-some-initial-definitions)
    + [class](#class)
    + [function with name "main"](#function-with-name-main)
    + [public](#public)
    + [(String[] args)](#string-args)
    + [void](#void)
    + [new](#new)
    + [static](#static)
    + [constructor](#constructor)
    + [this](#this)
  * [An example of how/when to use objects vs static](#an-example-of-howwhen-to-use-objects-vs-static)
    + [❌ ERROR](#-error)
    + [✅ Options 1, marking as static:](#-options-1-marking-as-static)
    + [✅ Options 2, creating an instance of the class:](#-options-2-creating-an-instance-of-the-class)
    + [What's the difference? Which should I pick? Why even use objects?](#whats-the-difference-which-should-i-pick-why-even-use-objects)
      - [Strings](#strings)
      - [Why do we have a "String" class at all?](#why-do-we-have-a-string-class-at-all)
      - [Another example](#another-example)
    + [What is a class, and what is not a class?](#what-is-a-class-and-what-is-not-a-class)
    + [What's the difference between an object and a variable?](#whats-the-difference-between-an-object-and-a-variable)
    + [What's the difference between a type and a class?](#whats-the-difference-between-a-type-and-a-class)
    + [What's the difference between a function and a method?](#whats-the-difference-between-a-function-and-a-method)
  * [More keywords](#more-keywords)
    + [final](#final)
    + [public vs private](#public-vs-private)
  * [Standards](#standards)
    + [Mark as private if possible](#mark-as-private-if-possible)
    + [getter and setter](#getter-and-setter)

## Part 1: Some initial definitions

This is the smallest possible Java program. Yes, you need all these words. 

The only optional things in the example below are

* The third word from the beginning, **Main**
* The third line which just prints "Hello world";

Everything else must be written exactly as shown. But what do they mean?

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```

### class

A template, blueprint or wrapper for some variables and functions that belong together. 

A always has a name. In the example above, the class is called "Main". But you can call it anything you want.

You could also make a "car" class that contains some variables like 

* `fuelLevel`
* `kilometersDriven`
* `modelName`

as well as some functions like 

* `startCar()`
* `turnOnHeadlights()`
* `break()`
* `turnOffCar()`

You can have multiple classes inside of a single .java file, and you can put classes inside of classes. That's all a bit more advanced and there are rules for how to do this and what is allowed. But, as a rule of thumb, you have one class per file, and the filename and class name must be the same.

### function with name "main"

In order to start your Java program, your computer needs to know where your code begins.
It is required that your Java program has a function called "main" which is where your program must begin. You cannot pick another name.

In java, the `def` keyword is not used to define a function. 

### public

If you mark something with `public`, it can be accessed from outside of the class. 

Imagine that your computer needs permission to start your Java program, so you need to mark the main function with `public`. Otherwise the main function would not be accessible to your computer, and it wouldn't be able to start running your Java program.

### (String[] args)

This is a parameter to the main function. It's one single parameter. In java, you always write the type of the parameter first, followed by the name of the parameter.

Examples:

* `drive(int numberOfKilometers)`
* `displayErrorMessageOnDashboard(String errorMessage)`

In this case, `String[]` is the type of the parameter, and "args" is the name.

`String[]` is essentially a list of Strings. 

You cannot change the type of the parameter in the main function. It must be `String[]`. But you can rename the variable to anything you would like.

The purpose of this String list parameter is that you can provide any number of arguments to your Java program when you run it. This is especially useful when you run your program from the command line like so:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello " + args[0] + "!");
    }
}
```

```
RBL-WG92YY ~/IdeaProjects/JavaExample/src: java Main.java "there, chicken"
Hello there, chicken!
```

### void

Like in Python, functions can return data.

Here is an example from Python:

```python
def get_number():
    return 44

number = get_number()
```

Notice how the `get_number()` function doesn't really say anywhere what it returns? It could be a number, a String, a dictionary, or anything else.

In Java, you need to specify which type of data you are returning from a function. 

The function above, in Java, would look something like this:

```java
int getNumber(){
    return 44;    
}

int number = getNumber();
```

Notice how the `getNumber` function now says `int` before the function name? That's the "return type of the function", i.e, the type of data the function returns.

But in some cases, we don't want or need to return anything. Here is an example from Python:

```python
def print_message():
    print("Hello!")

print_message()
```

In Java, you still need to be explicit and write the return type of the function. If the function doesn't return anything, we use the return type `void`:

```java
void printMessage(){
    System.out.println("Hello!");    
}

printMessage();
```

### new

This keyword is used when you want to create an object. 

It also automatically calls the `constructor` of the class.

What these things mean, we will learn later. But for now, it's just good to know it exists.

```java
Motorbike motorbikeObject = new Motorbike();
```

### static

Remember what we learned earlier in the [class](#class) explanation above. A `class` is a blueprint or template for variables and functions that you feel belong together.

Java is "object oriented". This means that you can use your class as a blueprint or template, and create multiple "instances" of it. You can create a Car class, which by itself doesn't do anything or hold any data, but you can then create a yellow car, a blue car, a fast car and so on, all using the same class. The yellow car is stored in one variable, the blue car in another variable, and so on. All these different cars will have the same functions and variables, but the values of the variables and the behavior of the functions might be different from one Car to another.

**Each instance of a class is called an object.**

Exactly how this is done, or what it means, we will get to that later.

But what is important here is the following two points:

* In Java, you cannot just access functions or variables directly in a class. Because a class is just a template. I.e., you need to create an instance of the class and use that specific instance's function.
* When your computer tries to start up your Java program, it's not yet in "Java land". It doesn't know about classes and objects and instances and so on. Your computer needs a function that it can run without needing to set up an object.

If you mark a variable or function with the `static` keyword, it means that it can be accessed directly through the class without needing to create an object.

This can be used in all kinds of situations. But it **must** be used for the main function so that your computer can run it without having to worry about objects and such.

### constructor

A `constructor` is a special kind of function which is used when creating an instance of a class. (an "object")

The constructor cannot be called like a normal function. Instead, Java calls the constructor when you use the `new` keyword. 

It allows you to assign specific values to variables in your object at the same time as your object is created.

The name of the function **must** be the same as the class name. It **never** has a return type. It is usually marked with `public` but this is not a requirement. The constructor may take arguments.

You can see the constructor below:

Motorbike.java
```java
public class Motorbike {

    public Motorbike(){
    }
    
    public String getNameOfVehicle(){
        return "Motorbike";
    }
}
```

This is known as an "empty" constructor, or a no-args constructor. The reason is that it does not take any arguments. It is not necessary to define an empty constructor yourself because it's always there by default, even if we can't see it.

Below is an example / proof that the constructor is called by Java when you create an instance of the class with the `new` keyword.

Motorbike.java
```java
public class Motorbike {

  public Motorbike(){
    System.out.println("vroom vroom");
  }
}
```

Main.java
```java
public class Main {
    public static void main(String[] args) {
      Motorbike motorbike = new Motorbike();
    }
}
```

Output
```
vroom vroom
```

But you can also do some more useful things in the constructor in order to "set up" the object.

```java
public class Motorbike {

  public int price;  
    
  public Motorbike(int newPrice){
    price = newPrice;
  }
}
```

Main.java
```java
public class Main {
    public static void main(String[] args) {
      Motorbike motorbikeExpensive = new Motorbike(10000);
      Motorbike motorbikeCheap = new Motorbike(500);
      System.out.println("Expensive bike! " + motorbikeExpensive.price);
      System.out.println("Cheap bike! " + motorbikeCheap.price);
    }
}
```

Output
```
Expensive bike! 10000
Cheap bike! 500
```

### this

Let's take a look at the constructor example above:

```java
public class Motorbike {

  public int price;  
    
  public Motorbike(int newPrice){
    price = newPrice;
  }
}
```

Notice how the variable inside of the Motorbike class is called `price` and the parameter in the constructor is called `newPrice`?

That was necessary, because otherwise the example would not have worked.

❌ DOESN'T WORK
```java
public class Motorbike {

  public int price;  
    
  public Motorbike(int price){
    price = price;
  }
}
```

The issue here is that, when you are inside the constructor (or any function for that matter), `price` will always refer to the parameter. Java thinks you are trying to assign the parameter to itself which doesn't make a lot of sense. It will let you do it, but the `price` variable inside the Motorbike class will not be updated, and will keep its default value of 0.

Instead, use the `this` keyword.

```java
public class Motorbike {

  public int price;  
    
  public Motorbike(int price){
    this.price = price;
  }
}
```

Now, Java knows that you mean the `price` **variable** on the left side, and the `price` **parameter** on the right side.

## An example of how/when to use objects vs static

This is a very simple example of how objects work in Java. 

There is a Motorbike class which has a single function which just return the String "Motorbike".

Let's see if we can call this function from the main function.

### ❌ ERROR

Motorbike.java

```java
public class Motorbike {

    public String getNameOfVehicle(){
        return "Motorbike";
    }
}
```

Main.java
```java
public class Main {
    public static void main(String[] args) {
        String nameOfVehicle = Motorbike.getNameOfVehicle();
        System.out.println(nameOfVehicle);
    }
}
```

Outputs:
```
java: non-static method getNameOfVehicle() cannot be referenced from a static context
```

As you can see, like I described above about static functions, you cannot just call a function defined in a class. 

You have two options. Either mark the function as `static` or create an instance of the class.

### ✅ Options 1, marking as static:

We just take the easy route here and mark the function with `static`. Now we can access it from outside of the Motorbike class.

Motorbike.java
```java
public class Motorbike {

    public static String getNameOfVehicle(){
        return "Motorbike";
    }
}
```

Main.java
```java
public class Main {
    public static void main(String[] args) {
        Motorbike motorbike = new Motorbike();
        String nameOfVehicle = motorbike.getNameOfVehicle();
        System.out.println(nameOfVehicle);
    }
}
```

Outputs
```
Motorbike
```

### ✅ Options 2, creating an instance of the class:

This is a different way to get rid of the error from before. We can create "an object", or an instance of the Motorbike class.

Notice how we literally create a variable with the type `Motorbike` and the name `motorBikeObject`. We then call the function `getNameOfVehicle()` through this variable.

Motorbike.java
```java
public class Motorbike {

    public String getNameOfVehicle(){
        return "Motorbike";
    }
}
```

Main.java
```java
public class Main {
    public static void main(String[] args) {
        Motorbike motorBikeObject = new Motorbike();
        String nameOfVehicle = motorBikeObject.getNameOfVehicle();
        System.out.println(nameOfVehicle);
    }
}
```

Outputs
```
Motorbike
```

### What's the difference? Which should I pick? Why even use objects?

You might ask yourself: Why not just mark everything as static? Why bother with objects?

If you mark a function or variable as static, it does indeed mean that you can access it outside of the class. That's nice. But it also means that you can call the function or access the variable directly on the class without referring to a specific instance of the class. But what does that mean?

#### Strings

One really simple example is the `String` class. Each new String you create is an instance of this `String` class. So each String is an object.

What if you wanted to get the length of a String? You could do the following:

```java
String favoriteMonkey = "Jangol";
int nameLength = favoriteMonkey.length();
```

I can reveal that the `length()` function in the String class is NOT marked with static. 

-> This means that you are forced to call the `length()` function on a specific object / instance of a String. 

-> Which means that the `length()` function knows that it is being run on the specific text "Jangol"

-> This also means that the `length()` function behaves differently depending on which object it is being called on.

Had the `length()` function been static, you would have been able to call it like this:

```java
String favoriteMonkey = "Jangol";
int nameLength = String.length();
```

which doesn't make a lot of sense. You are not telling Java anywhere what you are getting the length of. You are just calling the `length()` function directly on the `String` class which does not hold any text, and does not have any connection to your String with the text "Jangol".

So, in this case, it would not make sense to mark the `length()` function as static.

And you might ask yourself: If Strings are really objects, then where is their constructor? Why do we not use the `new` keyword for them?

When you write the following:

```java
String favoriteMonkey = "Jangol";
```

It is really just a shortcut for the following.

```java
char[] data = {'j', 'a', 'n', 'g', 'o', 'l'};
String favoriteMonkey = new String(data);
```

You don't need to know exactly how this works, but, in short: `String` is actually a class that has a variable which holds the binary data for some text. And when you create a String variable, you are actually using the "new" keyword to create a String object, and you are giving your text to the constructor, which then stores the text as binary bytes inside of that particular String object.

#### Why do we have a "String" class at all?

Well, each individual String has a unique piece of text. But ALL strings should have the same functions available for you to call, like

* `toUpperCase()`
* `toLowerCase()`
* `contains()`
* `concat()`
* `length()`
* etc ..

Every single String, no matter if it's "Good morning!!" or "I feel hollow inside", they should all provide you with the same functions. The only difference is the actual text the String holds.

That's a great example of classes and objects. The functions are defined on the class-level, because the same list of functions should always be available on every single String. But, by creating individual instances of the String class, you can make one String that has one text, and a different String that has another text.

#### Another example

Imagine if you wrote a Java program for controlling 8 different electric toy cars in a plastic race track. I make the claim that you would want to make a single `Car` class, because all the toy cars are all cars, and they have a lot in common.

So you make a `Car` with the following variables:

* `topSpeed`
* `color`
* `basedOnRealLifeCarModel`
* `driverName`

And the following functions:

* `start()`
* `turnLeft()`
* `turnRight()`
* `increaseSpeed()`
* `decreaseSpeed()`
* `stop()`
* `getDriverName()`

It doesn't matter if the car is red or blue, or based on a Lamborghini or Ferrari. They all have the same variables and functions. The only real difference is that the variables in one `Car` object might hold different values than the variables in another `Car` object. 

This is the beauty of classes and objects: A class just defines what kind of data is possible to store. An object actually contains the data. And you can make multiple different objects based on a single class. The objects all have the same variables as defined in the class, but might have different values for these variables. The objects also have all the same functions, but they might behave different depending on the object.

In our example, some cars have a high top speed, and some have a slower top speed. Some are blue and some are red. Some are Lamborghini and some are Ferrari. But they all are guaranteed to have the same functions and variables.

You can create 8 different instances of the `Car` class. Here is some pseudocode:

```
Car slowRedLamborghini = new Car(Lamborghini, 200 km/h, RED, Samuel);
Car slowBlueLamborghini = new Car(Lamborghini, 200 km/h, BLUE, Jangol);
Car fastRedLamborghini = new Car(Lamborghini, 350 km/h, RED, Eduardo);
Car fastBlueLamborghini = new Car(Lamborghini, 250 km/h, BLUE, Klaus);
Car slowRedFerrari = new Car(Ferrari, 200 km/h, RED, Knaus);
Car slowBlueFerrari = new Car(Ferrari, 200 km/h, BLUE, Kpaus);
Car fastRedFerrari = new Car(Ferrari, 350 km/h, RED, Hans);
Car fastBlueFerrari = new Car(Ferrari, 250 km/h, BLUE, Mitch);
```

You now have 8 different "objects", or instances of the `Car` class.

Notice that they all have the type `Car`. So you know that the `slowRedFerrari` and the `fastBlueLamborghini` both have a `turnLeft()` function, or a `topSpeed` variable, for example. 

The difference is that the `topSpeed` variable in one car might be 200 km/h, and 350 km/h in another

If we skip all the code for how to actually drive the toy cars around and finding a winner of the race, imagine that at the end you have found which of these 8 `Car` objects was the winner, and now you need to print the name of the driver. 

Imagine that `fastRedLamborghini` was the winning car.

Since they all have the type `Car`, you know that they all have a `getDriverName()` function. This means that you can create a generic function like this one:

```java
void printDriverNameOfWinningCar(Car winningCar){
    System.out.println(winningCar.getDriverName());
}
```

Notice how this function doesn't know which car actually won the race. All it knows is that it receives a `Car` as input. It could be any of those 8 Car objects we created. But it's of type `Car`, so we know it must have a `getDriverName()` function.

If we call the `getDriverName()` function on a specific car, it allows it to access the values for that specific `Car` object.

If you run this:
```java
printDriverNameOfWinningCar(fastRedLamborghini);
```

It will output
```
Eduardo
```

If you run this:
```java
printDriverNameOfWinningCar(slowBlueLamborghini);
```

It will output
```
Jangol
```

### What is a class, and what is not a class?

It's quite straight-forward. If you see this:

```java
public class XXX {

}
```
then you know that XXX is a class. Most things in Java are classes, even internal things in Java like lists and Strings, but not everything.

There are "primitive types". These are not classes. Examples are:

* `int`
* `boolean`
* `byte`
* `short`
* `long`
* `char`
* `double`

Notice that primitive types are written entirely in lowercase, while classes are capitalized.

### What's the difference between an object and a variable?

A variable is just a box (or really, a memory address in your pc) that holds some data.

An object is an instance of a class. These can be stored in a variable. 

A variable can contain an object, yes, but the variable can also contain data that is not an object. A variable can hold booleans, integers, etc., and these are not objects

### What's the difference between a type and a class?

A variable or a function parameter always has a type, but sometimes the type is a primitive type, and sometimes it's a class.

Here is an example:

```java
void printStringAndNumber(String printThis, int printThisToo){
    System.out.println(printThis + printThisToo);
}
```

The function takes two parameters.

* printThis
    * Has type `String` which is a class
* printThisToo
    * Has type `int` which is a primitive type, and not a class

Also, notice that primitive types are always written with all-lowercase letters and are usually marked in a special color.

Classes are always capitalized.

### What's the difference between a function and a method?

A method is a special case of a function. It's a function that is defined in a class. 

Methods, when run on a specific object, have access to variables stored in that specific object. 

This means that if you call the `length()` function on two different Strings, it can return two different results. 

```java
String string1 = "GOOD";
String string2 = "MORNING";
int length1 = string1.length(); // 4
int length2 = string2.length(); // 7
```

## More keywords

### final

A variable marked with this keyword cannot be updated, and must be given a value when it is created.

✅ You can create variables without a value, and you can update them later. As long as they are not marked with `final`
```java
String test;
test = "Hello!";
test = "Goodbye!";
```

❌ You cannot create a final variable without a value. 
```java
final String test;
```

❌ You cannot update the value of a final variable. 
```java
final String test = "Hello";
test = "Goodbye!!";
```

### public vs private

When it comes to specifying which parts of the code has access to your variable or function, you have the choice between `private` and `public`.

We learned `public` earlier. It allows the variable or function to be accessible from outside of the class.

A variable or function marked with `private` can only be accessed from within the class it is defined.

**Keep in mind:** `private` and `public` cannot be used for variables inside of functions. The reason is that these variables are always "forgotten" when the function is done anyway.

There's also the `protected` keyword, and you can also completely leave out `private` or `public`, but that's for more advanced use cases.

## Standards

### Mark as private if possible

A function or variable should always be marked as private unless not possible. This blocks your code from becoming a big interconnected spaghetti mess where everything has access to everything.

### getter and setter

It is common practice for a class to mark its own variables as private, and then only "give access" to the variable through "getters" and "setters". Here is an example:

Notice that the `price` variable is private, so another class cannot access it. But there are two public methods that allow reading and updating the `price` variable from outside of the class.

```java
public class Motorbike {

    private int price = 10000;
    
    public int getPrice(){
        return price;
    }
    
    public void setPrice(int newPrice){
        price = newPrice;
    }
}
```
