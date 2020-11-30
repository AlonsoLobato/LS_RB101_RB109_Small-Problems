##  RB101-RB109 - Small Problems --> EASY 2

**This set of exercises are solved using a PEDAC approach**

### Exercise 1: How old is Teddy?

Build a program that randomly generates and prints Teddy's age. To get the age, you should generate a random number between 20 and 200.

Example Output:

```ruby
'Teddy is 69 years old!'
```

#### My answer

##### Rules / requirements
- Write a program that
- Generates a random number
- Number between 20 and 200
- Interpolate the number in the sentence 'Teddy is X years old!'

##### Examples
*Given in the problem description*

#### Data Structure
- Integer
- String as output

#### Algorithm
1. Generate a random number between 20 and 200
2. Output the number interpolated in the string 'Teddy is #{number} years old!'

#### Code
```ruby
age = rand(20..200)
puts "Teddy is #{age} years old!"
```

#### Further exploration
Modify this program to ask for a name, and then print the age for that person. For an extra challenge, use "Teddy" as the name if no name is entered.

#### Algorithm
1. Generate a random number between 20 and 200
2. Ask for user's name
3. Output given name and random age
4. If no name is provided, use Teddy as name

#### Code
```ruby
puts "Please enter your name"
name = gets.chomp
age = rand(20..200)

if name != ''
  puts "#{name} is #{age} years old!"
else    
  puts "Teddy is #{age} years old!"
end
```

#### Other answer
```ruby
puts "Please enter your name"
name = gets.chomp
name = 'Teddy' if name.empty?
age = rand(20..200)
puts "#{name} is #{age} years old!"
```

==================================================================

### Exercise 2: How big is the room?

Build a program that asks a user for the length and width of a room in meters and then displays the area of the room in both square meters and square feet.

Note: 1 square meter == 10.7639 square feet

Do not worry about validating the input at this time.

Example:

```ruby
Enter the length of the room in meters:
10
Enter the width of the room in meters:
7
The area of the room is 70.0 square meters (753.47 square feet).
```

#### My answer

##### Rules / requirements
- Write a program that calculate the area of a surface
- Area equals length times width
- Get length and width from user
- Output the result in square meters and in square feet
  - 1 square meter equals 10.7639 square feet
- No need to validate inputs

##### Examples
*Given in the problem description*

#### Data Structure
- Float as input
- Float as output

#### Algorithm
1. Prompt user to input a length in meters
2. Promot user to input width in meters
3. Calculate area according to inputs
  - Area == length * width
4. Output the result in square meters and square feet
  - 1 square meter == 10.7639 square feet  

#### Code
```ruby
puts "Please enter length of the room in meters"
length = gets.chomp.to_f
puts "Please enter width of the room in meters"
width = gets.chomp.to_f

area_in_meters = (length * width).round(2)
area_in_feet = (area_in_meters * 10.7639).round(2)

puts "The area of the room is #{area_in_meters} square meters (#{area_in_feet} square feet)"
```

==================================================================

### Exercise 3: Tip calculator

Create a simple tip calculator. The program should prompt for a bill amount and a tip rate. The program must compute the tip and then display both the tip and the total amount of the bill.

Example:

```ruby
What is the bill? 200
What is the tip percentage? 15

The tip is $30.0
The total is $230.0
```

#### My answer

##### Rules / requirements
- Create a program that calculate tips based on tip rate of total bill
- Get from user both, the tip rate and the total bill amount
- Display both data

##### Examples
*Given in the problem description*

#### Data Structure
- Float as input
- Float as output

#### Algorithm
1. Prompt user for bill amount
2. Prompt user for tip rate they wish to pay
  - Divide by 100
3. Calculate the tip rate from total bill amount
4. Display both data

#### Code
```ruby
puts "Please enter the total bill amount"
total_bill = gets.chomp.to_f

puts "What tip percentage do you wish to apply?"
tip_rate = gets.chomp.to_f / 100

tip_amount = (total_bill * tip_rate).round(2)
grand_total = (total_bill + tip_amount).round(2)

puts "The tip is $#{tip_amount}"
puts "The total is $#{grand_total}"
```

##### NOTES 
- Use `Kernel#format` to force a float to x number of decimal digits.
- When used with variable interpolation we'd do `#{format("&.2f, variable")}` to add a symbol like `$` do `#{format("$&.2f, variable")}`
- This method is preferred over `Float#round` method

==================================================================

### Exercise 4: When will I Retire?

Build a program that displays when the user will retire and how many years she has to work till retirement.

Example:
```ruby
What is your age? 30
At what age would you like to retire? 70

It's 2016. You will retire in 2056.
You have only 40 years of work to go!
```

#### My answer

##### Rules / requirements
- Program that calculates number of years left to retire
- Prompt user for current age and desired retirement age
- Calculate year for retirement and how many years left until then

##### Examples
*Given in the problem description*

#### Data Structure
- String to integer as input
- Integer and string as output

#### Algorithm
1. Create a program that calculate number of years to retire
2. Prompt user for current age - transform input string to integer
3. Prompt user for desired age to retire - transform input from string to integer
4. Given the current year
  - Calculate date of retirement
  - Calculate number of years left of work
5. Output the calculation inserted into a string  

#### Code
```ruby
YEAR = 2020 # optionally we can do 'YEAR = Time.now.year' *see notes below

puts "What is your age?"
age = gets.chomp.to_i

puts "At what age would you like to retire?"
retirement_age = gets.chomp.to_i

time_left_to_retire = retirement_age - age

puts "It's #{YEAR}. You will retire in #{YEAR + time_left_to_retire}"
puts "You have only #{time_left_to_retire} years of work to go!"
```

##### NOTES 
- The current date (year, month, etc.) can be obtained with `Time` class
- `Time.now.year` will return `2020`, so we don't have to hardcode 2020 as constant 

==================================================================

### Exercise 5: Greeting a user

Write a program that will ask for user's name. The program will then greet the user. If the user writes "name!" then the computer yells back to the user.

Examples:

```ruby
What is your name? Bob
Hello Bob.
```

```ruby
What is your name? Bob!
HELLO BOB. WHY ARE WE SCREAMING?
```

#### My answer

##### Rules / requirements
- Program that ask user for name
- Then greets user with their name
- If user enters name followed by !
  - Greet would be capitalised and message would be different

##### Examples
*Given in the problem description*

#### Data Structure
- String as input
- String as output

#### Algorithm
1. Prompt user for their name
2. Greet user
  - If user input equals name
    - Output "Hello #name"
  - If user input equals name + !
    - Output "HELLO #NAME. WHY ARE YOU SCREAMING?"

#### Code
```ruby
puts "What is your name?"
name = gets.chomp

if name.include? '!'
  puts "HELLO #{name.upcase}. WHY ARE YOU SCREAMING?"
else
  puts "Hellos #{name}"
end  
```

#### School answer

```ruby
print 'What is your name? '
name = gets.chomp

if name[-1] == '!'
  name = name.chop
  puts "HELLO #{name.upcase}. WHY ARE WE SCREAMING?"
else
  puts "Hello #{name}."
end
```

##### NOTES 
- It's better to use index access to check if and only if the last char of the name is `!`
- Then, when outputting the name, we don't want to output the `!` if exist, so we use `String#chop` method to delete last char of a string.
- Note that this solution uses both `String#chomp` and `String#chop`. 
- These two methods are closely related, but slightly different: 
  - `#chomp` conditionally removes the tail end of a string (defaulting to a newline), 
  - while `#chop` removes the last character unconditionally. 
  - Both versions also have `!` versions that modify the string directly; we decided not to use these here because the use of the ! in both the method name and the string might be confusing.

==================================================================

### Exercise 6: Odd numbers

Print all odd numbers from 1 to 99, inclusive, to the console, with each number on a separate line.

#### My answer

##### Rules / requirements
- Print odd numbers in the range 1 to 99, both included
- Each number must be printed on a separate line

##### Examples
```ruby
1
3
5
...
```
#### Data Structure
- Integer as output

#### Algorithm
1. Create range 1 to 99
2. Print only odd numbers in the range
3. Each number printed on a separate line

#### Code
```ruby
for number in (1..99) 
  puts number if number.odd?
end
```

#### Further exploration

Repeat this exercise with a technique different from the one you just used, and different from the solution shown above. You may want to explore the use `Integer#upto` or `Array#select` methods, or maybe use `Integer#odd?`

```ruby
1.upto(99) {|number| puts number if number.odd?}
```

```ruby
[*1..99].select {|number| puts number if number.odd?}
```

```ruby
Array(1..99).select {|number| puts number if number.odd?}
```

==================================================================

### Exercise 7: Even Numbers

Print all even numbers from 1 to 99, inclusive, to the console, with each number on a separate line.

#### My answer

##### Rules / requirements
- Print even numbers in the range 1 to 99, both included
- Each number must be printed on a separate line

##### Examples
```ruby
2
4
6
...
```
#### Data Structure
- Integer as output

#### Algorithm
1. Create range 1 to 99
2. Print only even numbers in the range
3. Each number printed on a separate line

#### Code
```ruby
1.upto(99) {|number| puts number if number.even?}
```

==================================================================

### Exercise 8: Sum or Product of Consecutive Integers

Write a program that asks the user to enter an integer greater than 0, then asks if the user wants to determine the sum or product of all numbers between 1 and the entered integer.

Examples:

```ruby
>> Please enter an integer greater than 0:
5
>> Enter 's' to compute the sum, 'p' to compute the product.
s
The sum of the integers between 1 and 5 is 15.


>> Please enter an integer greater than 0:
6
>> Enter 's' to compute the sum, 'p' to compute the product.
p
The product of the integers between 1 and 6 is 720.
```

#### My answer

##### Rules / requirements
- Program that asks user for an integer greater than 0 
- Performs an addittion or multiplication 
- Of all numbers from 1 to the entered integer, both included

##### Examples
*Given in the problem description*

#### Data Structure
- Integer as input
- Integer as output

#### Algorithm
1. Prompt user for an integer > 0
2. Promt user for an operation to perform
  - s for sum
  - p for product (multiplication)
3. Perform the chosen operation with all numbers between 1 and the input integer
4. Return the result

#### Code
```ruby
puts "=> Please enter an integer greater than 0:"
number = gets.chomp.to_i
puts "=> Please enter 's' to compute the sum, 'p' to compute the product."
operation = gets.chomp

digits = []
1.upto(number) { |n| digits << n }

if operation == "s"
  sum = digits.sum
  puts "=> The sum of the integers between 1 and #{number} is #{sum}"
elsif operation == "p"
  product = digits.inject(:*)
  puts "=> The product of the integers between 1 and #{number} is #{product}"
else
  puts "=> Sorry. This operation is not valid"    
end
```

#### School answer
```ruby
def compute_sum(number)
  total = 0
  1.upto(number) { |value| total += value }
  total
end

def compute_product(number)
  total = 1
  1.upto(number) { |value| total *= value }
  total
end

puts ">> Please enter an integer greater than 0"
number = gets.chomp.to_i

puts ">> Enter 's' to compute the sum, 'p' to compute the product."
operation = gets.chomp

if operation == 's'
  sum = compute_sum(number)
  puts "The sum of the integers between 1 and #{number} is #{sum}."
elsif operation == 'p'
  product = compute_product(number)
  puts "The product of the integers between 1 and #{number} is #{product}."
else
  puts "Oops. Unknown operation."
end
```

##### NOTES 
- The School solution opted to divide the problem into separate methods. It creates a method for addition and one for multiplication.
- Note how the operations are performed:
  ```ruby
  1.upto(number) { |value| total += value }
  #AND
  1.upto(number) { |value| total *= value }
  ```
- However is good we get familiar with `Enumerable#inject` or `Enumerable#reduce` methods (they are aliases) 
- Note that all `Enumerable` methods can be used on `Array`.


==================================================================

### Exercise 9: String Assignment

Take a look at the following code:

```ruby
name = 'Bob'
save_name = name
name = 'Alice'
puts name, save_name
```

What does this code print out? Think about it for a moment before continuing.

#### My answer
```ruby
Bob
Alice
```

Correct!

Now, let's look at something a bit different:

```ruby
name = 'Bob'
save_name = name
name.upcase!
puts name, save_name
```

What does this print out? Can you explain these results?

#### My answer
```ruby
BOB
BOB
```

- `name` and `save_name` are two variables that point to the same address in memory where the string `'Bob'` is stored
- any change in the string will be reflected in both variables
- the `upcase!` method mutates the caller, in this case `name` (which points at `'Bob'` string in memory)
- so the string `'Bob'` mutates to `'BOB'` and that is reflected in any variable pointing to that string

#### School answer
- Because assignment in ruby just assigns a reference to a variable, both `name` and `save_name` refer to the same string, `Bob`. 
- When you apply `name.upcase!`, which mutates `name` in place, the value that `save_name` references also changes. 
- Thus, both `name` and `save_name` are set equal to `'BOB'`

==================================================================

### Exercise 10: Mutation

What will the following code print, and why? Don't run the code until you have tried to answer.

```ruby
array1 = %w(Moe Larry Curly Shemp Harpo Chico Groucho Zeppo)
array2 = []
array1.each { |value| array2 << value }
array1.each { |value| value.upcase! if value.start_with?('C', 'S') }
puts array2
```

#### My answer
```ruby
Moe
Larry
CURLY
SHEMP
Harpo
CHICO
Groucho
Zeppo
```

- As in the previous exercise, here are two variables, `array1` and `array2`, pointing at the same object in memory an array with names 
- We see how in line 3 `array1` is duplicated and assigned to a new variable `array2`, which means we now have to variables corresponding to the same object (an array with names).
- In line 4 an `upcase!` method is applied to some elements in the array. This method mutates the caller object in place.
- This change, made to the original method, is reflected in any variable pointing to it, so after the mutation, the changes affect both `array1` and `array2`.
- In this case the last line of code outputs `array2`, but the same thing will be printed if the code outputs `array1`

#### School answer
- The answer lies in the fact that the first `each` loop simply copies a bunch of references from `array1` to `array2`. When that first loop completes, both arrays not only contain the same values, they contain the same String objects. If you modify one of those Strings, that modification will show up in both Arrays.



=======

#### My answer

##### Rules / requirements

##### Examples

#### Data Structure

#### Algorithm

#### Code
```ruby

```

#### School answer
```ruby

```

#### Further exploration

##### NOTES 

```ruby

```