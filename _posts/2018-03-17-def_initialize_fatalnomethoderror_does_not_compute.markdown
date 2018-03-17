---
layout: post
title:      "def initialize::FatalNoMethodError Does Not Compute"
date:       2018-03-17 13:06:22 +0000
permalink:  def_initialize_fatalnomethoderror_does_not_compute
---


For some pesky reason, I have the darnedest time with the method initialize. I was asked to implement it as part of my CLI project and I knew what it did- I could explain it but it took some time and support to get it working within my gem project. It’s a silly thing, really, and I’ve gone to great extents to understand it better. 

Initialize is a special method that executes whenever a new object is created or -bonus word- instantiated within a class. So, let’s say you’re creating a class that produces a bunch of Cats, you may want those cats to have certain attributes and initialize ensures that the cats will not be lacking those attributes and gives you several ways to ensure that they have them. 

You could write a method like this, including instance variables if you knew the cats would carry the same attributes each time a new cat was created: 

```
class Cats 
	def initialize 
		@kind = “domesticated, house monster”
		@temperament = “potential mood swings”
		@appearance = “fluffy”
	end 
end
```


But what if each cat ISN’T domesticated. What if you ALSO have an ocelot? Or if there’s all kind of cats- lions, tigers, feral dumpster cats- what then?  You might be able to keep the @temperament and @appearance instance variables but the @kind wouldn’t apply anymore. You can change your initialize method so that it accepts an argument on each new cat to assign that attribute. 

```
class Cats 
	def initialize(kind) 
		@kind = kind
		@temperament = “potential mood swings”
		@appearance = “fluffy”
	end 
end
```

If MOST of your cats are domesticated, house monsters you can take it a step further and apply a default to your argument.

```
class Cats 
	def initialize(kind= “domesticated, house monster”) 
		@kind = kind
		@temperment = “potential mood swings”
		@appearance = “fluffy”
	end 
end
```

There are all sorts of things you can do with your objects through the initialize method. You can give them attributes in a hash or array and iterate over them. You can have a mix of class, instance, and method variables. And technically, if you don’t want to use initialize at all, you don’t have to- it’s most helpful for cases when you want to enforce some values upon creation. 

I imagine that this method gives other folks confusion too— in fact, my google endeavors provide proof  to that end. Rather than being a problem with understanding the ```initialize``` method, I feel that for me it has been more a problem with understanding abstraction and getting my initialize method to cooperate with the scope of my other methods and objects. 

For me, the most difficult part of programing continues to be abstraction and in this particular case, it throws me for a loop— I liken it to the Schrödinger’s Cat of programming. With or without initialize an object can exist but without initialization we cannot know whether the cat is alive or dead. What does it all mean!? The cat object is only a representation of the cat- this poor cat may or may not exist?! And what about the poor cat that may or may not exist and may or may not be dead or alive? You see- abstraction can easily put me in a place of existential crisis. I like to think that ```initialize``` is like the birther of methods- we no longer have to worry about whether the ruby object of the cat exists or not and we can decide or assign the fate of the cat with attribute values.   

   




