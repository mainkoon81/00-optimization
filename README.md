# 00-optimization

### What is an Evolutionary Algorithm? 
Given a population of individuals, the environmental pressure causes natural selection(survival of the fittest) which causes a rise in the fitness of the population.
 - Given a `quality function` to be maximized, we can randomly create a set of candidate solutions and use the `quality function` as an abstract fitness measure. 
 - Based on this fitness, some of the better candidate solutions are chosen to seed the next generation by applying `recombination / mutation` to them.
   - `recombination` is an **operator** applied to multiple selected candidates(parents), then results some new candidates(children).
   - `mutation` is an **operator** applied to one candidate, then results in one new candidate. 
   - Executing `recombination` and `mutation` leads to a set of **new offsprings** that compete with the old ones for a place in the next generation. This process will be iterated until a candidate with sufficient quality(solution) is found or a previously set computational limit is reached. 
   - There are two fundamental forces forming the basis of evolutionary systems. 
     - **variational operators** create the diversity. 
       - `recombination`:
       - `mutation`:
     - **selection** acts as a force, pushing quality.  



































