##  RB101-RB109 - Small Problems --> EASY 6

**This set of exercises are solved using a PEDAC approach**

### Exersise 1:

------------------------

### Exersise 2: Delete vowels

Write a method that takes an array of strings, and returns an array of the same string values, except with the vowels (a, e, i, o, u) removed.

-> input: array of strings
-> output> array of same values with vowels removed

-> rules: 
  -> vowels are a e i o u 
  -> if given array contains several words (substrings) return the same substrings
  -> consider upcase and lowcase chars
  
-> algorithm
  -> Goal: Clean up array by removing all vowels
  
  -> Steps:
    -> Initialize an array of valid chars --> vowels
    -> Iterate the strings in array 
      -> use map which returns new array based on return val from block
      -> to use map we need to access the chars in the subtrings, use chars, which returns an array of chars in word
      -> on the chars use select to select the chars that are included in the vowel array
      -> join back the chars
      -> return

```ruby
VOWELS = %w(a e i o u)

def remove_vowels(array)
  clean = array.map do |word|
    word.chars.select { |char| !VOWELS.include?(char.donwcase) }.join
  end
end

p remove_vowels(%w(abcdefghijklmnopqrstuvwxyz)) == %w(bcdfghjklmnpqrstvwxyz)
p remove_vowels(%w(green YELLOW black white)) == %w(grn YLLW blck wht)
p remove_vowels(%w(ABC AEIOU XYZ)) == ['BC', '', 'XYZ']
```

------------------------

### Exersise 3: Fibonacci Number Location By Length

---------------------INSTRUCTIONS-----------------------------------
The Fibonacci series is a series of numbers (1, 1, 2, 3, 5, 8, 13, 21, ...) such that the first 2 numbers are 1 by definition, and each subsequent number is the sum of the two previous numbers. This series appears throughout the natural world.

Computationally, the Fibonacci series is a very simple series, but the results grow at an incredibly rapid rate. 
For example, the 100th Fibonacci number is 354,224,848,179,261,915,075 -- that's enormous, especially considering that it takes 6 iterations before it generates the first 2 digit number.

Write a method that calculates and returns the index of the first Fibonacci number that has the number of digits specified as an argument. (The first Fibonacci number has index 1.)

You may assume that the argument is always greater than or equal to 2.

------------------------PROBLEM--------------------------------------
Input: 
- Integer that indicates the number of digits of a number

Output: 
- Integer that indicates how many FB num are needed to have one with same num of digits as input int

-------------------------RULES-----------------------------------------
Explicit:
- Given argument will always be 2 or greater

Implicit:
- FB num is a num resulting from adding the two previous FB numbers, always starting with 1, 1

------------------------EXAMPLES--------------------------------------
find_fibonacci_index_by_length(2) == 7          # 1 1 2 3 5 8 13
find_fibonacci_index_by_length(3) == 12         # 1 1 2 3 5 8 13 21 34 55 89 144
find_fibonacci_index_by_length(10) == 45
find_fibonacci_index_by_length(100) == 476
find_fibonacci_index_by_length(1000) == 4782
find_fibonacci_index_by_length(10000) == 47847

--------------------------ALGORITHM-----------------------------------
Goal:
- calculate FB of argument number of digits and return how many FB numb are needed to get there

- Calculate FB num
  - Fb = [1+1] = 2 | [1+2] = 3 | [2+3] = 5 | [3+5] = 8 | [5+8] = 13 | [8+13] = 21
  - Fb = [num1 + num2] = num3 | [num2 + num3] = num 4 | [num3 + num4] = num5
  - Fb: num = [1, 1] || num[0] + num[1] = result | num[1] + result = result 

```ruby

def find_fibonacci_index_by_length(given_digits)
  counter = 0                 
  fibo_nums = [1, 1]                 
  loop do
    fibo_nums << (fibo_nums[counter] + fibo_nums[counter + 1])                                   
    counter += 1                 
    break if fibo_nums.any? {|fb| fb.digits.size == given_digits}
  end
  fibo_nums.size
end

p find_fibonacci_index_by_length(2) #== 7          # 1 1 2 3 5 8 13
p find_fibonacci_index_by_length(3) #== 12         # 1 1 2 3 5 8 13 21 34 55 89 144
p find_fibonacci_index_by_length(10) #== 45
p find_fibonacci_index_by_length(100) #== 476
```

------------------------

### Exersise 4: Reversed Arrays (Part 1)

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes an Array as an argument, and reverses its elements in place; 
that is, mutate the Array passed into this method. The return value should be the same Array object.

You may not use Array#reverse or Array#reverse!.

------------------------PROBLEM--------------------------------------
Input: 
- Array 

Output: 
- Same array with elements in reverse order

-------------------------RULES-----------------------------------------
Explicit:
- Don't use the Array#reverse or Array#reverse! methods
- The method must mutate the original array
Implicit:
- Array can have any object as elements

------------------------EXAMPLES--------------------------------------
list = [1,2,3,4]
result = reverse!(list)
result == [4, 3, 2, 1] # true
list == [4, 3, 2, 1] # true
list.object_id == result.object_id # true

list = %w(a b e d c)
reverse!(list) == ["c", "d", "e", "b", "a"] # true
list == ["c", "d", "e", "b", "a"] # true

list = ['abc']
reverse!(list) == ["abc"] # true
list == ["abc"] # true

list = []
reverse!(list) == [] # true
list == [] # true

--------------------------ALGORITHM-----------------------------------
Goal:
- Reverse the order of elements in a given array -> mutate the original

Edge cases:
- If input array is empty, return an empty array
- If input array has only one element, return the same array

Other cases:
- [1,2,3,4] or ["a", "b", "e", "d", "c"]
- iterate array
- for odd num of elements in arrays
  - put index 0 element at index -1 position
  - put index -1 element at index 0 position
  - put index 1 element at index -2 position
  - put index -2 element at index 1 position
  - etc...
  - central element remains the same position
- for even num of elements in array  
  - put index 0 element at index -1 position
  - put index -1 element at index 0 position
  - put index 1 element at index -2 position
  - put index -2 element at index 1 position
  - etc...

- iterate by index? use a copy for iteration and delete elements which order is modified

PSEUD:
- array.clone
- array.each
  - clone.element[-1].replace clone.element[0]

```ruby
def reverse!(list)
  return list if list.empty? || list.size == 1

                             # list [1,2,3,4,5]
  index = 0
  list_copy = list.dup       # copy [1,2,3,4,5]

  list.each do |_|
    list[index] = list_copy[-1-index]
    index += 1
  end
  list
end

list = [1,2,3,4]
p result = reverse!(list)
p result == [4, 3, 2, 1] # true
p list == [4, 3, 2, 1] # true
p list.object_id == result.object_id # true

list = %w(a b e d c)
p reverse!(list) == ["c", "d", "e", "b", "a"] # true
p list == ["c", "d", "e", "b", "a"] # true

list = ['abc']
p reverse!(list) == ["abc"] # true
p list == ["abc"] # true

list = []
p reverse!(list) == [] # true
p list == [] # true
```

#### NOTES
- The same result can be obtained with each_with_index with which we wouldn't need an external index counter

------------------------

### Exersise 5: Reversed Arrays (Part 2)

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes an Array, and returns a new Array with the elements of the original list in reverse order. 
Do not modify the original list.

You may not use Array#reverse or Array#reverse!, nor may you use the method you wrote in the previous exercise.

------------------------PROBLEM--------------------------------------
Input: 
- Array of any type of object as elements  

Output: 
- New Array with same elements in reverse order

-------------------------RULES-----------------------------------------
Explicit:
- Don't use the reverse or reverse! methods
- Create a new data structure (don't mutate the given array)
Implicit:
- Interchange objects in indexes: index 0 to index -1, index 1 to index -2, index 2 to index -3, etc.
- Middle index (if array size is odd) stays the same
- Empty array return empty array
- Single element array return the same array

------------------------EXAMPLES--------------------------------------
reverse([1,2,3,4]) == [4,3,2,1]          # => true
reverse(%w(a b e d c)) == %w(c d e b a)  # => true
reverse(['abc']) == ['abc']              # => true
reverse([]) == []                        # => true

list = [1, 3, 2]                      # => [1, 3, 2]
new_list = reverse(list)              # => [2, 3, 1]
list.object_id != new_list.object_id  # => true
list == [1, 3, 2]                     # => true
new_list == [2, 3, 1]                 # => true

--------------------------ALGORITHM-----------------------------------
Goal:
- interchange elements of certain indexes so we end up with a new collection in reverse order

Edge cases:
- if emtpy array --> return same array
- if one element array --> return same array

Other cases:
- index 0 to index - 1
- index 1 to index -2
- index 2 to index -3
etc.

PSEUD
- create a copy of array for iteration
- create a new empty array to store elements from original in new order
- once copy array has been iterated and new array populated, return new array

```ruby
def reverse(array)                                  # [1,2,3,4]
  return array if array.empty? || array.size == 1

  new_list = []                                     #[4,3,2,1]

  array.each_with_index do |_, index|
    new_list[index] = array[-index-1]
  end

  new_list
end

p reverse([1,2,3,4]) == [4,3,2,1]          # => true
p reverse(%w(a b e d c)) == %w(c d e b a)  # => true
p reverse(['abc']) == ['abc']              # => true
p reverse([]) == []                        # => true

list = [1, 3, 2]                      # => [1, 3, 2]
new_list = reverse(list)              # => [2, 3, 1]
p list.object_id != new_list.object_id  # => true
p list == [1, 3, 2]                     # => true
p new_list == [2, 3, 1]                 # => true
```

------------------------

### Exersise 6: Combining Arrays

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes two Arrays as arguments, and returns an Array that contains all of the values from the argument Arrays. There should be no duplication of values in the returned Array, even if there are duplicates in the original Arrays.

------------------------PROBLEM--------------------------------------
Input: 
- Two arrays

Output: 
- A new array with all elements from two input arrays without duplicated values
-------------------------RULES-----------------------------------------
Explicit:
- Merge two arrays and remove duplicated elements
- Given arrays may have duplicates
Implicit:
- Given arrays contain only integers (would that work for other obj types?)
- Given arrays contain at least one element

------------------------EXAMPLES--------------------------------------
merge([1, 3, 5], [3, 6, 9]) == [1, 3, 5, 6, 9]

--------------------------ALGORITHM-----------------------------------
Goal:
- merge two arrays into a new one and remove the duplicates

- initialize a new array to the return value of:
  - flatten the input arrays
- uniq the resulting new array 

```ruby
def merge(arr1, arr2)
  new_array = []

  arr1.each {|item| new_array << item}
  arr2.each {|item| new_array << item}

  new_array.uniq!

end

p merge([1, 3, 5], [3, 6, 9]) == [1, 3, 5, 6, 9]
```

------------------------

### Exersise 7: Halvsies

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes an Array as an argument, and returns two Arrays (as a pair of nested Arrays) that contain the first half and second half of the original Array, respectively. If the original array contains an odd number of elements, the middle element should be placed in the first half Array.

------------------------PROBLEM--------------------------------------
Input: Array

Output: Two arrays nested in another new array with first and second half of elements of the original respectively

-------------------------RULES-----------------------------------------
Explicit:
- Array 1 with first half of elements in original array (+ 1 if array is odd)
- Array 2 with second half of elements in original array
- If input array has odd num of elements, the middle element goes in the first sub array

Implicit:

------------------------EXAMPLES--------------------------------------
halvsies([1, 2, 3, 4]) == [[1, 2], [3, 4]]
- even num of elements array
- 1st half [1,2] --> to array 1
- 2nd half [3,4] --> to array 2
- put arr1 and arr2 as element in arr3

halvsies([1, 5, 2, 4, 3]) == [[1, 5, 2], [4, 3]]
- odd num of elements array
- 1st half [1,5,2] --> to array 1 **half + 1 element
- 2nd half [4,3] --> to array 2
- put arr1 and arr2 as element in arr3

halvsies([5]) == [[5], []]
- single element array
- 1st half [5] --> to arr1
- 2nd half empty [] --> to arr2
- put arr1 and arr2 as element in arr3

halvsies([]) == [[], []]
- empty element array
- 1st half [] --> to arr1
- 2nd half empty [] --> to arr2
- put arr1 and arr2 as element in arr3
--------------------------ALGORITHM-----------------------------------
Goal:
- break given array in two halves and put each one as subarrays of nested array

Edge cases:
- if single element (size 0) add empty subarray
- if empty element (arr.empty) add emtpy subarray

Other cases:
- create empty array new_arr
- if array is has even num of elements  -->   [1, 2, 3, 4]
- iterate the array and add size/2 as an array to a new_arr and the rest as another array to new_array
- return new_arr
- if array has odd num of elements  -->  [1, 5, 2, 4, 3]
- iterate the array and add size/2 + 1 as an array to a new_arr and the rest as another array to new_array
- return new_arr

```ruby
def halvsies(array)            #[1, 2, 3, 4]
  new_arr = []

  if array.size == 1 || array.empty?
    new_arr << array
    new_arr << [] 

  elsif array.size.even?
    new_arr << array[0...array.size/2]
    new_arr << array[array.size/2..-1]

  elsif array.size.odd? 
    new_arr << array[0...array.size/2+1]
    new_arr << array[array.size/2+1..-1]
  end

  new_arr
end

p halvsies([1, 2, 3, 4]) == [[1, 2], [3, 4]]
p halvsies([1, 5, 2, 4, 3]) == [[1, 5, 2], [4, 3]]
p halvsies([5]) == [[5], []]
p halvsies([]) == [[], []]
p halvsies([3, 'g', :g, {'a'=> '/'}, 23]) == [[3, "g", :g], [{"a"=>"/"}, 23]]
```

------------------------

### Exersise 8: Find the Duplicate

---------------------INSTRUCTIONS-----------------------------------
Given an unordered array and the information that exactly one value in the array occurs twice 
(every other value occurs exactly once), how would you determine which value occurs twice? 
Write a method that will find and return the duplicate value that is known to be in the array.

------------------------PROBLEM--------------------------------------
Input: Unordered array of integers 

Output: Element of input array (integer) that appears twice

-------------------------RULES-----------------------------------------
Explicit:
- One element (only one) is repeated twice in the given array

Implicit:
- The given array has only integers
- One element is repeated, all the others are unique

------------------------EXAMPLES--------------------------------------
find_dup([1, 5, 3, 1]) == 1
- 1 is the element repeated (index 0 and index 3)

find_dup([18,  9, 36, 96, 31, 19, 54, 75, 42, 15,
          38, 25, 97, 92, 46, 69, 91, 59, 53, 27,
          14, 61, 90, 81,  8, 63, 95, 99, 30, 65,
          78, 76, 48, 16, 93, 77, 52, 49, 37, 29,
          89, 10, 84,  1, 47, 68, 12, 33, 86, 60,
          41, 44, 83, 35, 94, 73, 98,  3, 64, 82,
          55, 79, 80, 21, 39, 72, 13, 50,  6, 70,
          85, 87, 51, 17, 66, 20, 28, 26,  2, 22,
          40, 23, 71, 62, 73, 32, 43, 24,  4, 56,
          7,  34, 57, 74, 45, 11, 88, 67,  5, 58]) == 73 
- 73 is he element repeated (index X and Y)
--------------------------ALGORITHM-----------------------------------
Goal:
- Find repeated element in given array

- Create a new empty array
- Iterate the given array and compare each element with all the others
  - if the comparison is true (same value)
  - store the value in new array
- convert array to integer
- return integer  

- original = [1, 5, 5, 3].uniq #[1, 5, 5, 3]
- unique = [1, 5, 1, 3].uniq   #[1, 5, 3]
- original.each

```ruby
def find_dup(array)             #[1, 5, 3, 1]

  unique = array.uniq           #[1, 5, 3]

  duplicated = unique.map do |num1|
    array.select do |num2|
      num1 == num2
    end
  end

  duplicated.select! do |sub|
    sub.size == 2
  end

  duplicated[0][0]
end

p find_dup([1, 5, 3, 1]) == 1
p find_dup([1,2,4,4]) == 4
p find_dup([1, 2, 3, 7, 3, 9, 8]) == 3
p find_dup([18,  9, 36, 96, 31, 19, 54, 75, 42, 15,
          38, 25, 97, 92, 46, 69, 91, 59, 53, 27,
          14, 61, 90, 81,  8, 63, 95, 99, 30, 65,
          78, 76, 48, 16, 93, 77, 52, 49, 37, 29,
          89, 10, 84,  1, 47, 68, 12, 33, 86, 60,
          41, 44, 83, 35, 94, 73, 98,  3, 64, 82,
          55, 79, 80, 21, 39, 72, 13, 50,  6, 70,
          85, 87, 51, 17, 66, 20, 28, 26,  2, 22,
          40, 23, 71, 62, 73, 32, 43, 24,  4, 56,
          7,  34, 57, 74, 45, 11, 88, 67,  5, 58]) == 73
```

------------------------

### Exersise 9: Does My List Include This?

---------------------INSTRUCTIONS-----------------------------------
Write a method named include? that takes an Array and a search value as arguments. This method should return true if the search value is in the array, false if it is not. You may not use the Array#include? method in your solution.

------------------------PROBLEM--------------------------------------
Input: 
- Array of any obj type as element and an object of any type to search for in it
Output: 
- Boolean: true or false, depending if the given object appears or not in the array

-------------------------RULES-----------------------------------------
Explicit:
- Cannot use Array#include? method
Implicit:
- Array and given object could be of any type

------------------------EXAMPLES--------------------------------------
include?([1,2,3,4,5], 3) == true
-- Given argument 3 is included in array so true is returned

include?([1,2,3,4,5], 6) == false
--given argument 6 isn't included in array so false is returned

include?([], 3) == false
--given argument 3 isn't included in array (empty) so false is returned

include?([nil], nil) == true
include?([], nil) == false

--------------------------ALGORITHM-----------------------------------
Goal:
- Find the given object(argument2) in a given array(argument1)

Edge cases:
- If array is empty, return false

Other cases:
- Put arg2 in an array
- Compare arg1 and arg2 element by element (they are both arrays)
- If element1 == element2 put element1 in new array
- After iteration,
  - if new_arr is empty (no match found while comparing) return false
  - if new_arr has an element (match found) return true


```ruby
# solution 1
def include?(arr, obj)
  return false if arr.empty?

  arr2 = [obj]

  new_arr = arr2.map do |obj|                 # [3]
    arr.select do |item|                      # [1,2,3,4,5]
      obj == item
    end
  end

  new_arr[0][0] == obj
end

#solution 2
def include?(arr, obj)
  return false if arr.empty?
  arr.select {|item| item == obj}[0] == obj
end

p include?([1,2,3,4,5], 3) == true
p include?([1,2,3,4,5], 6) == false
p include?([], 3) == false
p include?([nil], nil) == true
p include?([], nil) == false
```

------------------------

### Exersise 10: Right Triangles

---------------------INSTRUCTIONS-----------------------------------
Write a method that takes a positive integer, n, as an argument, and displays a right triangle whose sides each have n stars. The hypotenuse of the triangle (the diagonal side in the images below) should have one end at the lower-left of the triangle, and the other end at the upper-right.

------------------------PROBLEM--------------------------------------
Input: 
- Positive integer as argument of a method

Output: 
- A drawed triangle with argument-side-size

-------------------------RULES-----------------------------------------
Explicit:

Implicit:
- draw the triangle using the * symbol
- If argument is X, each side of the triangle must have X numbers of *
- The three sides with the same number of *

------------------------EXAMPLES--------------------------------------
triangle(5)

    *
   **
  ***
 ****
*****
- argument is 5 so
- 5 * in side 1
- 5 * in hypot
- 5 * in base of triangle

--------------------------ALGORITHM-----------------------------------
Goal:
- Draw a triangle with * symbol based on given argument (positive integer)

- For a 5 as arg (size of 5 each side of triangle):
- print string of arg - (arg-1) times blank spaces + 1 time *
- print string of arg - (arg-2) times blank spaces + 1 time *
- print string of arg - (arg-3) times blank spaces + 1 time *
- print string of arg - (arg-4) times blank spaces + 1 time *
- print string of arg times *

```ruby
STAR = '*'
SPACE = ' '

def triangle(size)                                                          # 5
  counter = 1                                                               # 1 | 2 | 3

  size.times do                                                             # 5 times
    puts SPACE*(size-counter) + STAR*(size - (size-counter))                #    * 
    counter += 1                                                            #   **
  end                                                                       #  ***
end

triangle(5)
triangle(9)
```