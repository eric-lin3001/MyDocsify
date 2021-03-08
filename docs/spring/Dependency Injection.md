##### Dependency Injection



###### DI Demo:

- Java: 

```java
// Before
Triangle t = new Triangle();
t.setHeight("20")
// Now
// Main Class
ApplicationContext context = new ClassPathXmlApplicationContext("src/spring.xml");
Triangle triangle1 = (Triangle) context.getBean("tri");

```

- Triangle.class:

```java
public class Triangle {

    int height;

//    public void setHeight(int height) {
//        this.height = height;
//    }

    public Triangle(int height) {
        this.height = height;
    }

    public void draw(){
        System.out.println(String.format("Triangle Drawn with height %s!", height));
    }
}
```

- spring.xml:

  - Using 'property' tag(Prerequisite: height setter in Triangle.class):

    ```xml
    // property name here should be identical with member varoable name in Triangle.class!
    <beans>
        <bean id="triangle" class="com.sf.me.Triangle">
            <property name="height" value="20"></property>
        </bean>
    </beans>
    ```

  - Using 'constructor-args' tag(Prerequisite: A corresponding constructor):  

    ```xml
    <beans>
        <bean id="triangle" class="com.sf.me.Triangle">
            <constructor-arg value="20"></constructor-arg>
        </bean>
    </beans>
    ```

    

###### Benefits of DI:

Code is cleaner with the DI principle, and decoupling is more effective when objects are provided with their dependencies. 

The object does not look up its dependencies and does not know the location or class of the dependencies. 

###### **As a result, your classes become easier to test

,particularly when the dependencies are on interfaces or abstract base classes, which allow for stub or mock implementations to be used in unit tests.