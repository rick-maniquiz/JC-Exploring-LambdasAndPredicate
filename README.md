# Exploring Java Lambdas and Predicate

### Cadet Name: Rafael Nico T. Maniquiz

-----

### Exercise 1: The "New Way" - A Simple Lambda Expression

Now let's do the exact same thing, but with the clean syntax of a lambda expression.

**Code Snippet:**

```java
import java.util.function.Predicate;

public class LambdaLab {
    public static void main(String[] args) {
        // Create the same Predicate using a lambda expression.
        Predicate<String> isLong = s -> s.length() > 10;

        String str1 = "short";
        String str2 = "This is a very long string";

        System.out.println("Is '" + str1 + "' long? " + isLong.test(str1));
        System.out.println("Is '" + str2 + "' long? " + isLong.test(str2));
    }
}
```

**1. Prediction:**

```
Is 'short' long? false
Is 'This is a very long string' long? true
```

**2. Observation:**

<img src="https://github.com/rick-maniquiz/JC-Exploring-LambdasAndPredicate/blob/0c24f03a48297e88479966738fe85bf06758ef88/screenshots/1.png"/>

-----

### Exercise 3: Using Predicates to Filter a List

The real power of lambdas comes from passing them as arguments to other methods. Here, we'll write a method that filters a list based on any `Predicate` we give it.

**Code Snippet:**

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class LambdaLab {

    // A helper method to print the results of our filtering
    public static void filterAndPrint(List<String> list, Predicate<String> predicate, String description) {
        System.out.println("--- " + description + " ---");
        for (String item : list) {
            // Use the predicate's test method to filter
            if (predicate.test(item)) {
                System.out.println(item);
            }
        }
        System.out.println(); // Add a blank line for readability
    }

    public static void main(String[] args) {
        List<String> callSigns = new ArrayList<>();
        callSigns.add("Alpha");
        callSigns.add("Bravo");
        callSigns.add("Archangel");
        callSigns.add("Echo");
        callSigns.add("Avenger");

        // Define a predicate with a lambda to find call signs starting with "A"
        Predicate<String> startsWithA = s -> s.startsWith("A");

        // Pass the list and the predicate (the behavior) to our method
        filterAndPrint(callSigns, startsWithA, "Call signs starting with 'A'");
    }
}
```

**1. Prediction:**

```
--- Call signs starting with 'A' ---
Alpha
Archangel
Avenger

```

**2. Observation:**

<img src="https://github.com/rick-maniquiz/JC-Exploring-LambdasAndPredicate/blob/0c24f03a48297e88479966738fe85bf06758ef88/screenshots/3.png"/>

-----

### Exercise 4: Chaining Predicates (`and`, `negate`)

You can combine simple predicates to create more complex ones.

**Code Snippet:**

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

public class LambdaLab {

    // Re-using the filterAndPrint method from the previous exercise
    public static void filterAndPrint(List<String> list, Predicate<String> predicate, String description) {
        System.out.println("--- " + description + " ---");
        for (String item : list) {
            if (predicate.test(item)) {
                System.out.println(item);
            }
        }
        System.out.println();
    }

    public static void main(String[] args) {
        List<String> callSigns = new ArrayList<>();
        callSigns.add("Alpha");
        callSigns.add("Bravo");
        callSigns.add("Archangel");
        callSigns.add("Echo");
        callSigns.add("Avenger");

        Predicate<String> startsWithA = s -> s.startsWith("A");
        Predicate<String> hasLengthGreaterThan5 = s -> s.length() > 5;

        // Let's find call signs that start with 'A' AND have a length > 5
        Predicate<String> complexCondition = startsWithA.and(hasLengthGreaterThan5);
        filterAndPrint(callSigns, complexCondition, "Starts with 'A' AND length > 5");

        // Now let's find call signs that do NOT start with 'A'
        Predicate<String> doesNotStartWithA = startsWithA.negate();
        filterAndPrint(callSigns, doesNotStartWithA, "Does NOT start with 'A'");
    }
}
```

**1. Prediction:**

```
--- Starts with 'A' AND length > 5 ---
Archangel
Avenger

--- Does NOT start with 'A' ---
Bravo
Echo

```

**2. Observation:**

<img src="https://github.com/rick-maniquiz/JC-Exploring-LambdasAndPredicate/blob/0c24f03a48297e88479966738fe85bf06758ef88/screenshots/4.png"/>