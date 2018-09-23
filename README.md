# NamedTupleTools.jl
### Some NamedTuple utilities


#### Copyright © 2015-2018 by Jeffrey Sarnoff. This work is released under The MIT License.

-----


[![Build Status](https://travis-ci.org/JeffreySarnoff/NamedTupleTools.jl.svg?branch=master)](https://travis-ci.org/JeffreySarnoff/NamedTupleTools.jl)

-----

## Overview

`NamedTuples` are built from fieldnames, given as `Symbols` and field values, as they may be given.
These utilities make some uses of `NamedTuples` a little more straightforward.  


## Use
```julia
using NamedTupleTools

julia> namedtuple(:a, :b, :c)(1, 2.0, "three")
(a = 1, b = 2.0, c = "three")

#=
    namedtuple(  name1, name2, ..  )
    namedtuple( (name1, name2, ..) )
       where the `names` are all `Symbols` or all `Strings`

Generate a NamedTuple prototype by specifying or obtaining the fieldnames.
The prototype is applied to fieldvalues, giving a completed NamedTuple.
=#

julia> ntproto = namedtuple( :a, :b, :c )
NamedTuple{(:a, :b, :c),T} where T<:Tuple

julia> nt123 = ntproto(1, 2, 3)
(a = 1, b = 2, c = 3)

julia> ntAb3 = ntproto("A", "b", 3)
(a = "A", b = "b", c = 3)

julia> isprototype(ntproto)
true

julia> isprototype(nt123)
false


julia> delete!(nt123, :a) === (b = 2, c = 3)
true
julia> delete!(nt123, :a, :c) === delete!(nt123, (:a, :c)) === (b = 2,)
true
julia> delete!(ntproto, :b) === namedtuple(:a, :c)
true

julia> nt1 = (a = 1, b = 2, c = 3, d = 4);
julia> nt2 = (a = "one", c = 3.0);

julia> merge(nt1, nt2) === (a = "one", b = 2, c = 3.0, d = 4)
true
```
