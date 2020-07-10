# Week 1: Thoughts about variables, comments, program execution

## Variables

- Variables may be **typed** (i.e., the value of a variable must be of a specified data type) or **untyped** (i.e., a variable can hold information of any data type). This specification is dependent on the language and some, like Matlab, are designed to automatically figure out what type to assign a variable. For our purposes, using Matlab means that you don't have to worry about typing (but in certain cases---e.g., for performance purposes---we may want to explicitly declare a data type)

- Careful variable naming is incredibly important! Your variable names must be **both concise and descriptive**. Avoid single letters and, as much as possible, numbers in the name. So:
    ```Matlab
        % Variable names that you will regret when you try to read your code 6 months after writing it
        a = 1; 
        thisIsAVeryVeryLongVariableNameThatDoesntTellMeAnythingAboutWhatItContains = 0;
        01 = 1;
        % Variable names that are easy to follow
        gravityConstant = 9.8;
        box_width = 10;
    ```
- Note that variables cannot have spaces, but you can opt for [several accepted conventions](https://devopedia.org/naming-conventions), including [camel case](https://en.wikipedia.org/wiki/Camel_case) (e.g., lowercaseFirstWordButCapitalizeEveryOtherWord) and [snake case](https://en.wikipedia.org/wiki/Snake_case) (e.g., underscores_between_words).

- Try to **initialize** variables with some value, if only NaN or 0. In Matlab, **preallocating** variables (i.e., declaring a variable whose length does not change even if its value(s) do) provide a noticeable performance boost.

## Comments

- **Comment your code!** Whether you write a sentence for every line (extremely helpful when starting off) or include a short paragraph at the top of a block explaining what your code is doing, commenting enables you and others to better understand a) your intent and b) your execution. Like proper variable naming, you'll appreciate your comments most when you're forced to look at your code several days/weeks/months/years after writing it.

- Comments aren't executed, so feel free to comment out lines of your code that didn't work, were ineffective, or helped lead you to a working implementation. 

- Be expressive with your comments! Ideas, thoughts, links, etc. can all be included.

- In Matlab, there are two types of comments, **per line** (using %) and **block** (using %{ and %}):
    ```Matlab
        % I've commented out this line of code
        gravityConstant = 9.8; % I also can add a comment on the same line as a piece of code
        %{
            Here's a long block comment, where I might type up a whole paragraph about this code, my life, etc.
            I also can comment out bad code:
            badGravityConstant = 10;
        %}
    ```

## Coding conventions

- Each language has conventions that you should know and follow. In this section, we'll include several conventions you should know about Matlab

- End lines in a semicolon **unless** you want Matlab to echo the result of that line
    ```Matlab
        % Nothing gets printed out
        force = 100 * 9.8;
        % Matlab displays 9800 in its command window
        force = 100 * 9.8
    ```

- **Per element** multiplication and division is accomplished by using .* and ./.

- ...

## Program execution

- What sets Matlab apart from other languages is that it comes with a built-in Integrated Development Environment (IDE). When you start up Matlab, you see a file explorer, a space in which variables are display, a code editor, and a command window. You can interact directly with the command window:
    ```Matlab
        % Type the following and hit enter:
        1 + 2
        % Displays 3 in the command window
    ```
    You also can write scripts in the code editor and then hit run (the big green play button in the toolbar above the code editor):
    ```Matlab
        % Copy paste this entire codeblock into the code editor, save, and then hit run.
        % Close all existing figures
        close all
        % Create a new figure
        figure;
        % What is the circle radius?
        radius = 10;
        % Declare a matrix of theta values
        theta = 0:pi/50:2*pi;
        % Calculate X and Y coordinates (assuming an origin at 0,0);
        unitX = radius * cos(theta);
        unitY = radius * sin(theta);
        % Plot up
        plot(unitX, unitY);
        % Turn on grid
        grid on
        % Fix aspect ratio
        pbaspect([1,1,1]);
    ```
    Additionally, you can develop and execute **functions**, which we'll study in another week.

- When writing scripts or functions, avoid using **fixed numerical values.** Wherever possible, declare a variable, so that you can update your code easily (i.e., it is **parameterized**).
    ```Matlab
    % Imagine you want to change the value of mass or acceleration in multiple parts of your code. You'd have to read through your code, looking for every instance and then manually change it:
        force = 1000 * 9.8;
        biggerForce = 1000 * (10*9.8);
    % It's much easier to update your code by changing the value(s)assigned to a variable(s). As a bonus, using variables throughout makes your code much easier to read:
        mass = 1000;
        acceleration = 9.8;
        force = mass * acceleration;
        biggerForce = mass * (10*acceleration);
    ```
- ...