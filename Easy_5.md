##  RB101-RB109 - Small Problems --> EASY 5

**This set of exercises are solved using a PEDAC approach**

### Exersise 1: ASCII String Value

Write a method that determines and returns the ASCII string value of a string that is passed in as an argument. The ASCII string value is the sum of the ASCII values of every character in the string. (You may use String#ord to determine the ASCII value of a character.)

Examples
```ruby
ascii_value('Four score') == 984
ascii_value('Launch School') == 1251
ascii_value('a') == 97
ascii_value('') == 0
```

##### Alonso's version

##### P:
- generate the ASCII value of a given string
- it works by adding the ASCII value of each char in input string
- can access the ASCII value of a char with `char.ord` method
- if empty string, return 0
- space has an ASCII value (32)

##### A:
- iterate input string
- determine ASCII value of each char
- use `ord` method on each char
- save the value
- add all the values together
- return the total value

##### C:

```ruby
def ascii_value(input)
  return 0 if input.empty?                    # This is use as security in case arr is empty; if so, however, the each won't 
                                              # run because of empty element when arr eleme == ''. 
  total_ascii_val = 0

  input.chars.each do |char|
    total_ascii_val += char.ord
  end

  total_ascii_val
end
```

##### Nico's version
```ruby
def ascii_value(string)
  string.chars.map { |char| char.ord }.sum      # Array#sum method returns the sum of elements of array 
end


def ascii_value(string)
  string.chars.map(&:ord).sum                   # Same as above but using the short syntax in map (&:ord)           
end

def ascii_value(string)
  string.chars.inject(0) { |sum, char| sum + char.ord }   # Enum#inject (or reduce) 
end
```

------------------------

### Exersise 2: After Midnight (Part 1)

The time of day can be represented as the number of minutes before or after midnight. If the number of minutes is positive, the time is after midnight. If the number of minutes is negative, the time is before midnight.

Write a method that takes a time using this minute-based format and returns the time of day in 24 hour format (hh:mm). Your method should work with any integer input.

You may not use ruby's `Date` and `Time` classes.

Examples:
```ruby
time_of_day(0) == "00:00"
time_of_day(-3) == "23:57"
time_of_day(35) == "00:35"
time_of_day(-1437) == "00:03"
time_of_day(3000) == "02:00"
time_of_day(800) == "13:20"
time_of_day(-4231) == "01:29"
```

##### Alonso's version

##### ----------------------INSTRUCTIONS-----------------------------------

The time of day can be represented as the number of minutes before or after midnight. 
If the number of minutes is positive, the time is after midnight. 
If the number of minutes is negative, the time is before midnight.

Write a method that takes a time using this minute-based format and returns the time of day in 24 hour format (hh:mm). 
Your method should work with any integer input.

You may not use ruby's Date and Time classes.

Examples:

```ruby
time_of_day(0) == "00:00"
time_of_day(-3) == "23:57"
time_of_day(35) == "00:35"
time_of_day(-1437) == "00:03"
time_of_day(3000) == "02:00"
time_of_day(800) == "13:20"
time_of_day(-4231) == "01:29"
```

##### -------------------------PROBLEM--------------------------------------

Input: Integer

Output: Numerical string in 24 hour format 'hh:mm'

##### --------------------------RULES-----------------------------------------

Explicit: 
  -> argument integer represents number of minutes over or under midnight
  -> if positive -> minutes after midnight (00:00) 
  -> if negative -> minutes before midnight (00:00) 

Implicit:
  -> 24 hours equals 1440 minutes (24h * 60min)
  -> if input larger than 1439, hour starts at 0 
  -> in hours, a day start at 00:00 and end at 23:59
  -> in minutes, a day starts at 0 mins and ends at 1439 mins

Questions?

##### -------------------------EXAMPLES--------------------------------------

time_of_day(0) == "00:00"
  -> input is 0, not negative not positive, we don't count minutes
  -> so it's 00:00

time_of_day(-3) == "23:57"
  -> input is -3 | negative means before 00:00
  -> so it's 3 minutes under 00:00 --> 23:57

time_of_day(35) == "00:35"
  -> input is 35 | positive means before 00:00
  -> so it's 35 minutes over 00:00 --> 00:35

time_of_day(-4231) == "01:29"
  -> input is -4231 | negative means before 00:00
  -> so it's -4231 minutes under 00:00 --> 01:29

##### -------------------------DATA STRUCTURE-------------------------------

##### ---------------------------ALGORITHM-----------------------------------

- detect if given minutes are over or under 00:00
- if negative input --> under 00:00
- if positive input --> over 00:00

- given the input minutes, calculate how many minutes input is, starting at 1440 min in 24 hours
- once having number of minutes
  - divide by 60 to calculate hours
  - take remainder and calculate hours and minutes
  - if extra hour, add it to remainder
  - save hours and minutes in separate variables
  - convert the variable values to string
  - concatenate both strings with : simbol in between and return

##### --------------------------CODE---------------------------------
```ruby
def time_of_day(input)
  return "00:00" if input == 0

  hrs_in_day = 24
  mins_in_hr = 60   
  
  minutes = input % mins_in_hr      # div input by 60 and the remainder are the minutes
  minutes = minutes.to_s
  minutes.prepend('0') if minutes.size == 1

  hours = (input / mins_in_hr) % hrs_in_day    # div input by 60 and the result by 24 and the remainder are the hours
  hours = hours.to_s
  hours.prepend('0') if hours.size == 1

  hours + ":" + minutes
end
```

- For more information on remainder, modulo and divmod method:
https://launchschool.com/books/ruby/read/basics#modulovsremainder

##### Nico's version

##### -------------------------PROBLEM--------------------------------------

Input: integer representing minutes
Output: string representing time of day in "hh:mm" format

##### ---------------------------ALGORITHM-----------------------------------
**** working with integer divisions
- minutes_per_day = 60 * 24

- time_in_minutes = (minutes_per_day + (input % minutes_per_day) ) % minutes_per_day
**We use "(minutes_per_day + input%minutes*day)" to account for negative inputs

- assign `hours` to the result of integer division (`time_in_minutes` / 60)
- assign `minutes` to the remainder of dividing (`time_in_minutes` / 60)- 

- convert numbers below 10 to strings starting with 0. example: 6 --> "06"
- convert other numbers to_s

- concatenate `hours` converted to string + ":" + `minutes` converted to string and return that value

##### --------------------------CODE---------------------------------
```ruby
# Code using Numeric#remainder method

def time_of_day(int)
  minutes_per_day = 24 * 60
  time_in_minutes = (minutes_per_day + int.remainder(minutes_per_day))
                    .remainder(minutes_per_day)
  hours = time_in_minutes / 60
  minutes = time_in_minutes % 60
  to_string(hours) + ":" + to_string(minutes)
end
def to_string(int)
  int < 10 ? "0" + int.to_s : int.to_s
end
```

```ruby
# Code using Numeric#% method

def time_of_day(int)
  minutes_per_day = 24 * 60
  time_in_minutes = int % minutes_per_day
  hours = time_in_minutes / 60
  minutes = time_in_minutes % 60
  to_string(hours) + ":" + to_string(minutes)
end
def to_string(int)
  int < 10 ? "0" + int.to_s : int.to_s
end
```

```ruby
# Refactored

def time_of_day(int)
  hours = ((int / 60) % 24).to_s
  minutes = (int % 60).to_s
  [hours, minutes].each { |str| str.prepend("0") if str.size == 1 }
  hours + ":" + minutes
end
```

```ruby
# Using the divmod method
def time_of_day(int)
  (int % (24 * 60)).divmod(60).map { |num| format("%02d", num) }.join(":")
end
```

------------------------

### Exersise 3: After Midnight (Part 2)

As seen in the previous exercise, the time of day can be represented as the number of minutes before or after midnight. If the number of minutes is positive, the time is after midnight. If the number of minutes is negative, the time is before midnight.

Write two methods that each take a time of day in 24 hour format, and return the number of minutes before and after midnight, respectively. Both methods should return a value in the range 0..1439.

You may not use ruby's Date and Time methods.

Yes, we know that 24:00 isn't a valid time in 24-hour format. Humor us, though; it makes the problem more interesting.

##### -------------------------PROBLEM--------------------------------------

input = string
output = positive integer --> representing minutes

re-statement of the problem:

-- after_midnight method calculates the amount of minutes from midnight to input
-- before_midnight calculates the amount of minutes from input to midnight

##### ---------------------------ALGORITHM-----------------------------------

after_midnight method
- calculate input (hours and minutes) in minutes
  - hours * 60 minutes + minutes --> I have total minutes

- input[0...2].to_i --> hours as int obj
- input[3..-1].to_i --> minutes asint obj


 "00:10" before midnight ---> 00:00 -10 --- 1430

```ruby
def after_midnight(string)
  hours = (string[0..1].to_i) % 24
  minutes = (string[3..-1].to_i)
  
  hours * 60 + minutes
end

def before_midnight(string)
  hours, minutes = string.split(":").map(&:to_i)

  -((hours % 24) * 60 + (minutes)) % 1440
end

# def before_midnight(string)
#   -after_midnight(string) % 1440
# end

  
p after_midnight('00:00') == 0
p before_midnight('00:00') == 0
p after_midnight('12:34') == 754
p before_midnight('12:34') == 686
p after_midnight('24:00') == 0
p before_midnight('24:00') == 0

p after_midnight('27:73')
p before_midnight('27:73')
```

------------------------

### Exersise 4: Letter Swap

----------------------INSTRUCTIONS-----------------------------------
Given a string of words separated by spaces, write a method that takes this  string of words and returns a string in which the first and last letters of  every word are swapped.

You may assume that every word contains at least one letter, and that the  string will always contain at least one word. You may also assume that each string contains nothing but words and spaces

-------------------------PROBLEM--------------------------------------
Input:
    -> string of words (sub-strings) - can be single or multiple (space separated) 
Output:
    -> string of words (single or multiple) swaping 1st char by last char of each sub-string
    -> new string or mutated string (not specified)

--------------------------RULES-----------------------------------------
Explicit:
    -> input cannot be empty string
    -> minimum chars in substring is 1 
    -> minimum sub-string in string is 1
    -> if multiple sub-string, they'll be separated by space
    -> no invalid characters, only chars (could be numberic characters?)

Implicit:
    -> when swaping 1st char by last char, keep the original character case (if input 'Ah', output 'hA') 
Questions?

-------------------------EXAMPLES--------------------------------------
swap('Oh what a wonderful day it is') == 'hO thaw a londerfuw yad ti si'
  -> input: 'Oh what a wonderful day it is'
  -> sub-str 1: 'Oh' --> becomes 'hO'
  -> sub-str 2: 'what' --> becomes 'thaw'
  -> sub-str 3: 'a' --> becomes 'a' --> single char, cannot be swapped
  -> sub-str 4: 'wonderful' --> becomes 'londerfuw'
  etc...
swap('Abcde') == 'ebcdA'
  -> input: 'Abcde'
  -> sub-str 1 (and only): 'Abcde' --> becomes 'ebcdA'
swap('a') == 'a'
  -> input: 'a'
  -> sub-str 1 (and only): 'a' --> becomes 'a' --> single char, cannot be swapped

-------------------------DATA STRUCTURE-------------------------------
-> String as inpit
-> Array of substrings in string for iteration
-> String as output

---------------------------ALGORITHM-----------------------------------
-> Goal:
      -> iterate over each substring of input string and swap the char at index 0 for char at index -1
      -> return the string with swapped chars

-> Convert input str to array (split)
-> Detect index 0 of substrings
-> Detect index -1 of subtrings
-> Swap the chars at these two positions
-> Convert the array back to an string -- join(' ')
-> Return the new string       

#---------------------------------CODE------------------------------------
```ruby
def swap(str)
  substrs = str.split                                      # ["Oh", "what", "a", "wonderful", ....]
  substr_char = substrs.map { |substr| substr.chars}       # [["O", "h"], ["w", "h", "a", "t"], ["a"]...
  
  substr_char.each do |char|
    char_0 = char.shift
    char_1 = char.pop
    char.unshift(char_1)
    char.push(char_0)
  end

  substr_char.map! { |char| char.join }
  substr_char.join (' ')

end

p swap('Oh what a wonderful day it is') == 'hO thaw a londerfuw yad ti si'
p swap('Abcde') == 'ebcdA'
p swap('a') == 'a'
```

### Nico's solution
```ruby
def swap(string)
  new_words = string.split.map do |word| 
                word[0], word[-1] = word[-1], word[0]
                word
              end

  new_words.join(" ")
end
```
------------------------

### Exersise 5: Clean up the words 

----------------------INSTRUCTIONS-----------------------------------
Given a string that consists of some words (all lowercased) and an assortment of non-alphabetic characters, 
write a method that returns that string with all of the non-alphabetic characters replaced by spaces. 
If one or more non-alphabetic characters occur in a row, you should only have one space in the result 
(the result should never have consecutive spaces).

cleanup("---what's my +*& line?") == ' what s my line '

-------------------------PROBLEM--------------------------------------

Input: String of alphabetical and non alphabetical characters

Output: The same string, mutated, where every non alphabetica character is replaced by a space

--------------------------RULES-----------------------------------------

Explicit:
        -> Every non-alphabetic char in input string must be replaced by space
        -> If two or more non-alphabetic char consecutive, replace them all by ONE space
        -> The mutated string must not have consecutive spaces
        -> Input string will always be lowercase 

Implicit:
        -> The mutated string can begin and end in an empty space if the input starts or ends with non-alphabetic chars
Questions?

-------------------------EXAMPLES--------------------------------------
cleanup("---what's my +*& line?") == ' what s my line '
  -> input string: "---what's my +*& line?"
  -> replace --- by ' '
  -> replace ' by ' '
  -> replace +*& by ' '
  -> replace ? by ' '
  -> so the resulting string would be ' what s my line '  

-------------------------DATA STRUCTURE-------------------------------
-> string for input and mutated string for output
-> perhaps array to iterate the string elements
---------------------------ALGORITHM-----------------------------------
goal)
    -> mutate input string by replacing every non-alphabetic char (individually or in groups) by one single empty space

-> convert input into an array of characters (chars)
-> iterate the array and if non-alhpabetic char is detected, replace it in place by ' '
-> while iterating, when non-alphabetic char is detected, check if next char is also a non-alphabetic char
    -> if so, group them up and replace them all together by ' '
-> conver the resulting clean array back into an string
-> return that string

---------------------------------CODE------------------------------------
=end
```ruby
def cleanup(string)
  alpha = [*'a'..'z']
  stringchars = string.chars         # ['a', 'b', '&', '*', 'g']

  stringchars.map! do |char|
    if !alpha.include?(char) 
      char = ' '
    else
      char  
    end
  end

  # [" ", " ", " ", "w", "h", "a", "t", " ", "s", " ", "m", "y", " ", " ", " ", " ", " ", "l", "i", "n", "e", " "]
  
  #  [ " ", "w"
  count = 0 
  clone_arr = stringchars.clone
  clone_arr.each.with_index do |_, index|
     if clone_arr[index] == ' ' && clone_arr[index + 1] == ' '
       stringchars.delete_at(index - count)
       count += 1
     end
  end
  
  string[0..-1] = stringchars.join
end

p cleanup("---what's my +*& line?") #== ' what s my line '
```

### Helper method with Nico

```ruby
def delete_double_space!(array)
  count = 0 
  clone_arr = array.clone
  clone_arr.each.with_index do |_, index|
   if clone_arr[index] == ' ' && clone_arr[index + 1] == ' '
     array.delete_at(index - count)
     count += 1
   end
  end
end
  
def cleanup(string)
  alpha = [*'a'..'z']              
  stringchars = string.chars       
  
  stringchars.map! do |char|
    if !alpha.include?(char)
      char = ' '
    else
      char
    end
  end
    
delete_double_space!(stringchars)
string[0..-1] = stringchars.join
end
```

#### Notes:
- The first part of the problem is farly easy, we can clean an array of chars of unwanted characters by detecting them and swapping them with ' ' (empty space)
- The problem comes when we have several empty spaces and we want to reduce them to only one
- One solution is using the index of each char to check if next index is also a space (as deducted in the algorithm). What happened (to me initially) is that I was detecting the duplication and removing them at the same time. Because we are operating with indexes, when we delete a character the indexes get messed up and we ended up not deleting the correct chars.
- To solve this we've worked with two arrays, a copy (clone) of the original to iterate the indexes (we don't mutate this) and the original array where we perform the changes. 


### Regex solution by Nico
```ruby
p "---what's my +*& line?".gsub(/[^a-z]+/, " ")
#=> " what s my line "
```

### Alonso on March 8
```ruby
def cleanup(string)
  arr_char = string.chars
  
  clean = arr_char.map do |char|
    char.gsub(/[^a-z]/, ' ')
  end

  p clean 
  
  copy = clean.dup
  counter = 0
  copy.each_with_index do |_, index|
    if copy[index] == ' ' && copy[index + 1] == ' '
      clean.delete_at(index - counter)
      counter += 1
    end
  end

  clean.join
end

p cleanup("---what's my +*& line?") #== ' what s my line '
```

#### Notes:
- The counter variable that is used to delete elements from the clean array marks the index element to remove from the original in coparison with the copy. In some iterations we are deleting elements from the original so we use counter to adjust the index we need to delete next.

------------------------

### Exersise 6: Letter Counter (Part 1)

----------------------INSTRUCTIONS-----------------------------------
Write a method that takes a string with one or more space separated words and returns a hash that shows the number of words of different sizes.

Words consist of any string of characters that do not include a space.

-------------------------PROBLEM--------------------------------------
Input: String (words separated by spaces)

Output: Hash, where
  - keys are number of chars in each substring of different length 
  - values are the number of times a substring of that length appears in string

--------------------------RULES-----------------------------------------
Explicit:
  - words don't include spaces, if so it'll be considered a separate word
Implicit:
  - if input string is empty, return emtpy hash
  - input string is made of words (substrings) of consecutive valid chars
  - valid chars are alpha and non-alpha chars
  - if a word includes or end with a non-alpha ('end.'), the non-alpha is part of the word and counts a one char
  - count chars case insensitive (Albatros --> 8 chars | albatros --> 8 chars )
  - returning hash must be in ascending order

-------------------------EXAMPLES--------------------------------------
word_sizes('Four score and seven.') == { 3 => 1, 4 => 1, 5 => 1, 6 => 1 }
  - Four --> 4 characters
  - score --> 5 characters
  - and --> 3 characters
  - seven. --> 6 characters
  --> resulting hash: 1 word of 3 chars, 1 word of 4 chars, 1 word of 5 chars, 1 word of 6 chars

word_sizes('Hey diddle diddle, the cat and the fiddle!') == { 3 => 5, 6 => 1, 7 => 2 }
word_sizes("What's up doc?") == { 6 => 1, 2 => 1, 4 => 1 }
word_sizes('') == {}

---------------------------ALGORITHM-----------------------------------
- Convert input into an array of words (split method)
- Create an empty hash
- Iterate the array
- Count number of chars in first word in arr and create a key in new hash with that number
  - set value to 1
- Count num of chars of second word, if a key with that number exist in hash
  - increment the value + 1
  - otherwise, create a new key with that number and set value to 1
- Keep counting until the end of array

- Return the hash

```ruby
def word_sizes(string)
  return {} if string.empty?

  word_arr = string.split(' ')               # ["Four", "score", "and", "seven."]

  hash = word_arr.each_with_object({}) do |word, hash|
    if hash[word.size]
      hash[word.size] += 1
    else
      hash[word.size] = 1
    end
  end

  hash.sort.to_h
end

p word_sizes('Four score and seven.') == { 3 => 1, 4 => 1, 5 => 1, 6 => 1 }
p word_sizes('Hey diddle diddle, the cat and the fiddle!') == { 3 => 5, 6 => 1, 7 => 2 }
p word_sizes("What's up doc?") == { 6 => 1, 2 => 1, 4 => 1 }
p word_sizes('') == {}
```

------------------------

### Exersise 7: Letter Counter (Part 2)

----------------------INSTRUCTIONS-----------------------------------
Modify the word_sizes method from the previous exercise to exclude non-letters when determining word size. 
For instance, the length of "it's" is 3, not 4.
-------------------------PROBLEM--------------------------------------
Input: String

Output: Hash where
  - keys are the size of the words in input string
  - values are the number of times a word of same size appears in input string
  
--------------------------RULES-----------------------------------------
Explicit:
- count number of chars (size) in substrings of input string
- don't count non-alphabetical characters
Implicit:
- if input string is empty, return an empty hash
- don't consider chars case ('Bee' --> 3 chars | 'bee' --> 3 chars)
- returning hash in ascending order

-------------------------EXAMPLES--------------------------------------
word_sizes('Four score and seven.') == { 3 => 1, 4 => 1, 5 => 2 }
  - Four --> 4 chars
  - score --> 5 chars
  - and --> 3 chars
  - seven --> 5 chars (notice the dot isn't counted)
  - hash: 1 word of 3 chars; 1 word of 4 chars; 2 words of 5 chars
word_sizes('Hey diddle diddle, the cat and the fiddle!') == { 3 => 5, 6 => 3 }
word_sizes("What's up doc?") == { 5 => 1, 2 => 1, 3 => 1 }
word_sizes('') == {}

---------------------------ALGORITHM-----------------------------------
- clean up input string by removing non-alpha characters
- extract each substringn as element of array
- iterate array and create a hash (each_with_object) where
  - key is the size of a substring
  - value is 1
  - if another substring of same size appears, update the corresponging key to += 1

```ruby
def word_sizes(string)
  return {} if string.empty?

  string.gsub!(/[^a-z ]/i, '')

  hash = string.split(' ').each_with_object(Hash.new(0)) do |word, hash|
    hash[word.size] += 1
  end

  hash.sort.to_h
end

p word_sizes('Four score and seven.') == { 3 => 1, 4 => 1, 5 => 2 }
p word_sizes('Hey diddle diddle, the cat and the fiddle!') == { 3 => 5, 6 => 3 }
p word_sizes("What's up doc?") == { 5 => 1, 2 => 1, 3 => 1 }
p word_sizes('') == {}
```

------------------------

### Exersise 8: Alphabetical Numbers

----------------------INSTRUCTIONS-----------------------------------
Write a method that takes an Array of Integers between 0 and 19, and returns an Array of those Integers sorted based on the English words for each number:

zero, one, two, three, four, five, six, seven, eight, nine, ten, eleven, twelve, thirteen, fourteen, fifteen, sixteen, seventeen, eighteen, nineteen

-------------------------PROBLEM--------------------------------------
Input: Array of integers (from 0 to 19)

Output: Array with same elements sorted according to their names in English

--------------------------RULES-----------------------------------------
Explicit:
  - sort elements by alphabetical correspondence of number 1 --> one, 4 --> four (4 goes before 1)

Implicit:

-------------------------EXAMPLES--------------------------------------
alphabetic_number_sort((0..19).to_a) == [
  8, 18, 11, 15, 5, 4, 14, 9, 19, 1, 7, 17,
  6, 16, 10, 13, 3, 12, 2, 0
]

---------------------------ALGORITHM-----------------------------------
- Create a structure that determines the alphabetical representation of numbers from 0 to 19: hash
- iterate given string
  - use alphabetical structure (hash) to determine the alpabetical representation of each number
  - use that string representation to order the elements
  - use alphabetical structure (hash) to convert back the alpabetical representation to number, preserving the order  

```ruby
NUM_TO_ALPHA = { 0=>'zero', 1=>'one', 2=>'two', 3 =>'three', 4=>'four', 5=>'five', 6=>'six', 7=>'seven', 8=>'eight',          9=>'nine', 10=>'ten', 11=>'eleven', 12=>'twelve', 13=>'thirteen', 14=>'fourteen', 15=>'fifteen', 16=>'sixteen', 17=>'seventeen', 18=>'eighteen', 19=>'nineteen'}

def alphabetic_number_sort(array)
  alpha_array = array.map do |num|                        # ["eight", "eighteen", "eleven", "fifteen", "five",...]
    NUM_TO_ALPHA[num]
  end

  sorted_array = alpha_array.sort.map do |word|           # [8, 18, 11, 15, 5,...]
    NUM_TO_ALPHA.key(word)
  end
end

p alphabetic_number_sort((0..19).to_a) == [
  8, 18, 11, 15, 5, 4, 14, 9, 19, 1, 7, 17,
  6, 16, 10, 13, 3, 12, 2, 0
]
```
------------------------

### Exersise 9: ddaaiillyy ddoouubbllee

----------------------INSTRUCTIONS-----------------------------------
Write a method that takes a string argument and returns a new string that contains the value of the original string with all consecutive duplicate characters collapsed into a single character. You may not use String#squeeze or String#squeeze!.

-------------------------PROBLEM--------------------------------------
Input: 
- String with repeated characters

Output: 
- New string without repeated characters

--------------------------RULES-----------------------------------------
Explicit:
- cannot use squeeze method

Implicit:
- input string can have single or multiple subtrings
- input substrings can have alphabetical and non-alphabetical characters
- To be considered repeated char, must be a set of the same characters several times in a row
- If input string has only one char, return it
- If input string has no chars, return empty string

-------------------------EXAMPLES--------------------------------------
crunch('ddaaiillyy ddoouubbllee') == 'daily double'
- 'dd' -> becomes 'd'
- 'aa' -> becomes 'a'
- 'ii' -> becomes 'i'
- 'll' -> becomes 'l'
- 'yy' -> becomes 'y'
etc..

crunch('4444abcabccba') == '4abcabcba'
- '444' -> becomes '4'
crunch('ggggggggggggggg') == 'g'
- many times the same char becomes a single char of the same
crunch('a') == 'a'
crunch('') == ''

---------------------------ALGORITHM-----------------------------------
Goal:
- remove duplicated consecutive characters (alpha and non-alpha) from input and return new string

Edge cases:
- if input string size == 1 return the string
- if input string is empty return empty string

Other cases:
- convert input string into array for iteration
- use gsub to substitute repetition of same letters by only one
- use indexes to delete repeated characters
- use a new collection (array) to add characters
  - if next char is the same, don't add it
- convert the array back to string
- return the string  

```ruby
def crunch(string)
  return string if string.empty? || string.size == 1
  clean_array = []
  
  string.chars.each do |char|
    clean_array << char unless clean_array.last == char
  end

  clean_array.join
end

p crunch('ddaaiillyy ddoouubbllee') == 'daily double'
p crunch('4444abcabccba') == '4abcabcba'
p crunch('ggggggggggggggg') == 'g'
p crunch('a') == 'a'
p crunch('') == ''

# If squeeze method was allowed to use:

def crunch(string)
  return string if string.empty? || string.size == 1
  new_str = string.squeeze
end
```
------------------------

### Exersise 10: Bannerizer

---------------------INSTRUCTIONS-----------------------------------
Write a method that will take a short line of text, and print it within a box.
You may assume that the input will always fit in your terminal window.

------------------------PROBLEM--------------------------------------
Input: 
- String
Output:  
- Same string printed within a box
-------------------------RULES-----------------------------------------
Explicit:
- 
Implicit:
- to draw the box we'll use 
- + symbol for the four corners 
- - symbol for the upper and bottom parts 
- | symbol for the side parts
- between the text and the box there will always be one empty character in every part of the box
- if the input string is empty, an empty box will be printed

------------------------EXAMPLES--------------------------------------
print_in_box('To boldly go where no one has gone before.')
+--------------------------------------------+
|                                            |
| To boldly go where no one has gone before. |
|                                            |
+--------------------------------------------+

print_in_box('')
+--+
|  |
|  |
|  |
+--+
--------------------------ALGORITHM-----------------------------------
Goal:
- print a box that encloses a string with one empty space per side

- center method
- puts method
- string interpolation #{} 

- print a line starting with + and end with + and has as many - as characters in string.size + 2
- print the string with
  - | on index 0 - 2
  - | on index -1 + 2
- print a line starting with + and end with + and has as many - as characters in string.size + 2

```ruby
def print_in_box(string)
  size = string.size
  puts "+#{'-'*(size+2)}+"
  puts "|#{' '*(size+2)}|"
  puts "| #{string} |"
  puts "|#{' '*(size+2)}|"
  puts "+#{'-'*(size+2)}+"
end

print_in_box('To boldly go where no one has gone before.')
print_in_box('')
```
