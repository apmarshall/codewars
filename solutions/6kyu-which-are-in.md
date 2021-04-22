# Which Are In?

## The Problem

Given two arrays of strings a1 and a2 return a sorted array r in lexicographical order of the strings of a1 which are substrings of strings of a2.

### Examples

Example 1: 
```
a1 = [“arp”, “live”, “strong”]
a2 = [“lively”, “alive”, “harp”, “sharp”, “armstrong”]
```
returns `[“arp”, “live”, “strong”]`

#Example 2: 
```
a1 = [“tarp”, “mice”, “bull”]
a2 = [“lively”, “alive”, “harp”, “sharp”, “armstrong”]
```

returns `[]`

## Discussion

The "real life" method of working through these lists would probably be something like this:
 1. Take the first item from lista
 2. Look through listb for a match
 3. After finding the first match, add the item to our output list, repeat from step 1 for the next item on lista
 4. If no match found, repeat from step 1 for the next item in lista
 5. If no more items in lista, return the output list

There are two layers to this problem: the layer of the lists themselves and the layer of the items in the list. We need to traverse both: the lists to compare items and the items to compare sub-strings. Thus, we need at least two functions here:

```
def traverse_lists(lista, listb):
    # list, list -> list
    # given two lists, traverse them and return the sublist which meets the conditions
    
def traverse_strings(stra, strb):
    # str, str -> boolean
    # given two strings, traverse the second and return true if it contains a substring matching the first
```
    
 Our first function is clearly going to refer to the second as the mechanism by which it constructs its sublist, but they are performing two separate actions and therefore worth separating/decomposing.
 
 Let's take the first function first:
 
This function is going to be responsible for steps 1, 4, 5 and part of step 2 (deciding which items to compare). We have two variables here, `len(a) -> a, len(b) -> b`. We have to traverse both lists at least once, and the above method will likely traverse `b` *a* times, so our runtime for this is going to be `O(a + a*b)`, which will really be `O(a*b)`. I'm not sure there's much optimization we can do to improve that.

We're going to start with a recursive approach and then convert it to iterative to save on memory space:

```
def traverse_lists(lista, listb):
    if len(lista) == 0: return output
    else:
        if len(listb) == 0: traverse_lists(lista[1:], listb_orig)
        else:
            traverse_strings(lista[0], listb[0])
            traverse_lists(lista, listb[1:])
```

Iteratively, this is going to look like:

```
def traverse_lists(lista, listb):
    for x in range(len(lista)):
        for y in range (len(listb)):
            traverse_strings(lista[x], listb[y])
    return output
```

Now, let's turn to our second function. Here, we again have two variables: `len(lista[x] -> x, len(listb[y] -> y`. However, we don't need to traverse x, only y. So our runtime will be O(y). Recursively, this is going to look something like the following:

```
def traverse_strings(stra, strb):
    test = len(stra)
    if len(strb) < test: return
    else:
        if (strb[0:test] == stra): 
            output = output + stra
            return
        else:
            traverse_strings(stra, strb[1:])
```

Basically, what we are doing here is testing each sub-string of `strb` to see if it matches `stra`. If it does, we add `stra` to our output list. If it doesn't, we keep going. If we get to the end of strb, we return empty handed and traverse_lists will move on to the next potential match.

Three optimizations we've built in here to note already:

First, rather than checking the length of `stra` in every comparison, we are doing it once by creating the `test` variable. Second, we don't need to go all the way to the end of `strb`, just until our remaining number of characters is less than the length of `stra`, which tells us there can't be another opportunity for a match. And finally, we can stop comparing at our first match. In other words, the goal here isn't to find every match but only whether a match exists at all. The first time we've found one, we can add `stra` to our output list and then we're done comparing. This suggests that we should make a similar optimization to the `traverse_lists` definition: as soon as a string from `lista` is in the output, we can move on to the next item. Such an optimization might look like this:

```
# Recursively
if (lista[0] == output[-1]): traverse_lists(lista[1:], listb_orig)

# Iteratively
if (lista[x] == output[-1]): continue
```

So let's put this all together:

```
# Recursively
def in_array(array1, array2):
    output = []
    listb_orig = array2
    
    def traverse_lists(lista, listb):
        if len(lista) == 0: return output
        else:
            if len(listb) == 0: traverse_lists(lista[1:], listb_orig)
            if lista[0] == output[-1]: traverse_lists(lista[1:], listb_orig)
            else:
                traverse_strings(lista[0], listb[0])
                traverse_lists(lista, listtb[1:])
    
    def traverse_strings(stra, strb):
        test = len(stra)
        if len(strb) < test: return
        else:
            if (strb[0:test] == stra):
                output = output + stra
                return
            else:
                traverse_strings(stra, strb[1:])
                
# Iteratively:
def in_array(array1, array2):
    output = []
    
    for x in range (len(array1)):
        if array1[x] == output[-1]: continue
        for y in range (len(array2)):
            traverse_strings(array1[x], array2[y])
            
    def traverse_strings(stra, strb):
        test = len(stra)
        for t in range (len(strb)-test):
            if (strb[t:t+test] == stra):
                output = output + stra
                return
            else: continue
            
    return output
                
        