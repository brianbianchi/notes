## list
* mutible 
* `[1,'2',False]`
* `list.extend([])` - appends two lists
* `list.pop()` - removes last index

## tuple
* immutable
* `(1,'2', False)`

## range
* `range(stop)`
* `range(start, stop)`
* `range(start, stop, step)`

## enumerate
* `enumerate(iterable, start=0)`
* `list(enumerate(['h','i'], 3)) #output: [(3, 'h'), (4, 'i')]`

## slice
* `[start:stop:step]`
* `x = [0,1,2,3,4,5,6] x[4:2:-1] #output: [4,3]`

## set
* no position, unique, unorderedr
* empty set - `set()`
* `s = {4,5,6}`
* `s.add(56)`
* `s.remove(56)`
* `print(56 in s) # False` 
* `s1.union(s2) # combine sets`
* `s1.symmetric_difference(s2) # element not shared between s1 and s2`
* `s1.difference(s2) # in s1 but not s2`
* `s1.intersection(s2) # elements both share`

## dictionary
* key value pair
* `x = {'key': 4}`
* `x.values() # [4]`
* `x.keys() # ['key']`
* `x['key2']=2 # add to dictionary`
* `del x['key2'] # remove`

## comprehensions
* `x = [i for i in range (50) if i%5 == 0] #[0, 5, 15, 20, 25, 30, 35, 40, 45]`

## function
```python
def add(x, y, z=None);
    return x+y
```

## exceptions
* `raise Exception('error')`
* 
```python
try: 
    x=7/0
except Exception as e:
    print(e)
finally:
    print('always')
```

## lambda
* one line anon function
* `lambda x,y: x+y`
* `x=[1,2,3]`
`map(lambda i:i+2,x) #[3,4,5]`
`filter(lambda i: i%2==0,x) #[2]`

## f strings
* `f'Hello {4-56}' #'Hello -52'