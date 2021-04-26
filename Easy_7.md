##  RB101-RB109 - Small Problems --> EASY 7

**This set of exercises are solved using a PEDAC approach**

### Exersise 1: Combine Two Lists

---------------------INSTRUCTIONS-----------------------------------
Write a method that combines two Arrays passed in as arguments, and returns a new Array that contains all elements from both Array arguments, with the elements taken in alternation.

You may assume that both input Arrays are non-empty, and that they have the same number of elements.
 
------------------------PROBLEM--------------------------------------
Input: 2 Array (passed in as argum)

Output: New array --> combines element from 2 input arrays in alternation

-------------------------RULES-----------------------------------------
Explicit:
- Both input arrays have same num of elements
- Input array isn't empty
Implicit:

------------------------EXAMPLES--------------------------------------

 interleave([1, 2, 3], ['a', 'b', 'c']) == [1, 'a', 2, 'b', 3, 'c']
 --> arg1 --> [1, 2, 3]
 --> arg2 --> ['a', 'b', 'c']
 --> new_arr [idx0-arg1, indx0-arg2, indx1-arg1, index1-arg2, etc...
 ---> final resulting array --> [1, 'a', 2, 'b', 3, 'c']

--------------------------ALGORITHM-----------------------------------

Goal:
- Create a new array combining elements from 2 given arrays in alternate order

Egde cases
--> given args are single elem arrays
[1][3] --> [1,3]

Other cases:
- create a new_arr = []

- take arg 1
  - iterate its elements
  - add current element to new_arr
- take arg 2
  - iterate its elements
  - add current element to new_arr
- repeat with other element until the end

we can use index for both arrays and append each index iteration each respective index at `x`.

Ideas:
PSEUD: 

- iterate arrays with index ?? 
  - arr1.each_wit |itemn|
  - item # => `a`index 0
  - arr2.each_with
      item 
  - 
  
- iterate arrays with object([])
  - 

```ruby
# My solution
def interleave(arr1, arr2)

  new_arr = []
  
  arr1.each_with_index do |_, index|
    new_arr << arr1[index]
    new_arr << arr2[index]
  end
  
  new_arr
end

# Tonio refactoring
def interleave(arr1, arr2)

  new_arr = []
  
  0.upto(arr1.size-1) { |idx| new_arr.concat([arr1[idx]], [arr2[idx]]) }
  
  new_arr
end


p interleave([1, 2, 3], ['a', 'b', 'c']) == [1, 'a', 2, 'b', 3, 'c']
```

------------------------

### Exersise 2: Lettercase Counter

=begin
---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a string, and then returns a hash that contains 3 entries: one represents the number of characters in the string that are lowercase letters, one the number of characters that are uppercase letters, and one the number of characters that are neither.

------------------------PROBLEM--------------------------------------
Input: String of mixed alphanum and non-alphanum characters

Output: Hash with three keys-values pairs
:lowercase => num of lowercase chars in input
:upercase => num of upercse chars in input
:neither => num of non alphabetical chars

-------------------------RULES-----------------------------------------
Explicit:

Implicit:

------------------------EXAMPLES--------------------------------------
letter_case_count('abCdef 123') == { lowercase: 5, uppercase: 1, neither: 4 }
-:lowercase => ab def = 5
-:upercase => C = 1
-:neither =>  123 = 4 (there is an empty space that counts as non-alpha char)

letter_case_count('AbCd +Ef') == { lowercase: 3, uppercase: 3, neither: 2 }
letter_case_count('123') == { lowercase: 0, uppercase: 0, neither: 3 }
letter_case_count('') == { lowercase: 0, uppercase: 0, neither: 0 }
-if input string is empty, return has with keys with 0 as value

--------------------------ALGORITHM-----------------------------------
- Create constants with alphabetical chars
- Initialize hash var to emtpy hash
- Iterate the input string
  - convert it to array or use string.each_char
- If current char exist in alpha collection and is upercase 
  - create :upercase key and add 1 as value
  - if key already exist, add 1 to value (reassignment)
- If current char exist in alpha collection ans is lowecase
  - create :lowecase key and add 1 as value  
  - if key already exist, add 1 to value (reassignment)
- If current char does not exist in alpha collection
  - create :either key and add 1 as value
  - if key already exist, add 1 to value (reassignment)
- Return hash variable

```ruby
LOWCASE_ALPHA_CHARS = ('a'..'z').to_a
UPCASE_ALPHA_CHARS = ('A'..'Z').to_a

def letter_case_count(string)
  count_hash = {lowercase:0, uppercase:0, neither:0}

  string.each_char do |char|
    if LOWCASE_ALPHA_CHARS.include?(char)
      count_hash[:lowercase] += 1
    elsif UPCASE_ALPHA_CHARS.include?(char)
      count_hash[:uppercase] += 1
    else
      count_hash[:neither] += 1
    end
  end

  count_hash
end

p letter_case_count('abCdef 123') == { lowercase: 5, uppercase: 1, neither: 4 }
p letter_case_count('AbCd +Ef') == { lowercase: 3, uppercase: 3, neither: 2 }
p letter_case_count('123') == { lowercase: 0, uppercase: 0, neither: 3 }
p letter_case_count('') == { lowercase: 0, uppercase: 0, neither: 0 }
```

------------------------

### Exersise 3: Capitalize Words

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a single String argument and returns a new 
string that contains the original value of the argument with the 
first character of every word capitalized and all other letters lowercase.

You may assume that words are any sequence of non-blank characters.

------------------------PROBLEM--------------------------------------
Input: String made of several words (space separated substrings)

Output: New string with 1st char of words-substrings capitalized and the 
rest lowercase

-------------------------RULES-----------------------------------------
Explicit:

Implicit:

------------------------EXAMPLES--------------------------------------
word_cap('four score and seven') == 'Four Score And Seven'
- string made of 4 substrings all char lowercase
- new string has all 4 substrings capitalized

word_cap('the javaScript language') == 'The Javascript Language'
- string made of 3 substrings combining lower and uper case
- new string has all 3 substrings capitalized and other chars lowercase

word_cap('this is a "quoted" word') == 'This Is A "quoted" Word'
- string made of 5 substrings combining alpha a non alpha chars
- if non-alpha char is at begining of substring, capitalize it

--------------------------ALGORITHM-----------------------------------
- extract substrings to array 
- iterate each substring and 
  - capitalize or upcase index 0
  - lowercase every other index in substring
- join array and return (consider space (' ') when joining)

```ruby
def word_cap(string)
  cap = string.split.map do |word|
      word.capitalize
  end
  cap.join (' ')
end

p word_cap('four score and seven') == 'Four Score And Seven'
p word_cap('the javaScript language') == 'The Javascript Language'
p word_cap('this is a "quoted" word') == 'This Is A "quoted" Word'
```

------------------------

### Exersise 4: Swap Case

=begin
---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a string as an argument and returns a new string 
in which every uppercase letter is replaced by its lowercase version, 
and every lowercase letter by its uppercase version. 
All other characters should be unchanged.

You may not use String#swapcase; write your own version of this method.

------------------------PROBLEM--------------------------------------
Input: String

Output: New string swapping uppercase chars by lowercase chars and viceversa

-------------------------RULES-----------------------------------------
Explicit:
- Swap upper and lowercase chars
- Keep other chars the same (non-alphabetical chars)
- Don't use #swapcase method
Implicit:

------------------------EXAMPLES--------------------------------------
swapcase('CamelCase') == 'cAMELcASE'
- idx 0 - C && idx5 - C to lowercase
- all other idx to uppercase
swapcase('Tonight on XYZ-TV') == 'tONIGHT ON xyz-tv'
- same as example above
- but char - remains the same

--------------------------ALGORITHM-----------------------------------
- create a constant for uppercase chars (array)
- create a constant for lowercase chars (array)
- create a new var and initialize it to the return of:
- iterate each char of given string with map (return a new obj based on return val of block)
  - if current char is included in uppercase array, convert it to lowercase
  - if current char is included in lowercase arr, convert it to uppercase
  - if current char not included in any of above, keep it the same
- join the new array and return it as string    

```ruby
UPCASE = ('A'..'Z').to_a
LOWCASE = ('a'..'z').to_a

def swapcase(string)
  swapped = string.each_char.map do |char|
    if UPCASE.include?(char)
      char.downcase
    elsif LOWCASE.include?(char)
      char.upcase
    else
      char
    end
  end
  swapped.join
end

p swapcase('CamelCase') == 'cAMELcASE'
p swapcase('Tonight on XYZ-TV') == 'tONIGHT ON xyz-tv'
```

------------------------

### Exersise 5: Staggered Caps (Part 1)

=begin

----------------------INSTRUCTIONS-----------------------------------
Write a method that takes a String as an argument, and returns a new String that contains the original value using a staggered capitalization scheme in which every other character is capitalized, and the remaining characters are lowercase. Characters that are not letters should not be changed, but count as characters when switching between upper and lowercase.

-------------------------PROBLEM--------------------------------------

Input: String (single or multiple substrings)

Output: New string (same structure as input) with staggered capitalization

Staggered capitalization: starting at index 0 char interpolate upcase and lowcase char,being char at index 0 upcase, index 1 lowcase, etc.

--------------------------RULES-----------------------------------------

Explicit:
- take inout string and return new string with every other character capitalized, and the remaining characters are lowercase
- if current char is non-alphabetical, stays the same (but, counts as index for Staggering)

Implicit:
- if char of given string is upcase, but that position index corresponds to a lowercase, convert it to lowercase

-------------------------EXAMPLES--------------------------------------
staggered_case('I Love Launch School!') == 'I LoVe lAuNcH ScHoOl!'
staggered_case('ALL_CAPS') == 'AlL_CaPs'
staggered_case('ignore 77 the 444 numbers') == 'IgNoRe 77 ThE 444 NuMbErS'p 
-------------------------DATA STRUCTURE-------------------------------

---------------------------ALGORITHM-----------------------------------
 Goal:
 - return new string, with same structure as given string, where every other char is capitalized

- IDEAS:
- create an upcase constant array
- create an lowcase constant array


- iterate given string (maybe use chars to convert str to arr??)
- if current char is non-alpha
  - remains the same
- if current char is alpha AND is at upcase index AND is upcase
  - remains the same
- if current char is alpha AND is at upcase index AND is downcase
  - convert to upcase
- if current char is alpha AND is at downcase index AND is upcase
  - convert to upcase

- transform array back to string 
- return string
  
PSEUDO:

- iterate with each with index

```ruby
# Solution 1
def staggered_case(str)
  new_str = str.chars.map.with_index do |char, index|
    index.even? ? char.upcase : char.downcase
  end
  new_str.join
end

# Solution 2
def staggered_case(str)
  str.chars.map.with_index { |char, index| index.even? ? char.upcase : char.downcase }.join
end

p staggered_case('I Love Launch School!') == 'I LoVe lAuNcH ScHoOl!'
p staggered_case('ALL_CAPS') == 'AlL_CaPs'
p staggered_case('ignore 77 the 444 numbers') == 'IgNoRe 77 ThE 444 NuMbErS'
```

------------------------

### Exersise 6: Staggered Caps (Part 2)

Modify the method from the previous exercise so it ignores non-alphabetic characters when determining whether it should uppercase or lowercase each letter. The non-alphabetic characters should still be included in the return value; they just don't count when toggling the desired case.

=> Algorithm
  => Use and index to reference the desidered chars in the string (even and odd)
  => Iterate each char in the string
  => If the index is even, upcase the char
  => If the index is odd, downcase the char
  => Update the index only if the char is a valid char (ignore nums and punct when counting)

```ruby
VALID = ('a'..'z').to_a + ('A'..'Z').to_a

def staggered_case(string)
  idx = 0
  new = string.chars.each do |char|
    if idx.even?
      char.upcase!
    else
      char.downcase!
    end
    idx += 1 unless !VALID.include?(char)
  end
  new.join
end

p staggered_case('I Love Launch School!') == 'I lOvE lAuNcH sChOoL!'
p staggered_case('ALL CAPS') == 'AlL cApS'
p staggered_case('ignore 77 the 444 numbers') == 'IgNoRe 77 ThE 444 nUmBeRs'
```
------------------------

### Exersise 7: Multiplicative Average

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes an Array of integers as input, multiplies all the numbers together, divides the result by the number of entries in the Array, and then prints the result rounded to 3 decimal places. Assume the array is non-empty.

------------------------PROBLEM--------------------------------------
Input: Array of integers

Output: Float number with 3 decimals (resulting from multiplying all int in given arr and divide by size of arr)
-------------------------RULES-----------------------------------------
Explicit:
- Given array isn't empty
Implicit:
- 
------------------------EXAMPLES--------------------------------------
show_multiplicative_average([3, 5])                # => The result is 7.500
show_multiplicative_average([6])                   # => The result is 6.000
show_multiplicative_average([2, 5, 7, 11, 13, 17]) # => The result is 28361.667

--------------------------ALGORITHM-----------------------------------
Goal:
- Multiply all elements of given array and divide the result by num of elements in array (size)
- Round up the result to 3 decimals

- Iterate each element of array and multiply them to each other
- Divide the result of the multipplication by size of given array (by num of elements in array)
- Round up the result

- Multiply elements of an array
  - [1,2,3].inject(&:*)
- Number of elements in array
  - [1,2,3].count
- 

```ruby
def show_multiplicative_average(array)
  operation = ((array.inject(&:*)).to_f / (array.count).to_f).round(3)
end

p show_multiplicative_average([3, 5])                # => The result is 7.500
p show_multiplicative_average([6])                   # => The result is 6.000
p show_multiplicative_average([2, 5, 7, 11, 13, 17]) # => The result is 28361.667
```

------------------------

### Exersise 8: Multiply Lists

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes two Array arguments in which each Array contains a list of numbers, and returns a new Array that contains the product of each pair of numbers from the arguments that have the same index. You may assume that the arguments contain the same number of elements.

------------------------PROBLEM--------------------------------------
Input: Two arrays of integers

Output: New array (product of each pair of num of same index of input arrays)
-------------------------RULES-----------------------------------------
Explicit:
- The two given arrays contain the same num of elements
Implicit:
- No empty arrays
- Only integers as elements in input arrays
- Only integers (not float nums as elements of arrays)
------------------------EXAMPLES--------------------------------------
multiply_list([3, 5, 7], [9, 10, 11]) == [27, 50, 77]

--------------------------ALGORITHM-----------------------------------
Goal:
- Multiply the elements at same index of two given arrays and store the result in the same index of a new array

- Initialize empty array
- Iterate array 1 and multiply element at every index by same element-index of array 2
- store the result in same index of empty array
- return new array

- multiply elements of same index
  - map with index
  - arr1[index] * arr2[index]

```ruby
# Solution 1
def multiply_list(arr1, arr2)
  result = arr1.map.with_index do |_, index|
    arr1[index] * arr2[index]
  end
end

# Refactored
def multiply_list(arr1, arr2)
  arr1.map.with_index {|_, idx| arr1[idx] * arr2[idx]}
end

p multiply_list([3, 5, 7], [9, 10, 11]) == [27, 50, 77]
```

------------------------

### Exersise 9: Multiply All Pairs

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes two Array arguments in which each Array contains a list of numbers, and returns a new Array that contains the product of every pair of numbers that can be formed between the elements of the two Arrays. The results should be sorted by increasing value.

You may assume that neither argument is an empty Array.

------------------------PROBLEM--------------------------------------
Input: Two arrays of integers

Output: A new array of increasingly sorted integers that contains the product of every pair of numbers in both arrays
-------------------------RULES-----------------------------------------
Explicit:
- No empty arrays as input
- Sort the result increasingly
Implicit:

------------------------EXAMPLES--------------------------------------
multiply_all_pairs([2, 4], [4, 3, 1, 2]) == [2, 4, 4, 6, 8, 8, 12, 16]

--------------------------ALGORITHM-----------------------------------
Goal:
- Multiply every element of two given arrays and put them in an array and sort it increasingly

- Iterate array 1 and multiply every element by every element in array 2
- Store the result of the product in a new array
- Order the array from lower to larger
- Return the new array

PSEUD
- Map creates a new collection from the return value of the block
- I can iterate arr1 with map and multiply each value of arr1 by each val of arr2
- To access each element of array 2 in turns I can use a second iteration with map on arr2 
- I can alternatively use each and append the result to a new collection

```ruby
def multiply_all_pairs(arr1, arr2)
  result = []                         #[8, 12]
  arr1.each do |num1|                 # [2, 4]
    arr2.each do |num2|               # [4, 3, 1, 2]
      result << num1 * num2
    end
  end
  result.sort
end

p multiply_all_pairs([2, 4], [4, 3, 1, 2]) == [2, 4, 4, 6, 8, 8, 12, 16]
```

------------------------

### Exersise 10: The End Is Near But Not Here

---------------------INSTRUCTIONS-----------------------------------
Write a method that returns the next to last word in the String passed to it as an argument. Words are any sequence of non-blank characters. You may assume that the input String will always contain at least two words.
------------------------PROBLEM--------------------------------------
Input: String (of minimum two space separated substrings or words)

Output: String (of one word)
-------------------------RULES-----------------------------------------
Explicit:
- Input string will be minimum two space separated substrings or words
- Words or substrings are any sequence of non-blank characters (space separated substrings)

Implicit:

------------------------EXAMPLES--------------------------------------
penultimate('last word') == 'last'
- 'last' is the last-1 word in given string

penultimate('Launch School is great!') == 'is'
- 'is' is the last-1 word in given string

--------------------------ALGORITHM-----------------------------------
Goal:
- identify and return the last -1 substring (space separated run of chars) of given string

- Extract every substring to a new collection (probably an array)
  - I can use split method
- Access the last -1 element index position and return it  

```ruby
def penultimate(string)
  string.split[-2]
end

p penultimate('last word') == 'last'
p penultimate('Launch School is great!') == 'is'
```
