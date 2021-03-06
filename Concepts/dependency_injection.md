Dependency Injection follows dependency Inversion Principle.

Dependency Injection a 25 dollar term for a 5-cent concept. It is nothing but giving an object its instance variables. 

-Real Life Example.

-Introduction + Technical Example with Code.


Dependency injection is basically providing the objects that an object needs (its dependencies) instead of having it construct them itself. It's a very useful technique for testing, since it allows dependencies to be mocked or stubbed out. Basically, instead of having your objects creating a dependency or asking a factory object to make one for them, you pass the needed dependencies in to the object externally, and you make it somebody else's problem.


So in the end Dependency injection is just a technique for achieving loose coupling between objects and their dependencies. Rather than directly instantiating dependencies that class needs in order to perform its actions, dependencies are provided to the class (most often) via constructor injection.

// NO DI
public SomeClass() {
    myObject = Factory.getObject();
}

//DI 
public SomeClass (MyClass myObject) {
    this.myObject = myObject;
}


 
-Ways to achieve.

1. Frameworks
2. via the Constructors
3. Setters and Getters
4. Classes explicitly implement an interface for the dependencies they wish injected.

-Benefits and Applications where it is used/applied.
One of the major advantages of dependency injection is that it can make testing lots easier. 
Loose Coupling


/************* BEST EXPLANATION AND EXAMPLE*************/

Code without dependency injection


public class Car
{
    public Car()
    {
        GasEngine engine = new GasEngine();
        engine.Start();
    }
}

public class GasEngine
{
    public void Start()
    {
        Console.WriteLine("I use gas as my fuel!");
    }
}

and run it like : Car car = new Car();

The issue with this code that we tightly coupled to GasEngine and if we decide to change it to ElectricityEngine then we will need to rewrite Car class. And the bigger the application the more issues and headache we will have to add and use new type of engine.

Here we are violating dependency inversion principle. We are dependent on concretions and not on abstractions. In other words with this approach is that our high level Car class is dependent on the lower level GasEngine class which violate Dependency Inversion Principle(DIP) from SOLID. DIP suggests that we should depend on abstractions, not concrete classes.

//introduce this interface. This will act as controller.
 public interface IEngine
    {
        void Start();
    }

    public interface IEngine
    {
        void Start();
    }

    public class GasEngine : IEngine
    {
        public void Start()
        {
            Console.WriteLine("I use gas as my fuel!");
        }
    }

    public class ElectricityEngine : IEngine
    {
        public void Start()
        {
            Console.WriteLine("I am electrocar");
        }
    }

    public class Car
    {
        private readonly IEngine _engine;
        public Car(IEngine engine)
        {
            _engine = engine;
        }

        public void Run()
        {
            _engine.Start();
        }
    }


   //Dependency Injection
   Car gasCar = new Car(new GasEngine());
   gasCar.Run();
   Car electroCar = new Car(new ElectricityEngine());
   electroCar.Run(); 
   

