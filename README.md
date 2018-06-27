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

<img width="727" alt="screen shot 2018-06-27 at 11 40 28 am" src="https://user-images.githubusercontent.com/24247/41984757-776d96d0-79ff-11e8-8afb-909aa2202bca.png">
<img width="706" alt="screen shot 2018-06-27 at 11 40 33 am" src="https://user-images.githubusercontent.com/24247/41984758-7786108e-79ff-11e8-8e83-4fe308a4378c.png">


<img width="653" alt="screen shot 2018-06-27 at 11 40 17 am" src="https://user-images.githubusercontent.com/24247/41984783-86560556-79ff-11e8-8f5f-92dbe8064aff.png">
<img width="623" alt="screen shot 2018-06-27 at 11 40 23 am" src="https://user-images.githubusercontent.com/24247/41984784-867df502-79ff-11e8-9223-93421c24c02e.png">

<img width="541" alt="screen shot 2018-06-27 at 11 24 45 am" src="https://user-images.githubusercontent.com/24247/41984814-9aac619e-79ff-11e8-94a7-fb88feb3fe4f.png">
<img width="652" alt="screen shot 2018-06-27 at 11 25 01 am" src="https://user-images.githubusercontent.com/24247/41984815-9ac04a7e-79ff-11e8-83d3-7494daa8a110.png">

<img width="549" alt="screen shot 2018-06-27 at 11 40 48 am" src="https://user-images.githubusercontent.com/24247/41984726-5e66c198-79ff-11e8-9465-1067a9d672bd.png">
<img width="735" alt="screen shot 2018-06-27 at 11 40 42 am" src="https://user-images.githubusercontent.com/24247/41984739-6839050a-79ff-11e8-900e-ebd229e69e6f.png">

<img width="747" alt="screen shot 2018-06-27 at 11 39 59 am" src="https://user-images.githubusercontent.com/24247/41984689-4aa332f4-79ff-11e8-8739-04fafb8f1993.png">


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


