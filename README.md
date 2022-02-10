# Markdown docs

A documentation parser from Markdown to HTML.

## Understanding the parsing basics.

The parsing process is probably one of the most difficult tasks to handle in the IT world.
But, ***what the hell is parsing?***

Parsing is the process of getting information with a given format and converting that input into an output formatted in a different way.

For example parsing the date formats from:

```tsx
 const myDate = "20/12/2020 11:50"; // Format dd/MM/yyyy hh:mm
```

To the following date format

```tsx
const myParsedDate = "2020/12/20 11:50"; // Format yyyy/MM/dd hh:mm
```

To get the information inside the text **the code must understand the patterns living inside.**

## Converting patterns into blocks

The code will take some piece of plain text and get the information blocks inside of it. So we need some kind of program to handle that, lets call it the **tokenizer.** 

Imagine the following Markdown text

```markdown
# My title here
> aside paragraph for better visibility

## Secondary title here
Normal text with **bold** and *italic* 
```

The blocks inside

```html
Title: My title here
Aside: aside paragraph for better visibility

SecondaryTitle: Secondary title here
Text: Normal text with [Bold:bold] and [Italic: italic] 
```

The expected HTML output for our library

```html
<h1>My title here</h1>
<pre>
 aside paragraph for better visibility
</pre>

<h2>Secondary title here</h2>
<p>Normal text with <b>bold</b> and <i>italic</i></p>
```

The **tokenizer** must understand Markup language to get the block structure inside of it, but it is not the one who must translate that structure to the HTML output, that’s why we have another worker here, the **translator.**

## Translating the Abstract Block Tree into different languages.

Yes, a translator must now the language you want it to work on, but if your parser is anyway modular, chances are that upgrading it with two or three of them  wont be a problem at all.

The basic idea here is that if the abstract tree is well formed, the translator will make basic comparative operations such us:

```tsx
public String render( blocks : Block[] ) {
	let output = "";

	blocks.forEach(block -> {
		if(block.type == "Text") {
			output += "<p>" + render(block.children) + "</p>";
		}
		
		if(block.type == "Title") {
			output += "<h1>" + render(block.children) + "</h1>";
		}

		// --- Other type checkings ---

		return block.text;
	});

	return output;
}
```

[Starting to code.](pages/1.StartingToCode.md)

[Coding base abstractions](pages/2.CodingBaseAbstractions.md)

[Problems](pages/3.Problems.md)