##  RB101-RB109 - Small Problems --> EASY 4

**This set of exercises are solved using a PEDAC approach**

### Exercise 1: Short Long Short

Write a method that takes two strings as arguments, determines the longest of the two strings, and then returns the result of concatenating the shorter string, the longer string, and the shorter string once again. You may assume that the strings are of different lengths.

```ruby
short_long_short('abc', 'defgh') == "abcdefghabc"
short_long_short('abcde', 'fgh') == "fghabcdefgh"
short_long_short('', 'xyz') == "xyz"
```

##### Problem
- Of two given strings, determine the longest
- And return a new string made of concatenating the shortest + the longest + the shortest

##### Input/output
- Two strings as input
- One string as output

##### Examples
Given with the problem statement

##### Pseudocode
1. Find the longest of two strings
- put the two strings into an array
- sort the array elements by their lenght
- extract the shortest and the longests in different variables
2. Create new string made of strings concatenations
- shortest string + longest string + shortest string
3. Return new string

##### Code
```ruby
def short_long_short(str1, str2)
  strs_to_arr = []
  strs_to_arr << str1
  strs_to_arr << str2

  ordered_arr = strs_to_arr.sort_by { |elem| elem.length }
  long_str = ordered_arr[1]
  short_str = ordered_arr[0]

  new_str = short_str + long_str + short_str
end
```

##### School answer
```ruby
def short_long_short(string1, string2)
  arr = [string1, string2].sort_by { |el| el.length }
  arr.first + arr.last + arr.first
end
```

------------------------

### Exersise 2: What Century is That?

*This exercise was solved with Garry*

Write a method that takes a year as input and returns the century. The return value should be a string that begins with the century number, and ends with st, nd, rd, or th as appropriate for that number.

New centuries begin in years that end with 01. So, the years 1901-2000 comprise the 20th century.

```ruby
century(2000) == '20th'
century(2001) == '21st'
century(1965) == '20th'
century(256) == '3rd'
century(5) == '1st'
century(10103) == '102nd'
century(1052) == '11th'
century(1127) == '12th'
century(11201) == '113th'
```

#### Problem
- define method that takes a year (integer) as input and return the century (string)
- output must be followed by the ordinals st, nd, rd or th accordingly
- a century begins in year ending with `01` and end in year ending with `00`
  i.e. 1901 - 2000 --> 20th century

#### Data structure
- integer as input
- string as output
- perhaps array for easy index iteration?

#### Examples
century(2000) == '20th'
  # year ends with 00, no century change
century(2001) == '21st'
  # year ends with 01, new century
century(5) == '1st'
  # year smaller than 101 equals century 1
century(11201) == '113th'
  # larger year

#### Pseudocode
- If year lenght == 1
  - Century always 1st
- If year length == 3
  - The first digits + 1 indicates the century (year 256 --> century 3)
- If year length == 4
  - The first two digits + 1 indicates the century (year 1999 --> century 20)
- If year length == 5  
  - The first three digits + 1 indicates the century (year 10103 -- century 102)

- year / 100 + 1 == century
- except for years ending in 00

- append st, nd, rd, th to the century
  - rules
    - if ending in 1 append st except if previous digit is 1, in this case append th (11th)
    - if ending in 2 append nd except if previous digit is 1, in this case append th (12th)
    - if ending in 3 append rd except if previous digit is 1, in this case append th (13th)
    - otherwise append th
=end

#### Code
```ruby
def display_century(int)
  century_arr = int.digits.reverse  
  if century_arr.last == 1 && century_arr[-2] != 1
    int.to_s + 'st'
  elsif century_arr.last == 2 && century_arr[-2] != 1
    int.to_s + 'nd'
  elsif century_arr.last == 3 && century_arr[-2] != 1
    int.to_s + 'rd'
  else
    int.to_s + 'th'     
  end
end

def century(year)
  year_arr = year.digits.reverse

  if year_arr[-2..-1] == [0, 0]
    century = year / 100
  else
    century = (year / 100) + 1
  end

  display_century(century)
end

p century(2000) == '20th'
p century(2001) == '21st'
p century(1965) == '20th'
p century(256) == '3rd'
p century(5) == '1st'
p century(10103) == '102nd'
p century(1052) == '11th'
p century(1127) == '12th'
p century(11201) == '113th'
p century(20000) == '200th'
```

------------------------

### Exersise 3: Leap Years (Part 1)

**Solved with Nico; done on our own with a 15 minutes timer and solutions and process shared after**

In the modern era under the Gregorian Calendar, leap years occur in every year that is evenly divisible by 4, unless the year is also divisible by 100. If the year is evenly divisible by 100, then it is not a leap year unless the year is evenly divisible by 400.

Assume this rule is good for any year greater than year 0. Write a method that takes any year greater than 0 as input, and returns true if the year is a leap year, or false if it is not a leap year.

```ruby
leap_year?(2016) == true
leap_year?(2015) == false
leap_year?(2100) == false
leap_year?(2400) == true
leap_year?(240000) == true
leap_year?(240001) == false
leap_year?(2000) == true
leap_year?(1900) == false
leap_year?(1752) == true
leap_year?(1700) == false
leap_year?(1) == false
leap_year?(100) == false
leap_year?(400) == true
```

##### Alonso's version

##### Problem
- leap year = year / 4 reminder == 0 | unless year is also / 100 with reminder == 0
- if year / 4 reminder == 0 && !(year / 100 reminder == 0)
- if year / 100 reminder == 0 --> not leap unless year / 400 reminder == 0

- this rule is good for year > 0
- According to this rule, def a method that return true/false for input year (if leap)

##### Examples

leap_year?(2016) == true
  2016 % 4 == 0 => true
leap_year?(2015) == false
  2016 % 4 == 0 => false
leap_year?(2100) == false
leap_year?(2400) == true

leap_year?(240000) == true
leap_year?(240001) == false
leap_year?(2000) == true
leap_year?(1900) == false
leap_year?(1752) == true
leap_year?(1700) == false
leap_year?(1) == false
leap_year?(100) == false
leap_year?(400) == true

##### Data
- input integer
- output boolean

##### Pseudocode

- if input num / 4 remainder == 0 returns true, then leap
- unless num / 100 remainder == 0 returns true

- if year / 100 remainder != 0 returns false, no leap
- unless num / 400 remainder == 0 returns true
=end

##### Code
```ruby
def leap_year?(year)
  rule_one = year % 4 == 0 && year % 100 != 0
  rule_two = year % 100 != 0 && year % 400 == 0

  if year % 4 == 0 && year % 100 != 0
    return true
  elsif year % 100 != 0 && year % 400 == 0
    return true
  else
    return false
  end

  return true if year % 4 == 0 && year % 100 != 0
  return true if year % 100 != 0 && year % 400 == 0

  if year % 4 == 0 unless year % 100 != 0
    return true
  elsif year % 100 != 0 unless year % 400 == 0
    return false
  else
    return false
  end
end
```

##### Several versions done with Nico

```ruby
def leap_year?(year)
  if year % 4 == 0 && year % 100 != 0
    return true
  elsif year % 4 == 0 && year % 100 == 0 && year % 400 == 0
    return true
  else
    return false
  end
end
```
```ruby
def leap_year?(year)
  return true if year % 4 == 0 && year % 100 != 0
  return true if year % 100 == 0 && year % 400 == 0
  false
end
```
```ruby
def leap_year?(year)
  (year % 4 == 0) != (year % 100 == 0) || year % 400 == 0
end

def leap_year?(year)
  rule_one = year % 4 == 0 && year % 100 != 0 
  rule_two = year % 100 == 0 && year % 400 == 0

  return true if rule_one
  return true if rule_two
  false
end
```

##### Nico's versions

```ruby
def leap_year?(int)
  int % 100 == 0 ? int % 400 == 0 : int % 4 == 0
end
```
```ruby
def leap_year?(int)  
  if int % 100 == 0
    if int % 400 == 0
      true
    else
      false
    end
  else
    int % 4 == 0
  end
end
```
------------------------

### Exersise 4:




------------------------

### Exersise 5: Multiples of 3 and 5

**Solved with Garry; done on our own with a 12 minutes timer and solutions and process shared after**

Write a method that searches for all multiples of 3 or 5 that lie between 1 and some other number, and then computes the sum of those multiples. For instance, if the supplied number is 20, the result should be 98 (3 + 5 + 6 + 9 + 10 + 12 + 15 + 18 + 20).

You may assume that the number passed in is an integer greater than 1.

Examples

```ruby
multisum(3) == 3
multisum(5) == 8
multisum(10) == 33
multisum(1000) == 234168
```

##### Alonso's version

##### Problem
- find multiples of 3 or 5
- of a given integer from 1 to that integer (if int = 4, then 1, 2, 3, 4)
- then compute the sum of those

##### Examples
- given num = 20
- multiples are 3, 5, 6, 9, 10, 12, 15, 18, 20
- and the sum of all those is 98

##### Pseudocode
- find all integers from 1 to a given integer
- check if these integers % 3 == 0 OR if these integers % 5 == 0 (divisible by 3 or divisible by 5)
- save all that return true to one of these conditions
- sum them up and return the sum

##### Code
```ruby
def multisum(num)
  total_sum = 0
  arr = []
  (num + 1).times {|num| arr << num if num > 0}                 # Careful with times method, it takes all nums -1
  
  multiples = arr.select {|num| num % 3 == 0 || num % 5 == 0 }
  multiples.each {|num| total_sum += num}
  
  total_sum
end
```

##### Garry's version

##### P
Write a method that searches for all multiples of 3 or 5 that lie between 1 and some other number
compute the sum of those multiples
if the supplied number is 20, the result should be 98 (3 + 5 + 6 + 9 + 10 + 12 + 15 + 18 + 20).

Input: integer 
Output: integer 

##### E             
```ruby
multisum(3) == 3 => [3]                 # this practice ended up being super important!
multisum(5) == 8 => [3, 5]
multisum(10) == 33 [3, 5, 6, 9, 10]
```

##### A
- create a method called multisum that takes on argument, an integer
- create a range from 1 to input integer and convert into an array, save result to variable called arr 
- Create an empty array names results 
- iterate thorugh arr and push up mutliples of 3 and 5 
- add all elements together 
- return sum 

###### C
```ruby
def multisum(int)
  arr = (1..int).to_a             # note how this way is more clever than my solution: range from 1..int, both included
  results = []

  arr.each do |int|
    results << int if int % 3 == 0 || int % 5 == 0 
  end 

  results.sum                     # and also the use of the sum method which returns the sum of elements in an array
end 
```

------------------------

### Exersise 6: Running Totals

**Solved with Nico; done on our own with a 12 minutes timer and solutions and process shared after**

Write a method that takes an Array of numbers, and returns an Array with the same number of elements, and each element has the running total from the original Array.

Examples:

```ruby
running_total([2, 5, 13]) == [2, 7, 20]
running_total([14, 11, 7, 15, 20]) == [14, 25, 32, 47, 67]
running_total([3]) == [3]
running_total([]) == []
```

##### Alonso's version

##### Problem
- take array of numbers
- return array of numbers where each element is the sum of elemt and prev elements

##### Examples
`running_total([2, 5, 13]) == [2, 7, 20]`
- elem 0 -> 2
- elem 1 -> 7 (2 + 5)
- elem 2 -> 20 (2 + 5 + 13)
- etc...

##### Pseudocode
- iterate arr 
- add index[i] and index[i-1] and save it as new elem of new arr
- remove index used
- add new elem of new arr and index

##### Nico's solutions

```ruby
def running_total(arr)
  new_arr = []
    
  arr.each_with_index do |number, index|
    if index == 0
      new_arr << arr[0] 
    else
      new_arr << number + new_arr[index -1]
    end
  end
  
  new_arr
end


def running_total(arr)
  return arr if arr.empty?
  new_arr = [arr[0]]
  
  arr[1..-1].each_with_index do |number, index|
    new_arr << number + new_arr[index]
  end
  
  new_arr
end


def running_total(arr)
  sum = 0
  new_arr = []

  arr.each do |number|
    sum += number
    new_arr << sum
  end

  new_arr
end

def running_total(arr)
  return arr if arr.empty? 
  
  sum = 0
  new_arr = []
  index = 0
  
  loop do
    sum += arr[index]
    new_arr << sum
    index += 1
    break if index == arr.size
  end
  
  new_arr
end
```

------------------------

### Exersise 7: Convert a String to a Number!

The String#to_i method converts a string of numeric characters (including an optional plus or minus sign) to an Integer. String#to_i and the Integer constructor (Integer()) behave similarly. In this exercise, you will create a method that does the same thing.

Write a method that takes a String of digits, and returns the appropriate number as an integer. You may not use any of the methods mentioned above.

For now, do not worry about leading + or - signs, nor should you worry about invalid characters; assume all characters will be numeric.

You may not use any of the standard conversion methods available in Ruby to convert a string to a number, such as String#to_i, Integer(), etc. Your method should do this the old-fashioned way and calculate the result by analyzing the characters in the string.

Examples

```ruby
string_to_integer('4321') == 4321
string_to_integer('570') == 570
```

##### Alonso's solution

##### P
- create a method that takes an numerical string and returns an integer
- all valid input (all string digits): no spaces, no empty, no chars, no symbols, etc.

##### D
- input string
- output integer
- perhaps array for iteration 

##### A
- loop/iterate over each char of input string
- convert each character to its integer value ('1' -> 1)
- return the new integers in same order we iterate the input 

##### C
```ruby
def string_to_integer(input)  
  input_to_str_arr = input.chars      #=> for '4321' will return ['4', '3', '2', '1'] -> array of strings
  
  wanted_integer = 0
  index = 0
  arr_of_ints = []

  loop do
    case input_to_str_arr[index]
      when '0' then arr_of_ints << 0
      when '1' then arr_of_ints << 1
      when '2' then arr_of_ints << 2
      when '3' then arr_of_ints << 3
      when '4' then arr_of_ints << 4
      when '5' then arr_of_ints << 5
      when '6' then arr_of_ints << 6
      when '7' then arr_of_ints << 7
      when '8' then arr_of_ints << 8
      when '9' then arr_of_ints << 9
    end
    index += 1
    break if index == input_to_str_arr.size
  end

  arr_of_ints #=> [4, 3, 2, 1]
  # I couldn't progress from here: how to transform and array of integers to an integer made of the array elements?
end

p string_to_integer('4321') == 4321
p string_to_integer('570') == 570
```

##### How did a I get to the final solution?

##### NEW PROBLEM
- having this array of integers -> [4, 3, 2, 1]
- generate an integer formed by the array elements in the same order -> 4321
- don't use the `String#to_i` method or `Integer()` method

##### ALGORITHM
- iterate the input array and identify, based on the number of elements, the 1's place, 10's place, 100's place, 1000's place, etc.
- be aware that the decimal numbers (numbers represented in base 10), the 1's are in last position, etc.
- we can multiply each number by 10 to the indexth of element to represent the base 10 number
- in our example 
  - 1*(10**0) will take the last place in the new integer -> 1
  - 2*(10**1) will take the place before last in new int -> 20
  - 3*(10**2) will take the place before previous in new int -> 300
  - 4*(10**2) will take the place before previous in new int -> 4000

  - all them added together produces 4321, so the desired number
- let's code that

##### EXAMPLES
```ruby
arr = [1,7,6,4,5,6,7,8]

index = 0
sum = 0

arr.reverse.each do |digit|
   sum += digit*(10**index)
   index += 1
end

p sum # => 17645678 --> this is it!
```

##### CODE
```ruby
def string_to_integer(input)  
  input_to_str_arr = input.chars      #=> for '4321' will return ['4', '3', '2', '1'] -> array of strings
  
  wanted_integer = 0
  index = 0
  arr_of_ints = []

  loop do
    case input_to_str_arr[index]
      when '0' then arr_of_ints << 0
      when '1' then arr_of_ints << 1
      when '2' then arr_of_ints << 2
      when '3' then arr_of_ints << 3
      when '4' then arr_of_ints << 4
      when '5' then arr_of_ints << 5
      when '6' then arr_of_ints << 6
      when '7' then arr_of_ints << 7
      when '8' then arr_of_ints << 8
      when '9' then arr_of_ints << 9
    end
    index += 1
    break if index == input_to_str_arr.size
  end

  # at this point, arr_of_ints for '4321' will return [4, 3, 2, 1] -> array of integers 

  arr_of_ints.reverse.each_with_index do |digit, index|
    wanted_integer += digit*(10**index)
  end
  wanted_integer
end

p string_to_integer('4321') == 4321
p string_to_integer('570') == 570
```

- The heart of the problem is this line `wanted_integer += digit*(10**index)`
- Step by step:
```ruby
# digit = each element in arr
# base_10 =  10 ** index     
# p digit * base_10  
# Resulting, in each iteration on:
# - 1(digit), 1(base_10) = 1 (1st iteration)
# - 2(digit), 10(base_10) = 20 (2nd iteration)
# - 3(digit), 100(base_10) = 300 (3rd iteration)
# - 4(digit), 1000(base_10) = 4000 (4th iteration)
```

##### Garry's ideas...

sum = 4 
sum = sum * 10 
sum = sum + 3 
sum 

------ 
sum = 43 # 43 
sum = sum * 10 
sum  = sum + 2 
sum 

------
sum = 432 
sum = sum  * 10 
sum = sum + 1 
sum 

------
[4, 3, 2, 1] 
4 * 10 = 40
40 + 3 = 43 

sum = (4 * 1000) + (3 * 100) + (2 * 10) + (1 * 1)

------------------------

### Exersise 8: Convert a String to a Signed Number!

In the previous exercise, you developed a method that converts simple numeric strings to Integers. In this exercise, you're going to extend that method to work with signed numbers.

Write a method that takes a String of digits, and returns the appropriate number as an integer. The String may have a leading `+` or `-` sign; if the first character is a `+`, your method should return a positive number; if it is a `-`, your method should return a negative number. If no sign is given, you should return a positive number.

You may assume the string will always contain a valid number.

You may not use any of the standard conversion methods available in Ruby, such as `String#to_i`, `Integer()`, etc. You may, however, use the `string_to_integer` method from the previous lesson.

Examples
```ruby
string_to_signed_integer('4321') == 4321
string_to_signed_integer('-570') == -570
string_to_signed_integer('+100') == 100
```

##### Alonso's solution

##### P:
- Method that convert numeric strings to integers
- In this case, the strings may have a leading + or -
- + means the number to follow is positive
- - means the number to follow is negative
- no leading sign the number to follow is positive
- use the `string_to_integer` method from previous exercise

##### A:
- Pass input to `string_to_integer` as argument
- Check if char[0] == + or - or other char
  - if +, convert the string to integer as if the sign didn't exist --> remove the sign
  - if other sign, same, but don't remove any char
  - if -, convert the string to integer and prepend the result with - sign
- Return the result

##### C:
```ruby
def string_to_signed_integer(input)
  if input[0] == '-'
    - string_to_integer(input)
  elsif input[0] == '+'
    string_to_integer(input)
  else
    string_to_integer(input)
  end
end
```

------------------------

### Exersise 9: Convert a Number to a String!

In the previous two exercises, you developed methods that convert simple numeric strings to signed Integers. In this exercise and the next, you're going to reverse those methods.

Write a method that takes a positive integer or zero, and converts it to a string representation.

You may not use any of the standard conversion methods available in Ruby, such as Integer#to_s, String(), Kernel#format, etc. Your method should do this the old-fashioned way and construct the string by analyzing and manipulating the number.

Examples
```ruby
integer_to_string(4321) == '4321'
integer_to_string(0) == '0'
integer_to_string(5000) == '5000'
```

##### Alonso's solution

##### P:
- Define a method that converts integer to numeric strings, without using any built-in method (to_s, etc)
- The input could be positive or zero

##### A:
- Create collection of valid numeric strings, so we can access them by index
- Convert the integer to an array
- Iterate over the array and use each integer to access their string version by index
- Append each element into a new string

##### C:
```ruby
# CHARS = {1=> '1', 2=> '2', 3=> '3', 4=>'4', 5=>'5', 6=>'6', 7=>'7', 8=>'8', 9=>'9', 0=>'0'}
CHARS = %w(0 1 2 3 4 5 6 7 8 9)

def integer_to_string(integer)
  int_to_arr = integer.digits.reverse       # [4, 3, 2, 1] for example 1
  int_to_str = ''

  int_to_arr.each do |int|
    int_to_str << CHARS[int]
  end
  int_to_str
end
```

------------------------

### Exersise 10: Convert a Signed Number to a String!

In the previous exercise, you developed a method that converts non-negative numbers to strings. In this exercise, you're going to extend that method by adding the ability to represent negative numbers as well.

Write a method that takes an integer, and converts it to a string representation.

You may not use any of the standard conversion methods available in Ruby, such as Integer#to_s, String(), Kernel#format, etc. You may, however, use integer_to_string from the previous exercise.

Examples
```ruby
signed_integer_to_string(4321) == '+4321'
signed_integer_to_string(-123) == '-123'
signed_integer_to_string(0) == '0'
```

##### Alonso's solution

##### -------------------------PROBLEM--------------------------------------
Input: Integer. Can be a negative int (prepended by `-` symbol)
Output: "Numerical" string 

##### --------------------------RULES-----------------------------------------
Explicit: ->Don't use built-in methods
          ->
Implicit: -> All inputs are valid integers
          -> Input can be zero
          -> Input can be negative integer  

Questions?

##### -------------------------EXAMPLES--------------------------------------
4321 produces '+4321'
  -> input integer is positive, so output string must have + symbol

-123 prodces '-123'
  -> input integer is negative, so output string must have - symbol

0 produces '0'
  -> no symbols needed  

##### -------------------------DATA STRUCTURE-------------------------------
- Integer: positive, negative and zero
- Numerical string: prepended with + or - symbol when needed
- Array for iteration

##### ---------------------------ALGORITHM-----------------------------------
- Create a collection (array) with all valid versions of numerical integers (0 to 9 both included)
- Convert the input integer into array
- Consider the negative symbol if any
- Iterate the array and use the integer as index to access the collections with valid numerical strings
- Create an empty string
- Append every string version of integer to empty string
- Prepend the whole new string with 
  - '+' symbol if input is positive int
  - '-'symbol if input is negative int
  - do nothing if inpout is zero
- return new string  

##### ---------------------------------CODE------------------------------------
```ruby
STR_NUMS = %w(0 1 2 3 4 5 6 7 8 9)

def signed_integer_to_string(input)
  negative = input if input < 0
  input = -input if input < 0
  
  arr_of_ints = input.digits.reverse
  new_str = ''
  arr_of_ints.each do |int|
    new_str << STR_NUMS[int]
  end

  if input == 0
    new_str
  elsif negative
    new_str.prepend('-')
  else
    new_str.prepend('+')
  end
end
```
