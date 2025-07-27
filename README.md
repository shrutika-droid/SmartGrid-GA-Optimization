# Smart Grid Energy Allocation Optimization using Genetic Algorithms



## Overview



This repository presents a solution for optimizing energy allocation within a smart grid environment using a Genetic Algorithm (GA). The project simulates a grid with multiple energy sources (Solar, Wind, Hydro) and various consumer nodes over a 24-hour cycle, aiming to minimize total energy cost while efficiently meeting demand and managing supply constraints. A key aspect of this work is the implementation and analysis of parallel processing to accelerate the GA's performance, alongside a comparison with a simpler greedy baseline method.



## Problem Statement



The challenge is to optimally allocate energy from diverse sources to various demand nodes in a smart grid, considering:

* Fluctuating energy demand from different node types (residential, hospital, industrial, etc.).

* Variable energy generation capacity from renewable sources (solar, wind) and more stable sources (hydro).

* Associated energy generation costs for each source.

* Transmission line losses between sources and nodes.

* Penalties for unmet demand, over-allocation, and exceeding source capacities.



The objective is to find an energy allocation strategy that minimizes the total cost, which includes generation costs, transmission losses, and penalties.



## Methodology



### 1. Data Simulation

The environment is simulated with:

* *50 Consumer Nodes*: With varied demand profiles (urban/rural residential, hospital, school, industry, mall, agriculture).

* *3 Energy Sources*: Solar, Wind, and Hydro, each with dynamic capacities and specific generation costs.

* *24-Hour Cycle*: Simulating demand and supply fluctuations throughout a day.

* *Random Outages & Demand Spikes*: To introduce real-world unpredictability.



### 2. Genetic Algorithm (GA) Optimization

A Genetic Algorithm is employed to search for the optimal energy allocation.

* *Chromosome Encoding*: Each chromosome represents a complete energy allocation plan, detailed as a 3D matrix (Source x Node x Hour), where each gene specifies the energy flow from a source to a node at a given hour.

* *Fitness Function*: Evaluates the 'cost' of an allocation. It penalizes unmet demand, over-allocation, capacity violations, and includes energy generation cost and transmission losses. The GA aims to maximize (negative of) this cost, effectively minimizing the total cost.

* *Genetic Operators*: Standard GA operators like tournament selection, single-point crossover, and mutation are used to evolve the population over generations.



### 3. Parallelization Strategy

The most computationally intensive part of the GA, the *fitness evaluation* of each individual in the population, is parallelized.

* *Tool*: Python's multiprocessing module, integrated through the pygad library's parallel_processing parameter.

* *Mechanism*: The fitness calculations for a generation's population are distributed across all available CPU cores (multiprocessing.cpu_count() processes), significantly reducing the wall-clock time required per generation. This is an "embarrassingly parallel" problem ideal for multi-core CPUs.



### 4. Greedy Baseline

A simple greedy algorithm serves as a baseline for comparison. It attempts to meet demand by prioritizing the cheapest available energy source at each given hour and for each node, considering line losses. This method is fast but typically suboptimal.



## Setup and Installation



To run this project, you'll need Python 3.x and the following libraries. You can install them using pip:



```bash

pip install numpy matplotlib seaborn pygad
