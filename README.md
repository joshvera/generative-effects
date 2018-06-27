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
<p align="center"><img width="105" alt="unconnected-set" src="https://user-images.githubusercontent.com/24247/41985857-83eacea2-7a02-11e8-96f1-dbd0f13b164e.png"></p>
<p align="center"><img width="95" alt="connected-set" src="https://user-images.githubusercontent.com/24247/41985858-83ff280c-7a02-11e8-8a04-1fec6894e594.png"></p>


<p align="center"><img width="350" alt="more-sets" src="https://user-images.githubusercontent.com/24247/41985865-84607e90-7a02-11e8-8127-2e401eaff391.png"></p>
<p align="center"><img width="238" alt="other-sets" src="https://user-images.githubusercontent.com/24247/41985863-8436ef9e-7a02-11e8-8225-2b2f7b63f27f.png"></p>

<p align="center"><img width="213" alt="set-inequality" src="https://user-images.githubusercontent.com/24247/41985862-8421a56c-7a02-11e8-8dd2-9ff8c6e06ffb.png"></p>
<p align="center"><img width="405" alt="all-sets" src="https://user-images.githubusercontent.com/24247/41985864-84471b44-7a02-11e8-9114-5f64cedeaeda.png"></p>

<p align="center"><img width="393" alt="join-operation" src="https://user-images.githubusercontent.com/24247/41985860-840dd424-7a02-11e8-9ff8-dabdb441bebe.png"></p>

<p align="center"><img width="399" alt="generative-effect" src="https://user-images.githubusercontent.com/24247/41985856-83d4b8ba-7a02-11e8-887e-80b6510521ff.png"></p>



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


