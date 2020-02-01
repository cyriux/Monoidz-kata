## Solutions (don’t cheat, don’t look in advance!)

    public Food(isOrganic, calories, fat, salt)

In Java, C# or PHP monoids need to be Value Objects (values, immutable, equality by value), with no inheritance hierarchy. Or troubles arise.

    public final static Food NONE = new Food (true, 0, 0, 0) // neutral element for and()

    public Food and(Food other){
      return new Food(isOrganic && other.isOrganic, calories + other.calories, fat + other.fat, salt + other.salt);
    }

Given a list of Food items, just stream() and fold with ::and to combine them all

Need to introduce an equality based on the nutrition facts:

    AssertEquals(panini, bread.and(salad).and(tomato).and(cheese).and(fish));

Ratios don’t compose; instead accumulate the weight and the amounts, and derive the ratios at the last time:

    public Food(isOrganic, calories, fat, salt, weight)
    public double saltPer100g(){return 100 * salt / weight ;}

For averages and standard deviations; single values need to be promoted to another nested monoid that keeps track of the accumulated count, sum, and sumSquared:

    public Stats(count, sum, and sumSquared)
        public static from(value){
           this(1, value, value * value);}
        public Stats append(Stats other){
          return new Stats(count + other.count, sum + other.sum, sumSquared + other.sumSquared);}
        public double total(){return sum;}
        public double average(){return sum / count;}
        public double stdDev(){return sumSquared - (sum *  sum) / count;}
    
    public Food(Stats isOrganic, Stats calories, Stats fat, Stats salt, Stats weight)
    
    public Food and(Food other){
      return new Food(isOrganic.append(other.isOrganic), calories.append(other.calories), fat.append(other.fat), salt.append(other.salt));
    }
    
Ingredient list simply compose with an internal set (or map) that grows by concatenation (addAll() or putAll())

    public Food(Stats salt, Set ingredients)
    public Food and(Food other){
      return new Food(salt.append(other.salt), ingredients.addAll(other.ingredients));
    }

Daily nutrition ratios need to be given a Persona with its own nutrition facts.

To exclude an element, the monoid needs to be promoted to a group, with an operation that must always return an inverse. 
