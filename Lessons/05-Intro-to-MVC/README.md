<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->

<!-- .slide: class="header" -->
# Model View Controller

## [Slides](https://make-school-courses.github.io/MOB-1.2-Introduction-to-iOS-Development/Slides/03-CodingConstraints/README.html ':ignore')

<!-- > -->

## Agenda

-

<!-- > -->

## Learning Objectives

By the end of this lesson, students should be able to:

- Describe and use MVC in an Xcode project
- Implement navigation programmatically
- Send information between view controllers

<!-- > -->

## Navigation

So far we've been building apps with one screen. Most of the time you will need to interact between more than 2 screens in your apps. Think about how just a login screen and your main content are already 2 screens from the whole project. Screen transitions can be done both programmatically, using segues, or with a combination of both.

### Segues

*In real life:* Move or shift from one role, state, or condition to another without interruption.

*In iOS:*  A transition between two view controllers in your app’s storyboard file. Segues are the building blocks of iOS navigation.

The starting point of a segue is the button, table row, or gesture recognizer that initiates the segue. The end point of a segue is the view controller you want to display.

At runtime, UIKit loads the segues associated with a view controller and connects them to the corresponding elements. When the user interacts with the element, UIKit loads the destination view controller, notifies your app that the segue is about to occur, and executes the transition.

![segue](assets/segue.png)

### How to

**Step 1:** To create a segue between view controllers in the same storyboard file, Control-click element handling the user interaction in the first view controller and drag to the destination view controller.

![howto](assets/target.png)

**Step 2:** The Interface Builder then prompts you to select the type of relationship you want to create between the two view controllers.

| **Option**          | **Description**                            |
| -------------       | -------------------------------------------|
| Show (push)         | Allows you to navigate through a stack of view controllers, on top of each other. It pushes the destination view controller, from right to left on the stack.   |
| Show detail         | Used when you are working with split view controllers.|
| Present modally     | Shows View controllers with animations.    |
| Present as popover  | The view controller appears in a popover.  |
| Custom              | You may implement your own custom segue and have control over the behavior.    |



<!-- > -->

## In Class Activity


<!-- > -->

## Navigation


<!-- > -->

## Passing information



<!-- > -->

## After Class

[Tip Calculator Tutorial](https://www.makeschool.com/online-courses/tutorials/build-a-tip-calculator-in-swift-4/intro-tip-calculator)

<!-- > -->

## Additional Resources

[Apple Documentation on MVC](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html)<br>
[MVC analogy](https://medium.freecodecamp.org/model-view-controller-mvc-explained-through-ordering-drinks-at-the-bar-efcba6255053)<br>
[More on MVC](https://codeburst.io/mvc-design-pattern-analogy-to-an-old-school-landline-3dcd2e994063)<br>
