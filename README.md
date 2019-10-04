# Feedback-SwiftlintClosureLiteralCorrectionBug
Demonstrates an issue with Swiftlint.

## Issue
There seems to be an issue with `literal_expression_end_indentation` autocorrection. For the given example file, when the literal expression's ending indentation is incorrect, autocorrection removes syntax-relevant tokens while moving the square bracket.

## Steps to reproduce
1. Clone this repo
2. Run `swift example.swift` to verify that the file compiles
3. Run `swiftlint autocorrect --config config.yml`
4. run `swift example.swift` again to verify that the autocorrected file does not compile

The actual output looks like this:

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

I believe the expected output should be:

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
                            })
                            ],
                            four: "Hey")
print(example)
```