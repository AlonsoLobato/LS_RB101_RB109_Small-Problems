##  RB101-RB109 - Small Problems --> EASY 8

**This set of exercises are solved using a PEDAC approach**

### Exersise 1: Sum of Sums

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes an Array of numbers and then returns the sum of the sums of each leading subsequence for that Array. You may assume that the Array always contains at least one number.

------------------------PROBLEM--------------------------------------
Input: Array of integers

Output: Integer(sum of every subsequence of nums of the given array)
-------------------------RULES-----------------------------------------
Explicit:
- Given array will always contain at least one number
- Given array is always integer as elements

Implicit:
- Subsequence of nums is every sequence of nums from index 0: 
  - subsequence1: elements at index 0
  - subsequence2: elements at index 0 and index 1
  - subsequence3: elements at index 0, index 1 and index 2
  - etc. until the end of the array

------------------------EXAMPLES--------------------------------------
sum_of_sums([3, 5, 2]) == (3) + (3 + 5) + (3 + 5 + 2) # -> (21)
  - subsequence1: elements at index 0 --> 3
  - subsequence2: elements at index 0 and index 1 --> 3, 5
  - subsequence3: elements at index 0, index 1 and index 2 --> 3, 5, 2
  - sum each subsequence itself and sum each subsequence with all other subsequences --> 21
sum_of_sums([1, 5, 7, 3]) == (1) + (1 + 5) + (1 + 5 + 7) + (1 + 5 + 7 + 3) # -> (36)
sum_of_sums([4]) == 4
sum_of_sums([1, 2, 3, 4, 5]) == 35

--------------------------ALGORITHM-----------------------------------
Goal:
- Extract and sum nums of every possible subsequence of consecutive numbers, sum up all the sequences 

- Extract every possible subsequence of nums
  - initialize new_array to an empty array (=[])
  - access index0 to index0+1 of given array and add their values
  - append the result to new_array
  - repeat with accessing index0 to index0+2 of given array and add their values
  - append the result to new_array
  - keep repeating this operation until we reach the end of the array
  - sum up the content of new_array and return the result

- Methods
  - I can use each_with_index which will give me access to each element in array and its index
  - It'll return the original collection (each always does that)
  - I can append the result of the code/operation to the a new array (result)
  - I can access by index using element reference [] and a range (0..index)
  - I can use sum method to add up the elements of an array

```ruby
def sum_of_sums(array)
  result = []   #[3, 8, 10].sum --> 21

  array.each_with_index do |_, index|                 # [3, 5, 2]
    result << array[0..index].sum
  end
  result.sum
end

p sum_of_sums([3, 5, 2]) == (3) + (3 + 5) + (3 + 5 + 2) # -> (21)
p sum_of_sums([1, 5, 7, 3]) == (1) + (1 + 5) + (1 + 5 + 7) + (1 + 5 + 7 + 3) # -> (36)
p sum_of_sums([4]) == 4
p sum_of_sums([1, 2, 3, 4, 5]) == 35
```

------------------------

### Exersise 2: Madlibs


------------------------

### Exersise 3: Leading Substrings

---------------------INSTRUCTIONS-----------------------------------
Write a method that returns a list of all substrings of a string that start at the beginning of 
the original string. The return value should be arranged in order from shortest to longest substring.

------------------------PROBLEM--------------------------------------
Input: String

Output: Array with all possible substrings starting from char 0 contained in given string
-------------------------RULES-----------------------------------------
Explicit:
- The array of integers must be arrange in ascending order of size
- Each substring must start from char at index 0
Implicit:
- A substring is any possible combination of chars from given string
- A substring can be of any size from 1 char
------------------------EXAMPLES--------------------------------------
leading_substrings('abc') == ['a', 'ab', 'abc']
- all possible combinations of chars 'a', 'b' and 'c' starting at index 0 'a'
- 'a', 'ab', 'abc'
leading_substrings('a') == ['a']
- single char, the char itself is the only combination
leading_substrings('xyzzy') == ['x', 'xy', 'xyz', 'xyzz', 'xyzzy']
- all possible combinations of chars 'x', 'y', 'z', 'z' and 'y' starting at index 0 'x'
- 'x', 'xy', 'xyz', 'xyzz', 'xyzzy'

--------------------------ALGORITHM-----------------------------------
Goal:
- Find all possible substrings contained in a given string that start with char at index 0 of original string

- Initialize an empty array
- Iterate the original string
- Access the element at index 0 of the array
- From index 0, use some sort of index counter to iterate over the string and access runs of chars from 0 to counter/index
- Append each substring to the empty array
- Order the array in ascending order by size
- Return the array

```ruby
def leading_substrings(string)
  substrings = []

  string.each_char.with_index do |char, index|
    substrings << string[0..index]
  end

  substrings.sort_by! {|subs| subs.size}
end

p leading_substrings('abc') == ['a', 'ab', 'abc']
p leading_substrings('a') == ['a']
p leading_substrings('xyzzy') == ['x', 'xy', 'xyz', 'xyzz', 'xyzzy']
```

------------------------

### Exersise 4: All Substrings

---------------------INSTRUCTIONS-----------------------------------
Write a method that returns a list of all substrings of a string. The returned list should be ordered by where in the string the substring begins. This means that all substrings that start at position 0 should come first, then all substrings that start at position 1, and so on. Since multiple substrings will occur at each position, the substrings at a given position should be returned in order from shortest to longest.

You may (and should) use the leading_substrings method you wrote in the previous exercise:

------------------------PROBLEM--------------------------------------
Input: String

Output: Array of all possible substrings contained in the given string
-------------------------RULES-----------------------------------------
Explicit:
- Return the array of substring in order of which position index they begin at and in order of their size

Implicit:
- Substring is a run of any num of chars starting from any char position in combination with all elements of following index positions
------------------------EXAMPLES--------------------------------------
substrings('abcde') == [
  'a', 'ab', 'abc', 'abcd', 'abcde',
  'b', 'bc', 'bcd', 'bcde',
  'c', 'cd', 'cde',
  'd', 'de',
  'e'
]
- all possible substrings of string input 'abcde'
- starting at index 0 --> 'a', 'ab', 'abc', 'abcd', 'abcde'
  - 'a' is from index 0 up to index 0
  - 'ab' is from index 0 up to index 1
  - 'abc' is from index 0 up to index 2
  - etc.
- starting at index 1 -->  'b', 'bc', 'bcd', 'bcde',
  - 'b' is from index 1 up to index 1
  - 'bc' from index 1 up to index 2
  - 'bcd' from index 1 up to index 3
- etc.

--------------------------ALGORITHM-----------------------------------
Goal:
- Obtain all possible substrings combining each char of given string
- Starting at index 0 all combinations from 0 up to last index
- Starting at index 1 all combinations from 1 up to last index
- Starting at index 2 all combination from 2 up to last index
- etc.

Steps:
- Initialize an empty array to store substrings
- Access each character in the string (chars | each_char)
- Use double index counter and element reference to access every substring (each | each_with_index)
  - One for starting point
  - Another for ending point

- We can use range from 0 up to the index 
- We can use a second range from index up to the end of string -1, so we don't overrun the string

- At every iteration we reference a substring (element reference [])
- Append substrings to the substring array
- Order the array and return it

```ruby
def substrings(string)
  substrings = []

  (0..string.size).each do |index1|
    (index1..string.size-1).each do |index2|
     substrings << string[index1..index2]
    end
  end
  substrings
end

p substrings('abcde') == [
  'a', 'ab', 'abc', 'abcd', 'abcde',
  'b', 'bc', 'bcd', 'bcde',
  'c', 'cd', 'cde',
  'd', 'de',
  'e'
]
```

------------------------

### Exersise 5: Palindromic Substrings

---------------------INSTRUCTIONS-----------------------------------
Write a method that returns a list of all substrings of a string that are palindromic.  That is, each substring must consist of the same sequence of characters forwards as it does backwards. The return value should be arranged in the same sequence as the substrings appear in the string. Duplicate palindromes should be included multiple times.
You may (and should) use the substrings method you wrote in the previous exercise.
For the purposes of this exercise, you should consider all characters and pay attention to case; that is, "AbcbA" is a palindrome, but neither "Abcba" nor "Abc-bA" are. In addition, assume that single characters are not palindromes.

------------------------PROBLEM--------------------------------------
Input: String

Output: Array of substrings of string that are palondromics
-------------------------RULES-----------------------------------------
Explicit:
- Palindromic substring have same chars forward and backward
- Palindrom can be of any size bigger than 1 (Single chars aren't palindromics)
- Substrings in array must be ordered as they appear in original string
- If a palindromic is repeated in original string, should be put it in the array also repeated
- Case matters: 'Aba' is not a palindromic; AbA is a palindromic
Implicit:
- Char can be of any type: alpha and non alphabetical, symbols included
------------------------EXAMPLES--------------------------------------
palindromes('abcd') == []
- there are no palindromes in 'abcd'

palindromes('madam') == ['madam', 'ada']
- there are two palind in 'madam' --> 'madam' and 'ada'

palindromes('hello-madam-did-madam-goodbye') == [
  'll', '-madam-', '-madam-did-madam-', 'madam', 'madam-did-madam', 'ada',
  'adam-did-mada', 'dam-did-mad', 'am-did-ma', 'm-did-m', '-did-', 'did',
  '-madam-', 'madam', 'ada', 'oo'
]
- there are multiple palind in 'hello-madam-did-madam-goodbye'
- conside the '-' as a valid char in a palindrome --> '-madam-' is a palind and 'madam' is also a palind
palindromes('knitting cassettes') == [
  'nittin', 'itti', 'tt', 'ss', 'settes', 'ette', 'tt'
]

--------------------------ALGORITHM-----------------------------------
Goal:
- Find all substrings of a given string and identify which ones are palindromed and return them in an array

Steps:
- Initialize empty array to store found palind
- Find all substrings of given string
- Find all palindromes in the substrings list
- Assign them to the empty array of palind
- Return the array

- Find all substrings of given string
  - Initialize an empty array for substrings
  - Use a range from 0 to size of string executing a block with an index1 local variable that takes each val in range
  - Use a second range from index1 to size of string -1, executing a block with an index2 local variable that takes each val in range
  - Access each substring of original string using the two indexes we've created in steps 1 and 2
  - Append each found substring to the array
  - Return the array
  - end

- Find all palindromes in array of substrings
  - initialize empty array for palind
  - Palindrome is a string that is equal string and string reversed
  - If palindrom, append it to the empty array
  - return the array
  - end   

```ruby
# My first attempt is using helper methods:

def is_palind?(word)
  return true if word == word.reverse
end

def find_substrings(str)
  substr = []

  (0..str.size).each do |index1|
    (index1..str.size-1).each do |index2|
      substr << str[index1..index2]
    end
  end
  substr
end

def palindromes(string)
  palindrome = []

  find_substrings(string).each do |substring|
    palindrome << substring if is_palind?(substring) unless substring.size == 1
  end

  palindrome
end

# The second attempt was putting all the logic into one method
def palindromes(string)
  substrings = []
  palindrome = []

  (0..string.size).each do |idx1|
    (idx1..string.size-1).each do |idx2|
     substrings << string[idx1..idx2]
    end
  end

  substrings.each do |word|
    palindrome << word if word == word.reverse unless word.size == 1
  end

  palindrome
end

p palindromes('abcd') == []
p palindromes('madam') == ['madam', 'ada']
p palindromes('hello-madam-did-madam-goodbye') == [
  'll', '-madam-', '-madam-did-madam-', 'madam', 'madam-did-madam', 'ada',
  'adam-did-mada', 'dam-did-mad', 'am-did-ma', 'm-did-m', '-did-', 'did',
  '-madam-', 'madam', 'ada', 'oo'
]
p palindromes('knitting cassettes') == [
  'nittin', 'itti', 'tt', 'ss', 'settes', 'ette', 'tt'
]
```

------------------------

### Exersise 6: fizzbuzz

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes two arguments: the first is the starting number, and the second is the ending number.  Print out all numbers between the two numbers, except if a number is divisible by 3, print "Fizz", if a number is divisible by 5, print "Buzz", and finally if a number is divisible by 3 and 5, print "FizzBuzz".

------------------------PROBLEM--------------------------------------
Input: 2 integers --> starting and ending number of a collection of numbers

Output: combination of integers and strings, according to conditional on the elements of the given range
-------------------------RULES-----------------------------------------
Explicit:
- Print all nums from starting number up to ending numbers if:
  - aren't divisible by 3, divisible by 5 or both
- Print the string 'Fizz' if the num is divisible by 3
- Print the string 'Buzz' if the num is divisible by 5
- Print the string 'FizzBuzz' if the num is divisible by both 3 and 5  
Implicit:
------------------------EXAMPLES--------------------------------------
fizzbuzz(1, 15) # -> 1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz

--------------------------ALGORITHM-----------------------------------
- Create a collection of numbers from start to end given nums and print nums or string according to conditions

- Create a range (start..end)
- Iterate each num in the range
- Print num if
  - num isn't divisible by 5 (num % 5 != 0)
  - num isn't divisible by 3 (num % 3 != 0)
- Print Fizz
  - if num is divisible by 5 (num % 5 == 0)
- Print Buzz
  - if num is divisible by 3 (num % 5 == 0)
- Print FizzBuzz 
  - if num is divisible by 5 and 3 (num % 5 == 0 AND num % 3 == 0)
  

```ruby
def div_by?(num, div)
  num % div == 0 ? true : false
end

def fizzbuzz(num1, num2)
  (num1..num2).each do |num|
    if !div_by?(num, 3) && !div_by?(num, 5)
      puts num 
    elsif div_by?(num, 3) && !div_by?(num, 5)
      puts "Fizz"
    elsif div_by?(num, 5) && !div_by?(num, 3)
      puts "Buzz"
    elsif div_by?(num, 3) && div_by?(num, 5)
      puts "FizzBuzz"
    end
  end
end

fizzbuzz(1, 15) # -> 1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz
```

------------------------

### Exersise 7: Double char (part 1)

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a string, and returns a new string in which every character is doubled.

------------------------PROBLEM--------------------------------------
Input: String

Output: New string with every char from original string is doubled
-------------------------RULES-----------------------------------------
Explicit:
 
Implicit:
------------------------EXAMPLES--------------------------------------
repeater('Hello') == "HHeelllloo"
repeater("Good job!") == "GGoooodd  jjoobb!!"
repeater('') == ''
--------------------------ALGORITHM-----------------------------------
Goal:
- Iterate every char in a given string, double each char and assigned the result to a new string variable

- Iterate each char in a string
- Double each char
- Assigmed the new string to a string variable
- Return the variable  

Steps:
- To iterate each char in a string we can use each_char
- To duplicate current char we can reassign each current char to char * 2
- Initialize a new string and store the doubled chars in it
- Return the variable

```ruby
def repeater(string)
  new_string = ''

  string.each_char do |char|
    new_string << char*2
  end

  new_string
end

p repeater('Hello') == "HHeelllloo"
p repeater("Good job!") == "GGoooodd  jjoobb!!"
p repeater('') == ''
```

------------------------

### Exersise 8: Double char (part 2)

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a string, and returns a new string in which every consonant character is doubled. 
Vowels (a,e,i,o,u), digits, punctuation, and whitespace should not be doubled.

------------------------PROBLEM--------------------------------------
Input: String

Output: String where only consonants are doubled (not vowels, digits, punctuation or whitespaces)
-------------------------RULES-----------------------------------------
Explicit:
 
Implicit:
------------------------EXAMPLES--------------------------------------
double_consonants('String') == "SSttrrinngg"
double_consonants("Hello-World!") == "HHellllo-WWorrlldd!"
double_consonants("July 4th") == "JJullyy 4tthh"
double_consonants('') == ""
--------------------------ALGORITHM-----------------------------------
Goal:
- Create a new string based on a given string where all the consonant chars are duplicated but the rest of char aren't

Steps:
- Initialize an empty string variable
- Create a consonants constant variable
- Iterate the given string
- If current char is a consonant
  - Duplicate char and append it to the empty string
- If current char isn't a consonant
  - Appens it to empty string as it  is
- Return the new string    

Ideas:
- consonant chars constant:
  - ('a'..'z').to_a.select {|char| !'aeiou'.include?(char)}

```ruby
CONSONANTS = (('a'..'z').to_a|('A'..'Z').to_a).select {|char| !'aeiouAEIOU'.include?(char)}

def double_consonants(string)
  new_string = ''

  string.each_char do |char|
    if CONSONANTS.include?(char)
      new_string << char * 2
    else 
      new_string << char
    end
  end
  
  new_string
end

p double_consonants('String') == "SSttrrinngg"
p double_consonants("Hello-World!") == "HHellllo-WWorrlldd!"
p double_consonants("July 4th") == "JJullyy 4tthh"
p double_consonants('') == ""
```

------------------------

### Exersise 9: Reverse the Digits In a Number

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a positive integer as an argument and returns that number with its digits reversed. 
Don't worry about arguments with leading zeros - Ruby sees those as octal numbers, which will cause confusing results. 
For similar reasons, the return value for our fourth example doesn't have any leading zeros.

------------------------PROBLEM--------------------------------------
Input: Positive integer of several digits

Output: Same integer with its digits reversed
-------------------------RULES-----------------------------------------
Explicit:
 
Implicit:
------------------------EXAMPLES--------------------------------------
reversed_number(12345) == 54321
reversed_number(12213) == 31221
reversed_number(456) == 654
reversed_number(12000) == 21 # No leading zeros in return value!
reversed_number(12003) == 30021
reversed_number(1) == 1
--------------------------ALGORITHM-----------------------------------
Goal:
- Iterate an integer of several digits and reverse their order

Ideas:
- Use reverse in the integer

- Convert integer digits to array
- Reverse array
- Return converted to integer

- Convert integer digits to array
- Iterate the array and reassing their indexes (perhaps with a copy of original to keep indexes order)

```ruby
# Solution 1
def reversed_number(int)
  int.to_s.reverse.to_i
end

# Solution 2
def reversed_number(int)
  int.digits.join.to_i
end

# Solution 3
def reversed_number(int)
  arr = int.digits.reverse
  copy = arr.dup
  counter = -1
  arr.each_with_index do |_,index|
    arr[index] = copy[counter]
    counter -= 1
  end

  arr.join.to_i
end

p reversed_number(12345) == 54321
p reversed_number(12213) == 31221
p reversed_number(456) == 654
p reversed_number(12000) == 21 # No leading zeros in return value!
p reversed_number(12003) == 30021
p reversed_number(1) == 1
```

------------------------

### Exersise 10: Get The Middle Character

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a non-empty string argument, and returns the middle character or characters of the argument. 
If the argument has an odd length, you should return exactly one character. 
If the argument has an even length, you should return exactly two characters.

------------------------PROBLEM--------------------------------------
Input: Non-empty string

Output: String that is the middle char (or chars) of given string
-------------------------RULES-----------------------------------------
Explicit:
- Middle char
  - If string has odd length --> exactly middle char
  - If string has even length --> two middle chars
Implicit:
- Consider spaces and non-alphanum chars
------------------------EXAMPLES--------------------------------------
center_of('I love ruby') == 'e'
center_of('Launch School') == ' '
center_of('Launch') == 'un'
center_of('Launchschool') == 'hs'
center_of('x') == 'x'
--------------------------ALGORITHM-----------------------------------
Goal:
- Find middle char or two chars of a given string and return it

Idea:
- Iterate the string and select char or two chars so the num of chars to the left and to the right of them are same length

- Split string in two equal parts
  - 0 .. string length /2
  - string length / 2 .. -1
  - compare their size
    - if the same
      - return last char of first substring and first char of second substring joined
    - if different
      - return last char of larger substring


Steps:
- Iterate each char of string from start to end
- Iterate simultaneously each char of string from end to start
- Keep track of num of chars from start and from end
- Keep going with the iteration until one of the two counters is bigger than the other
- Once there, return the char or two chars


```ruby
# Solution 1
def center_of(string)
  half = string.length/2
  middle_even = string.size % 2 == 0  
  result = ''

  if middle_even == true                      #'abcd'
    result << string[half..half+1]
  elsif middle.even == false                  #'abcde'
    result << string[half+1]
  end
  result
end

# Solution 2
def center_of(string)
  center = string.size / 2

  if string.size.odd?         # 'abcde'
    string[center]
  else
    string[center-1, 2]       # 'abcd'
  end
end

p center_of('I love ruby') == 'e'
p center_of('Launch School') == ' '
p center_of('Launch') == 'un'
p center_of('Launchschool') == 'hs'
p center_of('x') == 'x'
```