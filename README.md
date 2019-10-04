# Feedback-SwiftlintClosureLiteralCorrectionBug
Demonstrates an issue with Swiftlint

Actual:

```
struct TakesAClosure {
    let closure: () -> Void
}

struct Example {
    let one: String
    let two: String
    let closureStructs: [String: TakesAClosure]
    let four: String
}

let example = Example(one: "Hey",
                            two: "Hey",
                            closureStructs: [
                            "A": TakesAClosure(closure: {
                                print("A")
                            }),
                            "B": TakesAClosure(closure: {
                                print("B")
                            ],
                            four: "Hey")
                            )

```