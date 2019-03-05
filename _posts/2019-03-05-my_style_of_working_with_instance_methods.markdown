---
layout: post
title:      "My style of working with instance methods"
date:       2019-03-05 20:16:54 +0000
permalink:  my_style_of_working_with_instance_methods
---

There are at least two cases to consider when working with instance methods. The first case is weather I'm working with an instance method that has already been defined in a class, such as the built-in ruby class hash or if I'm working with a class that has been already been created by a user/lesson. The second case is if I'm expected to create class from scratch and create my own instance methods to describe an object that may or may not exist in this world. Both cases have similar approaches, but different hurdles to consider that I'll be discussing below.

## The class instance method is already created.
Below an instance of class Hash and Array are created using both the new method and literal creation.
```
Hash[]
hash = Hash.new
Array[]
array = Array.new
```
This is extremely important to me, because it gives me insight into what instance variables that class has and the instance methods that class may use. For example both the hash and array method in their #new documentation describe completely different lables for the input they expect for their #new. With this I can get an idea of the instance methods the class may use and what to do with them. In the below code I can tell the Array class may have an instance variable called 'size' and the hash class may have instance variables called 'key' and 'value'. From this I can workout(with a high probability) that accessor instance methods exist for each instance variable. Of course I gain this knowledge from documentation on that class, but I'd apply this thought process to any other class which I didn't create. It would be admittedly difficult if not impossible for me to work with a class's instance methods without looking at documentation/implementation for how it's instantiated
```
hash = Hash["My Name", "Emmanuel"]                      # This instanciation method requires a ['key', 'value'..]
array = Array.new(5){|index| index * index}             # This instanciation method requires a new('size'){|'index'| 
                                                        # 'block'}
puts Hash.keys                                          # #keys exists because hashes have a methods and literals that 
                                                        # expect a 'key' 
puts array.size                                         # #size exist because arrays have methods or literals that 
                                                        # expect a 'size'
```
## The class instance method is created by me.
If I were creating a class instance method by myself I'd first need to think of what I intend to create. If I wanted to create a class called 'Goldfish' I'd assume it would be the pet of someone or have some sort of human interaction causing it to have a 'name', because people gotta put names on every living thing. So my simple implementation of a goldfish class would have instance methods of #new to initialize a name, a #name= to change the name and a #name to display it. I probably wouldn't need to provide too much documentation for this and just show it's implementation, because of it's simplicity. Though I definitely would if it was complex enough.
```
class Goldfish
  def initialize(name)
    @name = name
  end
  
  def name
    puts @name
  end

  def name=(name)
    @name = name
  end
end

myGoldFish = Goldfish.new("Goldfish")
myGoldFish.name
myGoldFish.name = "AuFish"
myGoldFish.name
```
