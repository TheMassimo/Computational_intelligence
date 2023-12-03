The goal of the lab 9 was to write a local-search algorithm (eg. an EA) able to solve the Problem instances 1, 2, 5, and 10 on a 1000-loci genomes, using a minimum number of fitness calls.

To try to solve this problem I tried to apply different types of approaches:
base_mode()
island_model_mix()
segregation_model_quantity()

First of all I tried with a basic approach (in the "base_mode" code) based on the code seen in class.
Naturally the results weren't the best so I proceeded like this:


I created additional selection operators (which I placed in a vector):

operator_functions = [elitism_selection, roulette_wheel_selection, tournament_selection]
(There is also "distance_selection" but this is only useful in base approch)


I created additional mutation operators (which I placed in a vector):

mutation_functions = [base_mutation, swap_mutation, scramble_mutation, insert_mutation, inversion_mutation, clone_mutation, mirror_mutation]


I created additional crossover operators (which I placed in a vector):

xover_functions = [one_cut_xover, two_cut_xover, three_cut_xover, uniform_xover]


In this way the number of possible techniques for mixing the gene is much greater.
Now in the basic approach I always use the roulette_wheel_selection operator with a combination of distance_selection.With distance I select the parents not based on fitness but on the levenshtein_distance's distance between the best genotype (based on fitness) and all the others, and then select the most distant one.
While for mutation and crossover I choose a random algorithm among all those present in the vectors mentioned above.

Furthermore in this approach I also use selected_extinction which allows me to extinguish a large part of the population and recreate it randomly if I am obtaining the same result for too many generations.
in this way I can solve (finding fitness 1):

Problem 1 with about less than 50k fitness calls
Problem 2 with about less than 300k fitness calls

In problem 5 i can find a value between 0.8 and 0.9 with about less than 1.5Mln fitness calls

In problem 10 I managed to reach a fitness between 0.3 and 0.4.
For this reason I implemented the island model by creating a number of islands equal to how many combinations exist between my selection, mutation and crossover functions.
Therefore each island uses a different strategy from the others
And in the end the best of each island migrate to the others
Also in this case the results obtained with problem 10 are similar.....

Finally I implemented the segregation model and in the end also in this case I took the best ones from each island to be able to use them as a new population for the basic approach but even this did not allow me to noticeably improve the fitness