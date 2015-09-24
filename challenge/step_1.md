# Introduction

In this section we will see how to structure code into reusable groups. This concept is the key take away, the specific implementation details of each section are less important. 

If you understand the key concepts you will be able to search for the specific implementation details when and if you need them.

## Methods

We will be grouping lines of code into 'methods'. Methods are blocks of reusable code which perform specific tasks. For example a method could determine and print a 'full name' from a given first and last name.

To implement this create a file called `main_person.rb`. Then add the following lines of code:

```ruby
# main_person.rb

# Defining the method
def print_full_name(first_name, last_name)
	result = "#{first_name} #{last_name}"
	puts result
end

# Instantiating variables 
first_name = "Sue"
last_name = "West"

# Invoking the method
print_full_name("Bob", "South") # passing hard coded strings into the method
print_full_name(first_name, last_name) # passing variables into the method
```

![anatomy of a method](https://www.safaribooksonline.com/library/view/head-first-ruby/9781449372644/graphics/f0036-01.jpg)  
The anatomy of a method [1]



A method can return a value which mean that the previous example could be re-written as the following:

```ruby
# main_person.rb

# Defining the method
def get_full_name(first_name, last_name)
	result = "#{first_name} #{last_name}"
	return result
end

# Instantiating variables 
first_name = "Sue"
last_name = "West"

# Invoking the method
full_name = get_full_name("Bob", "South")
puts full_name

puts get_full_name(first_name, last_name)

```

In Ruby the last line is always returned so the method could have been written like this:

```ruby
# main_person.rb

def get_full_name(first_name, last_name)
	result = "#{first_name} #{last_name}"
	result
end
```

Or an even shorter version:

```ruby
# main_person.rb

def full_name(first_name, last_name)
	"#{first_name} #{last_name}"
end

# Instantiating variables 
first_name = "Sue"
last_name = "West"

# Invoking the method
# On the next line, Ruby can tell the difference between the variable on the left and the method call on the right
full_name = full_name("Bob", "South") 
puts full_name

puts full_name(first_name, last_name)
```

Lets add a method called `display_name`: 

```ruby
# main_person.rb

# Defining the methods
def full_name(first_name, last_name)
	"#{first_name} #{last_name}"
end

def display_name(first_name, last_name)
	"#{first_name[0]}. #{last_name}"
end

# Instantiating variables 
first_name = "Sue"
last_name = "West"

# Invoking the methods
full_name = full_name("Bob", "South")
display_name = display_name("Bob", "South")

puts full_name
puts display_name

```

## Classes

Functions help to reduce code duplication, however having many of them soon makes the code base difficult to manage. To help with this we can group related functions into a structure known as a class. 

Applying this to the example we could change this:

```ruby
# main_person.rb

# Defining the methods
def full_name(first_name, last_name)
	"#{first_name} #{last_name}"
end

def display_name(first_name, last_name)
	"#{first_name[0]}. #{last_name}"
end

# Instantiating variables 
first_name = "Sue"
last_name = "West"

# Invoking the methods
full_name = full_name("Bob", "South")
display_name = display_name("Bob", "South")

puts full_name
puts display_name

```
To:

```ruby
# main_person.rb

# Defining the class
class Person
	# Defining the methods
	def full_name(first_name, last_name)
		"#{first_name} #{last_name}"
	end

	def display_name(first_name, last_name)
		"#{first_name[0]}. #{last_name}"
	end
end

# Instantiating variables 
first_name = "Sue"
last_name = "West"

# Instantiating the class to get an 'object'
user = Person.new

# Invoking the methods using the 'person object'
full_name = user.full_name("Bob", "South")
display_name = user.display_name("Bob", "South")

puts full_name
puts display_name
```

It is possible to move this class into a separate file. That way it can be easily reused by other scripts (programs). Create a new file called `person.rb`. To keep things simple, make this file in the same folder as `main_person.rb`. Move the class out of `main_person.rb` into `person.rb`. 

```ruby
# person.rb

# Defining the class
class Person
	# Defining the methods
	def full_name(first_name, last_name)
		"#{first_name} #{last_name}"
	end

	def display_name(first_name, last_name)
		"#{first_name[0]}. #{last_name}"
	end
end
```

```ruby
# main_person.rb

# Instantiating variables 
first_name = "Sue"
last_name = "West"

# Instantiating the class to get an 'object'
individual = Person.new

# Invoking the methods using the 'person object'
full_name = individual.full_name("Bob", "South")
display_name = individual.display_name("Bob", "South")

puts full_name
puts display_name
```
At this stage there will be errors if we try to run `main_person.rb`. This file does not 'know' about `person.rb`. In order to link these files we can use `require_relative`. 

```ruby
# main_person.rb

require_relative 'person'

# Instantiating variables 
first_name = "Sue"
last_name = "West"

# Instantiating the class to get an 'object'
user = Person.new

# Invoking the methods using the 'person object'
full_name = user.full_name("Bob", "South")
display_name = user.display_name("Bob", "South")

puts full_name
puts display_name
```

The path given to `require_relative` is relative to `main_person.rb`. When the program is run, the `Person` class will be accessible again and the code should work as before. 

### References and Credits
[1] - Anatomy of a method - https://www.safaribooksonline.com/library/view/head-first-ruby/9781449372644/ch02.html
