
<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->

<!-- .slide: class="header" -->

# Creating Custom Views

## [Slides](https://make-school-courses.github.io/MOB-1.2-Introduction-to-iOS-Development/Slides/04-CustomViews/README.html ':ignore')

<!-- > -->

## Agenda

- Review Onboarding assignment
- Creating custom views
- Refactor session
- xib files

<!-- > -->

## Learning Objectives

By the end of this lesson, students should be able to:

- Create custom views programmatically
- Refactor an Xcode project
- Implement views with xib files

<!-- > -->

## Onboarding assignment

- 👯 Get in pairs or groups of 3.
- 🕵🏻 Review each other's code.
- 🙌🏼 See if you can get unblocked with tips from your classmates.
- 💭 Remember what you said was the most challenging thing about constraints? Were you able to improve to some extent with the practice?
- 📝 Keep a list of the things you are still missing or would like to change after reviewing your code in groups.

<!-- v -->

**Demo of a possible solution.**

- Does it look like yours?
- What is similar and different?
- Do you have suggestions for improvements?

<!-- v -->

### 🤔

You probably noticed that the first solution has too much going on and have a feeling that it's not entirely right.

Facts:
- It sure works.
- It's not very readable.
- It takes time to find where things are.
- Can definitely be improved.

<!-- > -->

### Creating Custom Views

Creating custom views will help with:

- Making code **reusable**.
- Making code more **readable**.
- Sometimes **reduce** the amount of code.
- **Separation** of concerns.
- Help with the **structure** of files in the project.

We can create them 2 ways: **programmatically** & **xib** files.

<!-- > -->

## Programmatically

```swift
class MyCustomView: UIView {
    override init(frame: CGRect) {
        super.init(frame: frame)
        setup()
    }

    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        setup()
    }

    func setup() {
        self.backgroundColor = UIColor.purple
    }
}
```

<!-- v -->

```swift
class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()

        let myView = MyCustomView()
        myView.translatesAutoresizingMaskIntoConstraints = false
        self.view.addSubview(myView)

        myView.widthAnchor.constraint(equalToConstant: 100).isActive = true
        myView.heightAnchor.constraint(equalToConstant: 100).isActive = true
        myView.centerXAnchor.constraint(equalTo: view.centerXAnchor).isActive = true
        myView.centerYAnchor.constraint(equalTo: view.centerYAnchor).isActive = true

    }
}
```

<!-- > -->

## The true value of reusing

We now have a custom class for a view that's a purple square. We can create as many as we want in our project. That's useful, but we are not exploiting the most out of our custom class.

What if I want to make squares of different colors?

<!-- v -->

## Here comes the custom initializer

```swift
class MyCustomView: UIView {
    var color: UIColor!

    required init(color: UIColor) {
        super.init(frame: .zero)
        self.color = color
        self.setup()
    }

    override init(frame: CGRect) {
        super.init(frame: frame)
        setup()
    }

    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        setup()
    }

    func setup() {
        self.backgroundColor = color
    }
}
```

<!-- v -->

```swift
let myView = MyCustomView(color: UIColor.orange)
myView.translatesAutoresizingMaskIntoConstraints = false
self.view.addSubview(myView)
```

<!-- v -->

A small change but now we can customize the properties of our custom view.

This is useful when we are working with a design that reuses the same elements in all of the screens. Or when we notice that some views are very similar with subtle differences.

<!-- v -->

With this approach we can make as many changes in the properties of our views as we need. See what happens when we add this:

```swift
func setup() {
    self.backgroundColor = color
    self.layer.cornerRadius = 10
    self.layer.masksToBounds = true
}
```

<!-- > -->

## In Class Activity

Recreate the example to make a custom view.

Choose any color you want and give the view rounded corners.

<!-- > -->


## xib files

xib files are a great way to create custom views with all the benefits from the storyboard (regarding customization and setting constraints).

We can design in the interface builder and then use the view in a storyboard or programmatically.

xib files reduce the need of having storyboards and because of this, reduce the amount of bugs too.

<!-- v -->

## xibs or nibs?

Both terms mean a custom view that you can reuse in your project.

**XIB**  (XML Interface Builder) is a representation before the compiler turns it into **NIB** (NeXTSTEP Interface Builder). XIBs are easier for us to read while NIBs are easier for the computer to process.

<!-- > -->

## xib files

Demo Creating a xib file and using it in the storyboard.

[Tutorial](https://medium.com/better-programming/swift-3-creating-a-custom-view-from-a-xib-ecdfe5b3a960)

<!-- v -->

## IBDesignable

@IBDesignable can be applied to UIViews and the lets Interface Builder know that it should render the view directly in the canvas.

In this way we can see our custom views, for example in a storyboard without having to run the app each time we make a change.

<!-- > -->

## In Class Activity

Recreate the example of the square view, this time using a xib file. Up to you to then use the view programmatically or in the storyboard or both! 😀

<!-- > -->

## Refactoring our code

- To make our code more readable.
- To tidy up.
- To remove redundant code or comments.
- To make things reusable.
- To keep our code DRY.
- To split up long functions and files.

Remember to focus on progress, not perfection 😌

<!-- v -->

## In Class Activity

Demo of an example of the Onboarding flow refactored.

Then it's time for you to try it out.

Take the list of things you wanted to improve from earlier and refactor your code to achieve those goals.

This assignment will be graded by the instructor using [this code review rubric](https://docs.google.com/document/d/1SF9xCDK9qPnpu_Eu6DsgSgZl6D0InMvYG68k2-buUEQ/edit?usp=sharing).

<!-- v -->

## Lab & After Class

- Review a possible solution to the onboarding flow and how to use custom views with [this video](https://youtu.be/kJQcn06uIiI).

<!-- > -->

## Additional Resources

- [Xcode project without the main storyboard](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=6&cad=rja&uact=8&ved=2ahUKEwjFgpDr66vnAhX2CzQIHXEDDIoQwqsBMAV6BAgHEAQ&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DHtn4h51BQsk&usg=AOvVaw0pv5o1FniYa4BdXjKqT8yT)
- [Using xib files](https://medium.com/better-programming/swift-3-creating-a-custom-view-from-a-xib-ecdfe5b3a960)
- [IBDesignable & IBInspectable](https://nshipster.com/ibinspectable-ibdesignable/)
