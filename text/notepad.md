
Creating a very simple python action

After installing using the [Quick Start]https://github.com/apache/incubator-openwhisk#quick-start) go to your  whisk vm:


```
vagrant ssh
```

Create a python script with a main() function taking and returning a *dict*   
```
vagrant@vagrant-ubuntu-trusty-64:~$ nano hello.py
```

``` python
def main(args):
    name = args.get("name", "stranger")
    greeting = "Hello " + name + "!"
    print(greeting)
    return {"greeting": greeting}
```

Test the action
```
vagrant@vagrant-ubuntu-trusty-64:~$ wsk action create helloPython hello.py

vagrant@vagrant-ubuntu-trusty-64:~$ wsk action invoke --result helloPython --param name World
{
    "greeting": "Hello World!"
}
```

Get the URL of the action
```
vagrant@vagrant-ubuntu-trusty-64:~$ wsk action get helloPython --url
ok: got action helloPython
https://192.168.33.13/api/v1/namespaces/guest/actions/helloPython
```

Get the basic auth
```
vagrant@vagrant-ubuntu-trusty-64:~$ wsk property get --auth
whisk auth		23bc46b1-71f6-4ed5-8c54-816aa4f8c502:123zO3xZCLrMN6v2BKK1dXYFpXlPkccOFqm12CdAsMgRU4VrNZ9lyGVCGuMDGIwP
```
Or
```
wsk namespace list -v
```

Then from a browser in your host:
```
https://23bc46b1-71f6-4ed5-8c54-816aa4f8c502:123zO3xZCLrMN6v2BKK1dXYFpXlPkccOFqm12CdAsMgRU4VrNZ9lyGVCGuMDGIwP@192.168.33.13/api/v1/namespaces/guest/actions/helloPython
```
