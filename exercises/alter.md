
## Exercise 1

Define a type ``Alter a b`` with the following properties:

* It is a list of 0 or more values.

* Elements in even positions of the list have type ``a``.

* Elements in odd positions of the list have type ``b``.

These properties must follow from the type definition, i.e.
they must hold by construction. As usual, consider the first
element to have index zero.

## Exercise 2

What should be the type of a function that prepends an element
to an ``Alter`` list? Define it once you have the type.

## Exercise 3

What should be the type of a function that removes an element
from the beginning of an ``Alter`` list? Define it once you
have the type.

## Exercise 4

How would you calculate the length of an ``Alter`` list?

## Exercise 5

What should be the type of a function aimed to get the first
element of an ``Alter`` list? Define it once you have the
type.

## Exercise 6

Write a function that builds two regular lists from an ``Alter``
list. One list containing the elements in even indices, and the
other containing the elements in odd indices.

## Exercise 7

Is it possible to define a reverse function for ``Alter``? Justify your answer.

## Kinds and type classes

In Haskell, just like every value belongs to a type, every type belongs to a kind.

Regular non-parametric types have kind ``*`` (star). For example:

```haskell
Bool :: *
Int :: *
Double :: *
```

Parametric types use the ``->`` kind constructor in their kind. For example:

```haskell
Maybe :: * -> *
Either :: * -> * -> *
(,) :: * -> * -> *
[] :: * -> *
```

When applying a type constructor to another type, the kind changes accordingly:

```haskell
Maybe Bool :: *
Either String :: * -> *
[Int] :: *
```

Type classes have a kind associated. Every instance of a type class must have this
kind. The kind is calculated by looking at the use of the class type variable in the
methods of the class. For example:

```haskell
class Eq a where
  (==) :: a -> a -> Bool
  (/=) :: a -> a -> Bool
```

Here, ``a`` is being used without any parameters, therefore its kind must be ``*``.

The ``Functor`` class is defined as follows:

```haskell
class Functor f where
  fmap :: (a -> b) -> f a -> f b
```

Therefore, every instance of ``Functor`` must have kind ``* -> *``.

Often methods of a type class are assumed to satisfy a set of laws.

An instance of ``Functor`` should satisfy the following laws:

* ``fmap id = id``

* ``fmap (f . g) = fmap f . fmap g``

If we wanted to write a ``Functor`` instance for ``Either``, we couldn't do it
because ``Either`` has kind ``* -> * -> *``, but ``Functor`` requires kind
``* -> *``. However, we can partially apply the ``Either`` type constructor to obtain
a type of kind ``* -> *``, allowing us to write the ``Functor`` instance:

```haskell
instance Functor (Either e) where
  fmap _ (Left e) = Left e
  fmap f (Right x) = Right (f x)
```

## Exercise 8

What is the type of ``fmap`` in the ``Functor`` instance for ``Either``?

## Exercise 9

What is the kind of ``Alter``?

## Exercise 10

Is it possible to define a ``Functor`` instance for ``Alter``?
