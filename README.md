# juliakdb
leveraging the flexible julia meta programming capabilities, build kdb-like API and macros. 


# what's KDB? 
KDB was created by the legendary Arthur Whitney, the ultimate time series database used in almost all wall street firms. 
People use it to crunch massive amount of data at daily basis, the malgnitude is not less than what's generated by the social media giants. 

Coming with KDB is the q langauge, which ihmo, is the most productive, terse and expressive language. One of the most beautiful aspect of q is the space-driven function calls (rarely seen, many languages use brackets of sort to make function calls. Only Haskell supports it to some extend). 

In this repository, I'm taking a humble path to implement the features of kdb/q in Julia. 

# time series functions
## EMA (Exponential Moving Average)

# EMA(Exponential Moving Average)<a id="sec-1" name="sec-1"></a>

in kdb, `ema` function is builtin: 

    //generate 1 million 0, start with 1, use 1/1000 decay
    \t n:1000000?1.
    f:2%21
    \ts show a:f ema n
    10 8389152

Running this many times, it seems 10 ms runtime, 8M in kdb. 

    curry(f, x) = (xs...) -> f(x, xs...)    
    ema=(f,x,y)->(1-f)x + f*y
    n = rand(Float64, 1000000)
    f=2/21
    @time accumulate(curry(ema, f), n)

It takes about 6.5 ms, and 7.6M in julia. 

`Julia` is the clear winner in EMA!