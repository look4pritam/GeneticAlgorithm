# Genetic Algorithms – Encoding Methods

## Introduction

In a **Genetic Algorithm (GA)**, **encoding** means deciding how a possible solution to a problem is represented as a **chromosome**.

The choice of encoding is important because it determines how **selection, crossover, and mutation** can be applied.

| Encoding | Example | Typical Use |
|---|---|---|
| **Binary** | `101101` | Boolean decisions, feature selection |
| **Integer** | `[3, 7, 2, 9]` | Discrete parameters |
| **Real-valued** | `[0.25, 1.73]` | Continuous optimization |
| **Permutation** | `[3, 1, 4, 2]` | Routing, sequencing |
| **String** | `[A, B, C, X]` | Symbolic solutions |
| **Tree** | `(x × 2) + 5` | Program / expression evolution |

---

# 1. Binary Encoding

**Example:**

```text
101101
```

In binary encoding, each chromosome is represented using only **0 and 1**.

Each position is called a **gene**.

```text
Chromosome:  1  0  1  1  0  1
             ↑  ↑  ↑  ↑  ↑  ↑
             Gene positions
```

Each bit can represent a decision such as:

- `1` → selected / yes / ON
- `0` → not selected / no / OFF

## Example: Feature Selection

Suppose we have six features:

```text
Feature:     F1 F2 F3 F4 F5 F6
Chromosome:   1  0  1  1  0  1
```

Interpretation:

```text
F1 → selected
F2 → not selected
F3 → selected
F4 → selected
F5 → not selected
F6 → selected
```

Therefore, the chromosome:

```text
101101
```

represents one possible feature subset.

The GA can evaluate the performance of a machine-learning model using this feature subset and then evolve better subsets.

## Other Applications

Binary encoding is useful for:

- Feature selection
- Boolean optimization
- Selecting equipment/components
- Yes/no decisions
- Knapsack problems
- Configuration problems

## Advantages

- Very simple representation
- Easy crossover and mutation
- Easy to implement
- Natural for binary decision problems

## Limitation

Binary encoding is not always natural for continuous values.

For example, representing:

```text
Temperature = 37.52°C
```

using a long binary chromosome is possible, but real-valued encoding is usually more convenient.

---

# 2. Integer Encoding

**Example:**

```text
[3, 7, 2, 9]
```

In integer encoding, genes contain **integer values** rather than only 0 and 1.

For example, suppose four machine settings are represented by:

```text
Machine 1 → 3
Machine 2 → 7
Machine 3 → 2
Machine 4 → 9
```

The chromosome is:

```text
[3, 7, 2, 9]
```

Each gene can have a defined integer range.

For example:

```text
Gene 1: 0–10
Gene 2: 0–20
Gene 3: 1–5
Gene 4: 0–100
```

A valid chromosome might therefore be:

```text
[7, 13, 4, 82]
```

## Example: Scheduling

Suppose four jobs must be assigned to five machines:

```text
Job:          J1 J2 J3 J4
Chromosome:    2  5  1  3
```

This means:

```text
J1 → Machine 2
J2 → Machine 5
J3 → Machine 1
J4 → Machine 3
```

The fitness function can evaluate the schedule based on factors such as:

- Total processing time
- Machine utilization
- Resource usage
- Waiting time
- Production cost

## Applications

Integer encoding is useful for:

- Scheduling
- Resource allocation
- Number of machines
- Discrete parameter optimization
- Assignment problems
- Configuration problems

## Advantages

The chromosome directly represents the actual problem.

For example:

```text
[2, 5, 1, 3]
```

is much easier to interpret than converting each number into a binary representation.

## Important Consideration

Crossover or mutation can sometimes produce values that violate the allowed constraints.

For example, if a gene must be between `1` and `5`, a mutation producing `8` would be invalid.

Therefore, **constraint handling** or repair mechanisms may be required.

---

# 3. Real-Valued Encoding

**Example:**

```text
[0.25, 1.73]
```

Real-valued encoding represents genes using **floating-point numbers**.

It is particularly useful when the parameters being optimized are continuous.

For example:

```text
x = 0.25
y = 1.73
```

The chromosome becomes:

```text
[0.25, 1.73]
```

## Example: Mathematical Optimization

Suppose we want to minimize:

\[
f(x,y)=(x-2)^2+(y-5)^2
\]

A chromosome could be:

```text
[1.72, 4.63]
```

Another chromosome could be:

```text
[2.15, 5.21]
```

The GA evaluates the fitness of each chromosome and gradually searches toward the optimum:

```text
[2.0, 5.0]
```

## Example: Machine Learning Hyperparameters

A chromosome can represent several continuous hyperparameters:

```text
Learning rate = 0.001
Dropout       = 0.25
Weight decay  = 0.0001
```

Chromosome:

```text
[0.001, 0.25, 0.0001]
```

The GA can search for the combination that produces the best model performance.

## Applications

Real-valued encoding is useful for:

- Engineering optimization
- Neural-network parameters
- Hyperparameter optimization
- Scientific computing
- Drug discovery
- Physical parameter optimization
- Function optimization

## Advantages

- Natural representation of continuous parameters
- No need to convert numbers into binary
- High numerical precision
- Often efficient for continuous optimization

---

# 4. Permutation Encoding

**Example:**

```text
[3, 1, 4, 2]
```

Permutation encoding is used when the **order of elements matters**.

Every element normally appears exactly once.

For example:

```text
[3, 1, 4, 2]
```

contains:

```text
1, 2, 3, 4
```

but in a particular order.

## Example: Travelling Salesman Problem

Suppose there are four cities:

```text
A = 1
B = 2
C = 3
D = 4
```

A chromosome:

```text
[3, 1, 4, 2]
```

represents the route:

```text
C → A → D → B
```

The GA tries to find the route with minimum total distance.

For example:

```text
Route 1: [3, 1, 4, 2]
Route 2: [1, 3, 2, 4]
Route 3: [2, 4, 1, 3]
```

Each route has a different fitness based on its total distance.

## Applications

Permutation encoding is especially useful for:

- Travelling Salesman Problem
- Vehicle routing
- Job sequencing
- Task scheduling
- Production scheduling
- Examination timetabling

## Special Issue with Crossover

Normal crossover can create invalid permutations.

For example:

```text
Parent 1: [1 2 3 4]
Parent 2: [4 3 2 1]
```

A careless crossover might produce:

```text
[1 2 2 1]
```

This is **not a valid permutation** because `1` and `2` occur twice while `3` and `4` are missing.

Therefore, permutation GAs use specialized crossover operators such as:

- **PMX** – Partially Mapped Crossover
- **OX** – Order Crossover
- **CX** – Cycle Crossover

Common mutation operators include:

- Swap mutation
- Insertion mutation
- Inversion mutation

---

# 5. String Encoding

**Example:**

```text
[A, B, C, X]
```

String encoding represents a solution as a sequence of **symbols or characters**.

Unlike binary encoding, the possible values can be arbitrary symbols.

For example:

```text
[A, B, C, X]
```

could represent a sequence of operations:

```text
A → B → C → X
```

The alphabet could be:

```text
{A, B, C, D, X}
```

and every gene can contain one of these symbols.

## Example: Symbolic Optimization

Suppose a system has four possible operations:

```text
A = Add
S = Subtract
M = Multiply
D = Divide
```

A chromosome:

```text
[A, M, S, D]
```

represents a sequence of operations.

## Example: Genetic Algorithm for Text

A chromosome could represent:

```text
HELLO
```

as:

```text
[H, E, L, L, O]
```

The GA can mutate individual characters and evaluate how close the generated string is to a target string.

## Applications

String encoding can be used for:

- Symbolic solutions
- Rule generation
- Text evolution
- Pattern generation
- Sequence optimization
- Grammar-based systems

## Important Distinction

**String encoding and permutation encoding are not the same.**

Permutation:

```text
[3, 1, 4, 2]
```

usually requires every element to appear exactly once.

String:

```text
[A, A, C, B]
```

can generally contain repeated symbols.

---

# 6. Tree Encoding

Tree encoding represents a solution as a **tree structure** instead of a simple linear chromosome.

It is particularly important in **Genetic Programming (GP)**.

For example:

```text
(x × 2) + 5
```

can be represented as:

```text
        +
       / \
      ×   5
     / \
    x   2
```

Here:

- `+` is an operator
- `×` is an operator
- `x` is a variable
- `2` and `5` are constants

The tree represents the mathematical expression.

## Example

Consider:

```text
(x + 3) × (y - 2)
```

Its tree can be represented as:

```text
             ×
           /   \
          +     -
         / \   / \
        x   3 y   2
```

## Genetic Programming

Tree encoding is the foundation of **Genetic Programming**, where the objective may be to automatically evolve a program or mathematical expression.

For example, given:

```text
x    y
1    3
2    5
3    7
```

the GA/GP may discover:

```text
y = 2x + 1
```

as the underlying relationship.

## Applications

Tree encoding is used for:

- Genetic programming
- Symbolic regression
- Mathematical expression generation
- Rule generation
- Decision trees
- Program evolution
- Automated algorithm generation

## Special Genetic Operators

### Subtree Crossover

One subtree from Parent 1 is exchanged with a subtree from Parent 2.

### Subtree Mutation

A selected subtree is replaced with a newly generated subtree.

For example:

Before mutation:

```text
      +
     / \
    x   5
```

After mutation:

```text
      +
     / \
    x   ×
       / \
      2   y
```

---

# Comparison of the Six Encoding Methods

| Encoding | Example | Main Idea | Typical Application |
|---|---|---|---|
| **Binary** | `101101` | 0/1 decisions | Feature selection |
| **Integer** | `[3,7,2,9]` | Discrete numbers | Scheduling |
| **Real-valued** | `[0.25,1.73]` | Continuous numbers | Parameter optimization |
| **Permutation** | `[3,1,4,2]` | Ordering | Routing |
| **String** | `[A,B,C,X]` | Symbols | Symbolic sequences |
| **Tree** | `(x×2)+5` | Hierarchical structure | Program evolution |

---

# How to Choose an Encoding

A simple way to select an encoding is to ask what the solution naturally looks like.

```text
Is it a YES/NO decision?
        ↓
   Binary encoding

Is it a discrete number?
        ↓
   Integer encoding

Is it a continuous number?
        ↓
   Real-valued encoding

Is it an ordering of things?
        ↓
   Permutation encoding

Is it a sequence of symbols?
        ↓
   String encoding

Is it an expression or program?
        ↓
   Tree encoding
```

---

# Encoding and Genetic Operators

The encoding is not just a way of storing the solution. It also determines which **genetic operators** are appropriate.

| Encoding | Typical Mutation | Typical Crossover |
|---|---|---|
| Binary | Bit-flip mutation | One-point / two-point / uniform crossover |
| Integer | Integer mutation | Integer-aware crossover |
| Real-valued | Gaussian / polynomial mutation | Arithmetic / blend crossover |
| Permutation | Swap / insertion / inversion | PMX / OX / CX |
| String | Symbol replacement | One-point / two-point crossover |
| Tree | Subtree mutation | Subtree crossover |

For example:

```text
Binary
   ↓
Bit-flip mutation

Integer
   ↓
Integer mutation

Real-valued
   ↓
Gaussian / polynomial mutation

Permutation
   ↓
Swap / inversion mutation

Tree
   ↓
Subtree mutation
```

Therefore, when designing a Genetic Algorithm, the usual process is:

```text
Problem
   ↓
Choose representation / encoding
   ↓
Define chromosome
   ↓
Define fitness function
   ↓
Choose selection method
   ↓
Choose suitable crossover
   ↓
Choose suitable mutation
   ↓
Run Genetic Algorithm
   ↓
Best solution
```

## Key Takeaway

The **best encoding is the one that represents the problem naturally while allowing valid solutions to be efficiently generated and evolved**.

- Use **Binary** for yes/no decisions.
- Use **Integer** for discrete numerical parameters.
- Use **Real-valued** for continuous numerical parameters.
- Use **Permutation** when ordering is important.
- Use **String** when solutions consist of symbols or characters.
- Use **Tree** when solutions are expressions, rules, or programs.
