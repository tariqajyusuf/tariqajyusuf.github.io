---
title:  '"Are You Mocking Me?": Overriding Object Behavior in Python Unit Tests'
date:   2015-07-31 19:11 -0800
categories: tutorials
---
One of the things I've learned working at Google have been the importance of
testing code such that it executes reliably and consistently. Most of my
familiarity with tests comes from testing individual modules that I write (read
as [unit tests](http://artofunittesting.com/definition-of-a-unit-test/)). I've
commonly faced the problem where I have code that makes a
network or disk I/O request or relies on some input from an external module I
have no control over. Enter the concept of mocking.

Mocking, for the purposes of this discussion, is overriding behavior of a module
to consistent behavior such that the module being tested is properly isolated.
In the examples I'll be using here, we'll be referring to the [unittest.mock](
https://docs.python.org/3/library/unittest.mock.html) framework available in
Python 3.x. If you're using Python 2.7, the Voidspace mock library provides a
very similar interface. I'd suggest keeping that open in another tab so you can
refer to it as we go along.

**Aside**: Martin Fowler has a great discussion on the differences between
Mocks, Stubs, and Fakes that you can read [here](
http://martinfowler.com/articles/mocksArentStubs.html#TheDifferenceBetweenMocksAndStubs).
{: .notice--primary}

Let's begin, suppose you have the following Python class.

```py
class Barista(object):

  def MakeMocha(EspressoMachine e):
    if e.InService():
    shot := e.MakeShot()
    return self._mix(shot, _fridge.GetMilk(.25))
  else:
    raise Error("Espresso Machine is broken.")
  ...
```

Now suppose that making the shot takes a long time and you just want to make
sure that the Barista class can make the drink. A (non-exhaustive) unit test
would look something like:

```py
class BaristaTest(unittest.TestCase):
  ...
  def TestMakeMocha():
    expectedDrink = ...
    e = EspressoMachine(...)
    assertEquals(barista.MakeMocha(e), expectedDrink)
  ...
```

However the problem is that your test for `MakeMocha` assumes that
`EspressoMachine` is implemented correctly, furthermore you're also relying on
a potential production implementation that could call out to other resources and
thus "de-isolate" your test. This is where mocks are useful, instead of having
to write an interface and implement your own `FakeEspressoMachine`, you can use
mocks to isolate this test to the behavior of the `Barista` and eliminate any
variables that could come from the `EspressoMachine`.

With the mock library, we can use a decorator to override certain behavior
before we ask the `Barista` to make the drink and resume normal behavior after
they're done. Let's walk through a code example.

```py
# Import patch
from unittest.mock import patch

class BaristaTest(unittest.TestCase):
  ...
  def TestMakeMocha():
    expectedDrink = ...
    e = EspressoMachine(...)
    <b>with patch.object(EspressoMachine, 'MakeShot',
                      returnValue=EspressoShot()):</b>
      assertEquals(barista.MakeMocha(e), expectedDrink)
  ...
```

In this example we make use of the [`patch.object`](
https://docs.python.org/3/library/unittest.mock.html#patch-object) decorator.
This takes a class and method name and will override it with a class that will
allow us to specify a custom return value. You could also use this to specify
custom side effects (like throwing errors). This is great, now we can test the
`Barista`'s mocha making skills without having to have a working
`EspressoMachine`.

But we could take this one step further: How do we know if the `Barista` is
actually using the `EspressoMachine` at all? Luckily, `unittest.mock` provides 
us with some extra diagnostic goodies when we patch an object. Here's another
example:

```py
from unittest.mock import patch

class BaristaTest(unittest.TestCase):
  ...
  def TestMakeMocha():
    expectedDrink = ...
    e = EspressoMachine(...)
    with patch.object(EspressoMachine, 'MakeShot',
                    returnValue=EspressoShot()):
      assertEquals(barista.MakeMocha(e), expectedDrink)
      # Make sure that shot was called
      assert e.MakeShot.called
  ...
```

Now we're able to test if the `Barista` even calls the `EspressoMachine` at all.
Doing this allows you to not only black-box test the implementation of a method,
but allows you to make sure the correct side effects occur and correct functions
are called.

-T