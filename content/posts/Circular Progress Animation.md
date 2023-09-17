---
title: "Circular Progress Animation"
tags: ['Swift', 'SwiftUI', 'Animation', 'UX/UI']
date:  2023-09-17
draft: false
---

![CircularProgressAnimation.gif](/CircularProgressAnimation.gif)

This is undoubtably quite a lot of code that can be reduced, but I was happy with my first draft of this circular progress animation that I created in SwiftUI.

TimelineView() appears to be extremely efficient in creating animations that rely on a timer, without any of the inefficiencies of leaving a timer running constantly.

```swift
struct CircularProgress: View {
    
    var lineWidth: CGFloat = 40
    @State var secondsCounter: Double = 0
    @State var iconSizer: Bool = false
    
    var body: some View {
        
        TimelineView(.animation) { context in
            
            let _ = increaseSecondsCounter(secondsCounter: $secondsCounter)
            
            ZStack {
                
                if secondsCounter < 100 {
                    Text("\(Int(secondsCounter))%")
                        .font(.title.bold())
                        .foregroundColor(.green)
                } else {
                    Image(systemName: "bolt.fill")
                        .font(.system(size: iconSizer ? 40 : 60))
                        .foregroundColor(.green)
                        .animation(.spring(), value: iconSizer)
                }
                
                Circle()
                    .trim(from: 0, to: secondsCounter * 0.01)
                    .stroke(.green, style: StrokeStyle(lineWidth: lineWidth, lineCap: .round, lineJoin: .round))
                    .rotationEffect(.degrees(-90))
            }
            
            .frame(width: 200, height: 200)
        }
    }
    
    private func increaseSecondsCounter(secondsCounter: Binding<Double>) {
        
        if self.secondsCounter < 100 {
            DispatchQueue.main.async {
                secondsCounter.wrappedValue += 0.005
            }
        } else {
            let seconds = Calendar.current.component(.second, from: Date())
            
            if seconds.isMultiple(of: 2) {
                iconSizer = true
            } else {
                iconSizer = false
            }
        }
    }
}
```
