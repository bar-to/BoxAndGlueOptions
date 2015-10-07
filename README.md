# BoxAndGlueOptions
Playing with box-and-glue layout with hierarchy of containers and options

The vague idea is to have an array of data, and a set of containers.
Each container can have a parent container (recursively up).
Each container also has a set of glue points, and a list of glue-point-pairs (gpp).

So,
```
+3---+
1    2
|    |
+4---+
```
with pairs `[(1,2),(3,4)]` does left-to-right **then** top-to-bottom wrapping.

If we can't fit inside our container with any gpps, we create a new parent container and that glues according to its own
glue points and pairs.
That continues until we hit a parent container that has no gpps. That is a 'terminal' and there can only be one.

**Need** some way of specifing the glue points between child and parent.

If we still have data elements when we hit a terminal, that is 'overflow'.
The 'page' is the ultimate outer container, which is always terminal.

The layout function returns an array of the innermost container boxes and the overflow data (which might be empty)

For multiple sets of data, there needs to be some way of deciding where in the remaining page the next container should start.

To do a left~to~right, top~to~bottom flow in columns, root level is characters gluing left to right, inside
a row container gluing top to bottom, contained in a column container gluing left to right.

Future
--------

* Multiple data sets.
* Interleaving sets
* Flexible block sizes (min size, max size, element size)
