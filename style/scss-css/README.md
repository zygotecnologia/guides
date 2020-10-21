Scss and CSS
====

- [Scss and CSS](#scss-and-css)
- [Formatting and spacing](#formatting-and-spacing)
  - [File formatting](#file-formatting)
- [General rules](#general-rules)
  - [Do not use ID selectors](#do-not-use-id-selectors)
  - [Always use semicolon after each property](#always-use-semicolon-after-each-property)
  - [Always show zeros to the left, never shows zeros to the right](#always-show-zeros-to-the-left-never-shows-zeros-to-the-right)
  - [Use only one space only after the colon](#use-only-one-space-only-after-the-colon)
  - [Always use hexadecimal colors](#always-use-hexadecimal-colors)
  - [When dealing with numbers, zeros should not have a unit](#when-dealing-with-numbers-zeros-should-not-have-a-unit)
  - [Put a space before the opening brace `{` in rule declarations. Put closing braces `}` of rule declarations on a new line.](#put-a-space-before-the-opening-brace--in-rule-declarations-put-closing-braces--of-rule-declarations-on-a-new-line)
  - [Put blank lines between rule declarations.](#put-blank-lines-between-rule-declarations)
  - [Write CSS/SCSS in SMACSS format](#write-css/scss-in-smacss-format)

---------------------------------------------

# Formatting and spacing
## File formatting
* Use 2 space indentation (no tabs).
* Never leave trailing whitespace.
* When needed, always use double quotes.
* End each file with a newline.
* Mobile code comes first in the file.
* Partials are named _partial.scss
* Never use `inline-css`. Expcept as last resource in emails.
* Nested selector maximum deep: 5 classes

# General rules

## Do not use ID selectors
```css

#tag-id {
  some: css;
  ...
}

```
## Always use semicolon after each property
```css

/* Recommended */
.test {
  display: block;
  height: 100px;
}

/* Not recommended */
.test {
  display: block;
  height: 100px
}

```

## Always show zeros to the left, never shows zeros to the right

```css
/* Recommended */
.foo {
  padding: 2em;
  opacity: 0.5;
}

/* Not recommended */
.foo {
  padding: 2.0em;
  opacity: .5;
}
```

## Use only one space only after the colon

```css
/* Recommended */
h3 {
  font-weight: bold;
}

/* Not recommended */
h3 {
  font-weight:bold;
}

h3 {
  font-weight : bold;
}

h3 {
  font-weight :bold;
}
```

## Always use hexadecimal colors
* When using colors use the hexadecimal equivalent.
* The value must be in uppercase
* If all characters of the value are equal use the the shorthand instead

```css
/* Recommended */
p {
  color: #FFF;
}

/* Not recommended */
p {
  color: #ffffff;
}

p {
  color: #fff;
}

p {
  color: #FFFFFF;
}

p {
  color: white;
}
```

## When dealing with numbers, zeros should not have a unit

```css
/* Recommended */
$length: 0;

/* Not recommended */
$length: 0em;
```

## Put a space before the opening brace `{` in rule declarations. Put closing braces `}` of rule declarations on a new line.
```css
/* Recommended */
.foo {
  padding: 2em;
}

/* Not recommended */
.foo{
  padding: 2em;
}

.foo{
  padding: 2em; }

.foo{ padding: 2em; }
```
## Put blank lines between rule declarations.
```css
/* Recommended */
.foo {
  padding: 2em;
}

.second-foo {
  padding: 3em;
}

.third-foo {
  padding: 4em;
}

/* Not recommended */
.foo {
  padding: 2em;
}
.second-foo {
  padding: 3em;
}
.third-foo {
  padding: 4em;
}
```

## Sort element properties based on SMACSS rules
The properties should follow [SMACSS rules](http://smacss.com/book/formatting).

Order:
1. Box
2. Border
3. Background
4. Text
5. Other

Separate each block with an empty line.

To make this rule easier to follow you can use [sass-lint](https://github.com/sasstools/sass-lint) with the following configuration:

```yaml
rules:
  property-sort-order:
    - 1
    -
      order: 'smacss'
```

```css
/* Recommended */
.class {
  display: flex;
  height: 20px;
  margin: 10px;
  padding: 10px;
  position: absolute;
  width: 30px;

  border: 1px solid #CCC;

  align-content: center;
  color: red;
  cursor: pointer;
  font-size: 40px;
  z-index: 9999;
}

/* Not recommended (no space between blocks) */
.class {
  padding: 0;
  width: 100px;
  font-size: 1.25em;
  z-index: 1;
}

/* Not recommended (wrong order) */
.class {
  cursor: pointer;
  color: red;
  z-index: 1;
  width: 200px;
  font-size: 1.25em;
  position: relative;
  margin: 0 auto;
}
```

## Write CSS/SCSS in SMACSS format

* Keep classes lowercase and use dashes (not underscores or camelCase). Dashes serve as natural breaks in related class (e.g., .btn and .btn-danger).
```css
/* Recommended */
.btn-danger {
  ...
}

/* Not recommended */
.btnDanger {
  ...
}
```

* Avoid excessive and arbitrary shorthand notation. .btn is useful for button, but .s doesn't mean anything.

* Use meaningful names; use structural or purposeful names over presentational.

* Keep classes as short and succinct as possible.
```css
/* Recommended */
.btn-danger {
  ...
}

/* Not recommended */
.round-danger-button-with-white-letter {
  ...
}
```
* Prefix classes based on the closest parent or base class.
