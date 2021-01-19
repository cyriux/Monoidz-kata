# Monoids with Property-Based Testing

## The problem

Consider a simple stock management domain, with similar goods (items) in multiple warehouses.

For a given item to be ordered, its stock across 2 warehouses is the sum of its stock in each warehouse:

```
		assertEquals(new Stock(50), new Stock(20).combine(new Stock(30)));
```

Let's make that into one simple unit test on some hardcoded example values:

```
	@Test
	public void theTotalStockIsTheSumOfEachStocks() {
		assertEquals(new Stock(50), new Stock(20).combine(new Stock(30)));
	}
```

*TASK: Make this test pass by creating the simplest Stock class (constructor, equals, hashcode and toString for our own convenience)*

## Closure of Operations

If we generalize the previous assertion we can define an interesting property called the Closure of the Operation in the DDD book: "The type method signatures are all about the type itself as parameters and return types, and nothing else but primitives". 

Another way to express that property is "given any 2 values (instances) of the type, combining them still gives us an instance of that type". Let's make this property explicit in another dedicated automated test, using random values (instances):

```
	@Test 
	public void closureOfOperation() {
		final Stock a = forAnyStock();
		final Stock b = forAnyStock();
		assertTrue(a.combine(b) instanceof Stock);
	}
	
	private static Stock forAnyStock() {
		return new Stock((int) (Math.random() * 100)); // stock from 0 to 100
	}
```

Verifying that this holds true for every possible value is mostly the job of the compiler here, unless the operation can throw exceptions, hence the test, which also acts as a documentation here.

Turns out that the stock of zero quantity doesn't change the result when added to any other stock a: **a + 0 = a**. Let's now write that literally as an automated test: "for any value of stock, combining it with the stock zero gives the same stock":

```
		final Stock a = forAnyStock();
		assertEquals(a, a.combine(new Stock(0)));
```

This is another interesting property of the special element new Stock(0) that is called the NEUTRAL element. We can make it explicit by introducing this element as a constant and by naming this automated test accordingly:

```
	@Test
	public void neutralElement() {
		final Stock a = forAnyStock();
		assertEquals(a, a.combine(Stock.NEUTRAL)); // combine right
		assertEquals(a, Stock.NEUTRAL.combine(a)); // combine left
	}
```

Lastly, it doesn't matter how we combine the various stock together, since obviously **for any a, b, c, then a + (b + c) = (a + b) + c)**. Let's verify that again literally as an automated test:

```
        final Stock a = forAnyStock();
	final Stock b = forAnyStock();
	final Stock c = forAnyStock();
	assertEquals(a.combine(b).combine(c), a.combine(b.combine(c)));
```

This property doesn't look that exciting, but it is. In practice it means that one could precompute partial results **arbitrarily** within the multiple cells of the warehouses or across regions or countries and then **still be able to derive the correct result** from them all. This property is called **associativity** and is fundamental for everything data-intensive (think map-reduce). Let's now rename the test accordingly:

```
	@Test
	public void associativity() {
		final Stock a = forAnyStock();
		final Stock b = forAnyStock();
		final Stock c = forAnyStock();
		assertEquals(a.combine(b).combine(c), a.combine(b.combine(c)));
	}
```

## Summing it up so far: Monoids + Property-based Testing from scratch

So what do we have now? We have one simple class that works with one method and a special value that together verify the properties: 

- Closure of Operations
- Neutral element
- Associativity

And we know these properties really hold because we have automated tests that continously verify them for any value, using randomness. The more you run the tests, the more diverse values are tested, so yo gain confidence.

**Congratulations! You've just re-created a monoid and a property-based testing tool all by yourself!**

Of course our example is very minimal, in two ways:

1. **Trival Monoid example**: The class considered is so trivial we don't see much benefits of monoids so far; expanding the business into more complicated behavior would exhibit the benfits more visibly.
1. **Poor-Man PBT Tooling**: The randomness in the tests is managed by hand, only one case at a time, the tests don't strictly conform to what "unit tests" should be, so it's all a very limited form of property-based testing; Moving to specialized PBT tools offer the convenience of more readable code, testing multiple cases on each run, and would feature the very nice "shrinking" capability to better interpret what's happening whenever a property is not verified for some values.

In the following steps we can explore and expand both directions (more complicated domain behavior, or/hand using PBT tools) at your wish.

## Further steps into using serious PBT tools

A bootstrap for Js by [Mathieu](https://twitter.com/meveillard) is available here: https://github.com/mathieueveillard/js-kata-starter-pbt

## Further Steps into more interesting monoids

**without changing any of the 3 existing automated property tests** to stay with a monoid! 

- keep track of the min stock across all combined stocks
- keep track of the average stock (and std deviation of the stock) across all the combined stocks
- manage more than on good, by having stocks of multiple SKU

And switching to more diverse examples of other domains as well.


## The monoid implementation (spoiler of the first step of the exercise)


```
public static class Stock {

	public static final Stock NEUTRAL = new Stock(0);

	private final int quantity;

	public Stock(int quantity) {
		this.quantity = quantity;
	}

	public Stock combine(Stock other) {
		return new Stock(quantity + other.quantity);
	}

	@Override
	public int hashCode() {
		return quantity ^ 31;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		final Stock other = (Stock) obj;
		return quantity == other.quantity;
	}

	@Override
	public String toString() {
		return "" + quantity;
	}
}
```

# Further nice reading

As part of a great series on PBT, very extensive material: 
https://blog.johanneslink.net/2018/07/16/patterns-to-find-properties/

