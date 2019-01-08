---
layout: post
title:      "formatted like this"
date:       2019-01-08 11:51:07 -0500
permalink:  formatted_like_this
---

### Key concepts of Hashes

**Key - Value Pairs**

Hashes are a collection of Key - Value pairs. The Key-Value pairs when assigned to a variable are enclosed in '{}'. The Key can be anything from a number, string or even a class instance (this requires method overloading) . In most cases the Key will be a string ("") or symbol (:). The value can be anything as well and its data is usually related to the name of the hash and the key its assigned too. Some examples of Hashes are below.
````
hashStringEg = {"key" => "value"}
hashNumEg ={"num" => 9}
hashArrEg = {"arr" => [1, "2", "three"]}
hashSymEG = {key: "This is the Value!"}
````
So the above hashes aren't very useful without their values being used in some. In Ruby Hash values can be accessed with the name of the hash with the key enclosed in angle brackets([]) similar to an Array. 
````
hashStringEg["key"] # "value"
hashSymEg[:key] # "This is the Value!"
````
In 'hashStringEG' the the key called "key" is a string so it's enclosed in (""), while the key in 'hashSymEg' is a symbol so a colon (:) is placed before the kayname. 

**Nested Hashes**

Hashes can be nested as well. This is useful because it allows the creation of complex data structures. And for their values to have meaning to the programmer. Here's an example of a nested hash. 
````
info = {Person: {Name: "George", Height: 150, Location: {Planet: "Earth", Continent: "North America", Nation: "Cuba"}}}
````
Info is a nested hash of information about a 'Person' whose 'Name' is "George" and is '150' cm tall. His 'Location' is 'Planet' "Earth" on the 'Continent' of "North America" in the 'Nation' of "Cuba". This is alot of information and although the value labels may be self explanatory it proves helpful to have a 'Key' to explicity label them. 

**Conclusion**

Hashes have many other functions and uses such as using 'collection' to iterate through a hashes values possibly perform calculations or actions on them and return the result of them. It's possible to give hashes a default value by using 'Hash.new()' to assign uncreated keys a default value other than 'nil'. Besides these two methods the Hash class has many others revolving around searching, modifying and comparing hashes. It's a little beyond the scope the of the post to discuss this but all information can be found in the following link. 
http://ruby-doc.org/core-2.5.3/Hash.html
