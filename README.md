# BioDeepSpace

### The Most Basic Object is a Population
* We only care about population objects not individuals.
* We allways have a collection (or population) of small populations.
* Populations are only data. JSON objects with out any methods.
* Populations have metadata depending on the application. We propose to start with:
    * id
    * age
    * best-solution
    * best-fitness
    * target-fitness
    * state

* The actual population is a list of JSON objects. They are normally a list of individuals or even other populations.

For instance a population in python could be:
``` python
{
    'id':'8sfgsdfg098qt7981739487',
    'experiment_id':'8sfgsdfg098qt7981739487',
    'age':2,
    'pop':[[0,1,1,0,1,1,1,0],
           [1,1,1,0,1,1,1,0],
           [1,1,1,0,1,1,1,0],
           [1,1,1,0,1,1,1,0],
           [1,1,1,1,1,1,1,0],
           [1,0,1,1,1,1,1,1]]
     'best-solution':[1,0,1,1,1,1,1,1],
     'best-fitness': 7,
     'target-fitness': 8,
     'diversity':4,
     'algorithm':{'name':'GA', 'params':{'mutation_prob':.05}},
     'owner':'23321'
}
```
### We have several serverless functions that operate on population objects
These functions are not application dependant:
* get_best( *population_list* )
* reproduce(*population_list*, *kwparams*)
* exchange(*population_list*, *kwparams*)
* kill_old(*population_list*, *kwparams*)

### Search is done by pushing populations algorithms:
These functions can be developed by a 3rd party
* eval_functions(population)
* ga(population, iterations,  *kwparams*)
* pso(population, iterations,  *kwparams*)
* gwo(population, iterations,  *kwparams*)

Each function is Stateless and it could be seen as a short lived process, that runs a GA algorithm for only a few generations with a small population.
There are two variants:
* Function evaluation is done inside the algorithm. In this case an algorithm could run for several generations.
* Function evaluation is expensive or must be done by a 3rd party. In this case the function is limited to only one generation (selection, crossover, mutation).

### Function parameters can include the algorithm environment set-up
An example environment, from an [EvoWorker](https://github.com/mariosky/EvoWorker/blob/master/docker_exp.py):

``` python
env = {'FUNCTION': function, 'DIM': dim, 'INSTANCE': instance,  'FEmax': 500000,
       'EXPERIMENT_ID': EXPERIMENT_ID,
       'NGEN': es_conf[dim]['NGEN'], 'LOGGING': True}
```

### Experiment setup could depend on problem size
In this case by the dimension of a benchmark function

``` python
es_conf = {
    2: {'POP_SIZE':100, 'AGE':50, 'COLLECTION_SIZE': 20,  'PSO':1,  'GA':1 },
    3: {'POP_SIZE':200, 'AGE':50, 'COLLECTION_SIZE': 500, 'PSO':2, 'GA':2 },
    5: {'POP_SIZE':500, 'AGE':50, 'COLLECTION_SIZE': 800, 'PSO':3, 'GA':3 },
    10:{'POP_SIZE':800, 'AGE':50, 'COLLECTION_SIZE': 100, 'PSO':4, 'GA':4 }
}
```
### Other remarks
* Experiment setup could also be optimized
* The platform is created by a docker-file
* You can bring your own optimizer
* Ready for distributed COCO´s BBOB noiseless testbed benchmark
* Compatible with EvoSpace
* You can either pull or push asynchronously
