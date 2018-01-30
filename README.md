# Prodict
Prodict = Dictionary with IDE friendly(auto code completion) and dot-accessible attributes

# Motivation
Ever wanted to use a `dict` like a class and access keys as attributes? Prodict does exactly this. 

Although there are number of modules doing this, Prodict does a little bit more.

You can provide type hints and get auto code completion!

With type hints, you also get recursive object instantiations, which will blow your mind.

You will never want to use `dict` again.

# Examples

Example 0: Use is like regular dict, because **it IS** a dict
```python

from prodict import Prodict

p = Prodict(lang='Python', pros='Rocks!')
print(p)  # {'lang': 'Python', 'pros': 'Rocks!'}

p2 = Prodict.from_dict({'Hello': 'world'})

print(p2)  # {'Hello': 'world'}

print(issubclass(Prodict, dict))  # True

print(isinstance(p, dict))  # True

print(set(dir(dict)).issubset(dir(Prodict)))  # True


```
Example 1: Type hinting
```python
from prodict import Prodict
class Country(Prodict):
    name: str
    population: int


turkey = Country()
turkey.name = 'Turkey'
turkey.population = 79814871
```

![auto code complete](/auto-complete1.png?raw=true "Auto complete in action!")

Example 2:
```python
germany = Country(name='Germany', population=82175700, flag_colors=['black', 'red', 'yellow'])

print(germany.flag_colors)  # ['black', 'red', 'yellow']
print(type(germany.flag_colors)) # <class 'list'>
```

Example 3:
```python
class Ram(Prodict):
    capacity: int
    unit: str
    type: str
    clock: int


class Computer(Prodict):
    name: str
    cpu_cores: int
    rams: List[Ram]

    def total_ram(self):
        return sum([ram.capacity for ram in self.rams])


comp1 = Computer.from_dict({'name': 'My Computer', 'cpu_cores': 4})
print(comp1)
# {'name': 'My Computer', 'cpu_cores': 4}

comp1.rams = []
comp1.rams.append(Ram(capacity=8, unit='GB', type='DDR3', clock=2400))
comp1.rams.append(Ram.from_dict({'capacity': 4, 'unit': 'GB', 'type': 'DDR3', 'clock': 2400}))

print(comp1)
# {
#   'name': 'My Computer',
#   'cpu_cores': 4, 
#   'rams': [
#       {'capacity': 8, 'unit': 'GB', 'type': 'DDR3', 'clock': 2400},
#       {'capacity': 4, 'unit': 'GB', 'type': 'DDR3', 'clock': 2400}
#   ]
# }

print(comp1.rams)
#   [
#       {'capacity': 8, 'unit': 'GB', 'type': 'DDR3', 'clock': 2400},
#       {'capacity': 4, 'unit': 'GB', 'type': 'DDR3', 'clock': 2400}
#   ]
```


# Limitations
- You cannot use names of dict methods as attribute names.
- Requires Python 3.6+

