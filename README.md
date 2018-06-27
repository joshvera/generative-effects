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

<p align="center"><img width="500" alt="joins-and-meets" src="https://user-images.githubusercontent.com/24247/41992424-690714d8-7a16-11e8-85e2-2674c73a31e2.png"></p>

# Galois connections

posets are a special case of categories,
monotone functions between posets are a special case of functors between categories,
Galois connections between posets are a special case of adjoint functors between categories,
left adjoint monotone functions are a special case of left adjoint functors,
right adjoint monotone functions are a special case of right adjoint functors,
meets are a special case of limits, and
joins are a special case of colimits.


