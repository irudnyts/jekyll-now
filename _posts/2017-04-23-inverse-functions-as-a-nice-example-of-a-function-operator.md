---
layout: post
title: "&#128200; Inverse functions as a nice example of a function operator"
---

In the course I assist this spring ([Simulation Methods in Finance and Insurance](https://hec.unil.ch/hec/syllabus/descriptif/2015?dyn_lang=en)), there are plenty of places where one has to inverse a function.

For instance, [inversion method](https://en.wikipedia.org/wiki/Inverse_transform_sampling) of generating pseudo random numbers from a general distribution, which requires to use an inverse c.d.f. (or quantile function). Further on, one has compute a so-called generator of [Archimedean copula](https://en.wikipedia.org/wiki/Copula_%28probability_theory%29#Most_important_Archimedean_copulas). Even for calculating a value at risk ([VaR](https://en.wikipedia.org/wiki/Value_at_risk)) the inversion might be useful. Of course, one can argue that all these methods have already been implemented in R, but the story is rather about inversion. In R there are no built-in [function operator](http://adv-r.had.co.nz/Function-operators.html) that returns a inverse of mathematical functions. This [post](http://stackoverflow.com/questions/10081479/solving-for-the-inverse-of-a-function-in-r) propose a rather elegant solution (with corrected syntax):

```r
inverse <- function(f, lower, upper) {
    function(y) uniroot(function(x) f(x) - y, lower = lower, upper = upper)[["root"]]
}
```

Instead of explicitly define an inverse function, now all mathematical functions can be inversed by a line of code.

```r
log2 <- inverse(exp, 0.1, 10)
log2(exp(1))
```

Please, note that I avoid default values for arguments `lower` and `upper`, ’cause they really require a care.