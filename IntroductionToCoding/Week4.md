# Week 4: Adding feedbacks to your box model (and how to version control)

## Box model

Last week, we created a very simple box model that, unlike systems in the real world, lacked any sort of [feedback](https://en.wikipedia.org/wiki/Feedback). This lack of feedback --- and the absence of any sort of error checking (i.e., stopping when the system output negative numbers)---meant that our box model wasn't very useful. This week, we'll add several elements to our box model. 

### Residence time

To start off with, we'll write a function that calculates the [residence time](https://en.wikipedia.org/wiki/Residence_time) of the contents of a box at **steady state** (meaning that the system is not changing and that *F<sub>in</sub> = F<sub>out</sub>*). Residence time *T* is defined as:

<img src="https://render.githubusercontent.com/render/math?math=T = contents/\sum{flux}"></img>

at steady state. Your function, named something like `residenceTime`, should take as inputs: 
1. contents
2. F<sub>in</sub> 
3. F<sub>out</sub>

and output:
1. T
   
Assume that the input units are appropriately scaled (e.g., if the contents are in volume liters, F<sub>in</sub> and F<sub>out</sub> are in liters/minute). 

Inside your function, check to make sure that the fluxes sum to 0 (if they are not, you should display a message, using `disp` that says as much and then exit the function using `return`). If fluxes sum to 0, calculate the residence time and provide it as an output.

### Feedbacks

You may have noticed is that we've treated F<sub>in</sub> and F<sub>out</sub> as constants up to this point. Unfortunately, by doing so, we've ensured that our system can't really respond to our prescribed changes (i.e., if we increase F<sub>in</sub> relative to F<sub>out</sub>, the contents of our box will continue to increase, forever). Conversely, real systems can modulate perturbations by using feedbacks that alter fluxes in relation to conditions in the system. 

On Earth, one such example of a feedback is *silicate weathering.* As CO<sub>2</sub> increases (by, say, volcanic outgassing), Earth's temperature also increases. As Earth's atmospheric CO<sub>2</sub> and temperature go up, the weathering of silicate rocks also goes up (due to greater reactivity, among other factors). As silicate weathering sequesters carbon, atmospheric CO<sub>2</sub> drops. This feedback also works if CO<sub>2</sub> drops---Earth cools, silicate weathering slows down, and CO<sub>2</sub> is able to build up in the atmosphere. In this way, Earth keeps from becoming a sweltering hothouse or a ball of ice. **Essentially, F<sub>out</sub> is proportional to the amount of CO<sub>2</sub> in the system.**

So, let's model the silicate weathering feedback loop! At the heart of our model will be a function called `silicateWeatheringTimeStep`, which will take as inputs:
1. A value for F<sub>in</sub>
2. A value for atmospheric Carbon, C, (in mass, typically reported in gigatons)
3. A sensitivity parameter K<sub>w</sub> (see below)
   
and output:
1. A value for F<sub>out</sub>
2. Updated value for atmospheric carbon in the system

As F<sub>out</sub> is proportional to the amount of CO<sub>2</sub> in the system, we'll use a *weathering sensitivity parameter* K<sub>w</sub>. Therefore, at any given moment, F<sub>out</sub> can be calculated as K<sub>w</sub> * amount of CO<sub>2</sub>.

Note that we're making some simplifications here, namely that we're not worrying about converting CO<sub>2</sub> into mass of carbon or calculating partial pressure of CO<sub>2</sub>. In a more rigorous model, we'd be very careful with units and conversions. 

After defining `silicateWeatheringTimeStep`, you should create a controller function called `boxModel`. 

In box model, you'll start with the following inputs:

1. F<sub>in</sub>: 10
2. CO<sub>2</sub> in system: 100
3. Run length of model (i.e., time): 1000
4. Time resolution (i.e., time step): 1
5. Perturbation timing: [150, 750]
6. Perturbation amount: [50, 25]

You'll start your function by calculating K<sub>w</sub>, assuming a steady state condition (remember, that means that F<sub>in</sub> = F<sub>out</sub> and F<sub>out</sub> = K<sub>w</sub> * CO<sub>2</sub> in the system).

You should ensure that `boxModel` can model an arbitrary number of instantaneous perturbations (here, happening at time step 150 *and again* at time step 750, each instance with a different perturbation amount, first 50, then 25; see input listing). The specified perturbation amount should be added to the existing  CO<sub>2</sub> in the system *without* changing any other parameters. If programmed correctly, the model then should respond by equilibrating over some response time. 

You'll run your system for the given run length, using `silicateWeatheringTimeStep` to update the amount of CO<sub>2</sub> in the system at every time step. You should also keep track of F<sub>out</sub> at each time step. At the end of the run, `boxModel` should plot up CO<sub>2</sub> through time, as well as F<sub>out</sub> through time. 


**Try to reuse some of your code from last week!**

### A challenge

Once your model is working, try running it with an F<sub>in</sub> that starts at 10, runs for 100 time units, and then decreases to 5 over 100 time units. Run your model with no perturbations (so your inputs for perturbation timing and amount will be empty matrices---your code should be written to handle such a condition).

## On Version Control

This week, we will talk about version control. Notes will appear here before Friday's meeting. 