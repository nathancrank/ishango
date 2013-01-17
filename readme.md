# Ishango v0.1
Advanced Math in SASS
Nathan Crank
http://nathancrank.com/


## What is it?
Ishango.scss is a math framework for SASS. The initial goal of the project was to duplicate what Scott Kellum had done with his excellent Compass extension [Sassy-Math](https://github.com/scottkellum/Sassy-math), but without doing anything in Ruby. If that sounds hard, you're right, it was. SASS has clear limits in dealing with large numbers due to how it stores values in Ruby (see nex3's comment on [this GitHub issue thread](https://github.com/nex3/sass/issues/627) to better understand). As a result, there will be rounding errors, but nothing major (don't try log(8000000000)).

All of the functions provided are written in pure scss. That means that you can add it to any SASS project, with or without [Compass](http://compass-style.org), or alongside [Bourbon](http://bourbon.io).

## What can it do?
Ishango includes the following functions:
### comparative
- ``is-int($value)`` - test if value is an integer
- ``is-float($value)`` - test if value is an floating point value (false is is-int($value) == true)
- ``is-inf($value)`` - test if value is SASS's elusive "Infinity" value
- ``is-prime($value)`` - test if value is a prime number
### constants
- ``pi()`` or ``π()``
- ``tau()`` or ``τ()``
- ``golden-ratio()`` or ``φ()``
- ``e()`` - Euler Number
- ``Infinity()`` or ``infinity()`` or ``inf()`` or ``∞()`` - SASS's elusive "Infinity" value
- ``life-the-universe-and-everything()`` - returns 42 (It was late one night…)
### misc
- ``opp($value)`` - returns -1 * $value;
- ``abs-opp($value)`` - returns -1 * |$value|
- ``percent($value)`` - returns value(integer) as percent
- ``float-round($value, $prec)`` - round a floating point value at a particular decimal place $prec
- ``float-ceil($value, $prec)`` - round down a floating point value at a particular decimal place $prec
- ``float-floor($value, $prec)`` - round up a floating point value at a particular decimal place $prec
- ``remove-unit($value)`` - remove units from $value (1px returns 1, 2em returns 2, etc…)
- ``bool-flip($value)`` - returns true if $value is false, returns false if $value is true
### list manipulation
- ``mod-nth($list, $n, $new, $separator[optional]) - replace the $n position value in list with $new (ex. mod-nth("a b c", 2, x) == "a x c"). This allows you to use lists as full array replacements in SASS.
### approximate equality
- ``aprox-equal($value1, $value2, $prec[optional])`` - similar to using ==, verifies that both values are within accepted tolerance $prec (this is to make up for rounding errors in SASS's handling of large floating point numbers)
- ``not-aprox-equal($value1, $value2, $prec[optional])`` - verifies both values are not within accepted tolerance $prec
### nth-roots
- ``nth-root($value, $n)`` - returns $n root of $value
- ``sqrt($value)`` - returns square root of $value
- ``cubert($value)`` - returns cubic root of $value
### exponents
- ``exponent($value, $numerator, $denominator: 1)`` - returns the exponent for $value ^ ( $numerator / $denominator ). Only accepts integer values for $numerator and $denominator.
- ``square($value)`` - squares $value
- ``cube($value)`` - cubes $value
### factorial
- ``factorial($value)`` - returns $value! (5! == 120, 8! == 40320)
### logarithms
- ``log($value)`` - returns log10 of $value
- ``ln($value)`` - returns natural log of $value
### degree/radian conversions
- ``deg-to-rad($value)`` - convert degrees to radians ($value * π / 180)
- ``rad-to-deg($value)`` - convert radians to degrees ($value * 180 / π)
### taylor series
- ``maclaurin($value, $start, $key)`` - start a maclaurin series (this is here for sin and cos calculations, it is not intended to be used elsewise)
### trigonometry
- ``sin($value, $unit: deg)`` - returns sin of $value, $unit can be set as "deg" or "rad"
- ``cos($value, $unit: deg)`` - returns cos of $value, $unit can be set as "deg" or "rad"
- ``tan($value, $unit: deg)`` - returns tan of $value, $unit can be set as "deg" or "rad"
- ``csc($value, $unit: deg)`` - returns csc of $value, $unit can be set as "deg" or "rad"
- ``sec($value, $unit: deg)`` - returns sec of $value, $unit can be set as "deg" or "rad"
- ``cot($value, $unit: deg)`` - returns cot of $value, $unit can be set as "deg" or "rad"
### fibinocci sequence
- ``fibinocci($max, $start: 0 1 1)`` - returns list of the fibinocci sequence starting from $start through $max number of positions
- ``nth-fibinocci($n, $start)`` - returns the value of the number at position $n in a fibinocci sequence starting at $start

#### What is missing that is in Sassy-math?
We are missing a few key components:
- ``sinh()``, ``asin()``, ``asinh()``, ``cosh()``, ``acos()``, ``acosh()``, ``tanh()``, ``atan()``, ``atan2()``, ``atanh()``
- ``power()``
- ``random()`` - although sassy-math always just returns 4 anyhow… 


## Requirements
SASS >= v3.2.5

## Tests
There is a file test.scss that can be compiled to test all functions. You do have to verify the values manually after the test is compiled. This can be time consuming. Trust me. I have included a successfully compiled copy of the test as test.css. If you wish to test particular set of functions, simply comment out the remaining tests and compile.

## Limits
Due to the limits mentioned earlier in how SASS & Ruby handle large floating point values, you may notice slight errors in calculations on occasion. Any calculation that doesn't touch a floating point value should return extremely accurate values (basic exponents, factorials, etc…). Any calculation that uses floating point values (fractional exponents, log, etc…) will be acceptably accurate only up until a certain (varying) number of iterations. I have run thousands of numbers through each test and found that for most calculations that would be used in actually designing a webpage work fine. That is, unless you have a 161803398874989484820458683436563811772030917980px viewport or something insane (please prove me wrong and find a use for these giant values). Passing unitless arguments increases the chances of returning a non Infinity value (ex. factorial(256) works while factorial(256em) returns "Infinityem").

## What's with the ridiculous name?
The [Ishango Bone](http://en.wikipedia.org/wiki/Ishango_bone) is a bone tool found by Belgian Jean de Heinzelin de Braucourt in 1960 that is believed to be 20,000 years old, making it one of the oldest math related artifacts. The bone is a length of the fibula of a baboon that has groupings of notches that are believed to have been tally marks. This is one of the first (and only) math frameworks for SASS, hence the name.

## Future Plans?
Ishango is not a static project. There are still features missing that are needed to bring it inline with my goal of replicating and extending sassy-maths base. Future plans include:
- moving to binary math for improved accuracy with large numbers
- ``exp()`` function
- ``power()`` function
- ``sinh()``, ``asin()``, ``asinh()``, ``cosh()``, ``acos()``, ``acosh()``, ``tanh()``, ``atan()``, ``atan2()``, ``atanh()``
- ``random()`` function
- a method for catching ``NaN`` in addition to ``Infinity``
- Euclidean Greatest Common Factor
- Euclidean Highest Common Factor
- full Taylor series implementation 

Note that none of these future plans are concrete. I'd like to do all of these, but who knows which will happen and if they are all even possible in SASS. I hope they are.

## Comments and Contributions
I welcome all the help I can get here. I am far from a Mathematician. I took Algebra I & II twice each, and certainly not because I was just so gosh-darn good at it. Before making this I was not entirely clear on what a logarithm was. Turns out it's useful in all sorts of ways :)

Ff you find spots where my mathematical prowess has failed, please tell me in the GitHub issues section. If you wish to contribute code or refactored code, please do so via a pull request. Please make sure to update the test and readme as needed.