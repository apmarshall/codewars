# Powers of 3
7 kyu

Given a positive integer `N`, return the largest integer `k` such that `3^k < N`.

For example,

	largestPower(3) = 0
	largestPower(4) = 1

You may assume that the input to your function is always a positive integer.

## PseudoCode

	Integer (N) -> Integer (k)
	Return the largest k such that N > 3^k
	(def (largest-power N) 0) // stub
	
	(check-expect (largest-power 0), 0)
	(check-expect (largest-power 5), 1) // 3^1 = 3
	(check-expect (largest-power 9), 1) // boundary
	(check-expect (largest-power 10), 2) // 3^2 = 9
	(check-expect (largest-power 81), 3) // boundary
	(check-expect (largest-power 82), 4) // 3^4 = 81

Though it's easy to consider `N` as simply an integer, the examples point at two obvious boundaries and two less obvious ones. So let's delineate `N` as an enumeration. Our two most obvious cases are:

	N is one of:
		- an integer that is an exact power-multiple (don't know what the technical math term for this is) of 3. For example: 3 (3^1), 9 (3^2), 27 (3^3) or 81 (3^4)
		- an integer that is not an exact power multiple of 3
		
In the first case, k will be 1 integer lower than whatever k would solve the equation N = 3^k. We can solve this logorihmically as: `log3(N) = k log3(3)`, which turns into `k = log3(N)`. We then want to retun `k-1` in the first case.

In the second case, we can simply solve for k in the above equations and then truncate our result  to the integer part of the answer (in other words, drop the decimal/fraction portion).

There are at least two other boundaries that we should be aware of:

		- N == 0, 2, or 3 -> 0 // 3^1 = 3, so the largest k that satsifieds our requirements is 0. This will also hold for N == and N == 0, but:
		- N == 1 -> -1 // this is an edge case and a little bit of a "gotcha" in the way this problem is constructed
		
The `N == 2` case should be covered by our second case above. `N == 3` should be covered by our first case. However, `N == 0` may trigger an error is some languages (for example, in JavaScript, it may return `-infinity` when using `Math.log`), so it's good to keep these cases in mind. The edge case of `N == 1` is good to know about for reasons we are going to discuss in a moment.

Now that we've delineated all the possible cases we might encounter, let's start putting this into code:

The challenge of coding for our first case (N is an exact power-multiple of 3) is that we don't know offhand what all the power multiples of 3 are. If we did, we'd simply use that to solve this problem! Sure, we know a few offhand, but we pretty quickly run out of fingers and toes to count on, so counting on that knowledge isn't really a tenable solution. We could approximate this by asking whether `N % 3 == 0`, which will include all of our power-multiples, but also include a lot of false positive noise. So what's the best way to do this? The simplest answer is to substitue `N-1` for `N` and treat all of these the same way as the second case. In other words, we can collapse both of these cases and simply do this:

	return: trunc( log3 ( N-1 )) // return just the integer portion of getting the log base 3 of N-1
	
This works in our second case, too, because the truncated log3 of N and the truncated log3 of N-1 will always be the same unless N is a perfect power-multiple. But if N is a perfect power-multiple, then we didn't want the log3 of N, we wanted to return `(log3 N) - 1` (in other words, this is our first case). So walla, those two can be combined.

But this simplication also underscores the importance of laying out the edge cases we identified:

	- log3 (3-1) -> log3 (2) // this will work fine
	- log3 (2-1) -> log3 (1) // this won't work, it'll return -1 instead of 0
	- log3 (1-1) -> log3 (0) // this won't work, either, it'll return -infinity instead of -1
	- log3 (0-1) -> log3 (-1) // I don't know exactly what will happen here, but not our expected result
	
So, we still need to lay out a few base cases. We have, however, simplified things quite a bit. Here's what it should look like:

	(def (largest-power N 
		If: N == 0 || N == 2:
			return 0
		Else If: N == 1:
			return -1
		Else:
			return trunc (log3 ( N-1) )
	))
	
## JavaScript

Because JavaScript doesn't have the ability to calculate logorithms based on a custom base number, we need to translate this to a natural logorithm. So our mathematical equation looks like this:

	ln(N - 1) / ln(3)
	
We'll use the `Math.log` function to calculate this. When using `Math.log`, if the answer would be `0` (namely, if the input is `0, 2, or 3`), Math.log will return `-infinity.` This means we need to include `3` in our first list of exceptions.
	
Here's the code:

	function largestPower(n){
    if (n == 3 || n == 2 || n == 0) {
        return 0;
    }
    else if (n ==1) {
        return -1;
    }
    else {
        return Math.trunc(Math.log((n-1) / Math.log(3));
    }
}
	
## Python

In Python, we can use a custom base in the `log` function. So our code is slightly simpler:

	import math
	
	def largestPower(N):
		if (n == 2 || n == 0):
			return 0
		else if (n == 1):
			return -1
		else:
			return math.trunc(math.log(n-1, 3))

Note that in both Python and JavaScript we could use `log10` instead of `log`, for example:

	Math.log10(n-1) / Math.log10(3) // JavaScript
	
I found that this worked better in Python because of a rounding error using `log` that resulted in occassional off-by-1 results.