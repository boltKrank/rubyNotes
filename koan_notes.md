# Nots from Koan tutorial

See: [Ruby Koans](http://rubykoans.com/)

## Asserts

For further information see [Ruby Asserts](https://docs.ruby-lang.org/en/2.1.0/Test/Unit/Assertions.html)

### assert

Asserts are used for unit testing in Ruby. The general pattern is:

`assert(test, [fail message])`

or

`assert test, "fail message"`

Any time assert is found, it will not continue unless the assert is successful. i.e. returns true, a useful fail message is recommended to explain what was being tested and didn't return true.

### assert_equal

Requires 2 parameters, fails if both parameters aren't equal

`assert_equal input1, input2, "optional fail message"`

### assert_match

`assert_match, regex, regex_test, "optional fail message"`

This will return true if the regular expression matches regex_test

## Objects

[Ruby Objects](https://ruby-doc.org/core-2.6.5/Object.html)

### `.is_a?` (.kind_of? is an alias)

.is_a? returns true if the class type passed in matches the class type of the object calling the function.

`obj.is_a?(classname)`

if obj is an obj made from classname this will return true.

In the case of Ruby, `nil` is an object.

### `.nil?`

only returns true if call from a nil object

```ruby
nil.nil?  # returns true
Object.new.nil? # returns false
```

### .to_s

Returns a string representation of the object passed in.

### .inspect

Returns a string representation of the object's ID, which is by default the class name.

### .object_id

Returns an integer that identifies the object. Each time a new object is made it's given a new id.

```ruby
Object.new.object_id == Object.new.object_id            # This will return false
2.object_id == 2.object_id                              # This will return true
"Simon".object_id == "Simon".object_id                  # This will return false, because the state of the object may have changed
"Simon".freeze.object_id == "Simon".freeze.object_id    # This will return true, the object_id will become static once frozen.
```

### .freeze

Like *final* in Java, this makes the object static, RuntimeError exception will be thrown if changes are attempted.

### .clone

Makes a clone of the object. This clone is of the same state, but has a different object_id

### .class

Returns the type of class the object is.

```ruby
    object1 = Hash.new
    object2 = Array.new
    object1.class # returns Hash.  Empty Hash's are {}
    object2.class # returns Array. Empty Array's are []
```

## Arrays

Like everything else in Ruby, they're objects with in-built functionality to handle a series of other objects.

An empty array can be made by instantiating an Array object:

`myList = Array.new`

### Assigning values

Individual elements can be assigned:

`myList[0] = 'Simon'`

They can be added to the end of an array:

`myList <<< 333`

at this stage it would be: `['Simon',333]`

### Paralell assignment

You can assign multiple variables values from an array in a single statement. The position of the variable determines which elements value it is assigned.

```ruby
one,two,three = [0,1,2] #one = 0, two = 1, three = 3
```

### Accessing values

Values can be accessed by directly inputing their element index, or using methods such as `.first` and `.last`

### Positive and negative indexes

If the index is positive, it counts from the begining of the array, i.e.: [0,1,2,3]

If the index is negative, it counts from the end of the array, i.e: [-4,-3,-2,-1]

### Slicing arrays

When passing in 2 indexes to access an array, it returns a subset as follows:

`myArray[<starting_element>, <count>]`, it will add `<count>` elements starting from `<starting_element>` unless the array is smaller then it will go to the last element.

NOTE: if the `<starting_element>` is greater than the length of the array, it will return `nil`

### .push and .pop methods

Using .push on array puts the value at the end of the array. Using .pop returns and deletes the last value of the array.

### .shift and .unshift methods

The .shift method returns and deletes the first value of an array. The .unshift method adds to the begining of an array.

### Splats values - double and single splat (*) values

Splat values replace single parameters with arrays to allow more than one value to be passed in.

The single splat: example*, and the double splat: example**

Splats are used to accept parameters when you don't yet know the number of parameters that are coming in, or you want to act dynamically based on the number of parameters that come in.

*Example:*

```ruby
    element1, *element2 = [1,2,3,4,5,6,7] #element1 == 1, element2 == [2,3,4,5,6,7]
```

**NOTE:**

If we weren't using a splat value, then element2 would only equal the next element

*Example:*

```ruby
    element1, element2 = [1,2,3,4,5,6,7] #element1 == 1, element2 == 2
```

In the above example `element1` equals the first element, whilst `element2` is all remaining elements.

TODO: Check what happens with multiple splats ? Does it need to be the last parameter ?

### Ranges

An array: [5,6,7,8], a range: (5..8) or (5...8) if you want to exclude the last value, in this case `8`. To convert a range to an array, you use the .to_a method, i.e.:

```ruby
myRange = (5..15)
myArray = myRange.to_a
```

### Array ranges

You can reference ranges of values using the range notation in square brachets.

```ruby
myArray = [0,1,2,3,4,5,6,7,8,9]
myArrayRange1 = myArray[0..3]   #[0,1,2,3]
myArrayRange2 = myArray[0...3]  #[0,1,2]

myArrayRange1 = myArray[2..5]   #[2,3,4,5]
```

## Hashes

A Hash is like an array, but uses {} instead of []. It is made up of key-value pairs, returning a Nil object if the key doesn't exist.

### initialisation

Initialising a Hash is the same as initialising any object.

`myHash = Hash.new`

You can add a default, which is the value returned when no matching key is found.

`myHash = Hash.new("default_value")`

### adding to default value

When I add to an object using a key that doesn't exist, it's just going to add to that `default_value`

*Example:*

```ruby
    myHash = Hash.new([])
    myHash[:one] << 2 #Because the key :one doesn't exist, 2 will be added to the default array making it [2].
    myHash[:two] << 3 #Because the key :two doesn't exist, 2 will be added to the default array making it [2,3].
```

If you want the above to create the key and value, we can initialise the Hash like this:

`myHash = Hash.new {|hash, key| hash[key] = [] }`

*Example:*

```ruby
    myHash = Hash.new([])
    myHash[:one] << 2 #This will make myHash become: {:one => [2]}
    myHash[:two] << 3 #This will make myHash become: {:one => [2], :two => [3]}
```

In the above the values are added to arrays, as that's the datatype specified during the initialisation. This can be changed to any object type if needed.

*Example:*

`myHash = Hash.new {|hash, key| hash[key] = "" }  #String type`
`myHash = Hash.new {|hash, key| hash[key] = "".to_i } #String converted to integer`
`myHash = Hash.new {|hash, key| hash[key] = "".to_f } #String converted to float`

### fetch

*Usage:*

```ruby
hashObject.fetch(key_name)
hashObject.fetch(key_name, default_value)
hashObject.fetch(key_name) { |key| "default"} #if key_name doesn't exist run the supplied block and return the value (i.e. a default Hash object is returned then fetch'd)
```

### order

Hashes are cosidered unordered lists.

`{:two => 'two', :one => 'one'} == {:one => 'one', :two => 'two'}`

### methods

.keys : returns an Array of all the keys in they Hash
.keys.include?(key_name) : shows if a key exists in a Hash. **NOTE:** .include? is an Array method.

.values : returns an Array of all the values in they Hash
.values.include?(key_name) : shows if a value exists in a Hash. **NOTE:** .include? is an Array method.

.merge(hash_object) : returns current Hash with the Hash passed in, but does not alter current Hash.

## Booleans

### True or false

In Ruby, false is false, and nil is also false. Everything is is true. Such as 0, 1, [], {}, "", etc.

### Question marks

If a method ends in a question mark this means that a boolean is expected. i.e.:

`myObject.is_true?`

Will fail if a non-boolean value is returned.

## Strings

### Quotes

Double quotes ("") are used for Strings that need things parsed within.
Single quotes ('') are literals
Escaping : Backslashes are used to escape special characters.
Flexible quotes : and non-alphanumeric character after the % symbol makes a flexible quote.

*Example:*

```ruby
    %[this is a valid string]
    %~this is a valid string~
    %+this is a valid string+

    %+ They can
        also handle
        multiple
        lines +

    #Another way of doing multiple lines is via EOS (End of String):

    long_string = <<EOS
    This is the first line,
    this is the second line.
    EOS
```

### String methods

.split : splits the String into an Array of words, seperated by a token (space by default)
.split(/:/) : the above using ":" as a token
.join : joins an Array of words into a single string, seperating each with a token (space by default)

### Shovel operator (<<) in Strings

The shovel operator (<<)

## Symbols (:symbol)

A Symbol is an object type. It represents a location in memory, and this memory location is never changed. :my_symbol will always point to the same point.

Further info [see here](http://www.randomhacks.net.s3-website-us-east-1.amazonaws.com/2007/01/20/13-ways-of-looking-at-a-ruby-symbol/)

### Existing symbols

You can list all symbols in use with the statement:

```ruby
list_of_all_symbols_as_string = Symbol.all_symbols.map { |x| x.to_s }
puts list_of_all_symbols_as_string
```

### Converting strings to symbols

```ruby
    myString = "simon"
    myString.to_sym   #returns :simon

    mySymbol = :randomSymbol
    mySymbol.to_s       #returns "randomSymbol"  no :
```

## Objects and variables

## Methods

### Method structure

```ruby
    def myMethod(parameter1, parameter2, *otherParameters)
        #Do something
    end
```

Methods start with 'def' encompassing everything until it hits the 'end'.

### Calling methods

The above method can be called by
`myMethod(1,2,3)`
`myMethod 1,2,3`

### Arguments

The wrong number of arguments will cause a runtime error, it's not a syntax error. This is good to know when looking for the exception thrown. Usually it'll be ArgumentError

### Method return values

**TODO**  Check if this is right:
The last value returned is the method's return value.

Using the command 'return' explicity decides which value to return

```ruby

    def myMethod(a,b)
        :sym1
        return :sym2  #This is the return value
        :sym3
    end
```

When that return command isn't used, the last value is the return value.
The actual rule is "The last evaluated expression is returned"

```ruby

    def myMethod(a,b)
        :sym1
        :sym2  
        :sym3   #This is the return value
    end
```

### Check available methods

`myVariable.respond_to?(:method_name)`

This will return false, if the object of which myVariable is a type of doesn't have a method by the name 'method_name'

### Private methods

**TODO** Check below to see why it fails (I think it's because we've overridden the method with the symbol ??)
It looks like everything that comes after the 'private' keyword becomes private (not accessible from outside the object), and since the symbols point to the methods of the same name the method then become private.

```ruby
  def my_private_method
    "a secret"
  end
  private :my_private_method

  def test_calling_private_methods_with_an_explicit_receiver
    exception = assert_raise(NoMethodError) do
      self.my_private_method
    end
    assert_match /private method/, exception.message
  end
```

### Method arguments

```ruby
    def myMethod(arg1: 1, arg2: 2)
        [arg1, arg2]
    end
```

In the above, we can just call myMethod, and it'll return [1,2], but in the following

```ruby
    def myMethod(arg1, arg2: 2)
        [arg1, arg2]
    end
```

We'll get an error from calling myMethod, as there is no default for arg1 and it's expecting a value. ArgumentError will be thrown.

## Regular expressions

Regular expressions are Objects like everything else seems to be. The object type is Regexp. So default class types are like the following:

- 1 is Integer
- "Simon" is String
- \Hello\ is Regexp

**TODO:** Review the Regexp examples.

## Constants

In Ruby, any variable that starts with a capital letter is considered a constant.

**TODO** Look at scope when inheritence is used.

```ruby

    class MyClass

    end

    class MyOtherClass < MyClass # This class inherits from MyClass. Need to check what's inherited, and what's overridden.

    end
```

## Control statements

**TODO** practice 'unless' statements.

`unless a`

is the same as

`if a == false`

## Exceptions

Exceptions (error handlings).

```ruby
begin #Equivalent to try blocks in Java

rescue Exception => ex  #Like Java this will catch all exceptions
    ex.message #prints out the exception message
end
```

### Exception commands and methods

.ancestors : returns an Array that goes up the hierachy of Exceptions.

`raise`     - this raises an Excpetion object. Sytax is `raise "error message"` or `raise ExceptionObject, "error message"`
`fail`      - acts like a raise but throws error message, best thrown when things aren't running as they should.
`rescue`    - like "catch" in Java, it'll listen out for Exceptions of a certain type.
`ensure`    - a block of code that always runs during the Exception process.

Exceptions can be created on the fly. i.e.:

`raise MySpecialException.new("Special error message")`

## Iterating

Arrays have a method called `.each` it will go through each element of the array and perform an action as described after the `do`

*Example:*

```ruby
    array = [1,2,3,4,5]
    sum = 0
    array.each { |item| sum += item}
    puts sum
```

In the above example " |item| " is a temporary variable name we use for the values that come out.
If we were to do more names like " |item1,item2| " will do 2 elements at a time.

`.break` - You cat put a break condition in the iterations to stop it going to the end, if there isn't a need to.

```ruby
    array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    sum = 0
    array.each do |item|
      break if item > 3
      sum += item
    end
```

`.collect` - Used to make a transformation to each element in the collection
`.map` - does the same as `.collect`

```ruby
    array = [1, 2, 3]   # [1,2,3]
    new_array = array.collect { |item| item + 10 } # [11,12,13]
```

`.select` - deletes elements that don't match the boolean codition following.
`.find_all` - does the same as above.

`.find` - returns the first element that matches the condition

`.inject`  - Combins enum and binary operation.
*More info:* [See here](https://ruby-doc.org/core-2.3.1/Enumerable.html#method-i-inject)

## Blocks

`yield` processes the code block that was passed in.
*Example:*
```ruby
    def method_using_block
        yield
    end

    method_using_block { puts "Hello" }

    method_using_block do puts "Hello" end  # do and end can be used instead of { }
```
The above code will print out the string "Hello".

You can test whether a block has been passed in or not with the boolean check `block_given?` this returns false if a block hasn't been passed in.

```ruby

    def block_test
        if block_given?
            yield
        else
            :no_block
        end
    end

    block_test # This returns :no_block
    block_test { 1 + 1} # This returns 2
```

