##  RB101-RB109 - Small Problems --> EASY 3

**This set of exercises are solved using a PEDAC approach**

### Exercise 1: Searching 101

*This exercise was solved at a study session with Nicolas* 

Write a program that solicits 6 numbers from the user, then prints a message that describes whether or not the 6th number appears amongst the first 5 numbers.

Examples:

```ruby
==> Enter the 1st number:
25
==> Enter the 2nd number:
15
==> Enter the 3rd number:
20
==> Enter the 4th number:
17
==> Enter the 5th number:
23
==> Enter the last number:
17
The number 17 appears in [25, 15, 20, 17, 23].


==> Enter the 1st number:
25
==> Enter the 2nd number:
15
==> Enter the 3rd number:
20
==> Enter the 4th number:
17
==> Enter the 5th number:
23
==> Enter the last number:
18
The number 18 does not appear in [25, 15, 20, 17, 23].
```

#### Nicolas and I answer

##### Input / Output
- Input: 6 integers
- Output: string, including an interpolated array with 5 elements

##### Rules / requirements
- Request user six times to input an integer
- prompt starts with "==>"
- update prompt according to the order of the requested integer (1st, 2nd,...)
- the first five numbers should be appended to an array
- Output a msg that indicates if the last entered integer exists in the array 
- Output msg is a string with the array interpolated 

##### Questions
- Should the input always be integers? 
  - Yes
- Should we check if the input is valid? 
  - No, assume that input is valid integer
- What if the input is 0 or negative? 
  - No problem, these will also be considered integers

##### Examples
*Given in the problem description*

#### Data Structure
- Integers as input
- String as output
- Array to temporarily store integers

#### Algorithm
Set integers_array = []

Do 5 times:
  - get_integer from user
  - append integer to integers_array

get_integer from user
- check if integer is within integers_array 
- output string saying whether integer is within integers_array or not

Get integer from user
- pass a word to interpolate to the prompt msg
- promt a msg that says: ==> Enter the #{word} number:
- initialize user_input with the user's input as its value 
- convert user_input to integer
- return user_input

Get word to add to prompt
  - create a words_hash with numbers pointing to words
    for example: 0 => '1st', 1 => '2nd', etc.
  - check for the length of integers_array and use the return value as key for the hash

#### Code
```ruby
WORDS = { 
          0 => '1st', 
          1 => '2nd', 
          2 => '3rd', 
          3 => '4th', 
          4 => '5th', 
          5 => 'last' 
        }

INTEGERS_ARRAY = []


def get_input(key)
  word = WORDS[key]
  prompt ("Enter the #{word} number:")
  gets.chomp.to_i
end

def prompt(string)
  puts "==> #{string}"
end

def display_output(last)
  connector = INTEGERS_ARRAY.include?(last) ? "appears" : "does not appear"
  prompt("The number #{last} #{connector} in #{INTEGERS_ARRAY}.")
end

key = 0
5.times do
  INTEGERS_ARRAY << get_input(key)
  key += 1
end

last = get_input(key)

display_output(last)
```

#### School answer
```ruby
numbers = []

puts "Enter the 1st number:"
numbers << gets.chomp.to_i
puts "Enter the 2nd number:"
numbers << gets.chomp.to_i
puts "Enter the 3rd number:"
numbers << gets.chomp.to_i
puts "Enter the 4th number:"
numbers << gets.chomp.to_i
puts "Enter the 5th number:"
numbers << gets.chomp.to_i
puts "Enter the last number:"
last_number = gets.chomp.to_i

if numbers.include? last_number
  puts "The number #{last_number} appears in #{numbers}."
else
  puts "The number #{last_number} does not appear in #{numbers}."
end
```

------------------------

### Exercise 2: Arithmetic Integer

*This exercise was solved at a study session with Nicolas* 

Write a program that prompts the user for two positive integers, and then prints the results of the following operations on those two numbers: addition, subtraction, product, quotient, remainder, and power. Do not worry about validating the input.

Example:
```ruby
==> Enter the first number:
23
==> Enter the second number:
17
==> 23 + 17 = 40
==> 23 - 17 = 6
==> 23 * 17 = 391
==> 23 / 17 = 1
==> 23 % 17 = 6
==> 23 ** 17 = 141050039560662968926103
```

##### Input / Output: given input and desired output

- Input: 2 integers from user
- Output: 6 strings (results of 6 different math operations) with integers interpolation

##### Rules / requirements: understanding of the problem

- Ask user to input 2 integers
- Don't need to validate input
- We are only working with positive integers (no 0 or negative)
- Prompts should be precedded by ==>
- Print out the result of six operations with input integers: addition, subtraction, product, quotient, remainder, and power; in that order.
- Output the results as a full arithmetic operation as strings with integers interpolated

##### Questions: what's not clear in the problem description

##### Examples: test cases, edge cases
- Given with the problem description

##### Data Structures: used to obtain the desired solution
- Integers as input
- Array to store operation symbols as strings
- String with interpolated integers as output

##### Algorithm: pseudocode of different levels of abstraction
- Declare var `operators` = ["+", "-", "*", "/", "%", "**"]
- get_input from user and store in `input_one` or `input_two` accordingly
  
input_one = get_input("first")

get_input:
- it takes one argument (a string)
- prompt that string
- get input
- return the input converted to integer

prompt:
- it takes one argument (a string)
- prepend that string with "==> "
- puts string

##### Code: translating the proposed algorithm to code
```ruby
def prompt(msg)
  puts "==> #{msg}"
end

def get_input(string)
  prompt("Enter the #{string} number:")
  gets.chomp.to_i
end

first_num = get_input("first")
second_num = get_input("second")

operators = ["+", "-", "*", "/", "%", "**"]

operators.each do |operator|
  prompt("#{first_num} #{operator} #{second_num} = " + 
         first_num.method(operator).call(second_num).to_s)
end
```

------------------------

### Exercise 3: Counting the Number of Characters

Write a program that will ask a user for an input of a word or multiple words and give back the number of characters. Spaces should not be counted as a character.

input:
`Please write word or multiple words: walk`

output:
`There are 4 characters in "walk".`

input:
`Please write word or multiple words: walk, don't run`

output:
`There are 13 characters in "walk, don't run".`

##### Input / Output: given input and desired output
- Input: String
- Output: String with interpolated integer

##### Rules / requirements: understanding of the problem
- Ask user to enter a string of one or more words
- Output the number of char in user string, interpolated into a string
- Don't count blank spaces

##### Examples: test cases, edge cases
- Given with the problem statement

##### Data Structures: used to obtain the desired solution
- String

##### Algorithm: pseudocode of different levels of abstraction
- Prompt user to enter a string
- Count number of characters in string
- Output the number of charactes in string interpolated in a string

##### Code: translating the proposed algorithm to code

```ruby
puts "Please write word or multiple words:"
input_string = gets.chomp

num_chars = input_string.chars.count{|char| char != ' '}
puts "There are #{num_chars} characters in '#{input_string}'"
```

------------------------

### Exercise 4: Multiplying Two Numbers

Create a method that takes two arguments, multiplies them together, and returns the result.

Example:
```ruby 
multiply(5, 3) == 15
```
##### Input / Output: given input and desired output
- Input: Integers
- Output: Integer

##### Rules / requirements: understanding of the problem
- Define a method that multiply two integers passed in as arguments

##### Examples: test cases, edge cases
- Given with the problem description

##### Data Structures: used to obtain the desired solution
- Integer

##### Algorithm: pseudocode of different levels of abstraction
- Define a method `multiply`
- Method takes two arguments: 2 integers
- Return the result of multiplying the two arguments
- Output the result to screen

##### Code: translating the proposed algorithm to code
```ruby
def multiply (a, b)
  a * b
end

puts multiply(5, 3)
```

------------------------

### Exercise 5: Squaring an Argument

Using the multiply method from the "Multiplying Two Numbers" problem, write a method that computes the square of its argument (the square is the result of multiplying a number by itself).

Example:
```ruby
square(5) == 25
square(-8) == 64
```

##### Code:
```ruby
def multiply(a, b)
  a * b
end

def square(a)
  multiply(a, a)
end
```

##### Further exploration:
What if we wanted to generalize this method to a "power to the n" type method: cubed, to the 4th power, to the 5th, etc. How would we go about doing so while still using the multiply method?

```ruby
def to_n_power(a, power)
  multiply(a, 1) ** power
end
```

###### Nico's solution
```ruby
def power_to_the_n(num, power)
  result = power == 0 ? 1 : num
  
  (power.abs - 1).times do
    result = multiply(result, num)
  end

  power < 0 ? 1r/result : result
end
```

------------------------

### Exercise 6: Exclusive Or

The `||` operator returns a truthy value if either or both of its operands are truthy, a falsey value if both operands are falsey. The `&&` operator returns a truthy value if both of its operands are truthy, and a falsey value if either operand is falsey. This works great until you need only one of two conditions to be truthy, the so-called exclusive or.

In this exercise, you will write a function named `xor` that takes two arguments, and returns true if exactly one of its arguments is truthy, `false` otherwise. Note that we are looking for a boolean result instead of a truthy/falsy value as returned by `||` and `&&`.

Examples:
```ruby
xor?(5.even?, 4.even?) == true
xor?(5.odd?, 4.odd?) == true
xor?(5.odd?, 4.even?) == false
xor?(5.even?, 4.odd?) == false
```

##### Input / Output: given input and desired output
- Integer as input
- Boolean as ouput

##### Rules / requirements: understanding of the problem
- Method that takes two arguments
- Both args are integers method calls that return a boolean
- Our method must return true ONLY if ONE of the two arguments return true
- Our method must return false if both arguments return true or both return false

##### Algorithm: pseudocode of different levels of abstraction
- Define a method `xor` that takes two arg
- The args can be the int method odd? or even?
- `xor?` will return
  - `true` if either `odd?` or `even?` return true (not both)
  - `false` otherwise

##### Code: translating the proposed algorithm to code
```ruby
def xor?(a, b)
  if (a == true && b == false) || (a == false && b == true)
    return true
  elsif (a == true && b == true) || (a == false && b == false)
    return false    
  end
end
```

------------------------

### Exercise 7: Odd lists

Write a method that returns an Array that contains every other element of an Array that is passed in as an argument. The values in the returned list should be those values that are in the 1st, 3rd, 5th, and so on elements of the argument Array.

Examples
```ruby
oddities([2, 3, 4, 5, 6]) == [2, 4, 6]
oddities([1, 2, 3, 4, 5, 6]) == [1, 3, 5]
oddities(['abc', 'def']) == ['abc']
oddities([123]) == [123]
oddities([]) == []
```

##### Input / Output: given input and desired output
- Input: array 
- Output: array containing every other element of input starting at index 0 or an empty arr 

##### Rules / requirements: understanding of the problem
- Input arr can contain any type of obj or a mix of themm, or can also be empty
- We'll output an arra anyway
- The returning array is a new array

##### Questions: what's not clear in the problem description
- can arrays contain different types of objects?  || YES
- do we mutate input array or produce/return a new one? || New one
- 

##### Examples: test cases, edge cases
- given with the problem statement

##### Data Structures: used to obtain the desired solution
- arrays

##### Algorithm: pseudocode of different levels of abstraction
- define `oddities` method that takes an array as arg
- create an emtpy array `even_elements` and assigned it to []
- iterate over the array 
  - access every even element
  - store in `even_elements` the elements accessed at iteration step
- return the new array

- iteration
  - input_arr.select {element.even?}
  - if true append to even_elements

##### Code: translating the proposed algorithm to code

##### solution 1: Alonso
```ruby
def oddities(arr)
  
  index = -1
  
  arr.select do |elem| 
    index += 1
    index.even?
  end
end
```

##### solution 2: Nico

```ruby
def oddities(arr)
  arr.select.with_index do |_, index| 
    index.even?
  end
end
```

------------------------

### Exercise 8: Palindromic Strings (Part 1)

Write a method that returns true if the string passed as an argument is a palindrome, false otherwise. A palindrome reads the same forward and backward. For this exercise, case matters as does punctuation and spaces.

```ruby
palindrome?('madam') == true
palindrome?('Madam') == false          # (case matters)
palindrome?("madam i'm adam") == false # (all characters matter)
palindrome?('356653') == true
```

##### Problem
- Method to detect palindrome strings from input.
- Palindrome is a string that reads the same forward and backward.
- Punctuation, spaces, symbols and spaces count
- Case also count

##### Input/output
- String as input
- Boolean as output: true if palindrome, false otherwise

##### Examples
- given with the problem statement

##### Pseudocode
- Input string divide by two
- Take second half and read it from last to first char (reverse)
- Compare two halves
  - if equal --> palindrome true
  - else --> palindrome false
  
##### Code
```ruby
def palindrome?(str)
  if str.length.odd?
    str[0..str.length/2] == str[str.length/2..-1].reverse
  else
    str[0...str.length/2] == str[str.length/2..-1].reverse
  end
end
```

##### School answer
```ruby
def palindrome?(string)
  string == string.reverse
end
```

##### Further exploration
1. Write a method that determines whether an array is palindromic; that is, the element values appear in the same sequence both forwards and backwards in the array. 
2. Now write a method that determines whether an array or a string is palindromic; that is, write a method that can take either an array or a string argument, and determines whether that argument is a palindrome. 

You may not use an `if`, `unless`, or `case` statement or modifier.

##### Problem
1. determine if an array object is a palindrome considering its elements
2. determine if either an array or a string are a palindrome (any input)

##### Input/output
1. input array / output boolean
2. input array or string / output boolean

##### Examples
```ruby
palindrome?(['a', 'b', 'c', 'b', 'a']) == true
palindrome?([1, 2, 3, 2, 1]) == true
palindrome?([1, 2, 4, 6, 8]) == false
palindrome?('madam') == true
palindrome?('Madam') == false
```
##### Pseudocode
- Input array and divide by two
- Take second half and read it from last to first char (reverse)
- Compare two halves
  - if equal --> palindrome true
  - else --> palindrome false
- In this case, instead of reverse, we sort the input from last to first  

##### Code
```ruby
def palindrome?(input)
  if input.is_a?(String)
    input_to_arr = input.chars
    reversed_input = input_to_arr.sort{ input_to_arr.last <=> input_to_arr.first }
    input_to_arr == reversed_input
  elsif input.is_a?(Array)
    reversed_input = input.sort{ input.last <=> input.first }
    input == reversed_input
  end
end
```

------------------------

### Exercise 9: Palindromic Strings (Part 2)

Write another method that returns true if the string passed as an argument is a palindrome, false otherwise. This time, however, your method should be case-insensitive, and it should ignore all non-alphanumeric characters. If you wish, you may simplify things by calling the `palindrome?` method you wrote in the previous exercise.

```ruby
real_palindrome?('madam') == true
real_palindrome?('Madam') == true           # (case does not matter)
real_palindrome?("Madam, I'm Adam") == true # (only alphanumerics matter)
real_palindrome?('356653') == true
real_palindrome?('356a653') == true
real_palindrome?('123ab321') == false
```

##### Problem
Return true/false if input string is a palindrome

##### Rule
- method is case insensitive (Madam and madaM are a palindrome - true)
- all non alphanumeric chars are ignored
- palindrome is: a string that can be read in the same way in both direction: begin to end and reverse
- strings of numbers are also considered

##### Data structure
- input string
- output boolean

##### Pseudocode

0) Convert input into array so I can work with indexes...
  - input.chars -> return every char in array

1) Iterate the given input and remove all non alpha chars
  - Use select method and pass alpha == true as block condition
  - Store return new array as clean array


2) Divide the input string in two equal parts, reverse the second and compare it with first
  - clean_array.lenght / 2
    - index[0]up to lenght/2 - 1 -> half input
  - if equals return true
  - otherwise return false

##### Code
```ruby
def clean_array(str)
  chars_array = str.chars                                                   # convert input into array
  # alphanumeric = (('a'..'z').to_a + ('A'..'Z').to_a + ('0'..'9').to_a)     
  alphanumeric = [*?a..?z, *?A..?Z, *'0'..'9']                              # array of alphabetical chars
  
  chars_array.select do |char|                                              # retuns arr with only alphanumeric chars in input
    alphanumeric.include?(char)                                             
  end
end

def real_palindrome?(str)
  clean_input = clean_array(str).map(&:downcase)                            # all chars in clean array to lower case
  length = clean_input.length
  first_half_input = clean_input[0, (length + 1)/2]                         # returns first half of input
  second_half_input = clean_input[length/2, length]                         # returns second half od input  

  first_half_input == second_half_input.reverse                             # compare both half (second reversed)-> true/false
end


p real_palindrome?('madam') == true
  # first half = mad -> from index[0] to lenght/2 --> arr[index[x]..arr.length/2]
  # seconf half = dam -> length/2 to n-1 --> arr[index[x]..arr.length]

p real_palindrome?('Madam') == true           # (case does not matter)
p real_palindrome?("Madam, I'm Adam") == true # (only alphanumerics matter)
p real_palindrome?('356653') == true
p real_palindrome?('356a653') == true
p real_palindrome?('123ab321') == false
```

### Exercise 10: Palindromic numbers

Write a method that returns true if its integer argument is palindromic, false otherwise. A palindromic number reads the same forwards and backwards.

```ruby
palindromic_number?(34543) == true
palindromic_number?(123210) == false
palindromic_number?(22) == true
palindromic_number?(5) == true
```

##### Problem
- write method that return boolean if given argument (integer) is palindromic
- palindromic is number that reads the same forwards and backwards

##### Data
- integer as input
- boolean as output

##### Examples
palindromic_number?(34543) == true
  - input 34543
  - forward reading 34543

palindromic_number?(123210) == false
   input 123210
   fwrd - 123210
   bckwrd - 012321  
   
##### Questions
- validate input? NO (input is always integer)
- 0 as input? Yes, it's a palindrome (just one int)

##### Pseudocode
- convert input into array (easy to play with index)
- reverse method? reverse on intgers is valid?
- divide the input into two and reverse the second?

- input_to_array = input.to_s.chars -> return an array of string numbs
- length = input_to_array.length
- half_input = input_to_array[0..length/2-1] -> half input array
- reversed = half_input.reverse
- half_input == reversed
=end

##### Code
```ruby
def palindromic_number?(int)        # first try, didn't work
  input_to_array = int.to_s.chars
  
  length = input_to_array.length
  
  first_half_input = input_to_array[0..length/2-1]
  second_half_input = input_to_array[length..-1]
    
  first_half_input == second_half_input.reverse!
end

def palindromic_number?(int)      # second try, it works, much easier
  int.digits == int.digits.reverse
end

def palindromic_number?(int)      # alternative option, it works
  int_to_array = int.to_s.chars

  if int_to_array.length.odd?
    int_to_array[0..int_to_array.length/2] == int_to_array[int_to_array.length/2..-1].reverse
  else
    int_to_array[0...int_to_array.length/2] == int_to_array[int_to_array.length/2..-1].reverse
  end
end
```
