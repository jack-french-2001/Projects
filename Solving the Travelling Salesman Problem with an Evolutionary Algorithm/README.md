### Evolutionary Algorithm to solve Travelling Salesman Problems

Throughout the provided .ipynb file, multiple experiments are carried out in observing the impact that varying the parameters of an Evolutionary Algorithm has on solving a TSP on a set of cities from Burma and a TSP on a set of Brazilian cities. 

#### Notebook Execution

This notebook must be ran using a working Jupyter Kernel in the Jupyter Notebook application. 

To ensure that the notebook runs without any issues, the file structure must be preserved. All csv files and the requirements.txt file must be in the same directory as the notebook. 

The following command (also provided in the notebook) must be ran to ensure that all required packages/libraries are installed:
```python
pip install -r requirements.txt
```
and the cells of the .ipynb file must be executed in the order that they appear in in the notebook to ensure that no errors are obtained.

The cells which perform the experiments have been commented out due to the length (in time) of each experiment. Instead, data concerning the previously ran experiments is read in and formatted from the corresponding csv files via the:
```python
format_results
```
function. The csv file names are self-explanatory and all follow the same structure: "country_name_parameter_of_interest_experiment.csv". For example, the "brazil_crossover_type_experiment.csv" refers to the data collected from the experiment on the impact that varying the crossover_type has on solving the TSP for the Brazil instance using the Evolutionary Algorithm.

If the user desires to re-perform the experiments, the cells containing the code should be uncommented out and a new csv file, containing one line which is the following: 

run_params;run_average_fitnesses;run_best_fitnesses;run_best_solution;run_best_fitness;run_execution_time;convergence_gen,

should be created, for each re-ran experiment.

#### Example of reperforming the experiment, reading in and formatting the results and plotting them: 

Say the user wants to re-run the population size experiment on the Burma instance. The following steps should be completed:

1. Create a new csv file with the following line as the first and only line in the file: 
run_params;run_average_fitnesses;run_best_fitnesses;run_best_solution;run_best_fitness;run_execution_time;convergence_gen

2. Run the following block of code:
```python
pop_sizes = range(20, 220, 20)
for pop_size in pop_sizes:
    for i in range(1, 11):
        random.seed(i)
        print(f"Population Size: {pop_size}, Run: {i}")
        TSP(burma_dist_mat, 
            burma_city_ids, 
            p = pop_size, 
            tournament_size = int(pop_size * 0.2), 
            nb_mutations=1,
            replacement_type="worse", 
            crossover_type="ordered", 
            maxit = 10000, 
            output_file="YOUR_NEW_CSV_FILE_NAME.csv"
            )
burma_mean_conv_pop_exp, burma_mean_best_fit_pop_exp, burma_mean_elapsed_pop_exp, burma_runs_pop_exp = format_results("YOUR_NEW_CSV_FILE_NAME.csv", "p")
plot_results(burma_mean_conv_pop_exp, 
             burma_mean_best_fit_pop_exp, 
             burma_mean_elapsed_pop_exp, 
             burma_runs_pop_exp, 
             "p", 
             xticks=range(20, 220, 20), 
             ticksize=9,
             label_size=10,
             param_name="Population Size", 
             variable_type="continuous", 
             country="Burma")
```

Of course, the user must make sure that all previously defined functions have been loaded in.