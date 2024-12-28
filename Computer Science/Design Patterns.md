# Design Patterns Reference Sheet

## Creational Patterns

### Singleton
Ensures a class has only one instance and provides a global point of access to it.

```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
    
    # Thread-safe version
    @classmethod
    def instance(cls):
        if not hasattr(cls, "_instance"):
            with cls._lock:
                if not hasattr(cls, "_instance"):
                    cls._instance = cls()
        return cls._instance
```

**Use Cases:**
- Database connections
- Configuration managers
- Logging services

### Factory Method
Defines an interface for creating objects but lets subclasses decide which class to instantiate.

```python
from abc import ABC, abstractmethod

class Creator(ABC):
    @abstractmethod
    def factory_method(self):
        pass

    def some_operation(self):
        product = self.factory_method()
        return product.operation()

class ConcreteCreator1(Creator):
    def factory_method(self):
        return ConcreteProduct1()

class ConcreteCreator2(Creator):
    def factory_method(self):
        return ConcreteProduct2()
```

**Use Cases:**
- Document generators
- UI element creation
- Platform-specific component creation

### Abstract Factory
Provides an interface for creating families of related or dependent objects.

```python
class AbstractFactory(ABC):
    @abstractmethod
    def create_product_a(self):
        pass

    @abstractmethod
    def create_product_b(self):
        pass

class ConcreteFactory1(AbstractFactory):
    def create_product_a(self):
        return ConcreteProductA1()
    
    def create_product_b(self):
        return ConcreteProductB1()
```

**Use Cases:**
- Cross-platform UI toolkits
- Multiple database support
- Different rendering engines

### Builder
Separates the construction of a complex object from its representation.

```python
class Builder:
    def __init__(self):
        self.reset()

    def reset(self):
        self._product = Product()

    @property
    def product(self):
        product = self._product
        self.reset()
        return product

    def build_part_a(self):
        self._product.add("Part A")

    def build_part_b(self):
        self._product.add("Part B")

class Director:
    def __init__(self):
        self._builder = None

    @property
    def builder(self):
        return self._builder

    @builder.setter
    def builder(self, builder):
        self._builder = builder

    def build_minimal_product(self):
        self.builder.build_part_a()

    def build_full_product(self):
        self.builder.build_part_a()
        self.builder.build_part_b()
```

**Use Cases:**
- Complex object construction
- Document generation
- Configuration builders

### Prototype
Creates new objects by cloning an existing object, known as the prototype.

```python
import copy

class Prototype:
    def clone(self):
        return copy.deepcopy(self)

class ConcretePrototype(Prototype):
    def __init__(self, value):
        self.value = value
```

**Use Cases:**
- Object copying with complex state
- Reducing class explosion
- Configuration templates

## Structural Patterns

### Adapter
Allows incompatible interfaces to work together by wrapping an object in an adapter.

```python
class Target:
    def request(self):
        return "Target: Default behavior"

class Adaptee:
    def specific_request(self):
        return "Specific behavior"

class Adapter(Target):
    def __init__(self, adaptee):
        self._adaptee = adaptee

    def request(self):
        return f"Adapter: {self._adaptee.specific_request()}"
```

**Use Cases:**
- Legacy system integration
- Third-party library integration
- Interface compatibility

### Bridge
Separates an abstraction from its implementation so that both can vary independently.

```python
class Implementation(ABC):
    @abstractmethod
    def operation_implementation(self):
        pass

class Abstraction:
    def __init__(self, implementation):
        self.implementation = implementation

    def operation(self):
        return self.implementation.operation_implementation()
```

**Use Cases:**
- Platform-independent features
- Multiple orthogonal dimensions
- Device drivers

### Composite
Composes objects into tree structures to represent part-whole hierarchies.

```python
class Component(ABC):
    @abstractmethod
    def operation(self):
        pass

class Leaf(Component):
    def operation(self):
        return "Leaf"

class Composite(Component):
    def __init__(self):
        self._children = []

    def add(self, component):
        self._children.append(component)

    def operation(self):
        results = []
        for child in self._children:
            results.append(child.operation())
        return f"Branch({'+'.join(results)})"
```

**Use Cases:**
- File system structures
- GUI components
- Organization hierarchies

### Decorator
Attaches additional responsibilities to objects dynamically.

```python
class Component(ABC):
    @abstractmethod
    def operation(self):
        pass

class ConcreteComponent(Component):
    def operation(self):
        return "ConcreteComponent"

class Decorator(Component):
    def __init__(self, component):
        self._component = component

    def operation(self):
        return self._component.operation()
```

**Use Cases:**
- Adding features to objects
- Input/Output streams
- UI component enhancement

### Facade
Provides a unified interface to a set of interfaces in a subsystem.

```python
class Subsystem1:
    def operation1(self):
        return "Subsystem1: Ready!"

class Subsystem2:
    def operation2(self):
        return "Subsystem2: Ready!"

class Facade:
    def __init__(self):
        self._subsystem1 = Subsystem1()
        self._subsystem2 = Subsystem2()

    def operation(self):
        results = []
        results.append(self._subsystem1.operation1())
        results.append(self._subsystem2.operation2())
        return "\n".join(results)
```

**Use Cases:**
- Complex system simplification
- Library wrapping
- Service integration

### Proxy
Provides a surrogate or placeholder for another object to control access to it.

```python
class Subject(ABC):
    @abstractmethod
    def request(self):
        pass

class RealSubject(Subject):
    def request(self):
        return "RealSubject: Handling request"

class Proxy(Subject):
    def __init__(self, real_subject):
        self._real_subject = real_subject

    def request(self):
        if self.check_access():
            return self._real_subject.request()
        return "Proxy: Access denied"

    def check_access(self):
        return True
```

**Use Cases:**
- Lazy loading
- Access control
- Remote resource access

## Behavioral Patterns

### Observer
Defines a one-to-many dependency between objects.

```python
class Subject:
    def __init__(self):
        self._observers = []
        self._state = None

    def attach(self, observer):
        self._observers.append(observer)

    def detach(self, observer):
        self._observers.remove(observer)

    def notify(self):
        for observer in self._observers:
            observer.update(self._state)

class Observer(ABC):
    @abstractmethod
    def update(self, state):
        pass
```

**Use Cases:**
- Event handling
- User interface updates
- Publication/Subscription systems

### Strategy
Defines a family of algorithms and makes them interchangeable.

```python
class Strategy(ABC):
    @abstractmethod
    def execute(self, data):
        pass

class Context:
    def __init__(self, strategy):
        self._strategy = strategy

    def set_strategy(self, strategy):
        self._strategy = strategy

    def execute_strategy(self, data):
        return self._strategy.execute(data)
```

**Use Cases:**
- Sorting algorithms
- Payment methods
- Compression algorithms

### Command
Encapsulates a request as an object.

```python
class Command(ABC):
    @abstractmethod
    def execute(self):
        pass

class Invoker:
    def __init__(self):
        self._commands = []

    def add_command(self, command):
        self._commands.append(command)

    def execute_commands(self):
        for command in self._commands:
            command.execute()
```

**Use Cases:**
- GUI actions
- Transaction systems
- Command queuing

### State
Allows an object to alter its behavior when its internal state changes.

```python
class State(ABC):
    @abstractmethod
    def handle(self):
        pass

class Context:
    def __init__(self, state):
        self._state = state

    def transition_to(self, state):
        self._state = state

    def request(self):
        self._state.handle()
```

**Use Cases:**
- Workflow management
- Game state management
- Document state

### Template Method
Defines the skeleton of an algorithm in a method, deferring some steps to subclasses.

```python
class AbstractClass(ABC):
    def template_method(self):
        self.step1()
        self.step2()
        self.hook()

    @abstractmethod
    def step1(self):
        pass

    @abstractmethod
    def step2(self):
        pass

    def hook(self):
        pass
```

**Use Cases:**
- Framework development
- Algorithm standardization
- Application flow control

### Iterator
Provides a way to access elements of a collection sequentially.

```python
class Iterator(ABC):
    @abstractmethod
    def next(self):
        pass

    @abstractmethod
    def has_next(self):
        pass

class Collection:
    def __init__(self):
        self._items = []

    def get_iterator(self):
        return ConcreteIterator(self._items)
```

**Use Cases:**
- Collection traversal
- Custom iteration patterns
- Data stream processing

### Mediator
Defines an object that encapsulates how a set of objects interact.

```python
class Mediator(ABC):
    @abstractmethod
    def notify(self, sender, event):
        pass

class Component:
    def __init__(self, mediator):
        self._mediator = mediator

    def send(self, event):
        self._mediator.notify(self, event)
```

**Use Cases:**
- GUI component communication
- Air traffic control
- Chat room systems

### Chain of Responsibility
Passes requests along a chain of handlers.

```python
class Handler(ABC):
    def __init__(self):
        self._next_handler = None

    def set_next(self, handler):
        self._next_handler = handler
        return handler

    @abstractmethod
    def handle(self, request):
        if self._next_handler:
            return self._next_handler.handle(request)
        return None
```

**Use Cases:**
- Event handling
- Logging systems
- Request processing

## Implementation Considerations

### Pattern Selection Guidelines
1. **Problem Analysis**
   - Identify core issues
   - Consider maintainability
   - Evaluate flexibility needs

2. **Pattern Evaluation**
   - Match problem to pattern intent
   - Consider pattern trade-offs
   - Evaluate implementation complexity

3. **Implementation Strategy**
   - Start simple
   - Refactor gradually
   - Document decisions

### Anti-Patterns to Avoid
1. Pattern Overuse
2. Forced Pattern Fit
3. Pattern Misapplication
4. Overengineering

### Best Practices
1. Keep It Simple
2. Document Pattern Usage
3. Consider Maintainability
4. Balance Flexibility and Complexity
