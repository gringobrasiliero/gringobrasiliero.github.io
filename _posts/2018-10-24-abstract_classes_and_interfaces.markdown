---
layout: post
title:      "Abstract classes and Interfaces "
date:       2018-10-24 14:14:38 +0000
permalink:  abstract_classes_and_interfaces
---


## Abstract Classes

In the dictionary, the meaning of the word “abstract” is a thought or idea that has no physical existence, and is just conceptual. An abstract class is a class that is abstract, meaning that it is a concept, and can not be instantiated. If that is the case, how can abstract classes be useful, and how do we use them?
Abstract classes are created just to be inherited from. It is a base class. Child classes can inherit the properties, abstract methods (implementation written in child classes), and non-abstract methods (methods that are written in abstract class) that are defined inside of an Abstract class. This is useful as it helps to avoid code duplication. 
This is what an abstract method looks like in C#

```
namespace AbstractClassDemo
{
    abstract class HousePet
    {
        //Non-Abstract Method   
        public void Eat()
        {
            Console.WriteLine("Chomp chomp chomp.");
        }

        //Abstract Method   
        public abstract void speak();
    }
```

In the code above, you can see an abstract method called HousePet. It is set up like any other class, except a few key differences. It is declared as an “abstract class.” The class has a non-abstract method called Eat(). We defined Eat() as a non-abstract method because all house pets eat. So whenever we make a new class that inherits from HousePet, such as Dog, Cat, or Goat, we do not have to rewrite the method. So far, just a normal class right? 
We then look at this abstract method called speak within the class, however it is not defined. You would think that this would throw an error at you, however, in an abstract class, we are able to include abstract methods. What this abstract method does is require any class that inherits from it to define the method speak(). These abstract methods serve as a reminder that each class that inherits from this abstract class must include the abstract methods included. Since dogs, cats, and goats speak differently, we need to have their own custom implementation of speak in their respective classes. 

```
class Goat : HousePet
    {
        //Abstract Method implementation
        public override void Speak()
        {
            Console.WriteLine("Baaaaaaa!");
        }

        public void HappyHop()
        {
            Console.WriteLine("Hop hop hop hop");
        }

    }
```

So in the Goat class, you can see that we implemented the method speak, and we did so by using “public override void.” Since we implemented all of the abstract methods that the HousePet class requires, our Goat is a true housepet, and no errors are thrown at us. We also included another method that goats do, but is not required from the Base class. We are still able to implement our own methods inside of the child classes. 

## Interfaces

In the real world, an Interface is a medium to interact with something. It does have some similarities to a Abstract Class. It gets initiated through inheritance. Any classes that use the interface must define the definitions that are declared in the Interface. The thing is, an interface is not a class, and instead it is more of a contract for whatever classes that do inherit from it, to include everything that is specified. 

```
namespace InterfaceDemo
{
    Interface Ivehicle       //Definition of Interface    
    {
        void Accelerate();
        void Brake();
    }
```

Above, we defined an interface called Ivehicle. We use an “I” at the beginning out of convention. You can see that there is not a whole lot into it. We just declared Accellerate and Brake. Those are two methods that a vehicle needs to have. Any classes that belong to this interface must define everything that the interface has. 

```
    class Car: Ivehicle
    {
        public void Accelerate()
        {
            Console.WriteLine("Pushing the petal on the right makes this car go zoom!");
        }

        public void Brake()
        {
            Console.WriteLine("The petal on the left makes this car slow down.");
        }
```

In order to make a class belong to an interface, you just have to declare the interface where you name the class. Then you must define all of the methods that are defined in it, or else you will have errors thrown. A class can use multiple interfaces, where you can only inherit one Abstract class. 
Interfaces are useful in Service Oriented Architecture (SOA) as interfaces can be used to define service contracts. 

I hope that after this post, you are able to cipher the key similarities and differences that Abstract Classes and Interfaces have. Thank you for reading, and happy coding!



