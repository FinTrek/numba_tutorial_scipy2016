# Notes on Speed

Misc. and unorganized notes on speed in computation. May only be useful to myself. 

## SciPy 2016 Numba Tutorial Notes

Working through the Numba tutorial. Misc notes here. 

Tools: 

- cProfile
- line_profiler  -- needs to be installed seperately
- timeit


Note: I like this line:

    def sumulate(foo):
        if not isinstance(foo, int):
            return
            
Note Useful note:

> ## What's all this pyobject business?
> This means it has been compiled in object mode. This can be a faster than regular python if it can do loop lifting, but not that fast.
> We want those pyobjects to be int64 or another type that can be inferred by Numba. **Your best bet is forcing _nopython_ mode**: this will throw an error if Numba finds itself in object mode, so that you know that it can't give you speed.
> For the full list of supported Python and NumPy features in nopython mode, see the Numba documentation here: http://numba.pydata.org/numba-doc/latest/reference/pysupported.html

NOTe< REALLY COOL: This is how to write a file from notebook:

    %%file nopython_failure.py
    from numba import jit

    @jit
    def add(a, b):
        for i in range(100):
            c = i
            f = i + 7
            l = c + f
            
        return a + b

    add('a', 'b')
    
    
ALSO somwhow this creates annotated html output: 

    !numba --annotate-html fail.html nopython_failure.py
    
    
Cool, here is how to have nopython turned on by default?

    from numba import njit
    
    
Useful notes:

> ## Other compilation flags
> There are two other main compilation flags for @jit
> 
> cache=True
> 
> if you don't want to always want to get dinged by the compilation time for every run. This will actually save the compiled function into something like a pyc file in your __pycache__ directory, so even between sessions you should have nice fast performance.
> 
> nogil=True
> 
> This releases the GIL. Note, however, that it doesn't do anything else, like make your program threadsafe. You have to manage all of those things on your own **(use concurrent.futures)**.


Takeaways so far:

- use njit
- use cache
- *I think* use explicit definitions of types. Will see!



