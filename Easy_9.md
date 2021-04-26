##  RB101-RB109 - Small Problems --> EASY 9

**This set of exercises are solved using a PEDAC approach**

### Exersise 1: Welcome stranger

---------------------INSTRUCTIONS-----------------------------------
Create a method that takes 2 arguments, an array and a hash. 
The array will contain 2 or more elements that, when combined with adjoining spaces, 
will produce a person's name. The hash will contain two keys, :title and :occupation, 
and the appropriate values. Your method should return a greeting that uses the person's full name, 
and mentions the person's title and occupation.

------------------------PROBLEM--------------------------------------
Input: Two arguments: Array and hash
  - array => 2 or more elements that when joined is a person's name
  - hash => two keys :title and :occupation and the corresponding values

Output: String => greeting the person's name, title and occupation
-------------------------RULES-----------------------------------------
Explicit:

Implicit:
------------------------EXAMPLES--------------------------------------
greetings(['John', 'Q', 'Doe'], { title: 'Master', occupation: 'Plumber' })
- arg 1, array -> ['John', 'Q', 'Doe'] ==> index0 - name; index1 - middle name; index2 - last name
- arg2, hash -> title: master; occupation: plumber

- Return the string:
=> Hello, John Q Doe! Nice to have a Master Plumber around.
'Hello #{name} #{midname} #{lastname}!. Nice to have a #{hash[title]} #{hash[occup]} around.'
--------------------------ALGORITHM-----------------------------------
Goal:
- Return a greeting string using values of two variables, an array and a hash

```ruby
def greetings(arg1, arg2)
  puts "Hello #{arg1[0]} #{arg1[1]} #{arg1[2]}!. Nice to have a #{arg2[:title]} #{arg2[:occupation]} around."
end

greetings(['John', 'Q', 'Doe'], { title: 'Master', occupation: 'Plumber' })
#=> Hello, John Q Doe! Nice to have a Master Plumber around.
```

------------------------

### Exersise 2: Double Doubles

---------------------INSTRUCTIONS-----------------------------------
A double number is a number with an even number of digits whose left-side digits are exactly the same as its 
right-side digits. For example, 44, 3333, 103103, 7676 are all double numbers. 444, 334433, and 107 are not.

Write a method that returns 2 times the number provided as an argument, unless the argument is a double number; 
double numbers should be returned as-is.

------------------------PROBLEM--------------------------------------
Input: Integer

Output: Integer --> two times the number provided, unless is a double number
-------------------------RULES-----------------------------------------
Explicit:
- double number --> same digits in 1st half and 2nd half
- double number --> even num of digits
- if double num as argument --> return it as it is
- if no double num as argument --> multiply argument by two and return
Implicit:
- long numbers can be marked with underscores in Ruby (every three digits) but the underscores aren't part of the number but just a guide
------------------------EXAMPLES--------------------------------------
twice(37) == 74
--> argument not double num --> num * 2 and return

twice(44) == 44
--> argument is double num --> return it
--> digit 0 to digit.size/2 == digit.size/2 + 1 to -1

twice(334433) == 668866
--> argument not double num --> num * 2 and return

twice(444) == 888
twice(107) == 214
twice(103103) == 103103
twice(3333) == 3333
twice(7676) == 7676
twice(123_456_789_123_456_789) == 123_456_789_123_456_789
twice(5) == 10
--------------------------ALGORITHM-----------------------------------
Goal:
- Detect if a given num is double num; if so, return it; otherwise, multiply num by 2 and return result

Steps
- Helper method to detect double nums
  - check if num has even num of digits
  - if so,
    - check if 1st half and 2nd half of digits are the same
      - if so, return true
      - otherwise, return false
  - otherwise, return false
- Main method
  - if double num true --> return num
  - otherwise --> multiply num * 2 and return result

```ruby
def double_num?(num)
  return false if num.digits.size.odd?

  arr_digits = num.digits.reverse
  arr_half = arr_digits.size/2

  if arr_digits[0..arr_half-1] == arr_digits[arr_half..-1]
    true
  else
    false
  end
end

def twice(int)
  if double_num?(int)
    return int
  else
    int * 2
  end
end

p twice(37) == 74
p twice(44) == 44
p twice(334433) == 668866
p twice(444) == 888
p twice(107) == 214
p twice(103103) == 103103
p twice(3333) == 3333
p twice(7676) == 7676
p twice(123_456_789_123_456_789) == 123_456_789_123_456_789
p twice(5) == 10
```

------------------------

### Exersise 3: Always Return Negative

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a number as an argument. If the argument is a positive number, 
return the negative of that number. If the number is 0 or negative, return the original number.

------------------------PROBLEM--------------------------------------
Input: Integer

Output: Integer --> negative version of given number // unless the given num is already negative or zero
-------------------------RULES-----------------------------------------
Explicit:

Implicit:
------------------------EXAMPLES--------------------------------------
negative(5) == -5
negative(-3) == -3
negative(0) == 0      # There's no such thing as -0 in ruby

--------------------------ALGORITHM-----------------------------------
Goal:
Detect if a given number is positive, negative or zero. If positive, convert to negative and return; otherwise, return

Steps:
- Detect if a num is positive
  - num > 0
  - convert to negative (-num)
- Detect if a num is negative or zero
  - num  <= 0
  - return
=end

```ruby
def negative(num)
  return -num if num > 0
  num
end

p negative(5) == -5
p negative(-3) == -3
p negative(0) == 0 
```

------------------------

### Exersise 4: Counting Up

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes an integer argument, and returns an Array of all integers, in sequence, between 1 and the argument.

You may assume that the argument will always be a valid integer that is greater than 0.
------------------------PROBLEM--------------------------------------
Input: Integer

Output: Array of integers --> list of nums from 1 to the given int
-------------------------RULES-----------------------------------------
Explicit:
- Argument will always be a valid integer greater than 0

Implicit:
- If given integer is 1, return [1]
- The given integer is equal to the num of elements in returning array
------------------------EXAMPLES--------------------------------------
sequence(5) == [1, 2, 3, 4, 5]
- create an array of 5 elements
- populate from 1 up to given int

sequence(3) == [1, 2, 3]
sequence(1) == [1]

--------------------------ALGORITHM-----------------------------------
Goal:
Given a positive integer, build an array of integers from 1 to given integer, bith included

Ideas:
- Create an empty array
- Append 1 (<<)
- Append arr[0]+1
- Append arr[1]+1
- Append arr[2]+1

Steps:
- Create an array with int num of elements
- Iterate array num of elements (with map)
- Iterate with index (map.with_index)
- at each iteration
  - arr[idx] = 1 + idx
- return arr

```ruby
def sequence(int)
  seq_arr = Array.new(int) 

  seq_arr.map!.with_index do |item, idx|
    seq_arr[idx] = 1 + idx
  end
end

p sequence(5) == [1, 2, 3, 4, 5]
p sequence(3) == [1, 2, 3]
p sequence(1) == [1]
```

------------------------

### Exersise 5: Uppercase Check

---------------------INSTRUCTIONS------------------------------------
Write a method that takes a string argument, and returns true if all of the alphabetic characters 
inside the string are uppercase, false otherwise. Characters that are not alphabetic should be ignored.

------------------------PROBLEM--------------------------------------
Input: 
- String

Output: 
- Boolean: true if all chars in given string are uppercase; false otherwise
-------------------------RULES---------------------------------------
Explicit:
- Ignore non-alphabetical chars

Implicit:
- If empty string is given, return true (????)
------------------------EXAMPLES--------------------------------------
uppercase?('t') == false
uppercase?('T') == true
uppercase?('Four Score') == false
uppercase?('FOUR SCORE') == true
uppercase?('4SCORE!') == true
uppercase?('') == true

--------------------------ALGORITHM-----------------------------------
Goal:
- Detect if a given string chars are all uppercase or not

Ideas:
- Create a collection of uppercase alphabetical chars to check against
- Iterate given string to check if every char is included in the list of uppercase valid chars
- If so, return true; otherwise, return false
- Ignore non-alpha chars
  - Use select to select only valid chars and then check if they are uppercase

Steps:
- alpha_upp = ('A'..'Z').to_a
- alpha_low = ('a'..'z').to_a
- all_alpha = alpha_upp | alpha_low
- Select string.chars if char is included in all_alpha
- The return of prev. line check if all are included in alpha_upp
  - if so, return true
  - otherwise, return false

```ruby
ALPHA_UPCASE = ('A'..'Z').to_a
ALPHA_LOWCASE = ('a'..'z').to_a
ALL_ALPHA = ALPHA_UPCASE | ALPHA_LOWCASE

def uppercase?(string)
  only_alpha = string.each_char.select {|char| ALL_ALPHA.include?(char)}
  only_alpha.all? {|char| ALPHA_UPCASE.include?(char)}
end

p uppercase?('t') == false
p uppercase?('T') == true
p uppercase?('Four Score') == false
p uppercase?('FOUR SCORE') == true
p uppercase?('4SCORE!') == true
p uppercase?('') == true
```

------------------------

### Exersise 6: How long are you?

---------------------INSTRUCTIONS------------------------------------
Write a method that takes a string as an argument, and returns an Array that contains every word from the string, 
to which you have appended a space and the word length.

You may assume that words in the string are separated by exactly one space, and that any substring 
of non-space characters is a word.

------------------------PROBLEM--------------------------------------
Input: 
- String of substrings (words)

Output: 
- Array of words + space + lenght of word
-------------------------RULES---------------------------------------
Explicit:
Implicit:
------------------------EXAMPLES--------------------------------------
word_lengths("cow sheep chicken") == ["cow 3", "sheep 5", "chicken 7"]

word_lengths("baseball hot dogs and apple pie") ==
  ["baseball 8", "hot 3", "dogs 4", "and 3", "apple 5", "pie 3"]

word_lengths("It ain't easy, is it?") == ["It 2", "ain't 5", "easy, 5", "is 2", "it? 3"]

word_lengths("Supercalifragilisticexpialidocious") ==
  ["Supercalifragilisticexpialidocious 34"]

word_lengths("") == []
--------------------------ALGORITHM-----------------------------------
Goal:
- Obtain words of given string, determine their length and return the word plus lenth separate by blank space

Ideas:
- Split string in separate words: split returns an array of words
- Iterate each element and count lenght of element
- Reassign each element to element + ' ' + length of element


Steps:
- array = string.split
- array map word | word = word + ' ' + word.lenght
- return array

```ruby
def word_lengths(string)
  array = string.split

  array.map!.with_index do |word, idx|
    word = word + ' ' + word.size.to_s
  end 

end

p word_lengths("cow sheep chicken") == ["cow 3", "sheep 5", "chicken 7"]

p word_lengths("baseball hot dogs and apple pie") ==
  ["baseball 8", "hot 3", "dogs 4", "and 3", "apple 5", "pie 3"]

p word_lengths("It ain't easy, is it?") == ["It 2", "ain't 5", "easy, 5", "is 2", "it? 3"]

p word_lengths("Supercalifragilisticexpialidocious") ==
  ["Supercalifragilisticexpialidocious 34"]

p word_lengths("") == []
```

------------------------

### Exersise 7: Name Swapping

---------------------INSTRUCTIONS------------------------------------
Write a method that takes a first name, a space, and a last name passed as a single String argument, 
and returns a string that contains the last name, a comma, a space, and the first name.

------------------------PROBLEM--------------------------------------
Input: String (name and surname)

Output: String (surname, name)
-------------------------RULES---------------------------------------
Explicit:

Implicit:

------------------------EXAMPLES--------------------------------------
swap_name('Joe Roberts') == 'Roberts, Joe'

--------------------------ALGORITHM-----------------------------------
Goal:
- Given a name and surname, reverse the order of elements and separate them with a comma

Ideas:
- Convert string into array of words
- Reverse the order of elements
- Append a comma to the new 1st element

Steps:
- words = string.split --> return array of substrings in given string
- words.reverse --> Reverse the order of elements in array
- word[0]<< ',' --> append a comma to the end of element 0 (surname)

```ruby
def swap_name(name)
  words = name.split.reverse
  words[0] << ','
  words.join(' ')
end

p swap_name('Joe Roberts') == 'Roberts, Joe'
```

------------------------

### Exersise 8: Sequence Count

---------------------INSTRUCTIONS------------------------------------
Create a method that takes two integers as arguments. The first argument is a count, and the second is the first number 
of a sequence that your method will create. The method should return an Array that contains the same number of elements 
as the count argument, while the values of each element will be multiples of the starting number.

You may assume that the count argument will always have a value of 0 or greater, while the starting number can 
be any integer value. If the count is 0, an empty list should be returned.

------------------------PROBLEM--------------------------------------
Input: 
- Two integers: 1st --> count ; 2nd --> starting num of a list

Output: 
- Array with count num of elements starting at arg2 int and all the others multiples of that 2nd arg 
-------------------------RULES---------------------------------------
Explicit:
- Count arg --> always >= 0
- Starting arg --> any integer (positive or negative)

Implicit:
- 2nd argument is summatory: every element starting at 2nd arg, will be a num + 2nd arg
------------------------EXAMPLES--------------------------------------
sequence(5, 1) == [1, 2, 3, 4, 5]
-- arg1 -> 5 -> 5 elements array | arg2 -> 1 -> element[0]=arg2, element[1]=element[0]+arg2, element[2]=element[1]+arg2
sequence(4, -7) == [-7, -14, -21, -28]
sequence(3, 0) == [0, 0, 0]
sequence(0, 1000000) == []
--------------------------ALGORITHM-----------------------------------
Goal:
- Given 2 argument, create an array with arg1 num of elements that start at arg2 and add arg2 to each element up to end of arr

Ideas:
- Create new Array with arg1 elements --> Array.new(arg1) --> [nil, nil, nil, nil, etc...]
- Iterate array and reassign each element
  - element[0] = arg2
  - element[1] = element[0] + arg2
  - element[2] = element[1] + arg2
  - etc.. up to end of array

- Use .times
  - arg1 times do

Steps:
- array = Array.new(arg1)
- array[0] = arg2

- array map!.with_index item
  - array[index] += arg2
end

- create array with first element as arg2 | arr = [arg2]
- arg1.times do 
  arr << arr[index] + arg2

```ruby  
def sequence(count, start)
  return [] if count == 0
  
  array = [start]

  index = 0

  (count-1).times do 
    array << array[index] + start
    index += 1
  end

  array
end

p sequence(5, 1) == [1, 2, 3, 4, 5]
p sequence(4, -7) == [-7, -14, -21, -28]
p sequence(3, 0) == [0, 0, 0]
p sequence(0, 1000000) == []
```

------------------------

### Exersise 9: Grade book

---------------------INSTRUCTIONS------------------------------------
Write a method that determines the mean (average) of the three scores passed to it, 
and returns the letter value associated with that grade.

Numerical Score Letter	|  Grade
90 <= score <= 100	    |  'A'
80 <= score < 90	      |  'B'
70 <= score < 80	      |  'C'
60 <= score < 70	      |  'D'
0 <= score < 60	        |  'F'

Tested values are all between 0 and 100. There is no need to check for negative values or values greater than 100.

------------------------PROBLEM--------------------------------------
Input: 
- Three integers: three different scores

Output: 
- A string: the letter that corresponds to the average of the three grades passed
-------------------------RULES---------------------------------------
Explicit:
- All given scores are from 0 to 100
- No need to check for negative scores
- No need to check for scores greater than 100
Implicit:

------------------------EXAMPLES--------------------------------------
get_grade(95, 90, 93) == "A"
  - average of 95, 90 and 93 is 92 --> 92 corresponds to 'A'

get_grade(50, 50, 95) == "D"
  - average of 50, 50 and 95 is 65 --> 65 corresponds to 'D'

--------------------------ALGORITHM-----------------------------------
Goal:
- calculate the average of three given scores and return the letter string that correspond to that average according to a given table

Steps:
- Calculate average of the three argument
  - (arg1 + arg2 + arg3) / 3

- Create an case statement with result of avg
  case avg
  if 90 <= avg <= 100	then 'A' 
  if  80 <= avg < 90 then 'B'       
  if 70 <= avg < 80 then 'C'     
  if 60 <= avg < 70 then 'D' 	      
  else 'F' 	      
  end  

```ruby
def get_grade(grade1, grade2, grade3)
  average = (grade1 + grade2 + grade3) / 3

  if average >= 90 && average <= 100 
    'A' 
  elsif average >= 80 && average < 90 
    'B'       
  elsif average >= 70 && average < 80 
    'C'     
  elsif average >= 60 && average < 70 
    'D' 	      
  else 
    'F' 
  end
end

p get_grade(95, 90, 93) == "A"
p get_grade(50, 50, 95) == "D"
```

------------------------

### Exersise 10: Grocery List

---------------------INSTRUCTIONS------------------------------------
Write a method which takes a grocery list (array) of fruits with quantities 
and converts it into an array of the correct number of each fruit.

------------------------PROBLEM--------------------------------------
Input: 
- Nested array with two items per element: a string and an integer

Output: 
- Single array with number of string items determined by integer
-------------------------RULES---------------------------------------
Explicit:
- 
Implicit:
- 
------------------------EXAMPLES--------------------------------------
buy_fruit([["apples", 3], ["orange", 1], ["bananas", 2]]) ==
  ["apples", "apples", "apples", "orange", "bananas","bananas"]

--------------------------ALGORITHM-----------------------------------
Goal:
- Create a single array with elements determined by string and integer of given nested array

Ideas:
- Create an empty array
- Iterate each element of given nested array
- Multiply element 0 times element 2 and append the result to empty array
- flatten the result

Steps:
- grocery_list = []
- nested_arr each subarray
  - grocery_list append -> subarray[0] * subarray[1]
end

return grocery_list flatten

```ruby
def buy_fruit(nested_array)
  grocery_list = []

  nested_array.each do |subarray|
    grocery_list << [subarray[0]] * subarray[1]

  end

  grocery_list.flatten
end

p buy_fruit([["apples", 3], ["orange", 1], ["bananas", 2]]) ==
  ["apples", "apples", "apples", "orange", "bananas","bananas"]
```

------------------------

### Exersise 11: Group Anagrams

---------------------INSTRUCTIONS------------------------------------
Given the array:
words =  ['demo', 'none', 'tied', 'evil', 'dome', 'mode', 'live',
          'fowl', 'veil', 'wolf', 'diet', 'vile', 'edit', 'tide',
          'flow', 'neon']

Write a program that prints out groups of words that are anagrams. 
Anagrams are words that have the same exact letters in them but in a different order. 
Your output should look something like this:

["demo", "dome", "mode"]
["neon", "none"]
#(etc)
------------------------PROBLEM--------------------------------------
Input: 
- Array of strings
Output: 
- Nested array where each subarray are strings that are anagrams 
-------------------------RULES---------------------------------------
Explicit:
- Anagrams are words that have the same exact letters in them but in a different order. 
Implicit:
- Anagrams always are strings with same length
- All given strings are the same length (no need to check if same length is true)
------------------------EXAMPLES--------------------------------------

--------------------------ALGORITHM-----------------------------------
Goal:
- Find all words that are anagrams of each other in a list of words and put them as arrays inside an array

Ideas:
- Double loop
  - loop each word
    - loop each letter in words

  - need an index
  - need to stablish current word (change at every iteration of outer loop)
  - need to check if current word has same chars than current word + 1
  - if so, add to new array and move to next word and check the same
  - keep checking until a false is returned
  - then break and return array

  - next iteration of outer loop
    
Steps:
- returning_array = []
- index = 0
- loop do
  - initialize empty array; anagram = []
  - iterate each word included in the given array
  - stablish current_word as current word in iteration
  - add current word to anagram
  - check if current_word is equal than current_word + index
    - if so, put it also anagram
    - otherwise next word
  - if no true, clear anagram

```ruby
def anagrams(input_array)
  output_array = []
  index = 0                                    

  loop do
    break if index == input_array.size         
                 
    current_word = input_array[index]
    anagram = []                   

    input_array.each do |word|
      if current_word.each_char.sort.join == word.each_char.sort.join
        anagram << word
      else
        next
      end  
      anagram
    end
    
    output_array << anagram if anagram.size > 1
    index += 1
  end
  output_array.uniq.each {|subarr| p subarr}
end

words =  ['demo', 'none', 'tied', 'evil', 'dome', 'mode', 'live',
          'fowl', 'veil', 'wolf', 'diet', 'vile', 'edit', 'tide',
          'flow', 'neon']

anagrams(words)

#second version
words =  ['demo', 'none', 'tied', 'evil', 'dome', 'mode', 'live',
          'fowl', 'veil', 'wolf', 'diet', 'vile', 'edit', 'tide',
          'flow', 'neon']

def same?(array, string)
  array.each_with_object([]) do |word, obj_arr|
    if string.chars.sort.join == word.chars.sort.join
      obj_arr << word
    else
      next
    end
  end
end

def anagrams(words)
  counter = 0
  result = []
  
  loop do
    break if counter == words.size
    
    current_word = words[counter]     #'none'

    anagrams = same?(words, current_word)
  
    result << anagrams
    counter += 1
  end
    
 result.uniq.each {|anag| p anag} # nested array
end

anagrams(words)
```
