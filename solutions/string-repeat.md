# String Repeat

8kyu
@fundamentals

## Instructions:

Write a function called repeatStr which repeats the given string string exactly n times.

    repeatStr(6, "I") // "IIIIII"
    repeatStr(5, "Hello") // "HelloHelloHelloHelloHello"
    
## Pseudo Code:

    Natural + String -> String
    Given a natural (n) and a string (s), print the string n times
    (repeatStr(n, s) "") ;; signature
    
    (check-expect (repeatStr(6, "I")) "IIIIII")
    (check-expect (repeatStr(5, "Hello")) "HelloHelloHelloHelloHello")
    
Though we have two parameters, both are very simple data types, so our template will look like:
    (repeatStr(n, s)
        (times n) (print s))

## JavaScript
   function repeatStr(n, s) {
       return s.repeat(n);'
   }

## TypeScript

## Python
    def repeat_string(n, s):
        return(s*n)

## PHP

    function repeat_string($n, $str) {
        return str_repeat($str, $n);
    }
