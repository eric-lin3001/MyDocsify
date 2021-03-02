##### Polymorphism(多态)



1. ###### What is Polymorphism?

```java
// the code below shows a kind of polymorphism, food is data type,since tuna is inherited from food class, can be assigned to bucky(a reference variable).
// Also, it's called ”variable 'bucky' holds object 'tuna'“
Food bucky = new Tuna();
```

2. ###### Why we need it?

   - Polymorphism Array: When we need to call the same method from multiple subclasses, using Polymorphism is convenient and clean:

     ```java
     // Not Using Polymorphism:
     Tuna tuna = new Tuna();
     Tuna.eat();
     Potpie potpie = new Potpie();
     Potpie.eat();
     
     //Using Polymorphism:
     Food[] buckyArray = new Food[2];
     buckyArray[0] = new Tuna();
     buckyArray[1] = new Potpie();
     for(int i=0;i<2;i++){
       buckyArray[i].eat();
     }
     ```

   - Use Polymorphism in argument of a method:

     ```java
     //Fatty class:
     
     public void digest(Food food){
       food.eat();
     }
     
     // Main Class:
     Fatty fatty = new Fatty();
     Food food = new Food();
     Food tuna = new Tuna(); // Or Tuna tuna = new Tuna();
     Food potpie = new Potpie(); // Or Potpie potpie = new Potpie(); 
     
     fatty.digest(food);
     fatty.digest(tuna);
     fatty.digest(potpie);
     ```

   - Holding same type in an array, and it's convenient:

     ```java
     Food[] foods = new Food[2];  // Or Food foods[] = new Food[2]; Both representations are ok.
     foods[0] = new Tuna();
     foods[1] = new Potpie();
     
     for(Food food:foods){
       food.eat();
     }
     ```

     