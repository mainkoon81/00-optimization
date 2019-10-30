# 00-optimization

## Gradient-Free Optimization
### 1.EA: What is an Evolutionary Algorithm? 
Given a population of individuals, the environmental pressure causes natural selection(survival of the fittest) which causes a rise in the fitness of the population.
 - Given a `quality function` to be maximized, we can randomly create a set of candidate solutions and use the `quality function` as an abstract fitness measure. 
 - Based on this fitness, some of the better candidate solutions are chosen to seed the next generation by applying `recombination / mutation` to them.
   - `recombination` is a **variational operator** applied to multiple selected candidates(parents), then results some new candidates(children).
   - `mutation` is a **variational operator** applied to one candidate, then results in one new candidate. 
   - Executing `recombination` and `mutation` leads to a set of **new offsprings** that compete with the old ones for a place in the next generation. This process will be iterated until a candidate with sufficient quality(solution) is found or a previously set computational limit is reached. 
 - There are two fundamental forces forming the basis of evolutionary systems. 
   - **variational operators** create the diversity. 
   - **selection operator** acts as a force, pushing quality.
 - It helps the evolution optimise/approximise by approaching optimal values.   
 <img src="https://user-images.githubusercontent.com/31917400/67786791-5ff55580-fa67-11e9-813f-a2c214094b3c.jpg" />

Typically the candidate solutions are represented by different encoding.
 - **strings** over a finite alphabet in `Genetic Algorithm`
 - **trees** in `Genetic Programming`
 - **real-valued vectors** in `Evolution Strategy`
 - **finite state machine** in `Evolutionary Programming`
 
### [variation and selection] 
**Variational Operators** working on the candidate solutions must match the given representation. For example:
 - for solving a **Boolean satisfiabilty problem**(boolean formula with `0/1`, `and, or, not`... : `satisfied`/`unsatisfied`), the straighforward choice would be to use `bit-strings of length n` (where n is the number of logical variables) => so go with `Genetic Algorithm`. The `recombination operator` works on `strings`! 
 - for evolving a computer program that can play checkers, `trees`(as the synthetic expression forming the programs) are well suited => so go with `Genetic Programming`. The `recombination operator` works on `trees`!

**Selection Operator** takes only the `fitness information` into account, hence it works independently from the actual representation.   
 
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
         - Select 
End
```
Each of below components must be specified to define a particular EA. 
 - 1.representation(definition of individuals)
 - 2.evaluation(fitness) function
 - 3.population
 - 4.PARENT selection mechanism
 - 5.variation operator
   - recombination
   - mutation
 - 6.SURVIVOR selection mechanism

1. REPRESENTATION





























