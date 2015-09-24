# Reading a File

## Main Concepts

This covers reading input from a file system as apposed to the terminal. 

## Objective

In this section we are going to read a sentence from a file. Create a text file called `data.txt`. Create this file in the same location as the code files we have already made. 

Add a sentence to that file e.g.

```txt
The first fully programmable digital electronic computer was the ENIAC which was completed in 1946.
```

This is just example text, use any sentence you prefer. 

Next we will write a Ruby program that will ready and display the contents of this file. In the same directory as `data.txt`, create a file called `reader_main.rb` and add the following lines:

```ruby
contents = File.read('data.txt')

puts contents
```

The solution above works perfectly for us, as we have a text file with very little data. If we were reading a larger file we may choose to use one of the many other approaches ruby has to read from files: http://stackoverflow.com/questions/5545068/what-are-all-the-common-ways-to-read-a-file-in-ruby

