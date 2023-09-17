---
title: "Adding Transparency to Sheets in SwiftUI"
tags: ['Swift', 'SwiftUI', 'Animation']
date:  2023-09-12
draft: false
---
Native sheets in iOS are by default opaque, and require a bit of extra code to enable any form of transparency.

First we can create a new background view that conforms to UIViewRepresentable.

```swift
struct BackgroundClearView: UIViewRepresentable {
    func makeUIView(context: Context) -> UIView {
        let view = UIView()
        DispatchQueue.main.async {
            view.superview?.superview?.backgroundColor = .clear
        }
        return view
    }
    
    func updateUIView(_ uiView: UIView, context: Context) {}
}
```

And then we can use that transparent view as a background view within our sheet to enable transparency.

```swift
struct TransparentSheet: View {
    var body: some View {
        ZStack {
            Color.green.opacity(0.5)
                .offset(y: 100)
            
            Circle()
                .fill(.yellow)
                .frame(maxWidth: 200)
                .offset(y: -150)
        }
        
        .background(BackgroundClearView())
        .ignoresSafeArea()
        .presentationDetents([.height(500)])
    }
}
```

### In Action

![sheetTransparency.gif](/sheetTransparency.gif)
