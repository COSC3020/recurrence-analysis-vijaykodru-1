# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.


ANSWER:

Looking at the given function the recurrence relation can be derived as follow:

$T(n) = 3T(n/3) + n^5$

Starting off the base case where $n <= 1$ takes $O(1)$ time complexity. Next we can see that there are three recursive calls which represents the $3T$, and the $n/3$ is defined by recursive calls with n divided into 3 parts. We get the $O(n^5)$ from the nested loops where i is set to be < $n^2$, j is set to be < $n$, k is < $n^2$. In total it takes $O(n^5)$ time complexity.

Solving for total time complexity:

we know that T(1) = 1,

$T(n/3) = 3(3T(n/9) + (n/3)^5) + n^5$

$= 9T(n/9) + (n/3)^5 + n^5$

$= 9(3T(n/27) + (n/9)^5) + (n/3)^5 + n^5$

The above continues until the code uses recursion, we get

$= 3^i(n/3^i) + \sum_{j=0}^{i-1}(3^j)(n/3^j)^5$

$= 3^i(n/3^i) + n^5 \sum_{j=0}^{i-1}(3^j/3^5j)$

The recursion stops when the array size becomes 1 meaning $n/3^i=1$

if we solve for i we get $i=log_3(n)$

substitute this in the above equation we get 

$T(n) = 3^(log_3(n)) * T(n/3^(log_3(n))) + n^5 \sum_{j=0}^{log_3(n)-1}(3^j/3^5j)$

using logarithmic functions we know that $3^(log_3(n)) = n$

$T(n) = n * T(1) + n^5$

we know that $T(1) = 1$

Therefore the runtime analysis for the code is $\Theta(n^5)$