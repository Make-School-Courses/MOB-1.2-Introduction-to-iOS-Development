# TabBar Controller

<!-- > -->

## Learning Objectives

By the end of this lesson, students should be able to:

- Understand the view hierarchy when using a tab bar controller with a navigation controller
- Implement a TabBar Controller in an Xcode project

<!-- > -->

## A Review on UINavigationController

-
-
-

<!-- > -->

## What's a tab bar controller?

- `UITabBarController` is a `UIViewController` subclass.
- While navigation controllers manage a stack of related view controllers, a tab bar controller manages an **array** of **view controllers** that may not have direct relation to one another.
- The tab bar interface displays tabs at the bottom of the window for selecting between views.
- This class is generally used as-is, but may also be subclassed.

<!-- v -->

![clock](assets/clock.png)

<!-- v -->

Each tab of a tab bar controller interface is **associated with a view controller**.

When the user selects a specific tab, the tab bar controller **displays the root view** of the corresponding view controller, **replacing any previous views**.

<!-- v -->

## The view hierarchy

![views](assets/views.png)

You can use navigation controllers or custom view controllers as the root view controller for a tab.

<!-- > -->

## Getting familiar with the project

Download [this starter project](https://github.com/amelinagzz/tabbar-starter) where we will add a Tab Bar Controller to display all the continents.

<!-- v -->

## Step 0

Explore the starter project and find out:

- If we are using the storyboard or the programmatic approach.
- What are the contents of `ContinentVC`
- What are the contents of `DetailVC`
- What is the parent class of `TabBarController`
- What is the root view of the whole project, where can you find this?
- What's inside the assets folder

<!-- v -->

## Step 1

Set the main view's `rootViewController` to be the `TabBarController`.

<!-- v -->

## Step 2

Here's how you would add a view controller to the tab bar controller:

```swift
let vc = ContinentVC()
vc.imageName = "northAmerica"
vc.title = "North America"
vc.view.backgroundColor = UIColor.blue
vc.tabBarItem = UITabBarItem(tabBarSystemItem: .search, tag: 0)

viewControllers = [vc]
```
Try this for two more continents. Then run the app and see the result.

<!-- v -->

## Step 3

Look for the method associated with the button in `ContinentVC.swift`.

We want to present `DetailVC` when the button gets pressed.

```swift
let detailVC = DetailVC()
present(detailVC, animated: true, completion: nil)
```

Run the app and see if that works.

<!-- v -->

It worked. But we are not doing this using a navigation controller. A better way would be to have for each tab, its own navigation controller.

Using a tab bar controller with a navigation controller makes for a powerful combination. You can use them to give the user access to the main interfaces of the app, and to provide left-to-right navigation into more detailed view controllers.

![navigation](assets/navigation.png)

<!-- v -->

## Step 3

Go back to the setup of the tab bar controller and add a new instance of a UINavigationController, set its root view controller to be the `ContinentVC` instance you created before.

```swift
let vc = ContinentVC()
vc.imageName = "northAmerica"
vc.title = "North America"
vc.view.backgroundColor = UIColor.blue
let navController = UINavigationController(rootViewController:vc)
vc.tabBarItem = UITabBarItem(tabBarSystemItem: .search, tag: 0)
viewControllers = [navController]
```

Run the app and notice the major change.

<!-- v -->

## Step 4

We can now see the titles from each view controller, because we now get a navigation bar. This new addition will let us push view controllers into the stack and pop them as we please.

Let's try that. Instead of presenting a view controller, use the push animation.

```swift
self.navigationController?.pushViewController(detailVC, animated: true)
```

Run the app and see how you can navigate in the stack of view controllers.

<!-- v -->

## Step 5 - challenge

We aren't seeing all the continents so far.

- Add the remaining view controllers with their corresponding images and titles.
- What happens when you have more than 6 items in the tab bar?
- Avoid repeating yourself when creating the view controllers and navigation controllers. How can you optimize this?

<!-- v -->

Compare your implementation with a neighbor. Check for similarities, differences and make adjustments to your code if needed.

*Instructors solution*

<!-- > -->

## Custom Tab Bar

[UITabBar](https://developer.apple.com/documentation/uikit/uitabbar).

A control that displays one or more buttons in a tab bar for selecting between different subtasks, views, or modes in an app.

To configure the tab bar associated with a UITabBarController object, configure the view controllers associated with the tab bar controller. The tab bar automatically obtains its items from the tabBarItem property of each view controller.

<!-- v -->

There's a lot of properties we can modify in a tab bar:
- Icons
- View color
- Font
- Tint Color

<!-- v -->

## Step 6 - UITabBarItems

Let's change the icons of the tab bar.

```swift
vc.tabBarItem = UITabBarItem(title: vc.title, image: UIImage(named: "heart"), selectedImage: UIImage(named: "heart"))

//variation without title
vc.tabBarItem = UITabBarItem(title: "", image: UIImage(named: "heart"), selectedImage: UIImage(named: "heart"))
vc.tabBarItem.imageInsets = UIEdgeInsets(top: 0, left: 0, bottom: -3, right: 0)
```

<!-- v -->

## Step 7

Now let's change the tint color and the color of the items.

```swift
self.tabBar.barTintColor = UIColor.black
self.tabBar.tintColor = UIColor.white
```

Run the app.

<!-- v -->

## The Delegate

You use the [UITabBarControllerDelegate](https://developer.apple.com/documentation/uikit/uitabbarcontrollerdelegate) protocol when you want to augment the behavior of a tab bar.

- To determine whether specific tabs should be selected.
- To perform actions after a tab is selected.
- To perform actions before or after the user customizes the order of the tabs.

<!-- v -->

## Step 8

Implement the delegate to detect when we've selected a new tab.

1. Add UITabBarControllerDelegate in the class declaration.
1. Set the delegate to self
1. Add the method:

```swift
func tabBarController(_ tabBarController: UITabBarController, didSelect viewController: UIViewController) {
    print("Selected a new view controller")
}
```
<!-- v -->

## Lab + After Class

In our subscription box app we've been working with a temporary home page with buttons to go to the other sections of the app.

Replace the home screen with a tab bar controller.

You can see how it should look like in [the online design](https://zpl.io/bejlAMq). It's the "NewHome" screen.

<!-- > -->

## Additional Resources

- [Tutorial using the storyboard](https://code.tutsplus.com/tutorials/ios-from-scratch-with-swift-exploring-tab-bar-controllers--cms-25470)
- [TabBar + NavController Image source](https://learnappmaking.com/tab-bar-controller-uitabbarcontroller-swift-ios/)
- [Tab Bar programmatically](https://medium.com/@ITZDERR/uinavigationcontroller-and-uitabbarcontroller-programmatically-swift-3-d85a885a5fd0)
- [Video tutorial with storyboard](https://www.youtube.com/watch?v=n7NNAdaIDKQ)
