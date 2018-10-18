---
layout: post
title:      "Object Oriented Programming"
date:       2018-10-18 09:49:58 +0000
permalink:  object_oriented_programming
---


This week, I would like to share about the advantages and disadvantages of OO Programming. Before I can talk about that, I need to clarify. What is Object Oriented Programming?

Object Oriented Programming is a paradigm of programming where the solution to a programming problem is modeled as a collection of collaborating objects. There are four principles of OO programming, which are encapsulation, abstraction, inheritance, and polymorphism. 

## Encapsulation

Encapsulation is how you keep an objects state private. So, let’s say we have a cat. The cat has a level of hunger, sleepiness, and happiness.
In procedural programming, you could set this up like this:

```
Cat_hunger = 50
Cat_sleepiness = 50
Cat_happiness = 50
```

There are a couple problems with setting up your cats hunger, sleep, and happiness level this way. It only represents one cat, and it allows us to change their happiness, sleepiness, and hunger directly, which is not how it works in real life. You can’t directly change a cat’s hunger, but you can feed the cat, which changes their hunger level. Let’s make a cat the Object-Oriented way.
```
class Cat
    attr_reader :hunger, :sleepiness, :happiness
    def initialize()
        @hunger = 50
        @sleepiness = 50
        @happiness = 50
    end

    def feed
        @hunger -= 10
        puts @hunger
    end
end
```

Here we defined what a cat is.
Now we can create a new cat like so:
```
Nyan = Cat.new()
Puts nyan.hunger
#50
Nyan.hunger = 100
# undefined method `hunger='
Puts nyan.hunger
```

We can not directly change the cats hunger level at will, however, we can feed it, and its hunger level will go down!
```
nyan.feed()
puts nyan.hunger
#40
```

That is more like it. A Cats got to eat! 
When we moved the variables cat_hunger, cat_sleepiness, and cat_hunger into the Cat class, they became properties of the Cat, and doing so, kept the Cat’s properties internal, where we can not directly change the properties unless we are specifically allowed to, or through the methods that are defined within the cat class. This is encapsulation. 

## Abstraction

Abstraction is another key concept in Object Oriented programming, where its main goal is to hide unnecessary details from the user. For example, if you wanted to drink some coffee with your cat, you would have to make some. You put the filter and coffee into the machine and press a button. Done. Coffee with the cat. All of the details such as the water temperature, amount of water to pass through the coffee grounds, and how the hot water combined with the grounds produced coffee is all abstracted away and made it very easy to enjoy our cup of coffee with out cat. This is abstraction, and it is very beneficial to us in Object oriented programming. It allows us to keep it simple for our users to use the functions that we define in a class, and it also helps to hide the details. This is very important when you have secret algorithms that you do not want others to be able to copy. 

## Inheritance
In Object Oriented Programming, we can define many different classes, and some classes will be similar to others. Inheritance enables new objects to take on the properties of other existing objects. This is another important key concept of OO programming. So, we know that cats and dogs are different, however, they share a lot of the same qualities. Both dogs and cats have a hunger, sleepiness, and happiness level, and they both need to be fed. 
```
class Cat
attr_reader :hunger, :sleepiness, :happiness

  def initialize()
    @hunger = 50
    @sleepiness = 50
    @happiness = 50
  end

  def feed
    @hunger += 10
    puts @hunger
  end
end

class Dog
attr_reader :hunger, :sleepiness, :happiness

  def initialize()
    @hunger = 50
    @sleepiness = 50
    @happiness = 50
  end

  def feed
    @hunger += 10
    puts @hunger
  end
end

nyan = Cat.new()
sparky = Dog.new()
```

 Instead of rewriting each class with all the very similar qualities, we can inherit those qualities from a parent class. Lets make a parent class called HousePet.
```
class HousePet
  attr_reader :hunger, :sleepiness, :happiness

  def initialize(name)
    @name = name
    @hunger = 50
    @sleepiness = 50
    @happiness = 50
  end
  def feed
    @hunger += 10
    puts @hunger
  end
end

class Cat < HousePet
end

class Dog < HousePet
end

nyan = Cat.new()
sparky = Dog.new()
```

We were able to group together the similarities of the two animals in the HousePet class and inherit the traits in the child class. This is a good example of inheritance and is an important key concept that Object-Oriented Programming brings to the table. 

## Polymorphism

Polymorphism is a fun word to say, and an important concept of Object-Oriented programming. In Greek, polymorphism means “many forms.”

We know the power of inheritance, and this is great! But there comes a little problem with this. We have a parent class of HousePet with the child classes of Dog and Cat, and they both speak; however, we can not put speak in the HousePet class because dogs and cats speak differently! Polymorphism allow the child classes to inherit all of the qualities from its parent class, and it can keep its own methods that separate itself from the other child classes. So since dogs and cats can speak, lets add these methods to our classes. 
```
class HousePet
  attr_reader :hunger, :sleepiness, :happiness

  def initialize()
    @hunger = 50
    @sleepiness = 50
    @happiness = 50
  end
  def feed
    @hunger += 10
    puts @hunger
  end
end

class Cat < HousePet

  def speak
    puts "Meow!"
  end
end

class Dog < HousePet
  def speak
    puts "Woof Woof!"
  end
end

nyan = Cat.new()
sparky = Dog.new()

nyan.speak()
# Meow!
sparky.speak()
# Woof Woof!
```

Although we called speak on both the cat and on the dog, they were both able to respond in the appropriate way. No error saying that speak was already defined. No confusion. With polymorphism, we can separate the differences between the two child classes, and with inheritance, we were able to keep the similarities of the two. 

## Drawbacks
The only drawbacks of object-oriented program is the size, effort, and speed. 
Object-Oriented programs are much larger than other programs, which can also affect the speed. Fortunately, our computers are continuously becoming faster, so it is not as big of a problem as it was back when we were running windows 98. 

Making Object-Oriented Programs also require more effort to create. You must plan out how you are going to create the program, and it requires a little bit more code to get started, but it is worth it as it has many advantages.

## Advantages 

Objects can be reused across applications. If you have a class that you have already defined, it is easy to bring into your new program. 

Software is easier to maintain. Since the design is modular, you can update a part of the program without having to make a lot of changes throughout your code.
Better productivity. It might take a little bit more planning in the beginning to get started, however, it is worth it because your code is more organized, and you can take existing classes from other programs into your new ones, instead of having to redefine everything every time you create a new program. 

I hope this helped you gain a deeper understanding of OO programming and motivates you to begin writing code using Object-Oriented programming rather than procedural. 

