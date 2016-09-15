## Solutions (don’t cheat, don’t look in advance!)

    public Food(isVegan, isVegetarian, isPescetarian, isOrganic, calories, fat)

In Java, C# or PHP monoids need to be Value Objects (values, immutable, equality by value), with no inheritance hierarchy. Or troubles arise.

    public final static Food NONE = new Food (true, true, true, true, 0, 0) // neutral element for and()

    public Food and(Food)

Given a list of Food items, just stream() and fold with ::and to combine them all

Need to introduce an equality based on the nutrition facts. Assert Panini = bread and salad and  tomato and cheese and fish.

Ratios don’t compose; instead accumulate the weight and the amounts, and derive the ratios at the last time. Same thing for averages and standard deviations with count, sum, and sumSquared.

Ingredient list simply compose with an internal list that grows by concatenation. Same thing for generated labels if needed. Allergy ingredients are like the ingredient list but filtered by isKnownAllergen(). Daily nutrition ratios need to be given a Persona with its own nutrition facts.
