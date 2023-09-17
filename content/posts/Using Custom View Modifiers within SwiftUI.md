---
title: "Using Custom View Modifiers within SwiftUI"
tags: ['SwiftUI', 'UX/UI']
date:  2023-09-17
draft: false
---
Custom view modifiers are extremely easy to create in SwiftUI, and allow you to:
- reuse styles
- simplify your code
- maintain consistency
- update them quickly everywhere in your project

![CustomViewModifiersSwiftUI.jpeg](/CustomViewModifiersSwiftUI.jpeg)

```swift
import SwiftUI

struct ButtonIcon: ViewModifier {
    func body(content: Content) -> some View {
        content
            .foregroundStyle(.white)
            .padding(EdgeInsets(top: 10, leading: 25, bottom: 10, trailing: 25))
            .background(.green)
            .clipShape(Capsule())
    }
}
```

```swift
struct CustomViewModifiers: View {
    var body: some View {
        Button() {
            // take picture
        } label: {
            Image(systemName: "camera.fill")
                .modifier(ButtonIcon())
        }
    }
}
```
