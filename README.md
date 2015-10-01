# BoxAndGlueOptions
Playing with box-and-glue layout with hierarchy of containers and options

The vague idea is to have an array of data, and a set of containers.
Each container can have a parent container (recursively up).
Each container also has a set of glue points, and a list of glue-point-pairs (gpp).

The data is then used to create new containers. These are attached to the previous by the first gpp.
If that exceeds the bounds of the parent, the next pair is used instead. 
The next pair is attached to the last container that was added with that gp index, or the first item. So like
```
0000000,
1000000,
1000000...
```

(note: flag or 'attach via' property to change this?)

So on, until the bounds are not exceeded or we run out of gpps.
If we fit the new container, the next one resets to first gpp.

So,
```
+3---+
1    2
|    |
+4---+
```
with pairs `[(1,2),(3,4)]` does normal left-to-right, top-to-bottom wrapping.

If we can't fit inside our container with any gpps, we create a new parent container and that glues according to its own
glue points and pairs.
That continues until we hit a parent container that has no gpps. That is a 'terminal' and there can only be one.

If we still have data elements when we hit a terminal, that is 'overflow'.
The 'page' is the ultimate outer container, which is always terminal.

The layout function returns an array of the innermost container boxes and the overflow data (which might be empty)

For multiple sets of data, there needs to be some way of deciding where in the remaining page the next container should start.

Future
--------

* Multiple data sets.
* Interleaving sets
* Flexible block sizes (min size, max size, element size)
