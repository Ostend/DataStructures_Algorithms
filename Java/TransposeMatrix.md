# #867 Transpose Matrix

> Given a 2D integer array matrix, return the transpose of matrix.

> The transpose of a matrix is the matrix flipped over its main diagonal, switching the matrix's row and column indices.

**Example 1:**

> Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
> Output: [[1,4,7],[2,5,8],[3,6,9]]

---

# Technique

This one took longer to figure out than I want to admit.

Let’s start with the basics. **What is a matrix?**

Basically, a 2d array. Think of the face of a Rubik’s cube.
![unnamed](https://user-images.githubusercontent.com/60686512/157445457-5bace2da-436a-4be2-9249-42fd089013be.png)

It is a matrix of three columns and three rows.

Represented in code:

```java
    [[1,2,3],[4,5,6],[7,8,9]]
```

OR, to visualize better:

```java
    [[1,2,3],
     [4,5,6],
     [7,8,9]]
```

You can see better the columns (3) and the rows (3) represented.

This leetcode is asking to transpose the matrix. This means to flip it along the main diagonal. In other words, the rows and the columns are flipped.

Here is what the above matrix looks like flipped along the main diagonal:

```java
    [[1,4,7],
     [2,5,8],
     [3,6,9]]
```

Can you spot the difference?
Notice that the elements on the main diagonal `1,5,9` do not change position.

Notice that the columns have turned into rows, and the rows into columns: `1,4,7` when from a column to a row.

With this information, transposing a matrix is fairly simple.

1. Iterate through the number of the rows. In this case 3.
2. Iterate through the number of columns. In this case also 3.
3. Within the inner loop iteration, swap the elements.

##### Concepts

- 2D arrays
  - declaring empty 2D arrays
  - accessing 2D array elements
  - modifying 2D array elements

# Code

```java
class Solution {
    public int[][] transpose(int[][] matrix) {
        int[][] newMatrix = new int[matrix[0].length][matrix.length];
        for(int i=0; i<matrix.length; i++){
            for(int j=0; j<matrix[0].length; j++){
                newMatrix[j][i] = matrix[i][j];
            }
        }
        return newMatrix;
    }

}
```

##### Line by line

- ```java
    int[][] newMatrix = new int[matrix[0].length][matrix.length];
  ```

  Initializing a new empty matrix. The size of the matrix is represented by the values passed in `int[size][size]` on the left hand side assignment.
  In this case, because we are flipping the rows and columns, the size of the rows is assigned to `matrix[0].length`, which represents the column length in the original matrix. The size of the columns is assigned to `matrix.length`, which represents the row length of the original matrix.

  Why? Well not all matrices are `n x n` aka squares. <br/>
  **Ex.** <br /> The matrix below is a 2x3 matrix. Meaning, there are 2 rows and 3 columns.

  ```java
      [[1,2,3],
       [4,5,6]]
  ```

  To transpose this, the new matrix has to be defined to represent 3 rows and 2 columns.

  ```java
      [[1,4],
       [2,5],
       [3,6]]
  ```

  The rows become columns and the columns become rows. The demension of the matrix have changed.

- ```java
       for(int i=0; i<matrix.length; i++){
           for(int j=0; j<matrix[0].length; j++){
  ```
  The loops to iterate through and access the outer and inner arrays. The first for loop iterates over the outer array, or the rows, while the inner loop iterates over the inner array, or the columns.
- ```java
     newMatrix[j][i] = matrix[i][j];
  ```

  This is where the magic happens.
  the newMatrix is assigned the value of the mirror value in the origional matrix.
  **Break it down** <br/>

  ```java
      [[1,2],
       [3,4]]
  ```

  - **First iteration:**
    `i = 0` and `j = 0`
    Meaning: `matrix[i][j]` = 1
    `newMatrix[0][0] = 1`
    Now, newMatrix looks like: `[[1,x],[x,x]]`
  - **Second iteration:**
    `i = 0` and `j=1`
    Meaning: `matrix[i][j]` = 2
    `newMatrix[1][0] = 2`
    Now, newMatrix looks like: `[[1,x], [2,x]]`
  - **Third iteration:**
    `i=1` and `j=0`
    Meaning: `matrix[i][j]` = 3
    `newMatrix[1][0] = 3`
    Now, newMatrix looks like: `[[1,3],[2,x]]`
  - **Fourth iteration:**
    `i=1` and `j=1`
    Meaning: `matrix[i][j]` = 4
    `newMatrix[1][0] = 4`
    Now, newMatrix looks like: `[[1,3],[2,4]]`

  And there you have it, a matrix transposed aka a matrix flipped.
