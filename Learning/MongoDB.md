1. Indexing -
   It helps MongoDB find documents quickly instead of scanning the whole collection.
   unique:true
   or
   .index()
   Then now while searching for indexed key we get it faster
   Internally data is stored in a B-Tree structure where we skip half of the search space in every go until we found a match
   projection
   pagination
