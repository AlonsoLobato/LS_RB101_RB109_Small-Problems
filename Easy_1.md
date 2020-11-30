##  RB101-RB109 - Small Problems --> EASY 1

**This set of exercises are solved using a PEDAC approach**

### Exercise 1: Repeat yourself

Write a method that takes two arguments, a string and a positive integer, and prints the string as many times as the integer indicates.

#### My answer

##### Rules / requirements
- Define a method
- With two arguments
  - a string
  - a positive integer
- Print the string 'integer' number of times  

##### Examples
```ruby
string: 'hello', integer: 2 --> 'hello' 'hello'
string: 'good bye', integer: 3 --> 'goodbye' 'goodbye' 'goodbye'
```
```ruby
repeat('Hello', 3) --> 'Hello' 'Hello' 'Hello'
```

#### Data Structure
- String and integer for input
- String for output

#### Algorithm
1. Define a 'repeat' method
2. Method takes two arguments
  - a string and a integer (number)
3. Print the string in the screen 'integer' the number of times
4. Return the result of the multiplication

#### Code
```ruby
def repeat(str, number)
  number.times do
    puts str
  end  
end

repeat('Hello', 3)
repeat('Goodbye', 6)
```

==================================================================

### Exercise 2: Odd

Write a method that takes one integer argument, which may be positive, negative, or zero. This method returns true if the number's absolute value is odd. You may assume that the argument is a valid integer value.

Examples:
```ruby
puts is_odd?(2)    # => false
puts is_odd?(5)    # => true
puts is_odd?(-17)  # => true
puts is_odd?(-8)   # => false
puts is_odd?(0)    # => false
puts is_odd?(7)    # => true
```

Keep in mind that you're not allowed to use `#odd?` or `#even?` in your solution.

#### My answer

##### Rules / requirements
- Define a `is_odd?` method
- It takes one integer as argument
  - Argument can be `>0`, `<0` or `==0`
- Method returns `true` if input integer abosulute value is odd, `false` otherwise
- Assume argument is valid
- `#odd?` and `#even?` methods are not allowed in the solution!

**Questions**
- what does it mean absolute value of a number?
  - how far this number is from 0
  - e.g.: 6 and - 6 are 6 away from zero, so its absolute value is 6
- so in practice the absolute value is the positive version of the number itself  

##### Examples
*Given in the problem description*

#### Data Structure
- integer for input
- boolean for output

#### Algorithm
1. Define method `is_odd?`
2. Pass one integer as argument
3. Transform the integer to its positive form
  - if number is positive remain the same
  - if number is negative
    - add its value twice to transform it to its positive form  
4. Determine if argument is odd or even
  - number is even if remainder is cero when divided by 2 
  - odd otherwise
5. Return boolean result

#### Code
```ruby
def is_odd?(number)
  if number < 0
    number = number + number + number  
  end
  if number % 2 != 0
    return true
  else
    return false
  end     
end

# test cases
puts is_odd?(2)    # => false
puts is_odd?(5)    # => true
puts is_odd?(-17)  # => true
puts is_odd?(-8)   # => false
puts is_odd?(0)    # => false
puts is_odd?(7)    # => true
```

#### School answer
```ruby
def is_odd?(number)
  number % 2 == 1
end
```

##### NOTES 
- School solution doesn't bother to check if number is positive or negative, it just perform the Ruby modulo operator against 1, which returns `true` or `false`. Much more shorter than my solution :(
- To determine if a number is odd without using `#odd?` or `#even?`, we must check whether the number modulo 2 is 1. In Ruby, we use `%` to perform modulo operations, so we use it here to determine whether the number is odd.
- To determine if the absolute value is `even` is sufficient to check the modulo against 0, instead of 1 (division remaind zero)

#### Further exploration
- Careful with modulo operator `%`! In Ruby it handle negative values with no problem, but other prog languages use remainder operator, which doesn't handle negative numbers as easily.
- Rewrite `#is_odd?` to use `Integer#remainder` instead of `%`. 

```ruby
def is_odd?(number)
  number.remainder(2) != 0
end
```

==================================================================

### Exercise 3: List of digits

Write a method that takes one argument, a positive integer, and returns a list of the digits in the number.

Examples:

```ruby
puts digit_list(12345) == [1, 2, 3, 4, 5]     # => true
puts digit_list(7) == [7]                     # => true
puts digit_list(375290) == [3, 7, 5, 2, 9, 0] # => true
puts digit_list(444) == [4, 4, 4]             # => true
```

#### My answer

##### Rules / requirements
- Define a `digit_list` method
- Method takes one argument
- Argument is a positive integer `number`
- Return a list (array) of each digit in `number`

**Questions**
- May I assume input is always valid?
  - Valid equals positive integer  

##### Examples
*Given in the problem description*

#### Data Structure
- Integer as input
- Array of integers as output

#### Algorithm
1. Define method `digit_list`
2. Pass a positive integer `number` as argument
3. Determine number of digits in `number`
  - Iterate over `number` and access each of its digits
  - Use a loop and counter for iteration?
  - Integer must be transform to string to apply `lenght` and `[]` methods
  - Expected output is array of integers
    - transform elements of array from strings to integers
4. Declare empty array  
5. Add each digit to an array
6. Return the array
  - must be an array of integers

#### Code
```ruby
def digit_list(number)
  digits = []
  counter = 0
  while counter < number.to_s.length
    digits << number.to_s[counter].to_i
    counter +=1
  end
  digits
end

puts digit_list(12345) == [1, 2, 3, 4, 5]     # => true
puts digit_list(7) == [7]                     # => true
puts digit_list(375290) == [3, 7, 5, 2, 9, 0] # => true
puts digit_list(444) == [4, 4, 4]             # => true
```

#### School answer
```ruby
def digit_list(number)
  number.to_s.chars.map(&:to_i)
end
```

##### NOTES 
- Our goal is to convert a number to a list of its digits. 
- First, we convert the number to a string, then split it into an array of numeric characters. 
- This array is almost what we want, but we need an array of numbers, not an array of strings. `Enumerable#map` comes to the rescue. 
- You might find the `(&:to_i)` part weird, but this is Ruby syntactic sugar; it's shorthand for:
```ruby
something.map { |char| char.to_i }
```

- Another Rubyist solution, more simple than the one provided would be:
```ruby
def digit_list(number)
  number.digits.reverse
end
```

==================================================================

### Exercise 4: How Many?

Write a method that counts the number of occurrences of each element in a given array.

```ruby
vehicles = [
  'car', 'car', 'truck', 'car', 'SUV', 'truck',
  'motorcycle', 'motorcycle', 'car', 'truck'
]

count_occurrences(vehicles)
```

The words in the array are case-sensitive: `'suv' != 'SUV'`. Once counted, print each element alongside the number of occurrences.

Expected output:

```ruby
car => 4
truck => 3
SUV => 1
motorcycle => 2
```

#### My answer

##### Rules / requirements
- Define a method `count_ocurrences`
- Take an array as argument
- The method counts number occurrences of each elements of the array
- Words in the array are case sensitive (`suv` and `SUV` are different elements)
- The output is a key value pair
  - key is the word
  - value the number of occurrences

##### Examples
*Given in the problem description*

#### Data Structure
- Array of strings as input data
- Hash as output data
  - Symbols as keys
  - Integers as values 

#### Algorithm
1. Define `count_ocurrences` method
2. Pass in an array of strings as argument
3. Iterate over each element in array
  - Use some kind of loop or iterator (**I need to be more specific here**)
4. Count the number of times each element is present in array
  - Words with same characters but with different cases are considered different elements of array
5. Create a hash
 - Add Keys --> elements of array converted to symbols
 - Add values --> number of repetition of each element
6. Return the hash and output it to screen  

#### Code
```ruby
vehicles = [
  'car', 'car', 'truck', 'car', 'SUV', 'truck',
  'motorcycle', 'motorcycle', 'car', 'truck'
]

def count_occurrences(collection)
  ocurrences = {}

  collection.each do |element|
    ocurrences[element] = collection.count(element)
  end

  ocurrences.each do |key, value|
    puts "#{key} => #{value}"
  end
end

count_occurrences(vehicles)
```

#### Other student answer
```ruby
def count_case_sensitive_occurrences(array)
  occurrences = Hash.new(0)
  array.each { |el| occurrences[el.downcase] += 1 }
  occurrences.each { |k, v| puts "#{k} => #{v}" }
end

count_case_sensitive_occurrences(vehicles)
```

##### NOTES 
- For this exercise, we take advantage of the `Hash.new(0)` shortcut which sets default value for any key to `0`. If we do not pass 0 as a default value, keys will be initialized as `nil`, which cannot utilize the `+` operator. Remember that `Hash.new` is similar to `{}`.
- The `String#downcase` method makes this method case insensitive (`"suv" == "SUV"`)

==================================================================

### Exercise 5: Reverse it (part 1)

Write a method that takes one argument, a string, and returns a new string with the words in reverse order.

Examples:

```ruby
puts reverse_sentence('') == ''
puts reverse_sentence('Hello World') == 'World Hello'
puts reverse_sentence('Reverse these words') == 'words these Reverse'
```

#### My answer

##### Rules / requirements
- Define a method `reverse_sentence`
- Method takes one argument
- Argument is a string
- Return a new string
- New string contains words in reverse order
  - words means space-separate characters in input string
  - reverse order means word in last position will interchage with word in first place, word before last will interchange with second word, etc. 
  - word in the middle stay unchanged

##### Examples
*Given in the problem description*

#### Data Structure
- String as input
  - string may be made up of several space-separated words
- New string as output

#### Algorithm
1. Define `reverse_sentence` method
2. Pass in a string as argument
3. Create a new string to store re-ordered input string
4. Iterate over the input string
  - Determine number of words
    - we can use `String#split` method to convert string into array, which is easier to iterate by elements
    - we can use `Array#join(' ')` method to convert array into string
  - Determine position of every word
  - Reverse the order of words (first by last, second by second to last, third by third to last, etc.)
    - if string has odd number of words, the word in the middle stay unchanged
  - Add words in new order to new string
5. Return new string    

#### Code
```ruby
def reverse_sentence(string)
  array_of_words = string.split
  reverse_array_of_words = array_of_words.reverse
  reverse_array_of_words.join(' ')
end
```

#### School answer
```ruby
def reverse_sentence(string)
  string.split.reverse.join(' ')
end
```

##### NOTES 
- Note how the school solution uses the same built-in methods but they chained them all in one single line of code
- Remember that when we chain methods what one returns is used by the next as argument.

==================================================================

### Exercise 6: Reverse it (part 2)

Write a method that takes one argument, a string containing one or more words, and returns the given string with words that contain five or more characters reversed. Each string will consist of only letters and spaces. Spaces should be included only when more than one word is present.

Examples:

```ruby
puts reverse_words('Professional')          # => lanoisseforP
puts reverse_words('Walk around the block') # => Walk dnuora the kcolb
puts reverse_words('Launch School')         # => hcnuaL loohcS
```

#### My answer

##### Rules / requirements
- Define a method `reverse_words`
- Method takes one argument
- Argument is a string with one or more words
  - words are chains of characters space-separated
- Reverse words that are 5 or more characters long
  - Reversed words interchange their characters place: first goes last, second goes second to last, etc.
- Input strings will only contain letters and spaces
- Spaces should be considered when more than one word in present in input string
- Return reverse version of input string  

##### Examples
*Given in the problem description*

#### Data Structure
- String as input
- New string as output
- Array of strings to temporary store words

#### Algorithm
1. Define `reverse_words` method
2. Pass in a string as argument
3. Count number of words (space-separated chains of characters) in string
  - Try with `String#split` method to convert string into array, which is easier to iterate by elements
4. Count number of characters in each word
  - Try with `Array#[]` method to iterate over indexes 
  - If number of chars is => 5
    - Reverse the order of chars in word
5. Return reverse version of string   

#### Code
```ruby
def reverse_words(string)
  array_of_words = string.split
  array_of_words.each do |word|
    word.reverse! if word.length >= 5
  end
  array_of_words.join(' ')
end
```

==================================================================

### Exercise 7: Stringy Strings

Write a method that takes one argument, a positive integer, and returns a string of alternating 1s and 0s, always starting with 1. The length of the string should match the given integer.

Examples:
```ruby
puts stringy(6) == '101010'     #=> true
puts stringy(9) == '101010101'  #=> true
puts stringy(4) == '1010'       #=> true
puts stringy(7) == '1010101'    #=> true
```

#### My answer

##### Rules / requirements
- Define a method
- Method takes one argument
- Argument to be a positive integer
- Create a string of alternative 1s and 0s
- String always start by 1
- Length of that string is integer passed as argument to method
- String finishes by whichever digit (0-1) correspond to the end

##### Examples
*Given in the problem description*

#### Data Structure
- Integer as input
- String of 0s and 1s as output

#### Algorithm
1. Define `stringy` method
2. Pass in an integer `int` as argument
3. Create a new string of length `int` made of 1 and 0 alternatively
  - Create new empty string
  - Initialise a counter for iteration
  - Loop through the string 
    - Add 1 in the first position 
    - Add 0 in the second position
    - Add 1 in the third position
    - ...
      - Add 1 in even positions of string and 0 in odd positions of string
    - Break if length of string equals `int`
4. Return the resulting string

#### Code
```ruby
def stringy(int)
  string = ''
  counter = 0
  while string.length < int
    counter.even? ? string += '1' : string += '0'
    counter += 1
  end
  string  
end
```

#### School answer
```ruby
def stringy(size)
  numbers = []

  size.times do |index|
    number = index.even? ? 1 : 0
    numbers << number
  end

  numbers.join
end
```

##### NOTES 
- We use `#times` to iterate based on the number indicated by `size`. For each iteration, we use the `index` block parameter in a conditional to determine if the current number is even or odd. Since `#times` starts counting from 0, we know that the first number will be even. Knowing this, we can write our conditional to return `1` if index is even and `0` if index is odd.
- We assign that value to a variable and, on the next line, we add it to an array, `numbers`. After `#times` has finished iterating, we're left with an array filled with 1s and 0s in the correct order. Now, all we have to do is invoke `numbers.join` to return the desired output.

#### Further exploration
Modify `stringy` so it takes an additional optional argument that defaults to `1`. If the method is called with this argument set to `0`, the method should return a String of alternating 0s and 1s, but starting with `0` instead of `1`.

#### Code
```ruby
def stringy(int, default = 1)
  string = ''
  counter = 0
  while string.length < int
    if default == 1
      counter.even? ? string += '1' : string += '0'
    elsif default == 0
      counter.even? ? string += '0' : string += '1'
    end
    counter += 1
  end
  string
end

puts stringy(9) == '101010101'  #=> true
puts stringy(4, 0) == '0101'       #=> true
```

==================================================================

### Exercise 8: Array Average

Write a method that takes one argument, an array containing integers, and returns the average of all numbers in the array. The array will never be empty and the numbers will always be positive integers. Your result should also be an integer.

Examples:

```ruby
puts average([1, 6]) == 3 # integer division: (1 + 6) / 2 -> 3    #=> true
puts average([1, 5, 87, 45, 8, 8]) == 25                          #=> true
puts average([9, 47, 23, 95, 16, 52]) == 40                       #=> true
```

#### My answer

##### Rules / requirements
- Define a method
- Method takes one argument
- Argument is an array of integers
- Return the average of all numbers in that array
- Input array will never be empty
- Integers in input array will always be positive
- Return must be integer

##### Examples
*Given in the problem description*

#### Data Structure
- Array of integers as input
- Integer as output

#### Algorithm
1. Define `average` method
2. Pass in one argument
  - Argument is an array of positive integers
3. Iterate over int elements of array
  - Use built-in method
  - alternatively use counter, loop and access by index
4. Calculate average of all integers
  - int 1 + int 2 + int 3 + ... divided by total number of ints  
5. Return an integer as solution

#### Code
```ruby
# version using an iterator
def average(array)
  sum = 0
  array.each do |number|
    sum += number
  end
  average = sum / array.length
end

# Rubyist version using Array#sum built-in method
def average(array)
  array.sum / array.length
end
```

#### Further exploration
How to make the result a float number?

- In the first version initialise `sum` as `sum = 0.0`
- In the second version call `to_f` in `array.sum` as `array.sum.to_f`
- To round the number of decimal digits use numeric method `round(number_decimals_desired)`

==================================================================

### Exercise 9: Sum of Digits

Write a method that takes one argument, a positive integer, and returns the sum of its digits.

Examples:

```ruby
puts sum(23) == 5           # => true
puts sum(496) == 19         # => true
puts sum(123_456_789) == 45 # => true
```

For a challenge, try writing this without any basic looping constructs (while, until, loop, and each).

#### My answer

##### Rules / requirements
- Write a method
- Method takes one argument
- Argument to be a positive integer
- Sum digits of that integer
- Return the result

##### Examples
*Given in the problem description*

#### Data Structure
- Integer as input
- Integer as output

#### Algorithm
1. Define `sum` method
2. Pass in an integer as argument
3. Loop over the integer digit
  - Don't use while, loop, until, each, etc.
4. Sum all digits together
5. Return the sum

#### Code
```ruby
# Rubyist solution
def sum(int)
  sum = 0
  int.digits.each {|digit| sum += digit}
  sum
end

# Rubyist solution without basic loop constructs
def sum(int)
  int.digits.sum
end
```

#### School answer
```ruby
def sum(number)
  number.to_s.chars.map(&:to_i).reduce(:+)
end
```

##### NOTES 
- First convert the integer to string with `to_s`
```ruby
23.to_s # => '23'
```
- Then convert it to an array with `chars` or `split('')`
```ruby
23.to_s.chars # => ['2', '3']
```
- Then convert the array of strings into an array of integers with `map(&:to_i)`
```ruby
['2', '3'].map(&:to_i) # => [2, 3]
```
- Notice that `map(&:to_i)` is equals to: 
```ruby
["2", "3"].map { |element| element.to_i } # => [2, 3]
```
- Now add all the elements of the string with `reduce(:+)`
```ruby
number.to_s.chars.map(&:to_i).reduce(:+)
```
- Notice that all these methods can be invoked in one line, as each one uses the return value of its predecesor

==================================================================

### Exercise 10: What's my Bonus?

Write a method that takes two arguments, a positive integer and a boolean, and calculates the bonus for a given salary. If the boolean is `true`, the bonus should be half of the salary. If the boolean is `false`, the bonus should be `0`.

Examples:
```ruby
puts calculate_bonus(2800, true) == 1400    #=> true
puts calculate_bonus(1000, false) == 0      #=> true
puts calculate_bonus(50000, true) == 25000  #=> true
```

#### My answer

##### Rules / requirements
- Write a method
- Method takes two arguments
  - Argument one is a positive integer
  - Argument two is a boolean (true / false)
- If argument two is true, divide argument one by 2
- If argument two is false, return 0 
- Return the result    

##### Examples
*Given in the problem description*

#### Data Structure
- Integer and boolean as input
- Integer as ooutput

#### Algorithm
1. Define `calculate_bonus` method 
2. Pass in two argument
  - A positive integer
  - A valid boolean value: true or false
3. If boolean is true, divide the positive integer by 2 and return
4. If boolean is false, return 0
5. Return the value

#### Code
```ruby
def calculate_bonus(salary, bonus)
  if bonus == true
    salary / 2
  else
    0
  end
end
```

#### School answer
```ruby
def calculate_bonus(salary, bonus)
  bonus ? salary / 2 : 0
end
```

##### NOTES 
- Same logic as my solution but takes advantage of ternary operator
