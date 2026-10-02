# Local Search Lab: Traveling Salesman Problem

In this lab, I implemented and tested several local-search algorithms for the Traveling Salesman Problem (TSP). The goal was to find short routes through a set of U.S. state capitals by comparing different search strategies that improve a route without checking every possible route.

## Tools and Concepts Used

- Python and a Jupyter Notebook  
- City names and coordinate pairs representing U.S. state capitals  
- Euclidean distance to calculate the distance between cities  
- A closed tour, including the return trip from the final city back to the starting city  
- Route utility, represented as the negative total distance so that shorter paths have higher utility  
- Segment reversal to create neighboring routes  
- Randomized starting paths and random successor generation  

The main algorithms used were:

- Hill Climbing  
- Local Beam Search  
- Simulated Annealing  
- Late-Acceptance Hill Climbing (LAHC)  

## What I Did

I created a `TravelingSalesmanProblem` representation where a solution is a route that visits every city once and then returns to the starting city. I calculated the total route distance using Euclidean distance between city coordinates. Because the algorithms select solutions with the highest utility, I used the negative distance as the utility value. This made shorter routes produce better utility scores.

I implemented successor functions that create new possible routes by reversing a section of the current path. The `successors()` function generates all valid segment-reversal neighbors, while `get_successor()` selects one random neighbor. I made sure these functions created new problem objects instead of changing the current route directly.

I then implemented and tested four local-search solvers:

- **Hill Climbing:** Repeatedly selected the best neighboring route and stopped when no strictly better route was available or when it reached the epoch limit. This improved the route locally, but it could stop at a local optimum instead of the best possible route.
- **Local Beam Search:** Started with several randomized routes, generated successors from all current routes, and kept only the best routes based on the beam width. This allowed the search to explore several possible route areas at the same time.
- **Simulated Annealing:** Always accepted improvements but sometimes accepted worse routes based on temperature and probability. I used the schedule `initial_temperature * alpha ** time`, so worse moves became less likely as the temperature decreased.
- **Late-Acceptance Hill Climbing:** Selected the best neighbor and compared it with both the current solution and an earlier value stored in a fixed history array. This allowed some non-improving moves and helped the algorithm avoid getting stuck too quickly.

## What I Learned

This lab showed that local-search algorithms can find useful approximate solutions to difficult optimization problems, even when finding the exact best solution would take too much time. Each algorithm uses a different approach to avoid or reduce the problem of getting stuck in poor local solutions.

I also learned that it is important to keep the direction of the evaluation consistent. The assignment searched for the shortest route, but the solvers chose the highest utility, so I needed to negate the route distance. Other important details included counting the final return edge to the starting city and safely handling worse moves in simulated annealing using the temperature-based acceptance probability.

The results from these algorithms are approximate routes, not guaranteed optimal TSP solutions.
