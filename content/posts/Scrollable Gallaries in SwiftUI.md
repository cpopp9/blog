---
title: "Scrollable Gallaries in SwiftUI"
tags: ['SwiftUI', 'UX/UI', 'Animation']
date:  2023-09-17
draft: false
---
TabView in SwiftUI makes creating scrolling galleries a breeze when combined with the optional .tabViewStyle(PageTabViewStyle()) modifier.

In this example I overwrote the default appearance of the page indicators by running a simple function when the view appears so that the indicator dots are visible on a white background.

![ScrollableGalloriesSwiftUI.gif](/ScrollableGalloriesSwiftUI.gif)

```swift
import SwiftUI

struct ImageSlider: View {
    
    private let images = ["Barbie", "Oppenheimer", "Blue Beetle", "Haunted Mansion", "Mission Impossible"]
    
    var body: some View {
        TabView {
            ForEach(images, id: \.self) { item in
                Image(item)
                    .resizable()
                    .scaledToFit()
                    .padding(.horizontal)
            }
        }
        .frame(maxHeight: 650)
        .tabViewStyle(PageTabViewStyle())
        .onAppear {
            setupAppearance()
        }
    }
    
    func setupAppearance() {
        UIPageControl.appearance().currentPageIndicatorTintColor = .black
        UIPageControl.appearance().pageIndicatorTintColor = UIColor.black.withAlphaComponent(0.2)
    }
}
```
