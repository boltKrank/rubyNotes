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

## Exceptions

```ruby
begin #Equivalent to try blocks in Java

rescue Exception => ex  #Like Java this will catch all exceptions
    ex.message #prints out the exception message
end
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

### Accessing values

Values can be accessed by directly inputing their element index, or using methods such as `.first` and `.last`

### Positive and negative indexes

If the index is positive, it counts from the begining of the array, i.e.: [0,1,2,3]

If the index is negative, it counts from the end of the array, i.e: [-4,-3,-2,-1]

### Slicing arrays

When passing in 2 indexes to access an array, it returns a subset as follows:

`myArray[<starting_element>, <count>]`, it will add `<count>` elements starting from `<starting_element>` unless the array is smaller then it will go to the last element.

NOTE: if the `<starting_element>` is greater than the length of the array, it will return `nil`
