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

```java
public interface Tool {
  void MouseUp();
  void MouseDown();
}

public class SelectionTool implements Tool {
  @override
  void MouseUp() {
    system.out.println("Selection Icon")
  }

    @override
  void MouseDown() {
    system.out.println("Draw a dashed rectangle")
  }
}

public class BrushTool implements Tool {
  @override
  void MouseUp() {
    system.out.println("Brush Icon")
  }

  @override
  void MouseDown() {
    system.out.println("Draw a line")
  }
}

public class Canvas {
  public Tool currentTool;

  void MouseUp() {
    currentTool.MouseUp();
  }

  void MouseDown(){
    currentTool.MouseDown();
  }

  public Tool getCurrentTool() { return currentTool; }
  public void setCurrentTool(Tool currentTool) { this.currentTool = currentTool; }
}

public class Main {
  public static void main(String[] args) {
    var canvas = Canvas();
    canvas.setCurrentTool(new SelectionTool());
    canvas.MouseUp(); // Selection Icon
    canvas.MouseDown(); // Draw a dashed rectangle
  }
}
```

## Iterator Pattern

- allow to implement history in different shapes

- history class only have push and pop
- iterator class as interface for implementation
- implementation in different shape

```java
public interface Iterator { // Iterator<T>
  boolean hasNext();
  String current(); // T current();
  void next();
}

public class BrowserHistory {
  private List<String> urls = new ArrayList();

  public void push(String url) { urls.add(url); }

  public String pop() {
    var lastIndex = urls.size();
    var latUrl = urls.get(lastIndex);
    urls.remove(lastUrl);

    return lastUrl;
  }

  public Iterator createIterator() {
    return new ListIterator(this)
  }

  public class ListIterator implements Iterator {
    private BrowserHistory history;
    private int index;
    public ListIterator(BrowserHistory history) {
      this.history = history;
    }

    @override
    boolean hasNext(){
      return (index < history.urls.size());
    }

    @override
    String current() {
      return history.urls.get(index);
    }

    @override
    void next() {
      index++;
    }
  }
}

public class Main {
  public static void main(String[] args) {
    var history = new BrowserHistory();
    history.push("a");
    history.push("b");
    history.push("c");

    Iterator iterator = history.createIterator();
    while(iterator.hasNext()) {
      var url = iterator.current();
      system.out.println(url);
      iterator.next();
    }
  }
}
```

## Strategy Pattern

- use when you need to choose different strategy with polymorphisms
- similar to state strategy but not depend on state

```java
public interface Compressor {
  // byte[] compressor(byte[] image);
  void compress(String fileName);
}

public class JpegCompressor implements Compressor {
  @override
  void compress(String fileName) {
    system.out.println("Compressing using JPEG")
  }
}

public class PngCompressor implements Compressor {
  @override
  void compress(String fileName) {
    system.out.println("Compressing using PNG")
  }
}

public interface Filter {
  void apply(String fileName);
}

public class BlackAndWhiteFilter implements Filter {
  @override
  void apply(String fileName) {
    system.out.println("Applying B&W filter")
  }
}

public class ImageStorage {
  // first way
  // private Compressor compressor;
  // private Filter filter;

  // public ImageStorage(Compressor compressor, Filter filter) {
  //   this.compressor = compressor;
  //   this.filter = filter;
  // }

  // public void store(String fileName) {
  //   compressor.compress(fileName);
  //   filter.apply(fileName);
  // }

  // second way
  public void store(String fileName, Compressor compressor, Filter filter) {
    compressor.compress(fileName);
    filter.apply(fileName);
  }
}


public class Main {
  public static void main(String[] args) {
    // var imageStorage = new ImageStorage(new JpegCompressor(), new BlackAndWhiteFilter());
    // imageStorage.store("a");
    var imageStorage = new ImageStorage();
    imageStorage.store("a", new JpegCompressor(), new BlackAndWhiteFilter());
  }
}
```

## Template Method Pattern

- using inheritance for preventing duplication method in classes

```java
public abstract class Task {
  public void record() {
    system.out.println("Audit");
  }
}

public abstract class Task {
  private AuditTrail auditTrail;
  
  public Task() {
    this.auditTrail = new AuditTrail();
  }

  public Task(AuditTrail auditTrail) {
    this.auditTrail = auditTrail;
  }
  
  public void execute() {
    auditTrail.record();

    doExecute();
  }

  protected abstract void doExecute(); // protect prevent it to use directly
}

public class TransferMoneyTask implements Task {
  // public TransferMoneyTask(AuditTrail auditTrail) {
  //   super(auditTrail);
  // }

  @override
  public void doExecute() {
    system.out.println("Transfer money")
  }
}

public class Main {
  public static void main(String[] args) {
    var task = new TransferMoneyTask();
    task.execute();
  }
}
```

## Reference

- [Design Patterns in Plain English | Mosh Hamedani](https://www.youtube.com/watch?v=NU_1StN5Tkk&t=63s)