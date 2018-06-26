# CollectionSwipableCellExtension
Swipable buttons for UICollectionView and UITableView

The extension for UICollectionView and UITableView which appends buttons to a cell are shown on cell swiping.  
- supports swipe to delete gesture
- doesn’t require subclassing of cell class, it’s more useful for case when third-party cell already is used.
- the buttons UI is fully customised by providing own layout.
- right-to-left languages support

![Swipe to delete example](https://raw.githubusercontent.com/KosyanMedia/CollectionSwipableCellExtension/README/example/SwipeToDeleteExample.gif)

## Install

### Carthage
```
github "KosyanMedia/CollectionSwipableCellExtension" ~> 0.0.1
```

## Using

Initialize extension object with UITableView or UICollectionView and set a delegate.  
isEnabled property allows activate/deactivate functionality.

```swift
swipableExtension = CollectionSwipableCellExtension(with: tableView)
swipableExtension?.delegate = self
swipableExtension?.isEnabled = true
```

Implement methods of CollectionSwipableCellExtensionDelegate protocol, which return layout for buttons and define which cells are swipable.

```swift
func isSwipable(itemAt indexPath: IndexPath) -> Bool {
    return true
}

func swipableActionsLayout(forItemAt indexPath: IndexPath) -> CollectionSwipableCellLayout? {
    let actionLayout = CollectionSwipableCellOneButtonLayout(buttonWidth: 100, insets: .zero, direction: .leftToRight)
    actionLayout.action = { [weak self] in
        //do something
    }

    return actionLayout
}
```

Call resetSwipableActions() in UITableViewDelegate in order to exclude problems with cell's reuse.

```swift
func tableView(_ tableView: UITableView, didEndDisplaying cell: UITableViewCell, forRowAt indexPath: IndexPath) {
    cell.resetSwipableActions()
}
```

or UICollectionViewDelegate

```swift
func collectionView(_ collectionView: UICollectionView, didEndDisplaying cell: UICollectionViewCell, forItemAt indexPath: IndexPath) {
    cell.resetSwipableActions()
}
```

## Layout customization

We provide one simple layout CollectionSwipableCellOneButtonLayout. 
You can customize it by subclassing or create your own layout which implements CollectionSwipableCellLayout protocol.