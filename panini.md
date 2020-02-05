# Food !

*by Cyrille Martraire, based on the Kebab kata from Romeu Moura*

Let’s talk about food, from the perspective of **diet compatibilities** & **nutrition facts**.

You have **ingredients**: salad, cheese, tomato, bread, ham, fish… that you can combine in order to make a delicious **Panini**.

Each ingredient can be described by its diet compatibilities: vegan, vegetarian, or pescetarian, whether it's organic or not, and it has its own nutrition facts : calories, fat, salt and carbohydrates amounts (and many more). T

here are additional food items like drinks and deserts which can help create a meal together with a panini.

We want to derive the diet compatibilities & nutrition facts of any kind of Panini and for any meal built from these ingredients and food items.


# Initial exploration

Here are sample data:

- Salad is vegan, vegetarian, and pescetarian. It’s organic. Its nutrition facts are fat:0, salt:0, calories: 50.
- Cheese is not vegan, but is vegetarian and pescetarian. It’s not organic. Its nutrition facts are fat:80, salt:0, calories: 20000.
- Bread is vegan, vegetarian, and pescetarian. It’s organic. Its nutrition facts are fat:2, salt:0.2, calories: 100000.
- Ham is not vegan, not vegetarian, and not pescetarian. It’s not organic. Its nutrition facts are fat:150, salt:0.1, calories: 30000.

1. Explore how to code the calculation of a panini with just 2 ingredients. You may do it test-first.
1. Propose a refactoring towards a well-known design pattern.

# The Monoid way

Monoids are a ‘set’ and an ‘operation’ with specific properties: closure of the operation on the set, associativity, and neutral element.

In practice, monoids enable an arithmetic style, à la Object + Object = Object.

1. Ask for a demo with glasses of beer to understand the abstract idea in a concrete way.
1. Discuss common examples of monoids that you know already.
1. Try to turn the food example into a monoid fashion, into this style of assertions: “assert C = A + B”
 
# Extend!

Now we want to go further (depending on the time you have and your audacity):

- Express the nutrition numbers in *percent of the weight*
- Calculate the diet compatibilities *proportions* & *average* nutrition facts over millions of various meals served over a year
- Check if a meal is locally produced (all ingredient producers are located *within 100 kms*)
- Given that the facts results are already calculated for millions of meals, how to fix the results when you find out one particular meal was wrong *without recalculating it all*?

How easily can you extend the design to cope with these changes? Discuss and compare to other approaches.

