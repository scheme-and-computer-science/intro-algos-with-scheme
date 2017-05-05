# notes

## instrumentation of intermediate variables

It would be nice if, when we want to inspect the intermediate values of a variable, rather than having to write code like this:

```
(define (%merge-sort xs pred trace?)
  (let loop ((xs xs) (result '()))
       ...
       (if trace?
         (begin
           (display (first xs))
           (newline)
           (display (second xs))
           (newline)
           (newline)
           (loop ...))
        (loop ...))))
```

we could instead write code like this:

```
(define (%merge-sort xs pred trace?)
  (instrumented-let loop ((xs xs) (result '()))
          ... normal algorithm ...
          ...))
```

`INSTRUMENTED-LET` watches the values of all variables and prints their value each time through the loop.

I guess it will be implemented as syntax, but we'll see.

Also, it's not clear that this is the best name for it.

Oh!  And actually, it might be better to implement this in a similar fashion to `LOAD-MODULE`, where it just rewrites whole batches of Scheme code to generate the output needed, rather than having to manually rewrite the text of procedures.