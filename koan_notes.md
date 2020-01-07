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

###

