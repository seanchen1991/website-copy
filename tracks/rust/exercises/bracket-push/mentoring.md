### Concepts

- stack or recursion

### Reasonable solutions

A reasonable solution should do the following:

### Examples

```rust
#[derive(PartialEq)]
enum BracketTypes {
    Parenthesis,
    Square,
    Curly,
}

pub fn brackets_are_balanced(string: &str) -> bool {
    let mut bracket_stack = Vec::new();

    for ch in string.chars() {
        use BracketTypes::*;

        match ch {
            '(' => bracket_stack.push(Parenthesis),
            '[' => bracket_stack.push(Square),
            '{' => bracket_stack.push(Curly),
            ')' => {
                if bracket_stack.pop() != Some(Parenthesis) {
                    return false;
                }
            },
            ']' => {
                if bracket_stack.pop() != Some(Square) {
                    return false;
                }
            },
            '}' => {
                if bracket_stack.pop() != Some(Curly) {
                    return false;
                }
            },
            _ => {},
        }
    }

    bracket_stack.is_empty()
}
```

```rust
pub fn brackets_are_balanced(string: &str) -> bool {
    let complement = |c| match c {
        '[' => ']',
        '{' => '}',
        '(' => ')',
        _ => unreachable!(),
    };

    let mut expected: Vec<char> = vec![];

    for c in string.chars() {
        match c {
            '(' | '[' | '{' => expected.push(complement(c)),
            ')' | ']' | '}' => if expected.pop() != Some(c) {
                return false;
            },
            _ => {}
        }
    }

    expected.is_empty()
}
```

### Common Suggestions


