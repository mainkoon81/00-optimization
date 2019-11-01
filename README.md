# Optimization
<img src="https://user-images.githubusercontent.com/31917400/67963471-91505b80-fbf6-11e9-8718-e9462c829368.jpg" />

Gradient-based optimizers are efficient at finding local minima for high-dimensional, non-linearly-constrained, convex problems; however, most gradient-based optimizers have problems dealing with noisy and discontinuous functions, and they are not designed to handle multi-modal problems or discrete and mixed discrete-continuous design variables. 

## [Gradient-Free Optimization 01. EA]
### What is an Evolutionary Algorithm? 
Given a population of individuals, the environmental pressure(or our need?) causes natural selection(survival of the fittest) which causes a rise in the fitness of the population. It helps the evolution by approaching optimal values.   
 - There are two fundamental forces forming the basis of evolutionary systems. 
   - **variational operators** create the diversity via crossover & mutation 
   - **selection operator** acts as a force, pushing quality.
<img src="https://user-images.githubusercontent.com/31917400/67961213-4ed94f80-fbf3-11e9-86c3-f99fcf9c2218.jpg" />

### Which EA-algorithm?
Typically the candidate solutions are represented by **`different encoding`**.
 - **strings** over a finite alphabet in `Genetic Algorithm`
 - **trees** in `Genetic Programming`
 - **real-valued vectors** in `Evolution Strategy`
 - **finite state machine** in `Evolutionary Programming`

a) **Variational Operators** working on the candidate solutions must match the given representation. For example:
 - for solving a **Boolean satisfiabilty problem**(boolean formula with `0/1`, `and, or, not`... : `satisfied`/`unsatisfied`), the straighforward choice would be to use **bit-strings of length n** (where n is the number of logical variables) => so go with `Genetic Algorithm`. The **recombination operator** works on `strings`! 
 - for evolving a computer program that can play checkers, `trees`(as the synthetic expression forming the programs) are well suited => so go with `Genetic Programming`. The **recombination operator** works on `trees`!

b) **Selection Operator** takes only the `fitness information` into account, hence it works independently from the actual representation....so any EA goes.
 - PARENT Selection mechanism
 - SURVIVOR Selection mechanism
 
### [EA-Components]
```
Begin
    -Initialize POPULATION with random cadidate solutions;
    -Evaluate each candidate(using fitness func);
    
    -Repeat until (TERMINATION CONDITION) Do:
         - Select PARENTS
         - Recombine a pair of PARENTS
         - Mutate the resulting CHILD
         - Evaluate new candidates(using fitness func)
         - Select SURVIVORS
End
```
Each of below components must be specified to define a particular EA. 
 - 1.representation(definition of individuals)
 - 2.evaluation(fitness) function
 - 3.POPULATION
 - 4.PARENT(mating) selection mechanism
 - 5.variation operator
   - recombination
   - mutation
 - 6.SURVIVOR(replacement) selection mechanism

__1. REPRESENTATION:__
Define individuals by linking the **"real world"** to the `"EA world"`; Set up a bridge b/w the **"original problem context"** and the `"problem solving space"` where evolution will take place. The representation step specifies a mapping from the `phenotypes` onto a set of `genotypes`. The term "representation" is synonymous with **encoding**. 
 - **Genotypes**: The individuals within the EA world (mapping: **encoding**)...we focus on "data structure"!!!!
 - **Phenotypes**: Objects forming possible solution within the real world (inverse-mapping: **decoding**)
 - **one genotype implies only one phenotype** while one phenotype does not necessarily imply only one genotype presents. 
 - For example, given an optimazation problem on integers;
   - **Phenotype**: "18"
   - **Genotype**: "10010" (encoding with a binary code)
     - Note that the whole evolutionary search takes place in the genotype space.
   - A solution (good phenotype) is obtained by decoding the best genotype after termination. 

__2. Fitness Function:__
Define the basis for selection. Define what improvement means, representing the task to solve. This fitness function is a problem itself. It can be a mathematical equation that calculates the output based on the inputs. It might be a computer program or even a simulator. There is only one condition for a fitness function to follow, as the name suggests, it should be a function and a function always retains a unique value for every unique combination of inputs or parameters(features).
 - It assigns a quality measure to "genotypes"...????
 - It is typically composed from a quality measure in the "phenotype space"(inverse-representation).
 - It is typically associated with min/max.

__3. Population:__
### Unlike traditional optimization techniques, EA depend on **random sampling**. EA has a `population of candidate solutions`, unlike classical methods which always try to maintain a single best solution.

As a multi-set of genotypes, **Hold multiple possible solutions**;....it sounds DIVERSITY ? In population, we have set of individuals and each individual in the population is a possible solution for the given problem. We call these individuals as chromosomes. Each chromosome is made up of genes. What are genes ? These are the parameters(features) of the given optimization problem. Genes correspond to the values for each variable of the problem.
<img src="https://user-images.githubusercontent.com/31917400/67957182-20587600-fbed-11e9-886a-4c64fa71c48b.jpg" />

 - It forms a **unit of evolution**.
   - Individuals are just a static object, but the population is changing and adapting... 
   - In some case, if a population has an additional spatial structure(distance, neighbor, etc.), the additional structure needs to be defined.  
   - `selection operators` work at **population level** while `variational operators` work at individual level.
   - DIVERSITY of a population is a measure of "how many different solutions present?" Do you want to use entropy equation?

__4. PARENT Selection Mechanism:__
Distinguish **individuals** based on their quality, to allow the better individuals to become parents; Together with the **survivor selection** mechanism, **parent selection**(typically probabilistic: the fittest individuals have a higher chance) is responsible for pushing quality improvements. The basic part of the selection process is to stochastically(Roulette Wheel) select from one generation to create the basis of the next generation. 
<img src="https://user-images.githubusercontent.com/31917400/67944833-58ec5580-fbd5-11e9-843f-d7271a925199.jpg" /> These individuals consist of 10 bit chromosomes are being used to optimise a simple mathematical function (we can assume from this example we are trying to find the maximum). If the input range for `x` is between 0 and 10, then we can map the binary chromosomes to base 10 values and then to an input value between 0 and 10. The fitness values are then taken as `f(x)` where individual No. 3 is the fittest and No. 2 is the weakest from the table. Summing these fitness values, we can apportion a percentage total of fitness. This gives the strongest individual a value of 38% and the weakest 5%. These percentage fitness values can then be used to configure the roulette wheel. The number of times the roulette wheel is spun is equal to size of the population. As can be seen from the way the wheel is now divided, each time the wheel stops this gives the fitter individuals the greatest chance of being selected for the next generation and subsequent mating pool.

__5. Variation Operators:__
Creat new **individuals** from old ones; Generate new candidate solutions. The `recombination`(crossover) is applied to **multiple** selected candidates(parents), then results some new candidates(children). The `mutation` is applied to a **single** candidate, then results in one new candidate. Executing `recombination` and `mutation` leads to a set of **new offsprings** that compete with the old ones for a place in the next generation. This process will be iterated until a candidate with sufficient quality(solution) is found or a previously set computational limit is reached. 
 - a) **Recombination Operator**(crossover): It is applied to `2 genotypes`, merging information from the two into one new genotype(prospective child).
   - It is always stochastic 
     - choice of what parts of each parent.  
     - the way they are combined.
       - one point crossover: select a random crossover point and the tails of both the chromosomes are swapped to produce a new off-springs.
       - multi point crossover: select multiple random crossover points and the multiple places of both the chromosomes are swapped to produce a new off-springs.
     <img src="https://user-images.githubusercontent.com/31917400/67945540-0dd34200-fbd7-11e9-8b86-acec74649d28.jpg" />
     
 - b) **Mutation Operator**: It is applied to `1 genotype` and delivers a modified mutant: a **CHILD**. This may be defined as a random tweak in the chromosome, which promotes the idea of **diversity** in the population. The off-springs thus produced are again validated using the fitness function, and if considered fit then will replace the less fit chromosomes from the population.
   - It is always stochastic 
     - output child relies on using a pseudo random drawing to generate values from some given probability distribution.
     <img src="https://user-images.githubusercontent.com/31917400/67945791-af5a9380-fbd7-11e9-8a1a-9682548ef6e4.jpg" />

__6. Survivor Selection Mechanism:__
Distinguish **individual** based on their quality. If parent selection is stochastic, **survivor selection is deterministic**.  

### [Case study]: Genetic Algorithm
It's a popular strategy to optimize **non-linear systems** with a large number of variables. 
 - Parameters: variables in the system of interest...`phenotype`
 - `Gene`: encoded form of a parameter being optimized...`genotype` 
 - `Chromosome`: the complete set of genes which uniquely describe an individual
 - Locus: the position of a piece of data within a chromosome
 
### Set-up 
<img src="https://user-images.githubusercontent.com/31917400/68034529-b954c300-fcb9-11e9-994d-3008cd7d30b9.jpg" />

Genetic algorithms are radically different from the gradient based methods. Instead of "looking at one point at a time and stepping to a new point for each iteration", **`a whole population of solutions is iterated towards the optimum at the same time`**. Using a population, it explores multiple “buckets” (local minima) simultaneously, **increasing the likelihood of finding the global optimum**. 

### Steps (Single Objective Optimization)
1. Initialize a Population:
 - Each member of the population represents a design point `x` and has a value of the objective (fitness), and information about its constraint violations associated with it.
 
2. Determine Mating Pool by `crossover`:
 - **Each population member** is paired for reproduction by using one of the following methods
   - Random selection
   - Based on fitness, make the better members to reproduce more often than the others (parent selection then crossover)

3. Generate children by `mutation`:
 - Add some randomness in the offspring’s variables to maintain **diversity**.
 - Compute the fitness.

4. Tournament:
 - There are different schemes that can be used in this step. One method involves replacing the worst parent from each “family” with the best offspring.

5. Identify the Best Member:
 - Convergence is difficult to determine because the best solution so far may be maintained for many generations. As a rule of thumb, if the best solution among the current population hasn’t changed (much) for about 10 generations, it can be assumed as the optimum for the problem.

6. Return to Step 2.:
 - Note that since GAs are probabilistic methods (due to the random initial population and mutation), it is crucial to run the problem multiple times when studying its characteristics.

### Steps (Multi-Objective Optimization)
> What if we want to investigate the trade-off between two (or more) conflicting objectives? 

In the design of a supersonic aircraft, for example, we might want to simultaneously minimize `aerodynamic drag` and `sonic boom` and we do not know **what the trade-off is**. How much would the drag increase for a given reduction in sonic boom? In this situation there is no one “best design”. **`There is a set (a population) of designs`** that are the best possible for that combination of the two objectives. In other words, for these optimal solutions, the only way to improve one objective is to worsen the other. We have to evaluate a whole population, so we can use this to our advantage. This is much better than using composite weighted functions in conjunction with gradient-based methods since there is no need to solve the problem for various weights. 

The concept of `dominance` is the key to the use of GA’s in multi-objective optimization. As an example, assume we have a population of 3 members, `A`, `B` and `C`, and that we want to minimize two objective functions, `f1` and `f2`. Comparing members `A` and `B`, we can see that `A` has a higher (worse) `f1` than `B`, but has a lower (better) `f2`. Hence we cannot determine whether `A` is better than `B` or vice versa. Comparing `A` and `C`, once again we are unable to say that one is better than the other. 

On the other hand, `B` is clearly a fitter member than `C` since both of `B`’s objectives are lower. We say that `B` **dominates** `C`. <img src="https://user-images.githubusercontent.com/31917400/68038058-f96b7400-fcc0-11e9-9ed4-070e67c59d05.jpg" />
   






















































