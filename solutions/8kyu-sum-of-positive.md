# Sum of Positive:
8 kyu

## Problem:

You get an array of numbers, return the sum of all of the positives ones.

Example [1,-4,7,12] => 1 + 7 + 12 = 20

Note: if there is nothing to sum, the sum is default to 0.

## Pseudo-Code Discussion:
    Array = one of:
       - [] (empty)
       - number cons Array

    Array -> Number
    Return the sum of the positive numbers in the provided array.
    (sum-of-positive (array) 0)
    
    (check-expect (sum-of-positive ([1,-4,7,12]) 20))
    (check-expect (sum-of-positive ([]) 0))
    (check-expect (sum-of-positive ([-1,-2,-3,-4,-5]) 0))
    (check-expect (sum-of-psoitive ([1,2,3,4,5]) 15))
    
Because an array is a list that can be arbitrarily long, we need to be able to loop over it indefinitely. We can do this recursively using the following template:
    (sum-of-positive (array sum)
        (cond 
           [(empty? array) return 0]
           [else: 
               ( cond (is-positive? (first array)) (+ sum (first array)) (sum-of-positive ((rest array) sum)) 
                       else (sum-of-positive ((rest array) sum)))]))
                       
In this recursive function is an accumulator (sum) which is used to track the value of the sums of the positive numbers in the array. When calling the function, we give "sum" the value of 0 to initialize it.

Here's how we would write this in Java Script:

    function positiveSum(arr) {
        function sumOfPositives(arr sum) {
            if (arr.length == 0) {
               return 0;
            } else {
                if (arr[0] > 0) {
                    sum += arr[0];
                    return sumOfPositives (arr.shift, sum);
                } else {
                    return sumofPositives (arr.shift, sum);
                }
            }
        }
        return sumOfPositives(arr 0);
    }
   
However, JavaScript doesn't handle recursion like this very effectively or reliably, so really we want to convert this to a for loop:

    function positiveSum(arr) {
        let sum = 0;
        for (i = 0, j = arr.length; i<j; i++) {
            if (arr[i] > 0) {
                sum += arr[i];
            }
        }
        return sum;
    }
    
We can easily make this for loop type-script compliant:



Python can handle the recursion, so we'll start with a recursive version:

    def positve_sum(arr):
        def sum_of_positives(arr, sum):
           if not arr:
               return sum
           else:
               if arr[0] > 0:
                   sum += arr[0]
                   return sum_of_positives(arr[1:], sum)
               else: 
                   return sum_of_positives(arr[1:], sum)
        return sum_of_positives(arr, 0)

In PHP, the recursion will look like this:

    function positive_sum($arr) {
        function sum_of_positives($arr, $sum) {
            if (empty($arr)) {
                return $sum;
            }
            else {
                if ($arr[0] > 0) {
                    $sum += $arr[0];
                    $arr = (array)$arr;
                    $arr = array_shift($arr);
                    return sum_of_positives($arr, $sum);
                }
                else {
                    $arr = (array)$arr;
                    $arr = array_shift($arr);
                    return sum_of_positives($arr, $sum);
                }
            }
        }
        return sum_of_positives($arr, 0);
    }
    
While PHP can handle this recursion, it is particularly slow and consumes a lot of memory. So it's better to rewrite this as a loop using "foreach":

    function positive_sum($arr) {
        $sum = 0;
        foreach ($arr as $value) {
            if ($value > 0) {
                $sum += $value;
            }
        }
        return $sum;
    }
    
