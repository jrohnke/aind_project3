# Implement a Planning Search

## Synopsis

In this project I created a planning search agent to solve an air cargo logistics problem defined in classical PDDL (Planning Domain Definition Language). I implemented and compared different non-heuristic based progression search algorithms and two domain-independent heuristics to be used with the A* search algorithm.

## Problem description

The three problems that needed to be solved are shown below. They are defined in PDDL and are increasingly more complicated due to an increased number of variables (planes, cargo, and airports) and goal state requirements.

- Problem 1 initial state and goal:
```
Init(At(C1, SFO) ∧ At(C2, JFK) 
	∧ At(P1, SFO) ∧ At(P2, JFK) 
	∧ Cargo(C1) ∧ Cargo(C2) 
	∧ Plane(P1) ∧ Plane(P2)
	∧ Airport(JFK) ∧ Airport(SFO))
Goal(At(C1, JFK) ∧ At(C2, SFO))
```
- Problem 2 initial state and goal:
```
Init(At(C1, SFO) ∧ At(C2, JFK) ∧ At(C3, ATL) 
	∧ At(P1, SFO) ∧ At(P2, JFK) ∧ At(P3, ATL) 
	∧ Cargo(C1) ∧ Cargo(C2) ∧ Cargo(C3)
	∧ Plane(P1) ∧ Plane(P2) ∧ Plane(P3)
	∧ Airport(JFK) ∧ Airport(SFO) ∧ Airport(ATL))
Goal(At(C1, JFK) ∧ At(C2, SFO) ∧ At(C3, SFO))
```
- Problem 3 initial state and goal:
```
Init(At(C1, SFO) ∧ At(C2, JFK) ∧ At(C3, ATL) ∧ At(C4, ORD) 
	∧ At(P1, SFO) ∧ At(P2, JFK) 
	∧ Cargo(C1) ∧ Cargo(C2) ∧ Cargo(C3) ∧ Cargo(C4)
	∧ Plane(P1) ∧ Plane(P2)
	∧ Airport(JFK) ∧ Airport(SFO) ∧ Airport(ATL) ∧ Airport(ORD))
Goal(At(C1, JFK) ∧ At(C3, JFK) ∧ At(C2, SFO) ∧ At(C4, SFO))
```

## Solutions

The optimal solutions found by at least one of the search algorithms:

- Problem 1 solution in 6 steps:
```
Load(C1, P1, SFO)
Load(C2, P2, JFK)
Fly(P1, SFO, JFK)
Fly(P2, JFK, SFO)
Unload(C1, P1, JFK)
Unload(C2, P2, SFO)
```
- Problem 2 solution in 9 steps:
```
Load(C1, P1, SFO)
Fly(P1, SFO, JFK)
Load(C2, P2, JFK)
Fly(P2, JFK, SFO)
Load(C3, P3, ATL)
Fly(P3, ATL, SFO)
Unload(C1, P1, JFK)
Unload(C2, P2, SFO)
Unload(C3, P3, SFO)
```
- Problem 3 solution in 12 steps:
```
Load(C2, P2, JFK)
Fly(P2, JFK, ORD)
Load(C4, P2, ORD)
Fly(P2, ORD, SFO)
Load(C1, P1, SFO)
Fly(P1, SFO, ATL)
Load(C3, P1, ATL)
Fly(P1, ATL, JFK)
Unload(C1, P1, JFK)
Unload(C2, P2, SFO)
Unload(C3, P1, JFK)
Unload(C4, P2, SFO)
```

### Non-heuristic search
Tables 1-3 show the comparison between the following different non-heuristic search methods: breadth-first, depth-first, and uniform cost. The methods greedy best-first graph search with h1 and A* search with h1 also belong in this category as both of them are using the constant h1 heuristic, which, since it is constant, is not a true heuristic.

<img src="images/p1_table.png" width="500" style="background-color:white" title="Table 1: Problem 1">
<img src="images/p2_table.png" width="500" style="background-color:white" title="Table 2: Problem 2">
<img src="images/p3_table.png" width="500" style="background-color:white" title="Table 3: Problem 3">
<!--![Table 1: Problem 1](images/p1_table.png)-->
<!--![Table 2: Problem 2](images/p2_table.png)-->
<!--![Table 3: Problem 3](images/p3_table.png)-->

The tables are colour coded with blue showing the best, white the intermediate and red the worst search method for the respective metric (#nodes expanded, #goal tests, #new nodes, plan length, and time). The optimality metric shows if the solution is optimal in length, that is, it consists of the minimum possible number of steps required to go from the initial to the goal state.

Figures 1-3 show the performance of the search methods relative to each other.

![Figure 1: Problem 1](images/p1_bars1.png)
![Figure 2: Problem 2](images/p2_bars1.png)
![Figure 3: Problem 3](images/p3_bars1.png)