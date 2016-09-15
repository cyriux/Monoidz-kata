# Food !

*by Cyrille Martraire, based on the Kebab kata from Romeu Moura*

Let’s talk about food, from a nutrition facts perspective.

You have ingredients: salad, cheese, tomato, bread, ham, fish… that you can combine in order to make a delicious Panini.

Each ingredient can be described by its diet compatibilities: vegan, vegetarian, or pescetarian, its production conditions: organic or not, and has its own nutrition facts : calories, fat, salt and carbohydrates amounts (and many more). There are additional food items like drinks and deserts which can help create a meal together with a panini.

We want to derive the nutrition facts of any kind of Panini and for any meal meals built from these ingredients and food items.

 

# Initial exploration

Salad is vegan, vegetarian, and pescetarian. It’s organic. Its nutrition facts are fat:0, salt:0, calories: 50.
Cheese is not vegan, vegetarian, and pescetarian. It’s not organic. Its nutrition facts are fat:80, salt:0, calories: 20000.
Bread is vegan, vegetarian, and pescetarian. It’s organic. Its nutrition facts are fat:2, salt:0.2, calories: 100000.
Ham is not vegan, not vegetarian, and not pescetarian. It’s not organic. Its nutrition facts are fat:150, salt:0.1, calories: 30000.

1. Start coding 2 ingredients, test-first (not TDD), in exploration mode
1. Propose and discuss a way to code the calculation of the nutrition facts for a simple Panini.
1. Propose a refactoring towards a well-known design pattern.

# The Monoid way

Monoids are a ‘set’ and an ‘operation’ with specific properties: closure of the operation on the set, associativity, and neutral element.

In practice, monoids enable an arithmetic style, à la Object + Object = Object.

1. Ask for a demo with glasses of beer to understand the abstract idea in a concrete way.
1. Discuss common examples of monoids that you know already.
1. Try to turn the food example into a monoid fashion.
1. Refactor the tests to simplify the assertions in a style: “assert C = A + B”
 
# Extend!

Now we want to calculate more facts:

- the nutrition numbers in percent of the weight
- daily nutrition ratios
- ingredients list for paninis and meals
- allergy risks warnings for paninis and meals

How easy can you extend the design to cope with these changes? Discuss and compare to other approaches.

