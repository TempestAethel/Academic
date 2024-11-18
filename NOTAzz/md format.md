# Useful Markdown Syntax

## 1. Headings
Headings are created using `#` symbols. The number of `#` determines the level of the heading.

# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

## 2. Paragraphs
Paragraphs are created by simply writing text without any special symbols. To create a new paragraph, leave a blank line between lines of text.

This is the first paragraph.

This is the second paragraph.

## 3. Lists

### Unordered List
Use `-`, `+`, or `*` for unordered lists.

- Item 1
- Item 2
- Item 3

### Ordered List
Use numbers followed by a period for ordered lists.

1. First item
2. Second item
3. Third item

## 4. Links
Links are created using the following syntax:

[Link Text](http://example.com)

Example:

[OpenAI](https://www.openai.com)

## 5. Images
Images are similar to links, but with an exclamation mark `!` at the beginning.

![Alt Text](http://example.com/image.jpg)

## 6. Emphasis

### Italic
Use one `*` or `_` for italics.

*Italic text*

_Italic text_

### Bold
Use two `**` or `__` for bold text.

**Bold text**

__Bold text__

### Bold and Italic
Combine both for bold and italic text.

***Bold and Italic text***

## 7. Code

### Inline Code
Use backticks (`` ` ``) to wrap inline code.

Example: `let x = 10;`

### Code Block
To create a block of code, you can use three backticks (```` ``` ````) or indent the code with four spaces.

#### Example with three backticks:

```javascript
function helloWorld() {
    console.log("Hello, world!");
}
```

## 8. Blockquotes
Use `>` for blockquotes.

> This is a blockquote.

## 9. Horizontal Rule
Use three hyphens `---`, three asterisks `***`, or three underscores `___` for horizontal rules.

---

## 10. Tables

Create tables using pipes `|` and hyphens `-`.

| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Row 1, Col 1 | Row 1, Col 2 | Row 1, Col 3 |
| Row 2, Col 1 | Row 2, Col 2 | Row 2, Col 3 |

## 11. Task Lists
Use `- [ ]` for an unchecked task and `- [x]` for a completed task.

- [ ] Task 1
- [x] Task 2
- [ ] Task 3

## 12. Strikethrough
Use two tildes `~~` for strikethrough text.

~~This is strikethrough~~

## 13. Footnotes
Create footnotes using `[^1]` syntax and defining the footnote at the bottom.

This is a text with a footnote[^1].

[^1]: This is the footnote text.

## 14. Syntax Highlighting in Code Blocks
You can specify the language for syntax highlighting by adding the language name after the opening triple backticks.

```python
def hello():
    print("Hello, world!")
```

