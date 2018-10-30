# Displaying Collections in UIKit

## Lesson Overview
| **Time(min)** | **Activity**                            |
| ------------- | ----------------------------------------|
| 5             | Review of Last Class & Objectives       |
| 10            | TT Tableviews                           |
| 20            | UITableview Demo                        |
| 10            | Break                                   |
| 50            | Mood Tracker Pt. 1                      |
| 5             | Wrap up                                 |

## Objectives & Competencies
By the end of this lesson, students should be able to:

- Setup and display a list of data in a UITableView
- Identify the components of a UITableView (datasource & delegate)
- Select elements in a UITableView
- Use extensions to structure code

## UITableView

A view that presents data (a list of items) using rows arranged in a **single column**.

`UITableView` is a subclass of `UIScrollView`, this allows users to scroll through the elements in the table in vertical direction.

![tables](assets/tables.gif)

Each individual item of the table is a `UITableViewCell` object. A cell object has various parts but most of it is reserved for its content: text, image, or any other kind of distinctive identifier.

![cell](assets/cell.jpg)

When a cell object is reusable (the typical case) you assign it a **reuse identifier** in the storyboard.

![cell](assets/identifier.png)

At runtime, the table view stores cell objects in an internal queue. When the table view asks the data source to configure a cell object for display (when we scroll the table), the data source can access the queued object by sending a `dequeueReusableCellWithIdentifier:` message to the table view, passing in a reuse identifier. Then the data source sets the content of the cell before returning it. This reuse of cell objects is a performance enhancement because it eliminates the overhead of cell creation that can cause a shortage in memory.


When providing cells for the table view, there are three general approaches you can take.

- You can use ready-made cell objects in a range of styles.
- You can add your own subviews to the cell object’s content view.
- Use cell objects created from a custom subclass of UITableViewCell.

A table view is made up of zero or more **sections**, each with its own **rows**. Sections are identified by their index number within the table view, and rows are identified by their index number within a section. Sections have headers that appear at the top of each group and include a title. The footer appears below each group and also has a title. The entire table can also have its own header and footer.

Table views can have one of two styles, `UITableView.Style.plain` and `UITableView.Style.grouped`.

```swift
public enum Style : Int {

       case plain

       case grouped
   }
```

![tables](assets/tables.jpg)

A `UITableView` object must have an object that acts as a **data source** and an object that acts as a **delegate**.  

The data source must adopt the `UITableViewDataSource` protocol and provides information needed to construct tables and manages the data model when rows of a table are inserted, deleted, or reordered. It manages how many sections the table has, how many rows per section and handles how cells are drawn.

```swift
  // How many sections the table has. Default is 1 if not implemented.
  optional public func numberOfSections(in tableView: UITableView) -> Int

  // How many rows are there per section.
  public func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int

  // If using headers or footers. These use a fixed view, to do something different you need a custom view.
  optional public func tableView(_ tableView: UITableView, titleForHeaderInSection section: Int) -> String?
  optional public func tableView(_ tableView: UITableView, titleForFooterInSection section: Int) -> String?

  //Displays rows, preferably reusing cells.
  public func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell
```

The delegate must adopt the `UITableViewDelegate protocol`. Manages table row configuration and selection, row reordering, highlighting, accessory views, and editing operations. It deals with how the table behaves and looks.

```swift
  // When selecting a cell
  optional public func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath)

  // When deselecting a cell
  optional public func tableView(_ tableView: UITableView, didDeselectRowAt indexPath: IndexPath)

  // Changing the default header with a custom view
  optional public func tableView(_ tableView: UITableView, viewForHeaderInSection section: Int) -> UIView?

  // Defining the height of the rows (different cells can have different heights)
  optional public func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat
```
Many methods of `UITableView` take `NSIndexPath` objects as parameters and return values. They have properties we can access to manipulate objects in the table.

```swift
var section: Int
```
An index number identifying a section in a table view.
```swift
var row: Int
```
An index number identifying a row in a section of a table view.

Note: You decide how to structure you code. When using UITableViews some people prefer to include both protocol implementations inside an extension. This helps a lot with **code readability**. But take into consideration that using too many extensions increases the project **build time**. It's a personal choice between clear and readable code vs improvement in build time.

Here are some suggestions to ensure you are using `UITableView` the best way possible without affecting its performance:

- Reuse cells.
- Cache downloaded images.
- Avoid using attributed labels.
- If you are using different cell heights, be careful on how often the calculations are made.
- If you can, make your views opaque, transparent objects make the system work much harder.
- Avoid gradients (same idea as transparent objects).

## Demo

- Simple `UITableView` using storyboard.
- 1000 rows.
- Display "Hello world \(number of row)" in each row.
- Include an image for the cell's image view.

## Baseline Challenges

For the upcoming classes we'll be building an app to track the user's daily mood. This first part will cover:

- Creating a new Xcode Project
- Setting up the model needed
- Displaying a table
- Handling table events

Create a new project and follow the implementation for this part here: [Mood Tracker Part 1](https://github.com/Product-College-Labs/mood-tracker/blob/master/content/5.1-content.md)

## Resources

[UITableView in Apple Docs](https://developer.apple.com/documentation/uikit/uitableview)

[Why use reusable cells?](https://medium.com/ios-seminar/why-we-use-dequeuereusablecellwithidentifier-ce7fd97cde8e)

[Improving performance](https://medium.com/capital-one-tech/smooth-scrolling-in-uitableview-and-uicollectionview-a012045d77f)
