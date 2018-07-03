# Generative effects: Posets and Galois connections

Hey everyone

# Generative Effects

- Going to discuss generative effects within the context of posets (preorder sets) which have some really interesting properties
- I'm going to do that by showing some motivating examples and introduce you to different concepts that are central to category theory.

- First we need something categories to play with so let's start with an interesting one called the category of posets.
- Whenever you have a set of things and a reasonable way deciding when anything in that set is "bigger" than some other thing, or "more expensive", or "taller", or "heavier", or "better" in any well-defined sense, or... anything like that, you've got a poset.
- In Haskell we might define this using a typeclass

```haskell
class Eq a => PartialOrd a where
  lessThanOrEq :: a -> a -> Bool
  =< :: a -> a -> Bool
```

When y is bigger than x we write x =< y. x `lte` y.

Reflexivity :: x =< x

Transitivity :: a =< b && b =< c implies a =< c

## Observations and effects

Let's explore a couple of functions on sets. Here we have an unconnected set of three points. We'll call them the dot, circle, and star. The system I'll describe will be a way of connecting these dots together. We might think of these points as sites on a power grid, computers on a network, or people susceptible to some disease.

<p align="center"><img width="105" alt="unconnected-set" src="https://user-images.githubusercontent.com/24247/41985857-83eacea2-7a02-11e8-96f1-dbd0f13b164e.png"></p>

Connections in this system are symmetric, which is to say if a is connected to b, then b is connected to a. They're also transitive just like the partial order law we described above. If a is connected to b and b is connected to c then a is connected to c. We can contrast this system with a system like friendship. The friend of my friend is not necessarily my friend.

<p align="center"><img width="95" alt="connected-set" src="https://user-images.githubusercontent.com/24247/41985858-83ff280c-7a02-11e8-8a04-1fec6894e594.png"></p>

Say we had a function or an observation about this system which had the type of:

```haskell
isDotConnectedToStar :: PointSet -> Bool
```

For the following set it would be false.

<p align="center"><img width="350" alt="dot-not-connected-to-star" src="https://user-images.githubusercontent.com/24247/41985865-84607e90-7a02-11e8-8127-2e401eaff391.png"></p>

And for the following set it would be true.

<p align="center"><img width="238" alt="dot-connected-to-star" src="https://user-images.githubusercontent.com/24247/41985863-8436ef9e-7a02-11e8-8225-2b2f7b63f27f.png"></p>

Now let's define another operation on this type of system we'll call join. The join of two systems is given by combining their connections. We denote this with `⌄` that kind of looks like a union operation but it does a little more. The high-level way to say this is "to take the transitive closure of the union of the connections in A and B."

<p align="center"><img width="393" alt="join-operation" src="https://user-images.githubusercontent.com/24247/41985860-840dd424-7a02-11e8-9ff8-dabdb441bebe.png"></p>

- So this is fine in the above case, but below we see that the `isDotConnectedToStar` would be false for both point sets, but true for the join f the point sets. The join operation has led to what is called a generative effect, or an operation that does not preserve the observations of the systems. While this is a pretty simple example, knowing whether a function leads to generative effects is incredibly important within the context of any category, data structure and its operations.

<p align="center"><img width="399" alt="generative-effect" src="https://user-images.githubusercontent.com/24247/41985856-83d4b8ba-7a02-11e8-887e-80b6510521ff.png"></p>

## Back to order

Category theory is all about organizing and layering structures. If we think about the sets we've talked about and the `lessThanOrEq` relation we can see that our `isDotConnectedToStar` function preserves the order between our sets. Let's say we define `lessThanOrEq` by saying that sets with smaller connections are smaller than sets with larger connections.

<p align="center"><img width="213" alt="set-inequality" src="https://user-images.githubusercontent.com/24247/41985862-8421a56c-7a02-11e8-8dd2-9ff8c6e06ffb.png"></p>

If we take a look at the whole set, we can see that running the whole thing through `isDotConnectedToStar` preserves the order. The bottom set would be false, the left and right set would be false, the middle and top set would be true.

<p align="center"><img width="405" alt="all-sets" src="https://user-images.githubusercontent.com/24247/41985864-84471b44-7a02-11e8-9114-5f64cedeaeda.png"></p>

As we've already seen, the `isDotConnectedToStar` does not preserve through join operations so we need an additional inequality to describe that behavior:

```haskell
(isDotConnectedToStar a `join` isDotConnectedToStar b) `lessThanOrEq` isDotConnectedToStar (a `join` b)
```

# Monotone Maps

We've been talking about the properties preserved through certain functions we've defined. In the above case, that the `isDotConnectedToStar` function preserves order, but not joins. If we jump up a level, and talk about how posets themselves can be related we can talk about monotone maps. Monotone maps are functions that preserve poset orders. Let's take a look at some examples.

<p align="center"><img width="519" alt="monotone-map1" src="https://user-images.githubusercontent.com/24247/41991771-aa30feee-7a14-11e8-879e-c1a82e48c7ff.png"></p>
<p align="center"><img width="703" alt="monotone-map2" src="https://user-images.githubusercontent.com/24247/41991772-aa54a434-7a14-11e8-9121-6d40c98ff8ec.png"></p>

# Meets and joins

As we said earlier, posets are sets with a simple order functions between elements. We can use this structure to define two types of elements with special properties. In the generative effect example we talked about joins and now we'll also talk about meets.

The meets of some poset P would be the greatest lower bound elements of P. The joins of some poset P would be the lowest upper bounds of P. They are also referred to the infima and the suprema, respectively.

<p align="center"><img width="500" alt="joins-and-meets" src="https://user-images.githubusercontent.com/24247/41992424-690714d8-7a16-11e8-85e2-2674c73a31e2.png"></p>


# Back to Generative Effects
Adam Elie wrote his PhD Thesis in 2017 on Systems, Generativity and Interactional Effects where he thinks of monotone functions as observations. A monotone function of type P -> Q is a phenomenon of P as observed by Q. He defines generative effects of such a function to be its failure to preserve joins.

We say that a monotone function `m :: P -> Q` preserves meets if m(a `meet` b) = m(a) `meet` m(b). We say that a monotone function preserves joins if m(a `join` b) = m(a) `join` m(b).

We say that a monotone function `m :: P -> Q` sustains generative effects if there exist elements `a :: P, q :: P` such that

```haskell
m(a) `join` m(b) != m(a `join` b)
```

If what Adam proposes is true, the process of combining large systems or reasoning about their subsystems depends on our ability to preserve the joins or meets of that system, respectively.

# Galois connections

So now we've gotten to the cool part which are Galois connections. Galois connections are a fancy name for _a pair of functions that tell you the best possible way to recover data that can't be recovered_. More precisely, they tell you _the best approximation to reversing a computation that can't be reversed_.

```Haskell
-- a function that takes a set of balls and places them in a set of buckets
f :: Set Ball -> Set Bucket
f [1, 2, 3] = Set (First 1 2 2) (Second 1) (Third 1 1 2 3)

-- A function that takes a set of buckets and tells you which balls are in them
-- This might be called a pullback along f.
f* :: Set Bucket -> Set Ball
f* Set (First 3 2) (Second 1) = 3 2 1

leftAdjointF :: Set Ball -> Set Bucket
leftAdjointF [2, 3] = Set (Second 1) (Third 1 1 2 3)

rightAdjointF :: Set Ball -> Set Bucket
rightAdjointF [1] = Set (Second 1)
```

# Conclusion

Posets are a special case of categories,
Monotone functions between posets are a special case of functors between categories,
Galois connections between posets are a special case of adjoint functors between categories,
Left adjoint monotone functions are a special case of left adjoint functors,
Right adjoint monotone functions are a special case of right adjoint functors,
Meets are a special case of limits, and
Joins are a special case of colimits.
