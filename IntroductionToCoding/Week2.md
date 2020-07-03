# Week2: Two short exercises and some notes

## Exercises

1. Given an integer **n**, find the sum of all integers from **1 to n**. 

    Two hints that might be useful for solving this problem: 

    - If you want to generate a linearly spaced vector (which is a [one dimensional array](https://en.wikipedia.org/wiki/Array_data_structure#One-dimensional_arrays)) in Matlab, you can either use the function `linspace` or leverage the colon operator, like so:
        
    ```Matlab
        % linspace takes the general form linspace(x1, x2, n), 
        % where x1 is the first number, x2 is the second number, and n (which is optional) is the number of elements
        numberVector = linspace(1, 100, 100);
        % Alternatively, generate a vector from 1 to 100 with a spacing of 1 using the colon operator
        % The general form is x1:spacing:x2
        numberVector = 1:1:100;
    ```

    - The function `sum` will add up all of the entries in a vector and return a single number.

2. Given an integer **n**, output a matrix that serves as a multiplication table for all integers **1 to n**.

    Two hints:

    - The `'` operator [**transposes**](https://chortle.ccsu.edu/VectorLessons/vmch13/vmch13_14.html) a matrix.
    - This problem can be solved by some simple [matrix multiplication](https://www.mathsisfun.com/algebra/matrix-multiplying.html). 

## Some thoughts

- We didn't review functions in Week 1, but will focus on them in Week 2. For now, you should know that, generally, functions work by taking an input (or multiple inputs), doing something, and then returning an output. Many languages have **built-in functions** that make programming much easier. In Matlab, functions, like `sum`, have the form: `[output] = functionName(input)`. Note that you can have multiple inputs (see `linspace`) and outputs. Multiple inputs are separated by commas, while multiple outputs must be enclosed in square brackets (without those brackets, a function will only return the first output). 

- How do you know what built-in functions exist? What about trying to figure out the specific inputs, outputs, or algorithms of a function? Well, in addition to searching online, you can look through the [Matlab documentation](https://www.mathworks.com/help/). If you already have a function in mind, you can also type `doc functionName` in the command window (replace `functionName` with the function you're trying to understand). Doing so will pull up the documentation for the function of interest. Try it out with `linspace`!

- When working with Matlab, you need to get comfortable thinking in terms of matrices/arrays. Importantly, many functions in Matlab work by default on either **columns** or **rows**. So, if you had a matrix that was 5x5 (i.e., 5 rows by 5 columns; Matlab uses the mxn matrix notation, where m is rows and n is columns), the function `sum` would add up the elements in each column and give you a 1x5 matrix as an output. What if, instead, you wanted the sum of each row of elements? Read the documentation for `sum` to find out!

## On accessing and manipulating arrays in Matlab

- Each programming language has its own way of dealing with data. In Matlab, [all variables are arrays](https://www.mathworks.com/help/matlab/learn_matlab/matrices-and-arrays.html), regardless of the underlying data.
  
- There are many different kinds of arrays, but here we'll focus on numeric arrays, which are created by using square brackets:
```Matlab
    anEmptyNumericArray = [];
```

- Arrays are multidimensional. Typically, the first dimension corresponds to rows (*m*) and the second to columns (*n*). The most basic arrays are either row or column vectors:
```Matlab
    % A row vector, which has the dimensions 1 x 5
    % Note that (,) separates the elements into columns
    rowVector = [1, 2, 3, 4, 5];
    % A column vector, which has the dimensions 5 x 1
    % Note that (;) separates the elements into rows
    columnVector = [1; 2; 3; 4; 5];
    %% A 3x3 matrix
    firstMatrix = [1, 2, 3; 1, 2, 3; 1, 2, 3];
```

- In arrays or lists of data, each item has an **index**, which tells you where in the array to find that datum. Matlab is **1 indexed**: the first item in a row or column has an index of 1, and each subsequent item has an index of `n`, where `n` is the row or column number. Compare this to a **0 indexed** language, where the first item of an array has an index of 0 (and, in turn, each subsequent item has an index value of `n-1`).

- So, to access an item in an array, you use round brackets and the index or indicies of the items you're interested in:
```Matlab
    % Say I want the top left item in the firstMatrix we declared above
    % That has a row index of 1 and a column index of 1
    firstItem = firstMatrix(1, 1);
    % Now say I want the first two items in the first row
    % Those have a row index of 1
    % and column indicies of 1 and 2, which we can write 1:2
    firstTwoItems = firstMatrix(1, 1:2);
    % Now say I want all of the items. You can write :
    allItems = firstMatrix(:, :);
    % Another way to get all elements is to just use :
    allItems = firstMatrix(:);
    % What if I want the last item in the array? You can use the keyword end
    lastItem = firstMatrix(end, end);
    % Second to last item in the third row?
    secondToLast = (3, end - 1);
    % And so on
```
- You can put two arrays together, using the **concatenation operator** (make sure that your dimensions agree! i.e., if you have an array of size 3x3, you cannot add a row that is >3>, and you cannot add a column that is >3>):
```Matlab
    % Add a row to firstMatrix
    firstMatrix = [firstMatrix; 4, 4, 4];
    % Add a new column to the redefined first matrix:
    firstMatrix = [firstMatrix, [4; 4; 4; 4]];
```

- A little note: in programming, it's acceptable to assign the output of some action/function on a variable to itself (e.g., ```firstMatrix = firstMatrix + 1```).

- In Matlab, you can apply all sorts of **matrix operations** (e.g., transposition, multiplication, etc.) to numeric arrays, regardless of whether they are vectors, matrices, or some n<sup>th</sup> dimensional construction.

## Booleans
- At some point, you'll find yourself working with **booleans**, or true and false values. Importantly, a boolean can be represented as either `true` or `false`, `1` or `0`.

## On if statements and logical operators
- Okay, so you can open up Matlab and declare a variable. Now, what if we want to see if that variable meets some condition? For that, we can leverage [relational](https://www.mathworks.com/help/matlab/relational-operators.html) and [logical operators](https://www.mathworks.com/help/matlab/logical-operations.html) in conjunction with **if/then** statements. 
  
- Relational operators allow you to test conditions (like, is x equal to y?):
``` Matlab
    x = 1;
    y = 1;
    z = 2;
    % Is x equal to y?
    theSame = x == y;
    % theSame is 1 (i.e., true, see note on booleans)
    % is x greater than z?
    greaterThan = x > z;
    % greaterThan is 0
```
- Logical operators, which include AND (`&&`), OR (`||`), and NOT(`~`), allow you to build conditional statements, such as, "X equals Y AND Y is less than Z":
```Matlab
    % is x NOT equal to z?
    notEqual = x ~= z;
    % notEqual is 1
    % How about, is x equal to y but less than z?
    conditionalTest = (x == y) && (y < z)
    % conditionalTest is 1
```
- Note that `&&` and `||` represent the **short circuiting** versions of `&` and `|`. That means that Matlab won't evaluate subsequent conditions unless the first one is true. 
- Put in if statement!

## On loops and program flow

- A mainstay of programming are **loops**, which repeat the same code until some condition is reached
- Here, we'll discuss `for` loops, but there are other forms of repeatable code, including [`while`](https://www.mathworks.com/help/matlab/ref/while.html).
- In general, a `for` loop runs for a set number of **iterations**. In Matlab, `for` loops take the form:
```Matlab
    for indexVariable = startingIteration:endingIteration
        % Do something 
    end
```
- Note that the keyword `end` must be included at the end of your for loop (same for if statements and functions)!
- So, to write a for loop that iterates through integers 1 to 10, you would write:
```Matlab
    for idx = 1:10
        idx
    end
```
- You can use what you know about indexing (see above), to go through a matrix and make changes to it:
```Matlab
    % A preallocated variable!
    % A 10 by 1 vector of 0s
    output = zeros(10, 1);
    % Our input variable
    % A 1 by 10 vector of monotonically increasing integers
    input = 1:10;
    % Length gives you the size of the longest dimension of a vector or matrix
    % so you don't have to hardcode in that value
    for idx = 1:length(input)
        % Add 1 to each value in input
        % Since input is a vector, you can omit the column specification and instead write:
        % output(idx) = input(idx) + 1;
        output(idx, 1) = input(1, idx) + 1;
    end
    % Output is now 2:11
```
## On functions

- As noted above, a **function** takes an input and returns an output.
- In Matlab, a function can have *many* input **parameters** and *many* output parameters and takes the general form `function [outputParameter1, ...] = functionName(inputParameter1, inputParameter2, ...)` and ends with `end`.
- If you create a file with a function, the file name **must match** the function name! 
- Unlike a script, variables that are declared within a function remain within the function's **scope**. So, if you run a function, you will not see those variables in your workspace once the function is done running. If you want to keep a variable in the workspace (e.g., you want to use it for some other calculation in some other function), you must make sure that it is included as an outputParameter:
```Matlab
    function [summed, difference] = addAndSubtract1(inputMatrix)
        % Note that you still need to declare the variables summed and difference somewhere! 
        % Summed will just end up being inputMatrix + 1
        summed = inputMatrix + 1;
        % Difference is inputMatrix - 1;
        difference = inputMatrix - 1;
        % Squared, which is not included as an outputParameter, is just inputMatrix ^ 2
        % Note that if you run addAndSubtract1, you will never see squared, 
        % unless you include it as an output parameter! But Matlab will still do the calculation.
        squared = inputMatrix .^ 2;
    end
```
- Functions enable you to create reusable logic.  Used correctly, they enable you to practice the [**DRY**](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (i.e., don't repeat yourself) principle. For example, if you find yourself doing the same set of actions on multiple variables, turn those actions into a function!