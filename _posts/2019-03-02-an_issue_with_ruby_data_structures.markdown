---
layout: post
title:      "An Issue with Ruby Data Structures"
date:       2019-03-02 22:17:09 +0000
permalink:  an_issue_with_ruby_data_structures
---



### Hashes
Simple Discription of Hashes. 
They are key-value pairs, here's what some keys can be. 
```
Hash_Key_String = {"One" => 1, "Two" => 2, "Three" => 3}
Hash_Key_Symbol = {One: 1, Two: 2, Three: 3}
Hash_Key_Combo = {One: 1, "Two" => 2, Three: 3}
```
Here's what some values can be. 
```
Hash_Value_String = {Name: "Luigi", Location: "Mario World", Brother: "Mario"}
Hash_Value_Number = {One: 1, Two: 2, Three: 3}
Hash_Value_Hash = {Hash1: {Key1: 1}, Hash2: {Key1: 1, Key2: 2}} 
Hash_Value_Combo = {First_Month: "January", First_Month_Days: 31, Days: {1: "New Year's Day", 20: "MLK Day"}}
```
Here's how some can be created
```
Hash_Curly_Bracket = {key: 'value'}                # This can have multiple key-value pairs
Hasy_Angle_Bracket_Symbol[:key] = 'Value'          # One key-value pair at a time
Hash_New_Default = Hash.new(0)                     # Creates an empty hash with keys set to default of 0
Hash_Empty_Curly = {}                              # Empty Hash with no default values
```
### Hash Key as Instance of class
Hash Keys can be instances of a user defined classes. If that class specifically defines actions to do with that class instance when it's used as a key for a hash.
```
class Painting
  attr_reader :artist, :title

  def initialize(artist, title)
    @artist = artist
    @title = title
  end

  def ==(other)
    self.class === other and
      other.artist == @artist and
      other.title == @title
  end

  alias eql? ==

  def hash
    @artist.hash ^ @title.hash # XOR
  end
end

painting1 = Painting.new 'Leonardo Da Vinci', 'Mona Lisa'
painting2 = Painting.new 'Leonardo Da Vinci', 'Mona Lisa'

reviews = {}

reviews[painting1] = 'Great painting!'
reviews[painting2] = 'So pretty!'

reviews.length #=> 1
```
The class definition above makes it so that only class instances with either a different 'artist' or a different 'title' are added to the hash definition. If the hash already contains a 'class as key' with the same member values it will not add it to the hash as a key-value pair. 

### Hash Key as Instance of class code walkthrough
This code has two parts to it. The first part is the class definition which I've shrunk slightly to make it more readable and hopefully better to read. The second part is ruby code demonstrating how the class instance behaves when it's a key in a hash definition. 
#### The Class Definition
Below is a compressed version of the 'Painting' class for readability and will hopefully make it easier to understand the class. 
``` 
class Painting
  attr_reader :artist, :title
	
  def initialize(artist, title)

  def ==(other)

  alias eql? ==

  def hash
end
```

The 'attr_reader :artist, :title'  defines two instance variables called 'artist' and 'title' and is the same as writing the following in code. These two instance variables will be used in other methods. 
```
class Painting
  # attr_reader :artist, :title

  def artist
	  @artist
  end
	
  def title
	  @title
  end
end
```

Painting's 'initialize' takes two parameters with no default values so it must have two values of something when instance of Painting is created, weather it be some number or letter. Without doing this something like the following snippet will output the commented out error code. In order to get around this the Ruby coder could just replace the initialize method with the commented out one.
```
class Painting
  def initialize(artist, title)
    @artist = artist
    @title = title
  end
	
  # def intialize(artist = ' ', title = ' ')
  #   @artist = artist
  #   @title = title
  # end
end
painting1 = Painting.new 'Picasso' # wrong number of arguments (given 1, expected 2)
```
 
In the '==' that's been overridden makes sure that everything in the instance of the 'class as key' is copied and assigned as a new key/value pair. To be honest all the code after 'self.class === other' can be deleted and doesn't need to be there if the Ruby coder just wants the 'latest key value pair' more on this later, but for now here's the implementation.
```
class Painting
  
  def ==(other)
    self.class === other and
      other.artist == @artist and
      other.title == @title
  end
	
  # Can also be this.
  # def ==(other)
  #   other.class === other
  # end
end
```

The alias eql? statement makes sure that only the boolean logic in the '==' method is followed when eql? is called and makes use of the class more stable and consistent. It's considered good practice to do this when comparing class instances of the same user defined type.
```
class Painting
  def ==(other)
    self.class === other and
      other.artist == @artist and
      other.title == @title
  end

  alias eql? ==
end
```

The Hash method makes and returns a hash based on what the members of the current class instance of 'Painting' is. It's important to notice the '^' operator between '@artist.hash' and '@title.hash'. The '^' is called the  binary XOR operators and it returns a binary result that's a copy of bits that are in one, but not the other. This combined hash ensures that each 'class as key' has unique member values. 
```
class Painting
  def hash
    @artist.hash ^ @title.hash # XOR
  end
end
```
#### Using the Class
'painting1' and 'painting2' both have the same values for their members. Reviews is a hash used to store 'painting1' and 'painting2' as keys who's values are different reviews of the painting. When each class instance is 'used as a key' it makes the #hash method is used to create a hash value based on the member values of the 'Painting' class. If the hash has a 'class as key' with member values that are the same as previous 'class as key' it gets replaced with the most recent key-value pairs. This makes it so that reviews length is only 1 even though two different key-value pairs have attempted to add themselves to the hash instance.
```
painting1 = Painting.new 'Leonardo Da Vinci', 'Mona Lisa'
painting2 = Painting.new 'Leonardo Da Vinci', 'Mona Lisa'

reviews = {}
or 
reviews[painting1] = 'Great painting!'
reviews[painting2] = 'So pretty!'

reviews.length #=> 1

```
### Why this is Useful
This is useful because it automatically insures that the are not 'classes as keys' with duplicate values in a hash. You can also edit the #hash method like in the code below to only keep Paintings with different titles or only keep one painting from a specific artist. It's also valuable for keeping memory resources low in a program, by making limiting the size of hash from the beginning
```
class Painting
  def hash
    @title.hash
  end

  def hash
    @artist.hash
  end
end
```
