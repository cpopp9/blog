---
title: "Live Updates Animation"
tags: ['Swift', 'SwiftUI', 'Animation', 'UX/UI']
date:  2023-09-14
draft: false
---
I came across a simple yet beautiful animation in the New York Times app the other day denoting their live updates feed.

It has three dots, all with different shades of red, alternating to imply to the user that changes to the story are happening rapidly in real time.

I always love challenging myself to get better at animations within SwiftUI, so I set out to recreate this cool little design.

![liveUpdatesAnimation.gif](/liveUpdatesAnimation.gif)

## In Code

```swift
import SwiftUI

extension ShapeStyle where Self == Color {
    static var lightRed: Color {
        Color(#colorLiteral(red: 1, green: 0.4308977723, blue: 0.3956909776, alpha: 1))
    }
    
    static var lightestRed: Color {
        Color(#colorLiteral(red: 1, green: 0.7957689166, blue: 0.7784273028, alpha: 1))
    }
}

struct LiveUpdatesProgressStyle: ProgressViewStyle {
    
    enum Phase {
        case one, two, three
    }
    
    @State var startDate: Date = Date()
    
    func makeBody(configuration: Configuration) -> some View {
        return TimelineView(.periodic(from: .now, by: 1)) { context in
         
            let timeElapsed = context.date.timeIntervalSince1970 - startDate.timeIntervalSince1970
            
            let phase = animationPhase(timeElapsed: Int(timeElapsed))
            
            HStack {
                circles(phase: phase)
                
                Text("Live Updates")
                    .fontWeight(.heavy)
                    .foregroundColor(.red)
            }
        }
    }
    
    func animationPhase(timeElapsed: Int) -> Phase {
        
        let index = timeElapsed % 3
        
        if index == 0 {
            return .one
        } else if index == 1 {
            return .two
        } else {
            return .three
        }
    }
    
    
    func circles(phase: Phase) -> some View {
        let color1: Color
        let color2: Color
        let color3: Color
        
        switch phase {
        case .one:
            color1 = .lightestRed
            color2 = .lightRed
            color3 = .red
        case .two:
            color1 = .red
            color2 = .lightestRed
            color3 = .lightRed
        case .three:
            color1 = .lightRed
            color2 = .red
            color3 = .lightestRed
        }
        
        return HStack(spacing: 3) {
            Circle()
                .frame(width: 10)
                .foregroundColor(color1)
            
            Circle()
                .frame(width: 10)
                .foregroundColor(color2)
            
            Circle()
                .frame(width: 10)
                .foregroundColor(color3)
        }
    }
}
```
