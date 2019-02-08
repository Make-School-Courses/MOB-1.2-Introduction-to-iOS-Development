# Architecting an iOS App

## Class Learning Objectives/Competencies
By the end of this lesson, students should be able to:

- Define all SOLID principles
- Reflect when to use the principles
- Identify areas for refactoring code
- Add SwiftLint to a project

## Initial Exercise

SwiftLint

[SwiftLint repository](https://github.com/realm/SwiftLint) on Github.<br>

Steps:<br>
1. Install the pod `pod 'SwiftLint'`
1. Add new Run Script `"${PODS_ROOT}/SwiftLint/swiftlint"`
1. Create a `.swiftlint.yml` file to customize the rules
1. You can use the rules available on github as a template


Available [rules](https://github.com/realm/SwiftLint/blob/master/Rules.md) at the moment.

## SOLID principles

SOLID is an acronym named by [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin). It represents 5 principles of object-oriented programming:

- Single responsibility
- Open/Closed
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

The purpose of these principles is solving problems when architecting an app. Some of them are:

- Fragility: When we make a change, the change breaks unexpected parts of the app.

- Immobility: When we have a component that is difficult to reuse in other parts of the app because it has too many dependencies.

- Rigidity: When we need to make a change but it requires a lot of effort because it affects other parts of the app.

# Single Responsibility Principle

**"There should never be more than one reason for a class to change."**

When we create or change a class, we should think about how many responsibilities the class has.

Why? Every class should have **only one** responsibility and reason to change. Classes should be simple and easy to maintain.

For example:

- An `ImageDownloader` class that downloads images from a URL.
- A `Product` class that hols information about a product.
- A `UserLocation` class that keeps track of a user's location.

All these classes handle one thing only and you can get a good idea of what they do with their names.

It's not always easy to follow SRP principle when we keep adding small features to our apps. When trying to get it done quickly, we end up adding features to the `UIViewController`. We tell it to display views, set up table view cells, handle navigation, even making network requests. The `UIViewController` handles way too many responsibilities and when the time comes to modify code, it can be a headache just finding the section you need to change.

How to fix? Identify the multiple responsibilities in a class and split them up into new classes. These new classes should do only one thing. For example, you could have the tableview's delegates & datasource in another class. A good way of telling if you're ignoring the SRP principle is looking at the number of lines in your view controllers.

```swift
class Product {

  func save() {
    let productData = requestProductData()
    let product = parse(data: data)
    saveToDataBase(product: product)
  }

  private func requestProductData() -> Data {
    // send API request and wait for the response
  }

  private func parse(data: Data) -> Product {
    // parse the data and create an object of type Product
  }

  private func saveToDataBase(product: Product) {
    // save the product in a database
  }
}
```
What are the responsibilities of the class? What can we change to make it better?

```swift
class Product {

  let apiService: APIService
  let parseService: ParseService
  let dataBaseService: DataBaseService

  init(apiService: APIService, parseService: ParseService, dataBaseService: DataBaseService) {
      self.apiService = apiService
      self.parseService = parseService
      self.dataBaseService = dataBaseService
  }

  func save() {
      let productData = apiService.requestProductData()
      let product = parseService.parse(data: data)
      dataBaseService.saveToDataBase(product: Product)
  }
}

class APIService {
  func requestProductData() -> Data {
    // send API request and wait for the response
  }
}

class ParseService {
  func parse(data: Data) -> Product {
    // parse the data and create an object of type Product
  }
}

class DataBaseService {
  func saveToDataBase(product: Product) {
    // save the product in a database
  }
}
```
## Open/Closed principle

**Software entities (classes, modules, etc.) should be open for extension but closed for modification**

### Open
The behavior of the module can be extended. We can make it behave in new and different ways as the requirements of the app change, or as new needs are added.

### Closed
When extending a class, we shouldn't change the implementation.

Bottom line: Design modules that never change, when requirements change or are added, we add new code, not change code that already works.

```swift
class Rectangle {

    var width : Double = 0.0
    var height: Double = 0.0

    init(width: Double, height: Double) {
        self.width = width
        self.height = height
    }

}

class CalculateArea{
    func area(rectangle: Rectangle) -> Double {
        return rectangle.width * rectangle.height
    }
}
```
New requirement, calculate the area of a Circle too.

```swift
class Rectangle {

    var width : Double = 0.0
    var height: Double = 0.0

    init(width: Double, height: Double) {
        self.width = width
        self.height = height
    }

}

class Circle {

    var radius : Double = 0.0

    init(radius: Double) {
        self.radius = radius
    }

}

class CalculateArea{
    func area(shape: AnyObject) -> Double {
        let area = 0.0
        if shape is Rectangle{
            let rectangle = shape as! Rectangle
            return rectangle.width * rectangle.height
        }else if shape is Circle{
            let circle = shape as! Circle
            return 3.1416 * circle.radius * circle.radius
        }else{
            return area
        }
    }
}
```
New requirement, we need the area of a triangle. What is going to change?
The `CalculateArea` class will keep on growing as we add more shapes.

How to solve? Protocols :D

```swift
protocol Shape{
    func area() -> Double
}

class Rectangle: Shape{

    var width : Double = 0.0
    var height: Double = 0.0

    init(width: Double, height: Double) {
        self.width = width
        self.height = height
    }

    func area() -> Double {
        return width * height
    }
}


class Circle: Shape{
    var radius : Double = 0.0

    init(radius: Double) {
        self.radius = radius
    }
    func area() -> Double {
        return 3.1416 * radius *  radius
    }
}

class CalculateArea{
    func area(shape: Shape) -> Double{
        return shape.area()
    }
}
```
## Liskov Substitution Principle

**Functions that use references to base classes must be able to use objects of derived classes.**

We must make sure that the new subclass is extending the base class without changing their behavior. And we could in theory replace the subclass instance with an instance of the base class.

We have this protocol for birds

```swift
protocol Bird {
    var altitudeToFly: Double? {get}
    func setLocation(longitude: Double , latitude: Double)
    mutating func setAltitude(altitude: Double)
}
```

And we can create as many classes for birds as we want. But if we are asked to include penguins, they can't fly, so they wont set an `altitudeToFly`.

```swift
class Penguin: Bird {
    var altitudeToFly: Double?

    func setLocation(longitude: Double, latitude: Double) {  
    }

    func setAltitude(altitude: Double) {
        //Altitude can't be set because penguins can't fly
        //ignore the whole thing
    }
}
```
The class could ignore the whole method, but that's likely not the way to go. Penguins are birds, but the Bird protocol assumes that all birds can fly. The moment Penguin violates the assumption, the Liskov principle is not met.

Fixing things.

```swift
protocol Bird {
    var altitudeToFly: Double? {get}
    func setLocation(longitude: Double , latitude: Double)
}

protocol Flying {
    mutating func setAltitude(altitude: Double)
}

struct Owl: Bird, Flying {
    var altitudeToFly: Double?
    mutating func setAltitude(altitude: Double) {
        altitudeToFly = altitude
    }

    func setLocation(longitude: Double, latitude: Double) {
        //Set location value
    }
}

struct Penguin: Bird {
    var altitudeToFly: Double?
    func setLocation(longitude: Double, latitude: Double) {
        //Set location value
    }
}
```

Another example: If we subclass UIButton (ex. MyButtonSubclass), wherever we use UIButton we could replace by MyButtonSubclass and the app won’t crash or misbehave in any way.

## Interface Segregation Principle

**Clients should not be forced to depend upon interfaces that they do not use.**

Introduces the fat interface problem: When an interface has too many methods, that are not cohesive and has more information than it actually needs. Apply to both classes and protocols.

Let's say we handle gestures with a protocol.
```swift
protocol GestureProtocol {
    func didTap()
    func didDoubleTap()
    func didLongPress()
}
```

And UI elements can adhere to it. For example, a button.
```swift
class CustomButton: GestureProtocol {
    func didTap() {
        // send tap action
    }

    func didDoubleTap() {
        // send double tap action
    }

    func didLongPress() {
        // send long press action
    }
}
```
But what happens if we have another custom button with limited interactions (It can only be long pressed).

```swift
class LimitedButton: GestureProtocol {
    func didTap() { }

    func didDoubleTap() { }

    func didLongPress() {
      // send long press action
    }
}
```
It would execute the  `didLongPress` method but will ignore the other two. We shouldn't force this button to include this it doesn't need.

How to fix? Breaking down the protocol.

```swift
protocol TapProtocol {
    func didTap()
}

protocol DoubleTapProtocol {
    func didDoubleTap()
}

protocol LongPressProtocol {
    func didLongPress()
}
```

Another example: When you use `UITableView`, just two methods are required, the rest are optional.

## Dependency Inversion Principle

**High level modules should not depend on low level modules. Both should depend on abstractions**

Example: Our ViewControllers (high level) should not depend on a networking component (low level).

Why? To reduce coupling. Strong coupling makes it hard to change the code later. An example might be if you are using a library to handle network calls and then you decide to switch to another library, if your ViewController depends heavily on the library, it's going to take a lot of time.

In this example we have a class `Handler ` that saves a string in a file.

```swift
//This is the high level module, right now tightly coupled with FilesystemManager
class Handler {

    let fm = FilesystemManager()

    func handle(string: String) {
        fm.save(string: string)
    }
}

//This is the low-level module
class FilesystemManager {

    func save(string: String) {
        // Open a file
        // Save the string in this file
        // Close the file
    }
}
```
If we want to have different types of storing the string, we can use an abstract protocol and easily change from filesystem to other type of storage like storing to a database.

```swift
class Handler {

    let storage: Storage

    init(storage: Storage) {
        self.storage = storage
    }

    func handle(string: String) {
        storage.save(string: string)
    }
}

protocol Storage {

   func save(string: String)
}

class FilesystemManager: Storage {

    func save(string: String) {
        // Open a file in read-mode
        // Save the string in this file
        // Close the file
    }
}

class DatabaseManager: Storage {

    func save(string: String) {
        // Connect to the database
        // Execute the query to save the string in a table
        // Close the connection
    }
}
```

## In Class Activity

Open your SPD or personal mobile project (choose the one you think you can get the most benefit from having someone else review it) and have a peer go over it with you using the code review rubric.
- Identify areas of opportunity to make improvements.
- Identify if there needs to be any code refactoring.
- Discuss with your classmate your decisions when writing your code and be open to receive feedback.

After you are done, do the same process with their project.

## Additional Resources

[SOLID article](https://marcosantadev.com/solid-principles-applied-swift/)<br>
[Another article](https://codeburst.io/solid-design-principle-using-swift-fa67443672b8)<br>
[Yet another one](https://medium.com/@vinodhswamy/solid-principles-in-swift-7dc2b793fd68)<br>
[SRP](https://web.archive.org/web/20150202200348/http://www.objectmentor.com/resources/articles/srp.pdf)<br>
[Open/Closed](https://web.archive.org/web/20150905081105/http://www.objectmentor.com/resources/articles/ocp.pdf)<br>
[Liskov](https://web.archive.org/web/20150905081111/http://www.objectmentor.com/resources/articles/lsp.pdf)<br>
[Interface Segregation](https://web.archive.org/web/20150905081110/http://www.objectmentor.com/resources/articles/isp.pdf)<br>
[Dependency Inversion](https://web.archive.org/web/20150905081103/http://www.objectmentor.com/resources/articles/dip.pdf)
