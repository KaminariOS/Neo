# What is PECS (Producer Extends Consumer Super)?

Producer here means a generic collection that only supports `get()` operation but neither `set()` or `add()` operation, while consumer means the opposite.

In Java, there is no inheritance relationship between `Collection<A>` and `Collection<B>` even if class `B` subclasses class `A`. For example:

```Java
class Animal{}
class Panda extends Animal{}
public class Pecs {
     void test(){
         List<Animal> animals = new ArrayList<Panda>();
     } // Compilation error.
}
```

In order to make a generic collection be able to store any subtypes of `Animal`, we have to use generic wildcard `?`. For example:

```Java
class Animal{}
class Panda extends Animal{}
public class Pecs {
     void test(){
         List<? extends Animal> animals = new ArrayList<Panda>(); // No compilation error.
         Animal animal = animals.get(0);
         // No compilation error.
         animals.add(new Panda()); // Compilation error.
         animals.add(new Animal()); // Compilation error.
     }
}
```

By definition, the wildcard generic version of `animals` is obviously a producer. At first glance, it makes no sense that a collection of subtypes of `Animal` cannot accept a new  `Panda`. However, what happens if 
