# Exploring SwiftUI

## [Slides](https://make-school-courses.github.io/MOB-1.2-Introduction-to-iOS-Development/Slides/11-SwiftUI/README.html ':ignore')

<!-- > -->

## Learning Objectives

By the end of this lesson, students should be able to:

- Explain what is SwiftUI and how it works with Declarative syntax
- Familiarize with creating views following a tutorial
- Implement their own view in SwiftUI to build a profile
- Combine SwiftUI and UIKit in a project

<!-- > -->

## SwfitUI

![swiftui](assets/swiftui.png)

SwiftUI is an innovative way to build user interfaces across all Apple platforms using Swift.  

<!-- > -->

## Declarative syntax

*Declarative programming is a non-imperative style of programming in which programs describe their desired results without explicitly listing commands or steps that must be performed.*

Telling SwiftUI **what** we want the UI to look like and work, then it figures out **how** to make that happen.  

- Easy to read
- Natural to write

<!-- > -->

![codeExample](assets/codeExample.png)

<!-- > -->

![table](assets/table.png)

<!-- > -->

## Design Tools

With Xcode 11 came a lot of new tools to work with SwiftUI.

As we work in the code edit, we get to see a live preview of the app.

As we work in the design canvas, everything we edit is completely in sync with the code in the editor.

In any case, Xcode recompiles the changes instantly and inserts them into a running version of your app, visible, and editable at all times.

<!-- > -->

## Some facts

- SwiftUI runs on iOS 13, macOS 10.15, tvOS 13, and watchOS 6. And future versions of each.
- SwiftUI does not replace UIKit.
- SwiftUI uses AutoLayout behind the scenes. And also a flexible box layout system.
- SwiftUI is faster than UIKit.
- You can have a project than mixes SwiftUI and UIKit.

<!-- > -->

## In Class Activity

Complete the section ["Creating and Combining Views"](https://developer.apple.com/tutorials/swiftui/creating-and-combining-views) from the SwiftUI tutorials by Apple.

<!-- > -->

## Template contents



<!-- > -->

## What should we learn?

For now SwiftUI has limited API coverage, limited adoption and support.

It will be a big deal in years to come (maybe 2 or 3). But as iOS developers in the job industry **now**, we need to know about UIKit as a requirement.

The best option is to learn SwiftUI on the side as well once you feel comfortable with UIKit (a list of resources at the end of the lesson).

<!-- > -->

## In Class Activity

Using SwiftUI create the following layout for the Profile view in your subscription box app. (Do this in a new project)

![profile](assets/profile.png)

<!-- > -->

## Adding it to our existing project.

You will need to add the files from the profile into the subscription box project.

Then just use it as a regular view with the help of the class [UIHostingController](https://developer.apple.com/documentation/swiftui/uihostingcontroller).

```swift
let swiftUIView = ContentView()
let viewController = UIHostingController(rootView: swiftUIView)
```

<!-- > -->

## Additional Resources

- [What is SwiftUI](https://developer.apple.com/xcode/swiftui/)
- [SwiftUI tutorials](https://developer.apple.com/tutorials/swiftui/tutorials)
- [100 days of SwiftUI](https://www.hackingwithswift.com/100/swiftui)
- [SwiftUI by examples](https://www.hackingwithswift.com/quick-start/swiftui)
