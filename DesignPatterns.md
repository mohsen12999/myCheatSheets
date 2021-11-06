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

## Command Pattern

- invoker: the class run the method
- command: interface of method
- concreteCommand: method class implement the command interface
- receiver: class determine the job/method use concreteCommand

```java
public interface Command { // Command
  public void execute();
}

public class Button { // invoker
  private String label;
  private Command command;

  public Button(Command command) {
    this.command = command;
  }

  public void click() {
    command.execute();
  }
}

public class CustomerService { // receiver
  public void addCustomer() {
    system.out.println("Add customer");
  }
}

public class AddCustomerCommand implements Command { //concreteCommand
  private CustomerService service;

  public AddCustomerCommand(CustomerService service) {
    this.service = service;
  }

  @override
  public void execute() {
    service.addCustomer();
  }
}

public class Main {
  public static void main(String[] args) {
    var service = new CustomerService();
    var command = new AddCustomerCommand(service);
    var button = new Button(command);
    button.click();
  }
}
```

### Composite Command

```java
public class CompositeCommand implements Command {
  private List<Command> commands = new ArrayList<>();

  public void add(Command command) {
    commands.add(command);
  }

  @override
  public void execute() {
    for (var command:commands)
      command.execute();
  }
}

public class Main {
  public static void main(String[] args) {
    var composite = new CompositeCommand();
    composite.add(new ResizeCommand());
    composite.add(new BlackAndWhiteCommand());
    composite.execute();
  }
}
```

### undoable command

- momento pattern sometime need a lot of snap shot, undo a command just revert a command
- undoable command is a interface that inherit from command, because some command like save can not have undo

```java
public class HtmlDocument {
  private String content;

  public void makeBold() {
    content = "<b>"+content+"</b>";
  }
}

public interface Command {
  public void execute();
}

public interface UndoableCommand extends Command {
  public void unexecute();
}

public class History {
  private Deque<UndoableCommand> commands = new ArrayDeque<>(); // double ended que

  public void push(UndoableCommand command) {
    commands.add(command);
  }

  public UndoableCommand pop() {
    commands.pop();
  }
}

public class BoldCommand implements UndoableCommand {
  private String prevContent;
  private HtmlDocument document;
  private History history;

  public BoldCommand(HtmlDocument document, History history) {
    this.document = document;
    this.history = history;
  }

  @override
  public void execute() {
    prevContent = document.getContent();
    document.makeBold();
    history.push(this)
  }
  
  @override
  public void unexecute() {
    document.setContent(prevContent);
  }
}

public class Main {
  public static void main(String[] args) {
    var history = new History();
    var document = new HtmlDocument();
    document.setContent("Hello World!");

    var boldCommand = new BoldCommand(document, history);
    boldCommand.execute();
    system.out.println(document.getContent()); // <b>Hello World!</b>

    boldCommand.unexecute();
    system.out.println(document.getContent()); // Hello World!
  }
}
```

- can define one undo method for all command

```java

public class History {
  private Deque<UndoableCommand> commands = new ArrayDeque<>(); // double ended que

  public void push(UndoableCommand command) {
    commands.add(command);
  }

  public UndoableCommand pop() {
    commands.pop();
  }

  public int size() {
    return commands.size();
  }
}

public class UndoCommand implements Command {
  private History history;
  public UndoCommand(History history) {
    this.history = history;
  }

  @override
  public void execute() {
    if(history.size() > 0)
      history.pop().unexecute();
  }
}

public class Main {
  public static void main(String[] args) {
    var history = new History();
    var document = new HtmlDocument();
    document.setContent("Hello World!");

    var boldCommand = new BoldCommand(document, history);
    boldCommand.execute();
    system.out.println(document.getContent()); // <b>Hello World!</b>

    var undoCommand = new UndoCommand(history);
    undoCommand.execute();
    system.out.println(document.getContent()); // Hello World!
  }
}
```

## Observer Pattern

change on object value effect on other object value.

```java
public interface Observer {
  void update();
}

public class SpreadSheet implements Observer {
  @override
  void update() {
    System.out.println("SpreadSheet got Notified");
  }
}

public class Chart implements Observer {
  @override
  void update() {
    System.out.println("Chart got Updated");
  }
}

public class Subject { // observable class
  private List<Observer> observers = new ArrayList<>();

  void addObserver(Observer observer) {
    observers.add(observer);
  }

  void removeObserver(Observer observer) {
    observers.remove(observer);
  }

  void notifyObserver() {
    for(var observer : observers)
      observer.update();
  }
}

public class DataSource extends Subject {
  private int value;

  public int getValue() {
    return value;
  }

  public void setValue(int value) {
    this.value = value;
    notifyObserver();
  }
}

public class Main {
  public static void main(String[] args) {
    var dataSource = new DataSource();
    var sheet1 = new SpreadSheet();
    var sheet2 = new SpreadSheet();
    var chart = new Chart();

    dataSource.addObserver(sheet1);
    dataSource.addObserver(sheet2);
    dataSource.addObserver(chart);

    dataSource.setValue(1);
    // SpreadSheet got Notified
    // SpreadSheet got Notified
    // Chart got Updated
  }
}
```

in this way only notify of changing. for sending data we have 2 way, `pull` and `push`

### Push Style

send data in update method

```java
public interface Observer {
  void update(int value);
}

public class SpreadSheet implements Observer {
  @override
  void update(int value) {
    System.out.println("SpreadSheet got Notified: " + value);
  }
}

public class Chart implements Observer {
  @override
  void update(int value) {
    System.out.println("Chart got Updated" + value);
  }
}

public class Subject { // observable class
  private List<Observer> observers = new ArrayList<>();

  void addObserver(Observer observer) {
    observers.add(observer);
  }

  void removeObserver(Observer observer) {
    observers.remove(observer);
  }

  void notifyObserver(int value) {
    for(var observer : observers)
      observer.update(value);
  }
}

public class DataSource extends Subject {
  private int value;

  public int getValue() {
    return value;
  }

  public void setValue(int value) {
    this.value = value;
    notifyObserver(value);
  }
}

public class Main {
  public static void main(String[] args) {
    var dataSource = new DataSource();
    var sheet1 = new SpreadSheet();
    var sheet2 = new SpreadSheet();
    var chart = new Chart();

    dataSource.addObserver(sheet1);
    dataSource.addObserver(sheet2);
    dataSource.addObserver(chart);

    dataSource.setValue(1);
    // SpreadSheet got Notified: 1
    // SpreadSheet got Notified: 1
    // Chart got Updated: 1
  }
}
```

### Pull Style

observer concrete class connect with subject concrete class

```java
public interface Observer {
  void update();
}

public class SpreadSheet implements Observer {
  private DataSource dataSource;

  public SpreadSheet(DataSource dataSource) {
    this.dataSource = dataSource;
  }

  @override
  void update() {
    System.out.println("SpreadSheet got Notified:" + dataSource.getValue());
  }
}

public class Chart implements Observer {
  private DataSource dataSource;

  public SpreadSheet(DataSource dataSource) {
    this.dataSource = dataSource;
  }

  @override
  void update() {
    System.out.println("Chart got Updated:" + dataSource.getValue());
  }
}

public class Subject { // observable class
  private List<Observer> observers = new ArrayList<>();

  void addObserver(Observer observer) {
    observers.add(observer);
  }

  void removeObserver(Observer observer) {
    observers.remove(observer);
  }

  void notifyObserver() {
    for(var observer : observers)
      observer.update();
  }
}

public class DataSource extends Subject {
  private int value;

  public int getValue() {
    return value;
  }

  public void setValue(int value) {
    this.value = value;
    notifyObserver();
  }
}

public class Main {
  public static void main(String[] args) {
    var dataSource = new DataSource();
    var sheet1 = new SpreadSheet();
    var sheet2 = new SpreadSheet();
    var chart = new Chart();

    dataSource.addObserver(sheet1);
    dataSource.addObserver(sheet2);
    dataSource.addObserver(chart);

    dataSource.setValue(1);
    // SpreadSheet got Notified: 1
    // SpreadSheet got Notified: 1
    // Chart got Updated: 1
  }
}
```

## Reference

- [Design Patterns in Plain English | Mosh Hamedani](https://www.youtube.com/watch?v=NU_1StN5Tkk&t=63s)