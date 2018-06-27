# Generative effects: Posets and Galois connections

Hey everyone

# Generative Effects

- Going to discuss generative effects within the context of posets (preorder sets) which have some really interesting properties
- I'm going to do that by showing some motivating examples and introduce you to different concepts that are central to category theory.

- First we need something categories to play with so let's start with an interesting one called the category of posets.
- Whenever you have a set of things and a reasonable way deciding when anything in that set is "bigger" than some other thing, or "more expensive", or "taller", or "heavier", or "better" in any well-defined sense, or... anything like that, you've got a poset.
- In Haskell we might define this using a typeclass

class Eq a => PartialOrd a where
  lessThanOrEq :: a -> a -> Bool
  =< :: a -> a -> Bool

When y is bigger than x we write x =< y. x `lte` y.
Reflexivity :: x =< x
Transitivity :: a =< b && b =< c implies a =< c

## Observations and effects



# Monotone Maps

# Meets and joins

# Galois connections


posets are a special case of categories,
monotone functions between posets are a special case of functors between categories,
Galois connections between posets are a special case of adjoint functors between categories,
left adjoint monotone functions are a special case of left adjoint functors,
right adjoint monotone functions are a special case of right adjoint functors,
meets are a special case of limits, and
joins are a special case of colimits.


