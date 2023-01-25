# conways-game-of-life-react-redux
Creating Conway’s Game of Life with ReactJS/Redux
I just finished writing the code for the MVP of my final project for Flatiron School’s software engineering program. Over the last 5 months I have spent countless hours at my computer writing and re-writing line after line of code, learning Ruby on Rails, JavaScript and now front-end frameworks like ReactJS. I really wanted to challenge myself for the final project, and I think that this ended up being my favorite software project I’ve ever done!

# Introduction:
The Game of Life by is a cellular automaton created by mathematician John Conway (who recently passed away due to COVID-19 complications). The consists of a grid of cells that are either in a “live” state or “dead” state. A cell’s state is determined by its surrounding neighbors (also called Moore neighborhood). The rules to the game are simple, and there are only four of them:

1. Any live cell with less than two live neighbors dies, as if by underpopulation.
![1](https://user-images.githubusercontent.com/93249038/214484612-ba2f202b-8584-4ee1-b7d0-c377ec6b6cc5.jpg)


Both of these cells will die off in the next generation.
2. Any cell with more than three live neighbors dies, as if by overpopulation.

![2](https://user-images.githubusercontent.com/93249038/214484667-3a2111ad-6874-4ded-807f-43981abd1181.jpg)



The cell in the middle will die off in the next generation (along with the one above it because of rule #1)
3. Any cell with either two or three live neighbors lives on to the next generation.
![3](https://user-images.githubusercontent.com/93249038/214484683-9588c76c-8615-4172-b7ef-a6aaab2fa3a5.jpg)

The middle cell will live on, while the other two will die off.
4. Any dead cell with exactly three live neighbors will become alive.

The green cell is currently dead and will come back to life in the next generation.
Now, what makes Conway’s creation interesting isn’t really the rules of the game themselves, but the complex patterns that start to emerge on the grid based off of these 4 simple rules.

![4](https://user-images.githubusercontent.com/93249038/214484698-40322bda-5494-4c9f-9924-cf45ef46bf4d.jpg)

 learning a JavaScript framework that would work really well for storing the initial state of a grid like this to be saved to a back-end API.

# Implementing the game grid with ReactJS
The first thing to do was create an initial state of the game grid that could be instantiated with a Redux reducer. obviously needed a matrix, but  also knew that  wanted to let users customize the size of the grid, the cell size, and the speed between generations. Also, how would I keep track of whether each cell was currently alive or dead? I decided to write a dynamic function for creating the grid matrix, so that later on columns and rows could be edited. Each row would consist of a second array of boolean values, true for alive and false for dead. I also added a settings object to the initial state.
![5](https://user-images.githubusercontent.com/93249038/214484712-e8ffe434-5a78-45c1-ae95-8ce0c6e8fe98.jpg)


With the initial state figured out, next  needed to create a React component for rendering the initial grid, that could be clicked upon and updated. decided to display each cell of the grid as it’s own Cell component. For this passed in it’s location in the matrix as props, as well as giving it a className of it’s current state.


# Rendering the Grid

Rendering the Cell
Once users could click and set an initial state it was time to try to begin the simulation. The task seemed simple but took a while to get coded out. needed to iterate through the matrix, and for each cell check it’s surrounding neighbors. Then I would need to increment a counter for any live neighbors that were found and check that counter against the game’s rules to determine the cell’s state for the next generation. When comparing a cells neighbors, after looking at a few different ways to do it I decided that the easiest way would be to iterate through another array that would hold the neighbor’s position relative to the current cell. With that it was easy to get the number of live neighbors for every cell on the grid.


I did run into some issues with the fact that setState is an asynchronous function so I decided to render a stateless grid for when the simulation is actually running. In order to re render the screen I had to use the forceUpdate() function, but I am planning on refactoring the code to do this more efficiently.

One of my favorite parts of this project was creating the sliders to let users change the settings of the initial grid state. By using Redux dispatch actions, and keeping track of the Settings component’s state I was able to create a really nice looking UI for editing the settings using Material UI Slider components.


The speed is setting the setInterval amount in milliseconds, so less is faster and more is slower.
When setting up the back end of the project first created a normal “out-of-the-box” Rails API, but then realized that wasn’t sure how was going to store the grid as an array inside of an ActiveRecord model. In comes PostgreSQL to the rescue!

It turns out that it is actually really easy to store arrays with PostgreSQL databases and it plays really well with ActiveRecord models.  able to store the game settings as a hash, which made my whole back end process a breeze (minus trying to figure out how to use PostgreSQL and give my application SUPERUSER status in a Linux environment, which is necessary to enable storing hashes).


h
