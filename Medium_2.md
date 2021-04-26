##  RB101-RB109 - Small Problems --> MEDIUM 2

**This set of exercises are solved using a PEDAC approach**

### Exersise 1: Longests sentence

---------------------INSTRUCTIONS------------------------------------
Write a program that reads the content of a text file and then prints the longest sentence in the file based on 
number of words. Sentences may end with periods (.), exclamation points (!), or question marks (?). 
Any sequence of characters that are not spaces or sentence-ending characters should be treated as a word. 
You should also print the number of words in the longest sentence.

------------------------PROBLEM--------------------------------------
Input: 

Output: 
-------------------------RULES---------------------------------------
Explicit:
- A sentence is a sequence of word that end with '.' '?' or '!'
- A word is a sequence of characters that end with a ' '

Implicit:
------------------------EXAMPLES--------------------------------------

--------------------------ALGORITHM-----------------------------------
Goal:
- find the longest sentence in a given text and print it to screen along with its number of words

Ideas:
- Define sentence as sequence of words that ends with '.' '?' or '!'
- Find all sentences in given text according to above definition
- Define words as sequence of characters that ends with ' '
- Find all words in found sentences and count them
- Retrieve the sentence with larger number of words in it


```ruby
#text = "long text here..."  OR text = File.read('/Users/alonso/Downloads/book.txt')

arr_words = text.split

ending_chars = %w(. ? !)

sentences = []

arr_words.each do |word|
  sentence_end = arr_words.index {|word| ending_chars.include?(word[-1])}

  sentences << arr_words.slice!(0..sentence_end)
end

largest_sentence = sentences.max_by {|sentence| sentence.size}

puts largest_sentence.join(' ')
puts ""
puts "The largest sentence has #{largest_sentence.size} words"
```
------------------------

### Exersise 2: Now I Know My ABCs


------------------------

### Exersise 3: Lettercase Percentage Ratio

---------------------INSTRUCTIONS------------------------------------
In the easy exercises, we worked on a problem where we had to count the number of uppercase and lowercase characters, 
as well as characters that were neither of those two. Now we want to go one step further.

Write a method that takes a string, and then returns a hash that contains 3 entries: one represents the percentage of 
characters in the string that are lowercase letters, one the percentage of characters that are uppercase letters, 
and one the percentage of characters that are neither.

You may assume that the string will always contain at least one character.

------------------------PROBLEM--------------------------------------
Input: 
- String

Output: 
- Hash with three entries:
  - percentage of chars that are lowercase
  - percentage of chars that are uppercase
  - percentage of chars that are neither of the two above

-------------------------RULES---------------------------------------
Explicit:

Implicit:
- percentage of chars that meet a requirement --> (chars that meet the requirement/total chars in string) * 100

------------------------EXAMPLES--------------------------------------
letter_percentages('abCdef 123') == { lowercase: 50, uppercase: 10, neither: 40 }
letter_percentages('AbCd +Ef') == { lowercase: 37.5, uppercase: 37.5, neither: 25 }
letter_percentages('123') == { lowercase: 0, uppercase: 0, neither: 100 }

--------------------------ALGORITHM-----------------------------------
Goal:
- Find number of chars in a string that are uppercase, lowercase and non of those and calculate what % of total represent

Ideas:
- Convert string to array of chars
- Iterate string of chars and update different counters (in a hash) every time a lowcase, upcase or other char appears
- Count total num of chars in string
- Divide the three counters by total num and multiply by 100 (operate with float nums)
- Store the result in a hash
- return the hash

Steps:
- String to array of chars with string.chars
- Create hash with three symbols as keys and 0 as val -> { lowercase: 0, uppercase: 0, neither: 0 }
- Create reference collections (constants) of uppercase and lowercase chars
- Iterate the array of char and update the hash values in the corresponding key every time char is included in uppercase,
lowercase or neither
- Access the values of the hashes and apply the math to get the %

```ruby
def calc_percent(appearence, total)
  ((appearence.to_f / total.to_f) * 100).round(2)
end

UPCASE = ('A'..'Z').to_a
LOWCASE = ('a'..'z').to_a

def letter_percentages(string)
  counter = { lowercase: 0, uppercase: 0, neither: 0 }

  chars = string.chars

  chars.each do |char|
    if UPCASE.include?(char)
      counter[:uppercase] += 1
    elsif LOWCASE.include?(char)
      counter[:lowercase] += 1
    else
      counter[:neither] += 1
    end
  end

  total_chars = chars.size
  calc_percent(counter[:uppercase], total_chars)

  counter[:uppercase] = calc_percent(counter[:uppercase], total_chars)
  counter[:lowercase] = calc_percent(counter[:lowercase], total_chars)
  counter[:neither] = calc_percent(counter[:neither], total_chars)

  counter
end

p letter_percentages('abCdef 123') == { lowercase: 50, uppercase: 10, neither: 40 }
p letter_percentages('AbCd +Ef') == { lowercase: 37.5, uppercase: 37.5, neither: 25 }
p letter_percentages('123') == { lowercase: 0, uppercase: 0, neither: 100 }
```

------------------------

### Exersise 4: Matching Parentheses?

Write a method that takes a string as argument, and returns true if all parentheses in the string are properly balanced, false otherwise. To be properly balanced, parentheses must occur in matching '(' and ')' pairs.

=>Input: String containing opening and closing parens
=>Output: Boolean: True if the parens are balances in the string, false otherwise

=>Rules
- Balanced parentheses:  
  --> Always opening before closing parens
  --> Matching number of opening and closing parens
  --> Always 1 more opening than closing before the last closing appearance
  
=>Examples:

balanced?('What (is) this?') == true
-> Open first? --> yes
-> More open than close before last close? --> yes
-> Balanced total? --> yes

balanced?('What is) this?') == false
-> Open first? --> no

balanced?('What (is this?') == false
-> Open first? --> yes
-> More open than close before last close? --> yes
-> Balanced total? --> no

balanced?('((What) (is this))?') == true
-> Open first? --> yes
-> More open than close before last close? --> yes
-> Balanced total? --> yes

balanced?('((What)) (is this))?') == false
-> Open first? --> yes
-> More open than close before last close? --> yes
-> Balanced total? --> no

balanced?('Hey!') == true
-> No parens --> return true

balanced?(')Hey!(') == false
-> Open first? --> no

balanced?('What ((is))) up(') == false
-> Open first? --> yes
-> More open than close before last close? --> no

=> Algorithm

=> Goal
  ==> Check if 1st paren is an opening
  ==> Check if thre is always one more opening than closing before the last closing
  ==> Check if same num of opening and closing at the end
  
=> Steps  
  ==> Initialize a counter (hash) to control num of appearances of both
    ==> Reassign the counter to += 1 at every iteration if a '(' or a ')' appears
    ==> If closing counter is larger than opening --> return false
    ==> That's also the way to check if an opening paren comes before closing paren
    
  ==> If the prev is true
    ==> Compare num of opening and closing and return true if the num is equal
    ==> Otherwise return false    

```ruby
def balanced?(string)
  number_parens = {opening: 0, closing: 0}
  
  string.each_char do |char|
    if char == '('
      number_parens[:opening] += 1
    elsif char == ')'
      number_parens[:closing] += 1
    end
    
    if number_parens[:opening] < number_parens[:closing]
    return false
    end
  end

  if number_parens[:opening] == number_parens[:closing]
    true
  else
    false
  end
end

p balanced?('What (is) this?') == true
p balanced?('What is) this?') == false
p balanced?('What (is this?') == false
p balanced?('((What) (is this))?') == true
p balanced?('((What)) (is this))?') == false
p balanced?('Hey!') == true
p balanced?(')Hey!(') == false
p balanced?('What ((is))) up(') == false
```

------------------------

### Exersise 5: Triangle Sides

Triangle Sides
A triangle is classified as follows:

- equilateral All 3 sides are of equal length
- isosceles 2 sides are of equal length, while the 3rd is different
- scalene All 3 sides are of different length

To be a valid triangle, the sum of the lengths of the two shortest sides must be greater than the length of the longest side, and all sides must have lengths greater than 0: if either of these conditions is not satisfied, the triangle is invalid.

Write a method that takes the lengths of the 3 sides of a triangle as arguments, and returns a symbol :equilateral, :isosceles, :scalene, or :invalid depending on whether the triangle is equilateral, isosceles, scalene, or invalid.

=>Input 
  ==> 3 integers that are the length of the 3 sides of a triangle

=>Output 
  ==> Symbol :equilateral, :isosceles, :scalene, or :invalid

=>Rules
  ==> equilateral All 3 sides are of equal length
  ==> isosceles 2 sides are of equal length, while the 3rd is different
  ==> scalene All 3 sides are of different length
  ==> invalid
    ==> sum of lengths of two shortest sides isn't greater than length of longest side
    ==> any side does not have length greater than 0
  
=>Examples
  triangle(3, 3, 3) == :equilateral
  ==> 3 sides are larger than 0 --> valid
  ==> Sum of two shortest sides is larger that the other --> valid
  ==> 3 sides same length --> equilateral
  
  triangle(3, 3, 1.5) == :isosceles
  ==> 3 sides are larger than 0 --> valid
  ==> Sum of two shortest sides is larger that the other --> valid
  ==> 2 sides same length 1 different --> isosceles
  
  triangle(3, 4, 5) == :scalene
  ==> 3 sides are larger than 0 --> valid
  ==> Sum of two shortest sides is larger that the other --> valid
  ==> 3 sides different length --> scalene  
  
  triangle(0, 3, 3) == :invalid
  ==> 1 side is 0 --> invalid
  
  triangle(3, 1, 1) == :invalid
  ==> 3 sides are larger than 0 --> valid
  ==> Sum of two shortest sides isn't larger that the other --> invalid
  
=>Data Structure
  ==> Integer as input
  ==> Symbol as output
  
=>Algorithm
  =>Goal
    1) Find out if a triangle is valid ==> HELPER METHOD
      1.1) Find out if 3 integers are > 0 --> otherwise return :invalid
      1.2) Find out if 2 shortes sides added is > other side --> otherwise return :invalid
    
    2) If valid, find out which type of triangle it is
      --> If 3 integers are the same val --> return :equilateral
      --> If 2 integers are equal and 1 different --> return :isosceles
      --> If 3 integers are different --> return :scalene
     
```ruby
def valid_triangle?(int1, int2, int3) 
  sides_in_order = [int1, int2, int3].sort
  
  if int1 <= 0 || int2 <= 0 || int3 <= 0
    false
  elsif sides_in_order[0] + sides_in_order[1] < sides_in_order[2]
    false
  else
    true
  end
end

def triangle(int1, int2, int3)
  if valid_triangle?(int1, int2, int3)
    if int1 == int2 && int2 == int3
      :equilateral
    elsif int1 == int2 && int2 != int3 || int1 == int3 && int2 != int3
      :isosceles
    else
      :scalene
    end
  else
    :invalid
  end
end

p triangle(3, 3, 3) == :equilateral
p triangle(3, 3, 1.5) == :isosceles
p triangle(3, 4, 5) == :scalene
p triangle(0, 3, 3) == :invalid
p triangle(3, 1, 1) == :invalid
```

------------------------

### Exersise 6: Tri-Angles

A triangle is classified as follows:

right --> One angle of the triangle is a right angle (90 degrees)
acute --> All 3 angles of the triangle are less than 90 degrees
obtuse --> One angle is greater than 90 degrees.

To be a valid triangle, the sum of the angles must be exactly 180 degrees, and all angles must be greater than 0: if either of these conditions is not satisfied, the triangle is invalid.

Write a method that takes the 3 angles of a triangle as arguments, and returns a symbol :right, :acute, :obtuse, or :invalid depending on whether the triangle is a right, acute, obtuse, or invalid triangle.

You may assume integer valued angles so you don't have to worry about floating point errors. You may also assume that the arguments are specified in degrees.

=> Input: Three integers that are the degrees of the three angles of a triangle
=> Output: Symbol (:acute, :right, :obtuse or :invalid) according to the type of triagle

=> Rules
  ==> right --> One angle of the triangle is 90 degrees
  ==> acute --> All 3 angles of the triangle are less than 90 degrees
  ==> obtuse --> One angle is greater than 90 degrees

  ==> Valid triangle
    ==> The sum of the three angles must be exactly 180 degrees
    ==> All three angles must be greater than 0

  ==> All arguments are valid (no floating values, all integer degrees)
  
=> Examples:

triangle(60, 70, 50) == :acute
--> 3 sides add 180? --> yes
--> all sides > 0? --> yes
--> one arg is 90? --> no
--> all sides < 90 --> yes ---> :accute
--> one arg is > 90? --> no

triangle(30, 90, 60) == :right
--> 3 sides add 180? --> yes
--> all sides > 0? --> yes
--> one arg is 90? --> yes ---> :right
--> all sides < 90 --> no
--> one arg is > 90? --> no

triangle(120, 50, 10) == :obtuse
--> 3 sides add 180? --> yes
--> all sides > 0? --> yes
--> one arg is 90? --> no
--> all sides < 90 --> no
--> one arg is > 90? --> yes ---> :obtuse

triangle(0, 90, 90) == :invalid
--> 3 sides add 180? --> yes
--> all sides > 0? --> no

triangle(50, 50, 50) == :invalid
--> 3 sides add 180? --> no

=> Algorithm

  => Goal
    ==> Check if triangle is valid
    ==> If so, determine what type of triangle it is
    
  => Steps
    ==> Valid triangle> --> Helper Method
      ==> add up arg and must equal 180
      ==> check if all args are larger than 0
      
    ==> Invoke valid_triangle: if valid_triangle...
      ==> one arg is == 90 --> then :right
      ==> all args are < 90 --> then :acute
      ==> one arg is > 90 --> then :obtuse
    ==> if not valid triangle --> then :invalid  

```ruby
def valid_triangle?(arg1, arg2, arg3)
  if arg1 + arg2 + arg3 == 180 && arg1 > 0 && arg1 > 0 && arg1 > 0
    true
  else
    false
  end
end

def triangle(arg1, arg2, arg3)
  if valid_triangle?(arg1, arg2, arg3)
    if arg1 == 90 || arg2 == 90 || arg3 == 90
      :right
    elsif arg1 < 90 && arg2 < 90 && arg3 < 90
      :acute
    elsif arg1 > 90 || arg2 > 90 || arg3 > 90
      :obtuse
    end
  else
    :invalid
  end
end

p triangle(60, 70, 50) == :acute
p triangle(30, 90, 60) == :right
p triangle(120, 50, 10) == :obtuse
p triangle(0, 90, 90) == :invalid
p triangle(50, 50, 50) == :invalid
```

------------------------

### Exersise 7: Unlucky Days

------------------------

### Exersise 8: Next Featured Number Higher than a Given Value

A featured number (something unique to this exercise) is an odd number that is a multiple of 7, and whose digits occur exactly once each. So, for example, 49 is a featured number, but 98 is not (it is not odd), 97 is not (it is not a multiple of 7), and 133 is not (the digit 3 appears twice).

Write a method that takes a single integer as an argument, and returns the next featured number that is greater than the argument. Return an error message if there is no next featured number.

=> Input: Integer
=> Output: Integer that is the next featured num greater than input OR string 'error message'

=> Rules
  ==> Featured number
    --> Odd number
    --> Multiple of 7
    --> Whose digits aren't repeated
    Ex:
      --> 49: odd number, multiple of 7, digits not repeated --> featured
      --> 98: not odd --> not featured
      --> 97: odd number, not multiple of 7 --> not featured
      --> 133: odd number, multiple of 7, digits repeated --> not featured

=> Examples:

featured(12) == 21
  --> bigger than arg? -> yes
  --> odd? -> yes
  --> multiple of 7? -> yes
  --> uniq digits? => yes

featured(20) == 21
featured(21) == 35
featured(997) == 1029
featured(1029) == 1043
featured(999_999) == 1_023_547
featured(999_999_987) == 1_023_456_987
featured(9_999_999_999) # -> There is no possible number that fulfills those requirements

=> Algorithm

  => Goal
    ==> Find and return the first number that is
      => larger than arg
      => multiple of 7
      => odd num
      => whose digits aren't repeated
      
  => Steps
    ==> Larger than arg --> num > arg
    ==> Multiple of 7 --> num % 7 == 0
    ==> Odd --> num.odd?
    ==> Digits not repeated --> num.digits.size == num.digits.uniq.size

```ruby
def featured(int)
  mult_seven = {valid_mult: 7}
  
  loop do
    
    if mult_seven[:valid_mult] >= 9_876_543_210 
      return "There is no possible number that fulfills those requirements"
    end
    
    if mult_seven[:valid_mult] > int && 
      mult_seven[:valid_mult].odd? && 
      mult_seven[:valid_mult].digits.size == mult_seven[:valid_mult].digits.uniq.size
      return mult_seven[:valid_mult]
    else
      mult_seven[:valid_mult] += 7
    end
  end

end

p featured(12) == 21
p featured(20) == 21
p featured(21) == 35
p featured(997) == 1029
p featured(1029) == 1043
p featured(999_999) == 1_023_547
p featured(999_999_987) == 1_023_456_987
p featured(9_999_999_999) == "There is no possible number that fulfills those requirements"
```

------------------------

### Exersise 9: Bubble Sort

On each pass, each pair of consecutive elements is compared. 

If the first of the two elements is greater than the second, then the two elements are swapped. Otherwise, we move to next pair

This process is repeated until a complete pass is made without performing any swaps; at that point, the Array is completely sorted.

=>Examples
array = [5, 3]
bubble_sort!(array)
array == [3, 5]
---
array = [6, 2, 7, 1, 4]
bubble_sort!(array)
array == [1, 2, 4, 6, 7]
---
array = %w(Sue Pete Alice Tyler Rachel Kim Bonnie)
bubble_sort!(array)
array == %w(Alice Bonnie Kim Pete Rachel Sue Tyler)

=>Algorithm
==> Iterate a given array in runs of every two consecutive items
==> If the 1st item is greater than the 2nd
  ==> Swap their positions
==> Otherwise
  ==> Move to the next pair
==> Repeat this operation as many times as objects in the array  

```ruby
def bubble_sort!(array)
  (array.size).times do
    (0..array.size).each do |idx|
      array[idx, 2] = array[idx, 2].sort
    end
  end
  array
end

p bubble_sort!([5, 3]) == [3,5]
p bubble_sort!([6, 2, 7, 1, 4]) == [1, 2, 4, 6, 7]
p bubble_sort!(%w(Sue Pete Alice Tyler Rachel Kim Bonnie)) == %w(Alice Bonnie Kim Pete Rachel Sue Tyler)
```

------------------------

### Exersise 10: Sum Square - Square Sum

Write a method that computes the difference between the square of the sum of the first n positive integers and the sum of the squares of the first n positive integers.

=>Input: Integer
=>Output: Integer that is the difference between the square of the sum of the first n positive integers and the sum of the squares of the first n positive integers

=>Rules
 ==> square of the sum of the first n positive integers
  --> all ints from 1 to given int
  --> added
  --> the square of that sum
  
 ==> sum of the squares of the first n positive integers
  --> all ints from 1 to given int
  --> their squares
  --> the sum of these squares
  
=>Examples:
sum_square_difference(3) == 22
  => square of the sum of the first n positive integers --> (1 + 2 + 3)**2 
  => sum of the squares of the first n positive integers --> (1**2 + 2**2 + 3**2)

=> Algorithm
  ==> Goal
    ==> Obtain all ints from 1 to given integer
      ==> 1)Square of the sum of theses nums --> helper method
        --> add them all together
        --> obtain the square of the sum
      ==> 2)Sum of the squares of these nums --> helper method
        --> obtain the square of each num
        --> add them all together
      ==> Calculate the substraction of 1 minus 2 and return the result

```ruby
def square_of_sums(array)
  array.inject(:+)**2
end

def sum_of_squares(array)
  array.map {|num| num**2}.inject(:+)
end
 
def sum_square_difference(int)
  nums = (1..int).to_a
  square_of_sums(nums) - sum_of_squares(nums)
end

p sum_square_difference(3) == 22
p sum_square_difference(10) == 2640
p sum_square_difference(1) == 0
p sum_square_difference(100) == 25164150
```