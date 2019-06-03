# Return Negative

8kyu
@fundamentals, @numbers

## The Problem
In this simple assignment you are given a number and have to make it negative. But maybe the number is already negative?

Example:

    makeNegative(1); // return -1
    makeNegative(-5); // return -5
    makeNegative(0); // return 0
    makeNegative(0.12); // return -0.12

Notes:

    The number can be negative already, in which case no change is required.
    Zero (0) is not checked for any specific sign. Negative zeros make no mathematical sense.


## Pseudo Code

    Number -> Number
    Given a number, return it's negative inverse if and only if the given number is positive. Otherwise, return the number.
    
    (check-expect (makeNegative(1), -1))
    (check-expect (makeNegative(-5), -5))
    (check-expect (makeNegative(0), 0))
    (check-expect (makeNegative(0.12), -0.12))
    
This is a very simple problem that requires a conditional test before execution. Though it's tempting to simply treat "num" as a number, given the boundaries we are testing for, it's actually more helpful to treat "num" as an enumeration/itemization so that we build our template and tests accordingly:
    num is one of:
        - number <= 0;
        - number > 0;

    (makeNegative(num)
       (cond [(num <= 0) (return num)]
             [(num > 0) (return num*-1)]) 
    )

## JavaScript

    function makeNegative(num) {
        if (num <= 0) {
            return num;
        }
        if (num > 0) {
           return num * -1;
        }
    }

## TypeScript

    export function makeNegative(num :number): number => {
        if (num <= 0) {
            return num;
        }
        if (num > 0) {
            return num * -1;
        }
    }


## Python

    def makeNegative(num):
        if num <= 0:
            return num
        if num > 0:
            return num * -1
