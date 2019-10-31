# Optimization

## [Gradient-Free Optimization 01. EA]
### What is an Evolutionary Algorithm? 
Given a population of individuals, the environmental pressure(or our need?) causes natural selection(survival of the fittest) which causes a rise in the fitness of the population. It helps the evolution by approaching optimal values.   
 - There are two fundamental forces forming the basis of evolutionary systems. 
   - **variational operators** create the diversity via crossover & mutation 
   - **selection operator** acts as a force, pushing quality.
<img src="https://user-images.githubusercontent.com/31917400/67786791-5ff55580-fa67-11e9-813f-a2c214094b3c.jpg" />

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
Define the basis for selection. Define what improvement means, representing the task to solve. This fitness function is a problem itself. It can be a mathematical equation that calculates the output based on the inputs. It might be a computer program or even a simulator. There is only one condition for a fitness function to follow, as the name suggests, it should be a function and a function always retains a unique value for every unique combination of inputs or parameters.
 - It assigns a quality measure to "genotypes"...????
 - It is typically composed from a quality measure in the "phenotype space"(inverse-representation).
 - It is typically associated with min/max.

__3. Population:__
### Unlike traditional optimization techniques, EA depend on **random sampling**. EA has a `population of candidate solutions`, unlike classical methods which always try to maintain a single best solution.

As a multi-set of genotypes, **Hold multiple possible solutions**;....it sounds DIVERSITY ? In population, we have set of individuals and each individual in the population is a possible solution for the given problem. We call these individuals as chromosomes. Each chromosome is made up of genes. What are genes ? These are the parameters of the given optimization problem. Genes correspond to the values for each variable of the problem.
<img src="https://user-images.githubusercontent.com/31917400/67883939-de6ff700-fb3c-11e9-8e53-d4b0718e11e9.jpg" />

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














