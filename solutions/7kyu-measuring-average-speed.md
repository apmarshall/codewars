@fundamentals, @basic-language-features, @numbers, @strings

#JavaScript, #PHP

# The Problem:

Speed is a crucial measure of success for any aspiring warrior, so let's write a function to calculate it.

Average Speed is calculated by dividing distance by time. Given two strings as input the first of which indicates a codewarrior's distance travelled (in metres or kilometres) and the second indicating the time it takes them to travel (in seconds or minutes), return a string indicating their speed in miles per hour rounded to the nearest integer.

For the purposes of this kata one metre per second is defined as 2.23694 miles per hour.

So for example given the input values of distance & time "3km" and "5min" we should return a speed value of "22mph".

# Discussion and Pseudocode

Let's start with the basic shell of our function:

	string + string -> string
	Given two strings, one specifying distance (in m or km) and one time (in seconds or minutes), return a string specifying average speed in miles per hour rounded to the nearest integer
	def average-speed (dist, time) "0mph" // stub
	expect: average-speed ("3km", "5min") "22mph" //example

So what we can see from the description and the example is that we are going to need to do a few things:

First, we need to parse our input strings into their number and letter portions.

Second, we need to interpret the letter portions so we know what unit of measurement we're dealing with.

Third, we need to convert the input units into miles per hour.

And finally, we need to return the output string.

So actually, our initial function is going to look like this:

	def average-speed (dist, time) 
		output (convert (interpret (parse (dist, time) ) ) )

And now we can start working on our sub-functions:

	string + string -> number + number + string + string
	Given two strings, one specifying distance (in m or km) and one specifying time (in seconds or minutes), return the number portion of both strings as numbers and the letter portions of both in string form
	def parse (dist, time) 0, 0, "m", "s" // stub
	expect: parse ("3km", "5min") 3, 5, "km", "min"

Interpret:
	number + number + string + string -> number + number
	Given two numbers (one representing distance and one time) and two strings (giving units of distance or time), interpret the strings to identify the units and convert the numbers to common bases of meters and seconds, respectively.
	def interpret (numD, numT, strD, strT) 0, 0 // stub
	expect: interpret (3, 5, "km", "min") 3000, 300

Convert:
	number + number -> number
	Given two numbers, one representing distance in meters and one representing time in seconds, convert the corresponding number of meters/second to miles per hour.
	def convert (numD, numT) 0 // stub
	expect: convert (3000, 300) 22
	
Output:
	number -> string
	Given a number representing miles per hour, output this number into a string appended with the unit "mph"
	def output (numMPH) "0mph" // stub
	expect: output (22) "22mph"