# Genetic Algorithms

## Pritam Prakash Shete

### Computer Division, BARC

### Centre for Excellence in Basic Sciences

------------------------------------------------------------------------

# Topics

-   Genetic Algorithms -- What?
-   Evolutionary inspiration and GA terminology
-   Core components of a GA
-   Population, chromosome and gene
-   Encoding methods
-   Fitness function
-   Selection and selection methods
-   Crossover and crossover methods
-   Mutation and mutation methods
-   GA workflow and worked example
-   Termination criteria
-   Advantages, disadvantages and applications

------------------------------------------------------------------------

# Genetic Algorithms -- What?

-   A Genetic Algorithm (GA) is a population-based optimization and
    search technique.
-   It is inspired by natural selection and biological evolution.
-   A GA evolves a population of candidate solutions over successive
    generations.
-   Better solutions receive a greater opportunity to contribute to
    future generations.
-   The objective is to find a high-quality solution within a practical
    computational budget.

**Search → Evaluate → Select → Recombine → Mutate → Improve**

------------------------------------------------------------------------

# Evolutionary Inspiration

Genetic Algorithms are inspired by the process of biological evolution.

-   Population
-   Selection
-   Reproduction
-   Mutation
-   New generation

The analogy is useful because GA repeatedly preserves useful
information, recombines it, introduces variation, and evaluates the
resulting solutions.

------------------------------------------------------------------------

# GA Terminology

### Population

Collection of candidate solutions.

### Chromosome

One complete encoded candidate solution.

### Gene

One component or parameter within a chromosome.

### Fitness

Numerical measure of solution quality.

**Population → Chromosomes → Genes**

------------------------------------------------------------------------

# Core Components of a GA

1.  **Population** -- Candidate solutions
2.  **Representation** -- Chromosome / genes
3.  **Fitness** -- Evaluate solution quality
4.  **Selection** -- Choose parents
5.  **Crossover** -- Combine parents
6.  **Mutation** -- Introduce variation
7.  **Replacement** -- Form next generation
8.  **Termination** -- Decide when to stop

------------------------------------------------------------------------

# Population in GA

**Population = set of candidate solutions**

Example:

``` text
10110
01101
11001
00111
10010
```

A population provides diversity:

-   Multiple solutions can be evaluated simultaneously.
-   Good solutions can be selected.
-   Different solutions can be recombined.
-   Mutation can explore new regions of the search space.

### Population size

-   **Small population:** Lower computational cost, but less diversity.
-   **Large population:** More diversity, but higher computational cost.
-   **Goal:** Balance exploration and computation.

------------------------------------------------------------------------

# Chromosome and Gene

**Chromosome = one complete candidate solution**

Example:

``` text
Chromosome = 1 0 1 1 0
```

Each position represents a gene:

``` text
Gene 1   Gene 2   Gene 3   Gene 4   Gene 5
   1        0        1        1        0
```

Genes are the components of a chromosome.

The meaning of a gene depends on the chosen representation.

**Gene → Chromosome → Population**

------------------------------------------------------------------------

# Encoding Methods in GA

Encoding defines how a candidate solution is represented as a
chromosome.

  Encoding      Example          Typical use
  ------------- ---------------- --------------------------------------
  Binary        `101101`         Boolean decisions, feature selection
  Integer       `[3, 7, 2, 9]`   Discrete parameters
  Real-valued   `[0.25, 1.73]`   Continuous optimization
  Permutation   `[3, 1, 4, 2]`   Routing, sequencing
  String        `[A, B, C, X]`   Symbolic solutions
  Tree          `(x × 2) + 5`    Program / expression evolution

**The problem determines the encoding.**

------------------------------------------------------------------------

# Fitness Function

The **fitness function** evaluates how good a candidate solution is.

``` text
Chromosome
     ↓
Fitness Function
     ↓
Fitness Score
```

Example:

\[ f(x)=x\^2 \]

  Chromosome      x   Fitness
  ------------ ---- ---------
  `00101`         5        25
  `01010`        10       100
  `11100`        28       784

For maximization, higher fitness is better.

For minimization problems such as distance or cost, the objective may
need to be transformed so that better solutions receive higher fitness.

------------------------------------------------------------------------

# Selection in GA

**Selection chooses chromosomes that will become parents.**

The basic principle is:

> Better fitness generally gives an individual a higher probability of
> being selected.

Example:

  Chromosome     Fitness
  ------------ ---------
  A                   25
  B                   80
  C                   45
  D                   95
  E                   60

The better solutions have greater selection probability, while enough
diversity should be maintained for exploration.

------------------------------------------------------------------------

# Selection Methods

### Roulette Wheel Selection

Probability is proportional to fitness.

\[ P_i = `\frac{F_i}{\sum_j F_j}`{=tex} \]

### Tournament Selection

Randomly choose a small group and select the best member.

### Rank Selection

Rank individuals by fitness and use rank rather than raw fitness.

### Elitism

Copy the best individuals directly into the next generation.

### Stochastic Universal Sampling

Fitness-proportionate selection using evenly spaced sampling points.

### Truncation Selection

Only the best fraction of the population is allowed to reproduce.

### Selection Pressure

-   Low pressure → more diversity and exploration.
-   High pressure → faster convergence but greater risk of premature
    convergence.

------------------------------------------------------------------------

# Crossover (Recombination)

Crossover combines genetic information from selected parents to create
offspring.

Example:

``` text
Parent 1 = 101 | 110
Parent 2 = 011 | 001

Child 1  = 101 | 001
Child 2  = 011 | 110
```

**Selection chooses WHO becomes a parent.**

**Crossover determines HOW parent information is combined.**

Crossover mainly recombines information already present in the
population.

------------------------------------------------------------------------

# Crossover Methods

### Single-Point Crossover

One crossover point is selected and the tails are exchanged.

``` text
Parent 1: 101 | 11010
Parent 2: 011 | 00111
```

### Two-Point Crossover

The segment between two crossover points is exchanged.

``` text
Parent 1: 11 | 0101 | 10
Parent 2: 00 | 1110 | 01
```

### Multi-Point Crossover

Multiple crossover points allow several segments to be exchanged.

### Uniform Crossover

Each gene is independently selected from either parent.

### Arithmetic Crossover

Used for real-valued chromosomes.

\[ C = `\alpha `{=tex}P_1 + (1-`\alpha`{=tex})P_2 \]

### BLX-α

Allows real-valued offspring to explore an extended range around the
parents.

### Permutation Crossover

For ordering problems, use operators such as:

-   Order Crossover (OX)
-   Partially Mapped Crossover (PMX)
-   Cycle Crossover (CX)

------------------------------------------------------------------------

# Mutation

**Mutation makes small random changes to genes.**

Example:

``` text
Before: 1 0 1 1 0 1
After:  1 0 0 1 0 1
            ↑
         mutation
```

Mutation helps:

-   Maintain population diversity.
-   Explore new regions of the search space.
-   Reduce the risk of premature convergence.
-   Introduce genetic configurations not previously present.

### Mutation rate

A relatively small mutation probability is commonly used, but the
appropriate value depends on the problem and encoding.

------------------------------------------------------------------------

# Mutation Methods

### Bit-Flip Mutation

Binary encoding:

``` text
0 → 1
1 → 0
```

### Random Resetting

Integer gene is replaced with another valid value.

``` text
[2, 5, 8, 3, 7]
       ↓
[2, 5, 4, 3, 7]
```

### Creep Mutation

Makes a small change to an integer.

``` text
7 → 8
```

### Gaussian Mutation

For real-valued chromosomes:

\[ x' = x + N(0,`\sigma`{=tex}) \]

### Polynomial Mutation

Controlled bounded perturbation for real-valued genes.

### Swap Mutation

Exchange two positions in a permutation.

``` text
[1, 2, 3, 4, 5]
      ↓
[1, 5, 3, 4, 2]
```

### Inversion Mutation

Reverse a selected section.

``` text
[1, 2, 3, 4, 5, 6]
        ↓
[1, 5, 4, 3, 2, 6]
```

### Insertion / Scramble

Move one element or randomly rearrange a selected segment.

------------------------------------------------------------------------

# Genetic Algorithm -- Overall Workflow

``` text
Initialize Population
        ↓
Evaluate Fitness
        ↓
Select Parents
        ↓
Crossover
        ↓
Mutation
        ↓
Form New Population
        ↓
Check Termination
        ↓
   Not terminated?
        ↓
Evaluate next generation
        ↺
```

The process repeats until a termination criterion is satisfied.

------------------------------------------------------------------------

# Worked Example -- Maximize f(x) = x²

Represent (x `\in [0,31]`{=tex}) using a 5-bit chromosome.

  Chromosome      x   Fitness (x\^2)
  ------------ ---- ----------------
  `00101`         5               25
  `01010`        10              100
  `11100`        28              784
  `00111`         7               49

The best solution in this population is:

``` text
Chromosome = 11100
x = 28
Fitness = 784
```

The GA would then use selection, crossover and mutation to search for
still better solutions.

------------------------------------------------------------------------

# Termination Criteria

Termination criteria define when the GA should stop.

### Maximum Generations

Stop after a fixed number of generations.

### Target Fitness

Stop when a desired fitness value is achieved.

### No Improvement

Stop after the best fitness has not improved for a specified number of
generations.

### Time Limit

Stop after a fixed computational time.

### Evaluation Budget

Stop after a fixed number of fitness evaluations.

In practice, multiple criteria can be combined.

------------------------------------------------------------------------

# Advantages of Genetic Algorithms

-   Works with large and complex search spaces.
-   Does not require gradient information.
-   Can work with black-box, discontinuous or non-differentiable
    objectives.
-   Supports binary, integer, real-valued and permutation
    representations.
-   Population-based search naturally supports exploration.
-   Can be extended to multi-objective optimization.
-   Fitness evaluations can often be parallelized.
-   Flexible and adaptable to many optimization problems.

------------------------------------------------------------------------

# Disadvantages of Genetic Algorithms

-   Can be computationally expensive.
-   Does not generally guarantee the global optimum.
-   May suffer from premature convergence.
-   Performance depends on population size and parameter choices.
-   Fitness-function design can be difficult.
-   Constraint handling may require penalties or repair mechanisms.
-   Results can vary between runs because of stochastic operators.
-   May require many fitness evaluations before convergence.

------------------------------------------------------------------------

# Applications of Genetic Algorithms

### Engineering Design

Optimize structures, shapes and system parameters.

### Scheduling

Allocate jobs, machines, resources and timetables.

### Routing

Find efficient routes and sequences.

### Machine Learning

Feature selection and hyperparameter / architecture search.

### Drug Discovery

Optimize candidate molecules against multiple objectives.

### Operations Research

Solve combinatorial and constrained optimization problems.

------------------------------------------------------------------------

# GA vs Traditional Optimization

## Traditional Gradient-Based Methods

-   Often use derivatives or gradients.
-   Typically follow one search trajectory.
-   Very effective when objectives are smooth and well behaved.
-   Can be less suitable for black-box or discontinuous objectives.

## Genetic Algorithms

-   Population-based search.
-   No gradient required.
-   Flexible representation.
-   Useful for black-box, discrete and combinatorial problems.
-   Uses stochastic exploration.

**The right optimizer depends on the structure and cost of the
problem.**

------------------------------------------------------------------------

# Example -- Molecular Optimization

A GA can treat molecular design as an optimization problem.

``` text
Candidate Molecules
        ↓
Fitness:
Docking / QED / ADMET
        ↓
Selection
        ↓
Crossover + Mutation
        ↓
New Candidate Molecules
        ↓
Fitness Evaluation
        ↺
```

The fitness function should reflect the actual design objective and
constraints.

Generated candidates should also remain valid under the chosen molecular
representation.

------------------------------------------------------------------------

# Summary

-   GA is a population-based evolutionary optimization method.
-   A population contains chromosomes.
-   Chromosomes contain genes.
-   Encoding defines how candidate solutions are represented.
-   Fitness measures solution quality.
-   Selection chooses parents.
-   Crossover recombines parent information.
-   Mutation introduces variation.
-   Termination criteria decide when to stop.
-   GA is flexible and powerful, but computational cost and parameter
    tuning must be considered.

**Explore → Evaluate → Select → Recombine → Mutate → Repeat**

------------------------------------------------------------------------

# Questions?

## Thank You

### Genetic Algorithms
