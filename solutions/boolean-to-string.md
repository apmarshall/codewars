# Convert boolean values to strings 'Yes' or 'No'.

8kyu

@fundamentals, @booleans, @best-practices

## The Problem:

Complete the method that takes a boolean value and return a "Yes" string for true, or a "No" string for false.

## Pseudo Code

    Boolean -> String
    Given a boolean, return the string "Yes" for true and the string "No" for false.
    
    (check-expect (bool-to-string (true)), "Yes")
    (check-expect (bool-to-string (false)), "No")
    
This is another case where, given the boundaries we are testing for, following the template for an enumeration/itemization is better than simply dealing with the boolean outright:

    (bool-to-string (bool)
        (cond [(bool == true) (return "Yes"))]
              [(bool == false) (return "No")])
    )

Alternatively, since we are working with booleans, we can shortcut this process using a simple "boolean" test:

    (bool-to-string (bool)
        if (boolean? bool) (return "Yes")
        else (return "No")
    )

## JavaScript

Version 1:
    function boolToString (bool) {
        if (bool == true) {
            return "Yes";
        }
        if (bool == false) {
            return "No";
        }
    }
    
Version 2:
    function boolToString (bool) {
       if (bool) {
          return "Yes";
       } else {
          return "No";
       }
    }

## TypeScript

Version 1:
    export function boolToString (bool: boolean): String => {
        if (bool == true) {
            return "Yes";
        }
        if (bool == false) {
            return "No";
        }
    }
    
Version 2:
    export function boolToString (bool: boolean): string => {
        if (bool) {
            return "Yes";
        } else {
            return "No";
        }
    }

## Python
Version 1:
    def bool_to_string (bool):
        if bool == true:
            return "Yes"
        if bool == false:
            return "No"

Version 2:
    def bool_to_string (bool):
        if bool:
            return "Yes"
        else:
            return "No"

## PHP
Version 1:
    function boolToString($bool) {
        if ($bool == true) {
            return "Yes";
        }
        if ($bool == false) {
            return "No";
        }
    }
    
Version 2:
    function boolToString($bool) {
        if ($bool) {
            return "Yes";
        } else {
            return "No";
        }
    }
