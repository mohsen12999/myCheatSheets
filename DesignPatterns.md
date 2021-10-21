# Design Patterns

- base on `Design Patterns: Elements of Reusable Object-Oriented Software` write by GoF (Gang of four)
- 24 design pattern in 3 category: `Creational`, `Structural`, `Behavioral`
  - `Creational`: different way to create object
  - `Structural`: relationship between objects
  - `Behavioral`: interaction/commination between objects

## The Essentials

- Classes
- Interfaces - a contract that specifies the capabilities that a class should provide
- Encapsulation - bundling a data and methods to operate data and hiding the value and state
- Abstraction - reduce complexity by hiding unnecessary detail
- Inheritance
- Polymorphism - ability of object to get many difference forms
- UML - Unified Modeling Language

  - uml shape

  | Class Name                                |
  | ----------------------------------------- |
  | + Public Property <br> - Private Property |
  | + Public Method <br> - Private Method     |

  - inherit: arrow show the parent
  - composition relationship: arrow with diamond from the class to field, use directly as field
  - dependency relationship: - use in methods

- 3 type of relationship
  - inheritance
  - composition - use directly as field
  - dependency - dashed arrow - has reference to class, like injection

## Memento Pattern

best way for implementation undo

- momento: state class used like an interface
- originator: main class, use momento as state class, dependency relationship
- caretaker: list of state, with push and pop state method, composition relationship

```java
public class EditorState {
  private final content;

  public EditorState(String content) {
    this.content = content;
  }
  
  public getContent() {
    return content;
  }
}

public class Editor {
  private String content;

  public EditorState createState() {
    return new EditorState(content);
  }

  public void restore(EditorState state) {
    content = state.getState();
  }

  public setContent(String content) {
    this.content = content;
  }
  
  public getContent() {
    return content;
  }
}

public class history {
  private List<EditorState> states = new ArrayList<>();

  public void push(EditorState state) {
    states.add(state);
  }

  public EditorState pop() {
    var lastIndex = states.size() - 1;
    var lastState = states.get(lastIndex);
    states.remove(lastIndex);

    return lastState;
  }
}

public class Main {
  public static void main(String[] args) {
    var editor = new Editor();
    var history = new History();

    editor.setContent("a"); // a
    history.push(editor.createStat());

    editor.setContent("b"); // b
    history.push(editor.createStat());
    
    editor.setContent("c"); // c
    editor.restore(history.pop());// undo -> "b"
  }
}
```

## State Pattern

allow object behave different when state changes

- State - abstract class, not use directly in program, with handle methods
- Context
- Concrete states - classes inherit from State class and implement handle methods differently

## Reference

- [Design Patterns in Plain English | Mosh Hamedani](https://www.youtube.com/watch?v=NU_1StN5Tkk&t=63s)
