# BioDeepSpace


### The Most Basic Object is a Population

* We only care about population objects not individuals.
* We allways have collection of small populations.
* Populations are only data. JSON objects with out any methods.
* Populations can have arbitrary metadata depending on the application. We propose to start with:
    * id
    * age
    * best-solution
    * best-fitness
    * target-fitness
* The actual population is a list of JSON objects. They are normally a list of individuals or even other populations.

For instance a population in python could be:

``` python
{
    'id':'8sfgsdfg098qt7981739487',
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
     'algorithm':{'name':'GA', 'params':{'mutation_prob':.05}}
}
```

### We have several serverless functions that operate on Population objects
