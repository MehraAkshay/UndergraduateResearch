# Week 3: Exercises and some notes

## Exercises

This week, we will have a single assignment, with two parts. 

1. Given a real number *a*, a time step *deltaT*, and a span of time made up of a start value *timeStart* and an end value *timeEnd*, write a function that:
   - Produces a vector of time values, *tValues*, from *timeStart* to *timeEnd*, with spacing *deltaT*.
   - Creates a second vector, *aValues*, of equal length to the first, whose elements all have the value *a*.
   - Plots *a* against time. 

    Name the function something like **constantSignal**. 

    Two hints:
   - If the first line in your function is `close all`, Matlab will close any open figure windows before proceeding. 
   - The function `plot(x, y)` will plot the values in `x` and `y` as a line. See `doc plot` for more information. 

   The function above can be thought of as a simulation of a system at **[steady state](https://en.wikipedia.org/wiki/Steady_state)**. We can represent such a system using a simple box model:
     <p align="center">
     <img src="boxModel.png" width="250" />
     <p>
     which has some input flux (F<sub>in</sub>), some output flux (F<sub>out</sub>), and a *reservoir* with some contents. At steady state, F<sub>in</sub> = F<sub>out</sub>. Imagine, for example, you fill up a bathtub with water (i.e., the contents). Then, you open the drain. If the amount of water coming out of the faucet (i.e., the input flux) is exactly the same as the amount of water leaving down the drain (i.e., the output flux), the water level in the bathtub will not change.

2. Now, say we want to understand what happens if F<sub>in</sub> is not equal to F<sub>out</sub>. We can do so by using the vectors that we created in step 1 as a starting point. Write a function that takes in the variables *tValues* and *aValues*, along with a perturbation time *pT*, and perturbation values *fIn* and *fOut*. Your function, titled something like **perturbationTest**, should:
    - Create a new vector called *perturbedValues*.
    - At each time step, decide whether the value of *a* should be updated (hint, if the time is less than the value of *pT*, nothing should change). If nothing should be done, the value of *a* should be copied into *perturbedValues*.
    - If it is necessary to update, add the value of *fIn* to the last value inserted into *perturbedValues* and subtract the value of *fOut* from the result, then store the final value in *perturbedValues*.
    - Plot *perturbedValues* against time. 
    - Also plot up the original values of *a* vs. time on the same figure (hint: use the function `hold on`).
    - Output *perturbedValues*. 
3. For both 1 and 2, use the following values for the named variables:
    Variable | Value
    --- | ---
    *a* | 100.0
    *timeStart* | 1.0
    *timeEnd* | 100.0
    *deltaT* | .01
    *pT* | 25.0
    *fIn* | 10.0
    *fOut* | 5.0

    Note: run the function in step 2 twice, flipping the values of *fIn* and *FOut*.

## On debugging

 As your programs become longer and more complex, you might find yourself searching, in frustration, for some small error. Or, you may be handed someone's extensive (and completely un-commented) codebase and then left with the task of figuring out what the code actually is doing. In both cases, what you need is a means to **debug.** Here, we'll walk through several strategies for debugging:

 1. **Print out the result of each line**
   
    In Matlab, either remove the `;` at the end of a line or use `disp()` to have the results of a computation show up in the command window. 

    You'd be surprised at how effective this strategy can be. One example of the usefulness of printing out results:
    ```Matlab
    y = [];
    for x = 1:10
        y(x) = x + 1;
        % Is y(x) getting properly updated?
        % Print it out!
        y(x)
    end
    ````
1. **Use breakpoints**
   
    Breakpoints are locations in your code where the code literally breaks (i.e., pauses execution). By using a breakpoint, you can get a snapshot of the workspace right before executing the line of code that you've chosen. 
    In Matlab, you can use `dbstop` or [create breakpoints using the GUI](https://www.mathworks.com/help/matlab/matlab_prog/set-breakpoints.html).

    Breakpoints are an excellent tool to figure out what is going on inside nested loops and/or functions. 
    
    **An important note**: If you have one function that calls a second function that has a breakpoint (or a `keyboard` command, see below), execution *will* stop when the second function gets to the breakpoint.

2. **Use interactive debugging (i.e., `keyboard`)**

    In Matlab, put the command `keyboard` wherever you want to pause execution of code (like with breakpoints).

    `keyboard` is my personal favorite tool for trying to understand what my code is doing---often, I'll declare a function, write some lines of code, then include the term `keyboard` and run the function. I'll check to see whether variables in the workspace are being properly updated (e.g., did the I create a 10x10 matrix instead of the 10x1 vector that I wanted?). Then, I'll continue to develop my code by writing a few more lines, adding `keyboard` in locations of special interest, and rerunning the function. That way, I'm usually able to catch small errors early.

    When using `keyboard`, you can continue code execution by either calling `dbcont`, `dbquit`, or pressing the green run button in the menubar. 

    An example:
    ```Matlab
    y = [];
    for x = 1:10
        y(x) = x + x;
        % The execution will pause on the next line
        % Then, you can check what the workspace looks like
        keyboard
    end
    ```
