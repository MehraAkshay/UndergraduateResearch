# Week2: Two short exercises and some notes

## Exercises

1. Given a number **n**, find the sum of all numbers from **1 to n**. 

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

2. Given a number **n**, output a matrix that serves as a multiplication table for all numbers **1 to n**.

    Two hints:

    - The `'` operator [**transposes**](https://chortle.ccsu.edu/VectorLessons/vmch13/vmch13_14.html) a matrix.
    - This problem can be solved by some simple [matrix multiplication](https://www.mathsisfun.com/algebra/matrix-multiplying.html). 

## Some thoughts

- We didn't review functions in Week 1, but will focus on them in Week 2. For now, you should know that, generally, functions work by taking an input (or multiple inputs), doing something, and then returning an output. Many languages have **built-in functions** that make programming much easier. In Matlab, functions, like `sum`, have the form: `[output] = functionName(input)`. Note that you can have multiple inputs (see `linspace`) and outputs. Multiple inputs are separated by commas, while multiple outputs must be enclosed in square brackets (without those brackets, a function will only return the first output). 

- How do you know what built-in functions exist? What about trying to figure out the specific inputs, outputs, or algorithms of a function? Well, in addition to searching online, you can look through the [Matlab documentation](https://www.mathworks.com/help/). If you already have a function in mind, you can also type `doc functionName` in the command window (replace `functionName` with the function you're trying to understand). Doing so will pull up the documentation for the function of interest. Try it out with `linspace`!

- When working with Matlab, you need to get comfortable thinking in terms of matrices/arrays. Importantly, many functions in Matlab work by default on either **columns** or **rows**. So, if you had a matrix that was 5x5 (i.e., 5 rows by 5 columns; Matlab uses the mxn matrix notation, where m is rows and n is columns), the function `sum` would add up the elements in each column and give you a 1x5 matrix as an output. What if, instead, you wanted the sum of each row of elements? Read the documentation for `sum` to find out!

- We need to talk about array indexing in more detail next week, and I'll update this document accordingly before Friday's meeting. 