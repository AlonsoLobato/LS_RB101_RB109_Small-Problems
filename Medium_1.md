##  RB101-RB109 - Small Problems --> MEDIUM 1

**This set of exercises are solved using a PEDAC approach**

### Exersise 1: Rotation (Part 1)

---------------------INSTRUCTIONS------------------------------------
Write a method that rotates an array by moving the first element to the end of the array. The original array should not be modified.

Do not use the method Array#rotate or Array#rotate! for your implementation.
------------------------PROBLEM--------------------------------------
Input: Array

Output: New array with first element of given array at last index position and the rest pushed down one position
-------------------------RULES---------------------------------------
Explicit:
- Don't use the methods Array#rotate or Array#rotate!

Implicit:
- Rotated array: the element at index 0 goes to last index position and the rest of elements are pushed down
- Does not matter the obj type as elements in the array, the method should always work
- If one element array given, return it
------------------------EXAMPLES--------------------------------------
rotate_array([7, 3, 5, 2, 9, 1]) == [3, 5, 2, 9, 1, 7]
=> original array index 0 ==> 7
=> new array last index ==> 7
=> rest of elements, pushed down one position

rotate_array(['a', 'b', 'c']) == ['b', 'c', 'a']
rotate_array(['a']) == ['a']

x = [1, 2, 3, 4]
rotate_array(x) == [2, 3, 4, 1]   # => true
x == [1, 2, 3, 4]                 # => true

--------------------------ALGORITHM-----------------------------------
Goal:
- Create a new array based on given array where element at index 0 goes to index -1

Ideas:
- Iterate given array with a method that return a new collection (map)
- Extract index 0, removing it from the array
- Pushing that element to at the end of array

```ruby
def rotate_array(array)
  return array if array.size == 1

  arr_copy = array.map {|item| item.dup}
  item_zero = arr_copy.delete(array[0])

  arr_copy << item_zero
end

p rotate_array([7, 3, 5, 2, 9, 1]) == [3, 5, 2, 9, 1, 7]
p rotate_array(['a', 'b', 'c']) == ['b', 'c', 'a']
p rotate_array(['a']) == ['a']
```

------------------------

### Exersise 2: Rotation (Part 2)

---------------------INSTRUCTIONS------------------------------------
Write a method that can rotate the last n digits of a number.
Note that rotating just 1 digit results in the original number being returned.

You may use the rotate_array method from the previous exercise if you want. (Recommended!)

You may assume that n is always a positive integer.

------------------------PROBLEM--------------------------------------
Input: 
- Two integers as arguments: a positive int to rotate; a positive integer n that indicates the index position of the digit to rotate
Output: 
- Integer: rotated version of the original number
-------------------------RULES---------------------------------------
Explicit:

Implicit:
- Rotate: move digit at index n (n is given as argument) to the last index position of given integer, keeping the rest untouched
------------------------EXAMPLES--------------------------------------
rotate_rightmost_digits(735291, 1) == 735291
=> rotate 1st last digit --> result in the same number, rotating 1 position
rotate_rightmost_digits(735291, 2) == 735219
=> rotate 2nd last digit --> result in index -2 in index -1
rotate_rightmost_digits(735291, 3) == 735912
=> rotate 3rd last digit --> result in index -3 in index -1
rotate_rightmost_digits(735291, 4) == 732915
rotate_rightmost_digits(735291, 5) == 752913
rotate_rightmost_digits(735291, 6) == 352917


--------------------------ALGORITHM-----------------------------------
Goal:
- Given an index, starting from last index position, get that index and put it in the last index position, keep rest the same

Steps:
- Convert integer to array of digits
- Delete and save index position n (given arg2)
- Push it to the end of array
- Convert it back to integer
- Return

```ruby
def rotate_rightmost_digits(int, idx)
  arr_digits = int.digits.reverse

  digit_at_given_idx = arr_digits.delete(arr_digits[-idx])

  arr_digits << digit_at_given_idx

  arr_digits.join.to_i

end

p rotate_rightmost_digits(735291, 1) == 735291
p rotate_rightmost_digits(735291, 2) == 735219
p rotate_rightmost_digits(735291, 3) == 735912
p rotate_rightmost_digits(735291, 4) == 732915
p rotate_rightmost_digits(735291, 5) == 752913
p rotate_rightmost_digits(735291, 6) == 352917
```

------------------------

### Exersise 3: Rotation (Part 3)

---------------------INSTRUCTIONS------------------------------------
If you take a number like 735291, and rotate it to the left, you get 352917. If you now keep the first digit fixed in place, 
and rotate the remaining digits, you get 329175. Keep the first 2 digits fixed in place and rotate again to 321759. 
Keep the first 3 digits fixed in place and rotate again to get 321597. Finally, keep the first 4 digits fixed in place 
and rotate the final 2 digits to get 321579. The resulting number is called the maximum rotation of the original number.

Write a method that takes an integer as argument, and returns the maximum rotation of that argument. 
You can (and probably should) use the rotate_rightmost_digits method from the previous exercise.

Note that you do not have to handle multiple 0s.

------------------------PROBLEM--------------------------------------
Input: 
- Integer
Output: 
- Integer that is the maximum rotation of the original number
-------------------------RULES---------------------------------------
Explicit:
- Rotate number:
  - Get number at index 0 and put it in the position of index -1, keeping the rest in the same position

- Maximum rotation number:
  - Starting at any given number
  - Rotate digit at index 0, then with the resulting number
  - Rotate digit at index 1, then with the resulting number
  - Rotate digit at index 2, then with the resulting number
  - etc.
  - Until rotate digit at index -1
  
Implicit:
- Don't worry about leading zeros 
------------------------EXAMPLES--------------------------------------
max_rotation(735291) == 321579
=> iteration 1 --> index 0 to index -1 position --> 352917
=> iteration 2 --> index 1 to index -1 position --> 329175
=> iteration 3 --> index 2 to index -1 position --> 321759
=> iteration 4 --> index 3 to index -1 position --> 321597
=> iteration 5 --> index 4 to index -1 position --> 321579
=> iteration 6 --> index 5 to index -1 position --> 321579 --> this last iteration isn't neccessary

max_rotation(3) == 3
=> if given integer has only 1 digit, return the integer

max_rotation(35) == 53
max_rotation(105) == 15 # the leading zero gets dropped
max_rotation(8_703_529_146) == 7_321_609_845
--------------------------ALGORITHM-----------------------------------
Goal:
- Iterate a given number digits-in-num-1 times and at every iteration rotate the index position given by increasing counter

Steps:
- Obtain size of given integer (will determine number of iterations)
- Convert integer to array of digits in integer for iteration
- Use a counter, index to reference the digit we have to rotate at every iteration

```ruby
def max_rotation(int)                          # 735291 
  num_iterations = int.to_s.chars.size-1       # 5
  digits_array = int.digits.reverse            # [7, 3, 5, 2, 9, 1]

  (0...(num_iterations)).each do |num|
    num_to_rotate = digits_array.delete(digits_array[num])
    digits_array << num_to_rotate
  end

  digits_array.join.to_i
end

p max_rotation(735291) == 321579
p max_rotation(3) == 3
p max_rotation(35) == 53
p max_rotation(105) == 15 # the leading zero gets dropped
p max_rotation(8_703_529_146) == 7_321_609_845
```

------------------------

### Exersise 4: 1000 Lights

------------------------

### Exersise 5: Diamonds!

Write a method that displays a 4-pointed diamond in an n x n grid, where n is an odd integer that is supplied as an argument to the method. You may assume that the argument will always be an odd integer.


=> input: odd integer
=> ouput: string made of '*' char that forms a diamond based on given integer

=> rules
  > argument will always be an odd num
  > num determines the height and width of the diamon (num of '*' in central line)
  > the rest of the output will be made of empty strings ('') which are invisible in screen
  > num determines the size of the imaginary grid where the diamon will be drawn
  
=> examples

diamond(1)

*

diamond(3)

 *
***
 *

diamond(9)

    *        --> 5 --> given num / 2 are blank spaces + first odd * '*'
   ***       --> 6 --> given num / 2 - 1 are blank spaces + second odd * '*'
  *****      --> 7 --> given num / 2 - 2 are blank spaces + third odd * '*'
 *******     --> 8
*********    --> 9 
 *******     --> 8
  *****      --> 7
   ***       --> 6
    *        --> 5
    
=> algorithm

  => goal
    > create a grid of num by num
    > made of empty spaces and '*'
    > the position of the stars will be determined by the argument
    
  => steps
    > from 1 to the argument / 2 times '' + 
    
```ruby
# Solution 1

def diamond(odd_num)
  return puts 'this diamon is not possible' if odd_num.even?

  index = 0
  spaces = odd_num / 2 
  
  loop do 
    if (index + 1).odd?
      puts ' ' * spaces.abs + '*' * (index + 1) 
      spaces -= 1
    end
    break if index == odd_num
    index += 1
  end
  
  loop do 
    if (index - 1).odd?
      puts ' ' * spaces.abs + '*' * (index - 1)
      spaces -= 1
    end
    break if index == 1
    index -= 1
  end
  
end
```

```ruby
# Solution 2
def diamond(odd_num)
  #return puts 'this diamond is not possible' if odd_num.even?

  index = 1
  spaces = odd_num / 2 
  
  loop do 
    puts ' ' * spaces.abs + '*' * (index) 
    spaces -= 1
    break if index >= odd_num
    index += 2
  end
  
  loop do 
    index -= 2
    puts ' ' * spaces.abs + '*' * index
    spaces -= 1
  
  break if index <= 1
  end
  
end
```

```ruby
# Solution 3
def diamond(num)
  odds = (1..num).select(&:odd?)
  parts = odds.map { |int| ("*" * int).center(num) }
  
  puts [parts, parts.reverse[1..-1]]
end

diamond(1)
diamond(3)
diamond(5)
diamond(7)
diamond(9)
```

------------------------

### Exersise 6: Word to Digit

---------------------INSTRUCTIONS------------------------------------
Write a method that takes a sentence string as input, and returns the same string with any sequence 
of the words 'zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine' converted 
to a string of digits.


------------------------PROBLEM--------------------------------------
Input: string containing the words: 'zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight' or 'nine'

Output: same string (mutation) where the string numbers above are converted to their corresponding string digit version
-------------------------RULES---------------------------------------
Explicit:

Implicit:
- only numbers from zero to nine
- the number 10 will be read as 'one zero' -- '1 0'
------------------------EXAMPLES--------------------------------------
word_to_digit('Please call me at five five five one two three four. Thanks.') == 'Please call me at 5 5 5 1 2 3 4. Thanks.'
- Every appearance of a string number is substituted by its corresponding digit.

--------------------------ALGORITHM-----------------------------------
Goal:
- Detect every appearance of a string number and substitute it, in the same order, by its string digits representation
- 'one' --> '1' ; 'two' --> '2' ; ... ; 'nine' --> '9'

Ideas
- Create a hash where keys are the string numbers and the value their digit representation (string also)
- Iterate each word of given string
- Every time we encounter a string number, which would also exist in the hash as a key, we access that key and place the value instead

Steps
- Create a hash where
    - keys are words 'zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'
    - values are words '0', '1', '2', '3', '4', '5', '6', '7', '8', '9'
- Access each word in the given string --> convert it to array with split    
- Iterate every word of the array and if current word exist in the hash
    - substitute current word by hash value
- Join back the array into a string and return    

```ruby
def word_to_digit(string)
    string_digits = {'zero'=> '0', 'one'=> '1', 'two'=> '2', 'three'=> '3', 'four'=> '4', 'five'=> '5', 'six'=> '6', 'seven'=> '7', 'eight'=> '8', 'nine'=> '9'}
    
    string_digits.each do |k,v|
        string.gsub!(k, v)
    end
    
    string
end

p word_to_digit('Please call me at five five five one two three four. Thanks.') #== 'Please call me at 5 5 5 1 2 3 4. Thanks.'
```

------------------------

### Exersise 7: Fibonacci Numbers (Recursion)
  
