---
title: "Swipe to delete from lists in SwiftUI"
tags: ['Swift', 'SwiftUI']
date: 2022-11-20T09:03:20-08:00
draft: false
---
SwiftUI includes a native solution for a swipe to delete function from within lists, which works exactly as you would expect with just a few lines of additional code.

The code itself is simple, and involves us creating a ForEach of our array within our list, and adding a **.onDelete** modifier to trigger the **removeItems** function that we have created below our view body.

💡 It’s important to note that our **.onDelete** modifier will not work on the list itself - it needs to be called specifically on a ForEach within a list.


```swift
import SwiftUI

struct DeleteFromList: View {
    @State var shoppingList = ["🍌 Bananas", "🍓 Strawberries", "🌽 Corn", "🥕 Carrots", "🥨 Pretzels", "🧀 Cheese", "🧅 Onions", "🍤 Shrimp"]
    
    var body: some View {
        List {
            ForEach(shoppingList, id: \.self) { item in
                Text(item)
            }
            .onDelete(perform: removeItems)
        }
    }
    
    func removeItems(atOffsets: IndexSet) {
        shoppingList.remove(atOffsets: atOffsets)
    }
    
}
```

### In Action

![swipeToDeleteSwiftUI.gif](/swipeToDeleteSwiftUI.gif)

As you can see a simple swipe gesture from right to left exposes a delete dialog inline with the item the user has selected. When tapped the item gets deleted from the array and disappears from the list.
