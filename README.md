Game of Life in Python
This project implements the classic "Game of Life" by John Conway using the Python programming language with the turtle library.

Description
John Conway's "Game of Life" is a cellular automaton where the state of each cell in a grid evolves based on the states of its neighboring cells. This program simulates the evolution of cells on a 2D grid, where each cell can be either alive or dead.

Rules
Any live cell with two or three live neighbors survives.
Any live cell with fewer than two live neighbors dies from loneliness.
Any live cell with more than three live neighbors dies from overpopulation.
Any dead cell with exactly three live neighbors becomes a live cell.
Installation and Running
To run the project, you need Python 3.6 or higher and the freegames library.

Install freegames using pip:

bash
Копировать код
pip install freegames
Run the program:

bash
Копировать код
python game_of_life.py
Code
Here is the main code of the program:

python
Копировать код
from random import choice
from turtle import *
from freegames import square

cells = {}

def initialize():
    """Randomly initialize the cells."""
    for x in range(-200, 200, 10):
        for y in range(-200, 200, 10):
            cells[x, y] = False

    for x in range(-50, 50, 10):
        for y in range(-50, 50, 10):
            cells[x, y] = choice([True, False])

def step():
    """Compute one step in the Game of Life."""
    neighbors = {}
    for x in range(-190, 190, 10):
        for y in range(-190, 190, 10):
            count = -cells[x, y]
            for h in [-10, 0, 10]:
                for v in [-10, 0, 10]:
                    count += cells[x + h, y + v]
            neighbors[x, y] = count

    for cell, count in neighbors.items():
        if cells[cell]:
            if count < 2 or count > 3:
                cells[cell] = False
        elif count == 3:
            cells[cell] = True

def draw():
    """Draw all the squares."""
    step()
    clear()
    for (x, y), alive in cells.items():
        color = 'red' if alive else 'black'
        square(x, y, 10, color)
    update()
    ontimer(draw, 100)

setup(420, 420, 370, 0)
hideturtle()
tracer(False)
initialize()
draw()
done()
License
This project is licensed under the MIT License. See the LICENSE file for details.

