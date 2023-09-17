---
title: "Using FocusState within SwiftUI"
tags: ['SwiftUI', 'UX/UI']
date:  2023-09-17
draft: false
---
@FocusState is a property wrapper within SwiftUI that allows us to track where the user is focused within our app.

In this example, we can suggest to the user to start on the first text field by preselecting focus for them, and provide visual feedback when they switch between fields.

![FocusStateSwiftUI.gif](/FocusStateSwiftUI.gif)

```swift
import SwiftUI

struct FocusStateTest: View {
    
    private enum FocusedField {
        case firstName, schoolAttended
    }
    
    @State private var firstName = ""
    @State private var schoolAttended = ""
    @FocusState private var focusedField: FocusedField?
    
    var body: some View {
        VStack {
            TextField("First Name", text: $firstName)
                .focused($focusedField, equals: .firstName)
                .padding()
                .overlay(
                    RoundedRectangle(cornerRadius: 16)
                        .stroke((focusedField == .firstName ? .green : .clear), lineWidth: 2)
                )
            
            TextField("School Attended", text: $schoolAttended)
                .focused($focusedField, equals: .schoolAttended)
                .padding()
                .overlay(
                    RoundedRectangle(cornerRadius: 16)
                        .stroke((focusedField == .schoolAttended ? .green : .clear), lineWidth: 2)
                )
        }
        .padding()
        .onAppear {
            focusedField = .firstName
        }
    }
}
```
