##  RB101-RB109 - Small Problems --> ADVANCE

**This set of exercises are solved using a PEDAC approach**

------------------------

### Exersise 3: Transpose 3x3 

A 3 x 3 matrix can be represented by an Array of Arrays in which the main Array and all of the sub-Arrays has 3 elements. For example:
1  5  8
4  7  2
3  9  6

can be described by the Array of Arrays:
matrix = [
  [1, 5, 8],
  [4, 7, 2],
  [3, 9, 6]
]

An Array of Arrays is sometimes called nested arrays because each of the inner Arrays is nested inside an outer Array.

To access an element in matrix, you use Array#[] with both the row index and column index. So, in this case, matrix[0][2] is 8, and matrix[2][1] is 9. An entire row in the matrix can be referenced by just using one index: matrix[1] is the row (an Array) [4, 7, 2]. Unfortunately, there's no convenient notation for accessing an entire column.

The transpose of a 3 x 3 matrix is the matrix that results from exchanging the columns and rows of the original matrix. For example, the transposition of the array shown above is:
1  4  3
5  7  9
8  2  6

Write a method that takes a 3 x 3 matrix in Array of Arrays format and returns the transpose of the original matrix. Note that there is a Array#transpose method that does this -- you may not use it for this exercise. You also are not allowed to use the Matrix class from the standard library. Your task is to do this yourself.

Take care not to modify the original matrix: you must produce a new matrix and leave the original matrix unchanged.

=> input: nested array
=> output: nested array, that is the transposed version of the input 

=> rules
  > in the original array, each subarray represents a row in a imaginary matrix
  > in the original array, each index position element of each subarray, represents a colum
  
  > transposed means that  
    > given an array of arrays
      > create a new nested array where each index position element of each subarray
      > become the elements of each subarray in the new nested array
      
=> algorithm
  
  => steps
    > initialize a variable to an empty array - new_matrix (will be returned)
    > iterate each subarray in the given nested array
      > access the elements of these subarray at a particular index position
      > put them in a new array, inside new_matrix
      > index position needs to be updated somehow
        > so we first access the index 0 elements of each subarray
        > then we access the index 1 elements
        > etc...

    > return new_matrix populated with new subarrays
    
```ruby
def transpose(matrix)
  new_matrix = []
  counter = 0
  
  matrix.size.times do 
    column = []
    matrix.each do |row|                      # [1, 5, 8]
      row.each_with_index do |elem, idx|      # 1 5 8
        if idx == counter
          column << elem                      # 1  #[1, 4, 3]
        end
      end
    end
    counter += 1
    new_matrix << column
  end
  new_matrix
end

#p transpose([[1, 5, 8], [4, 7, 2], [3, 9, 6]]) == [[1, 4, 3], [5, 7, 9], [8, 2, 6]]

matrix = [
  [1, 5, 8],
  [4, 7, 2],
  [3, 9, 6]
]

new_matrix = transpose(matrix)

p new_matrix == [[1, 4, 3], [5, 7, 9], [8, 2, 6]]
p matrix == [[1, 5, 8], [4, 7, 2], [3, 9, 6]]
```

------------------------

### Exersise 4: Transpose MxN

```ruby
#[1, 2, 3, 4, 5]
#[4, 3, 2, 1, 0]
#[3, 7, 8, 6, 2]

#Solution1
def transpose(matrix)
  new_matrix = []
  counter = 0
  
  matrix[0].size.times do 
    column = []
    matrix.each do |row|                      # [1, 5, 8]
      row.each_with_index do |elem, idx|      # 1 5 8
        if idx == counter
          column << elem                      # 1  / [1, 4, 3]
        end
      end
    end
    counter += 1
    new_matrix << column
  end
  new_matrix
end

#Solution2
def transpose(matrix)
  new_matrix = []
  matrix[0].size.times { new_matrix << [] }
  
  matrix.each do |row|
    row.each_with_index do |item, idx|
      new_matrix[idx] << item 
    end
  end
  
  new_matrix
end

#Solution3
def transpose(matrix)                    # [[1, 2, 3], [4, 5, 6], [7 ,8, 9]]
  new_matrix = []                        # [[1, 4], [2, 5], [3, 5]]
  
  matrix.each do |row|
    row.each_with_index do |elem, idx|
      sub_arr = new_matrix[idx]
      sub_arr.nil? ? new_matrix << [elem] : sub_arr << elem
    end
  end
  
  new_matrix
  
end

matrix = [
  [1, 5, 8],
  [4, 7, 2],
  [3, 9, 6]
]

new_matrix = transpose(matrix)

p new_matrix == [[1, 4, 3], [5, 7, 9], [8, 2, 6]]
p matrix == [[1, 5, 8], [4, 7, 2], [3, 9, 6]]

p transpose([[1, 2, 3, 4]]) == [[1], [2], [3], [4]]
p transpose([[1], [2], [3], [4]]) == [[1, 2, 3, 4]]
p transpose([[1, 2, 3, 4, 5], [4, 3, 2, 1, 0], [3, 7, 8, 6, 2]]) ==
  [[1, 4, 3], [2, 3, 7], [3, 2, 8], [4, 1, 6], [5, 0, 2]]
p transpose([[1]]) == [[1]]
```  

------------------------

### Exersise 5: Rotating Matrices

As we saw in the previous exercises, a matrix can be represented in ruby by an Array of Arrays. For example:
1  5  8
4  7  2
3  9  6

can be described by the Array of Arrays:
matrix = [
  [1, 5, 8],
  [4, 7, 2],
  [3, 9, 6]
]

A 90-degree rotation of a matrix produces a new matrix in which each side of the matrix is rotated clockwise by 90 degrees. For example, the 90-degree rotation of the matrix shown above is:
3  4  1
9  7  5
6  2  8

A 90 degree rotation of a non-square matrix is similar. For example, the rotation of:
3  4  1
9  7  5

is:
9  3
7  4
5  1

Write a method that takes an arbitrary matrix and rotates it 90 degrees clockwise as shown above.

This program should print "true" three times for the test cases below.

=> input: nested array
=> output: new nested array based on input that represents a matrix that is rotated 90 degrees clockwise

=> rules
  > rotate an matrix means
    > first row (subarray) becomes last column in new nested array 
    > second row (subarray) becomes column before last in new nested array
    > third row (subarray) becomes column before last -1 in new nested array

  > for every rotation the elements within the subarray maintain the same order

=> examples:
  input:  [[1, 5, 8], [4, 7, 2], [3, 9, 6]]
  output: [[3, 4, 1], [9, 7, 5], [6, 2, 8]]
  
  input:  [[3, 7, 4, 2], [5, 1, 0, 8]]
  output: [[5, 3], [1, 7], [0, 4], [8, 2]]

=> algorithm
  => goal
    > generate a new nested array based on given nested array where
      > each item in subarray 0
        > will be last item of each subarray of new nested array
      > each item in subarray 1
        > will be the last -1 item of each subarray of new nested array
      > each item in subarray last
        > will be the first item of each subarray of new nested array
    
  => steps
    > initialize variable `rotated` to empty array
    
    > access first subarray of nested array
    > access each element of that subarray
    > populate each subarray of `rotated` with element of subarray as --> prepend method
      > element at index 0  --> element -1 of subarray 0
      > element at index +1 --> element -2 of subarray +1
      > element at index +2 --> element -3 of subarray +2
      > etc. until the end of array
    > repeat this for as many subarrays existing in given nested array
    
```ruby
def rotate90(matrix)
  
  rotated_matrix = []
  counter = 0
  items_in_row = matrix.first.size
  
  items_in_row.times do
    new_column = []
    
    matrix.each do |row|   
      row.each_with_index do |item, item_idx|           
        if counter == item_idx
          new_column.prepend(item)
        end
      end
      
    end
    counter += 1
    rotated_matrix << new_column
  end
  
  rotated_matrix
end

# p rotate90([[1, 5, 8], [4, 7, 2], [3, 9, 6]]) == [[3, 4, 1], [9, 7, 5], [6, 2, 8]]
# p rotate90([[3, 7, 4, 2], [5, 1, 0, 8]]) == [[5, 3], [1, 7], [0, 4], [8, 2]]

matrix1 = [
  [1, 5, 8],
  [4, 7, 2],
  [3, 9, 6]
]

matrix2 = [
  [3, 7, 4, 2],
  [5, 1, 0, 8]
]

new_matrix1 = rotate90(matrix1)
new_matrix2 = rotate90(matrix2)
new_matrix3 = rotate90(rotate90(rotate90(rotate90(matrix2))))

p new_matrix1 == [[3, 4, 1], [9, 7, 5], [6, 2, 8]]
p new_matrix2 == [[5, 3], [1, 7], [0, 4], [8, 2]]
p new_matrix3 == matrix2
```

------------------------

### Exercise 7: Merge Sorted Lists

Write a method that takes two sorted Arrays as arguments, and returns a new Array that contains all elements from both arguments in sorted order.

You may not provide any solution that requires you to sort the result array. You must build the result array one element at a time in the proper order.

Your solution should not mutate the input arrays.

=> input: two sorted arrays
=> output: new array that contains all elements from both argument in sorted order

=> rules
  > cannot use the sort method
  > don't mutate the arguments

=> algorithm
  => goal
    > merge two arrays which elements are sorted
    
  => steps
    > use an index variable to reference elements from both arrays
    > initialize a new variable to empty array
    > initialize a loop
    > reference index element of each array and append it to new array
    > do it to the end of longest array
    
  => steps
    > join both arrays into an unsorted one
    > sort two elements --> helper method
      > if element1 > element2
        > element1, element2 = element2, element1
      > else
        > nothing
    >    
  
```ruby
def sort(array)
  new_arr = array.dup
  
  new_arr.size.times do
    idx = 0
    loop do
      if new_arr[idx] > new_arr[idx + 1]
        new_arr[idx], new_arr[idx + 1] = new_arr[idx + 1], new_arr[idx]
      end
      idx += 1
      break if idx + 1 >= new_arr.size
    end  
  end
  new_arr
end

def merge(array1, array2)
  sort(array1 + array2)
end

p merge([1, 5, 9], [2, 6, 8]) == [1, 2, 5, 6, 8, 9]
p merge([1, 1, 3], [2, 2]) == [1, 1, 2, 2, 3]
p merge([], [1, 4, 5]) == [1, 4, 5]
p merge([1, 4, 5], []) == [1, 4, 5]
```