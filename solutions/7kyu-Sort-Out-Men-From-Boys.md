# Sort Out the Men From the Boys
7 kyu 

@fundamentals, numbers, basic language features, conditional statements, control flow, algorithms

## Scenario

> Now that the competition gets tough it will Sort out the men from the boys .

> Men are the Even numbers and Boys are the odd  !alt !alt

*Task*

Given an array/list [] of n integers , Separate The even numbers from the odds , or Separate the men from the boys  !alt !alt

*Notes*

- Return an array/list where Even numbers come first then odds
- Since , Men are stronger than Boys , Then Even numbers in ascending order While odds in descending .
- Array/list size is at least *4*** .
- Array/list numbers could be a mixture of positives , negatives .
- Have no fear , It is guaranteed that no Zeroes will exists . !alt
- Repetition of numbers in the array/list could occur , So (duplications are not included when separating).

*Input >> Output Examples:*

    menFromBoys ({7, 3 , 14 , 17}) ==> return ({14, 17, 7, 3}) 

Explanation:

Since , { 14 } is the even number here , So it came first , then the odds in descending order {17 , 7 , 3} .

    menFromBoys ({-94, -99 , -100 , -99 , -96 , -99 }) ==> return ({-100 , -96 , -94 , -99})

Explanation:

Since , { -100, -96 , -94 } is the even numbers here , So it came first in ascending order , *then** *the odds in descending order { -99 }

Since , (Duplications are not included when separating) , then you can see only one (-99) was appeared in the final array/list .

    menFromBoys ({49 , 818 , -282 , 900 , 928 , 281 , -282 , -1 }) ==> return ({-282 , 818 , 900 , 928 , 281 , 49 , -1})

Explanation:

Since , {-282 , 818 , 900 , 928 } is the even numbers here , So it came first in ascending order , then the odds in descending order { 281 , 49 , -1 }

Since , (Duplications are not included when separating) , then you can see only one (-282) was appeared in the final array/list .

## Psuedocode and Discussion

Our input is an array/list of numbers, which can be of arbitrary length:

    ListOfNumbers is one of:
        - empty []
        - ListOfNumbers + empty []
        
This means we are likely to want to use a recursive template for our function.

    ListOfNumbers -> ListOfNumbers
    Return a ListOfNumbers with even numbers first in ascending order followed by odd numbers in descending order
    
    def (MenFromBoys (ListOfNumbers)) [] // Stub
    
    (Check-expect (MenFromBoys (7, 3 , 14 , 17)) 14, 17, 7, 3) // one even
    (Check-expect (MenFromBoys (49 , 818 , -282 , 900 , 928 , 281 , -282 , -1)) -282 , 818 , 900 , 928 , 281 , 49 , -1) // mix
    (Check-expect (MenFromBoys (-94, -99 , -100 , -99 , -96 , -99)) -100 , -96 , -94 , -99) // one odd
    (Check-expect (MenFromBoys ()) []) // empty input returns empty output
    (Check-expect (MenFromBoys (7, 3 , 15 , 1)) 17, 15, 7, 3) // no evens
    (Check-expect (MenFromBoys (8, 4 , 14 , 2)) 2, 4, 8, 14) // no odds
    (Check-expect (MenFromBoys (2, 2, 2, 2,)) 2) // eliminate duplicates
    
There appear to be three distinct things happening here:
- First, the input list is being separated into lists of evens and lists of odds (without duplicates)
- Second, those respective lists are being sorted (ascending and descending, respectively)
- Third, those lists are being combined together to form the output list

So our main/out function is going to look like this:

    def (MenFromBoys (ListOfNumbers) 
        Combine( Sort( Separate (ListOfNumbers)))
    )
    
Which leaves us with three "wish-list" functions:

    ListOfNumbers -> ListOfNumbers:Even; ListOfNumbers:Odd
    Given a list of numbers, produce two lists, the first of the even numbers and the second of the odd numbers
    def (Separate (ListOfNumbers)) [] [] // stub
        
    ListOfNumbers:Even; ListOfNumbers:Odd -> ListOfNumbers:Even; ListOfNumbers:Odd
    Given two lists of numbers, sort the numbers (ascending if even, descending if odd)
    def (Sort( ListOfNumbers)) [] // stub
    
    ListOfNumbers:Even; ListOfNumbers:Odd -> ListOfNumbers
    Given two lists of numbers, adjoin them into a single list
    def (Combine (ListOfNumbers, ListOfNumbers)) [] //stub

Note that the expected output of our first function, `Separate`, is two lists, not one. This matches the expected input of our second function, `Sort`, and the expected input of our third function `Combine`.

Now lets work on the first function. First, some test cases:

    (Check-expect (Separate (7, 3 , 14 , 17)) [14], [7, 3, 17]) // one even
    (Check-expect (Separate (49 , 818 , -282 , 900 , 928 , 281 , -282 , -1)) [818, -282, 900, 928],[49, 281, -1]) // mix
    (Check-expect (Separate (-94, -99 , -100 , -99 , -96 , -99)) [-94, -100, -96], [-99]) // one odd
    (Check-expect (Separate ()) [], []) // empty input returns empty output
    (Check-expect (Separate (7, 3 , 15 , 1)) [],[7, 3, 15, 1]) // no evens
    (Check-expect (Separate (8, 4 , 14 , 2)) [8, 4, 14, 2], []) // no odds
    (Check-expect (Separate (2, 2, 2, 2,)) [2], []) // eliminate duplicates
    
Now, our basic template:
    def (Separate (ListOfNumbers) 
        cond: empty? (...)
        else:
            (...(first ListOfNumbers)
                (Separate(rest ListOfNumbers)))
    )
    
We are obviously going to need some sort of "accumulator" here to keep track of our output. In fact, we can go ahead and say we are going to need two accumulators: one for our even list and one for our odd list. Here's what that looks like:
    
    def (Separate (ListOfNumbers) 
        (local [Separate (ListOfNumbers, Even, Odd)
            cond: empty? (... Even, Odd)
            else:
                (... Even, Odd
                    (first ListOfNumbers)
                    (Separate(rest ListOfNumbers, Even, Odd))
                            (... Even, Odd, first ListOfNumbers)
        ])
        Separate (ListOfNumbers, Even, Odd))

Now we can fill in this template. Essentially, what we want to do at each stage is: (1) if the number is even, add it to the even list, or (2) if the number is odd, add it to the odd list. When we run out of numbers, we'll return both lists. Here's what that's going to look like:

    def (Separate (ListOfNumbers)
        (local [Separate (ListOfNumbers, Even, Odd) 
            cond: empty? (return Even, Odd)
            else:
                cond: ((first ListOfNumbers) % 2 == 0):
                    Add (first ListOfNumbers) to Even
                else: Add (first ListOfNumbers) to Odd
                (Separate (rest ListOfNumbers, Even, Odd))
        ])    
        Separate (ListOfNumbers, [], []))
        
Wala! That function should now be done. On to the other two.

## Python

## PHP

## JavaScript

## TypeScript