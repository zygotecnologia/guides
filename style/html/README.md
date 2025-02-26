HTML
====
* List and description of the usable HTML tags:
[usable tags](USABLE_TAGS.md)

- [HTML](#html)
- [Formatting and Spacing](#formatting-and-spacing)
  - [Use soft-tabs with a two space indent;](#use-soft-tabs-with-a-two-space-indent)
  - [Use only lowercase;](#use-only-lowercase)
- [Tag use rules](#tag-use-rules)
  - [To bold text, use the **strong** tag;](#to-bold-text-use-the-strong-tag)
  - [Use **span** tag only to apply styles inside from other text tag;](#use-span-tag-only-to-apply-styles-inside-from-other-text-tag)
  - [Don't use tags **h(h1, h2, h3, h4..)** outside titles and subtitles;](#dont-use-tags-hh1-h2-h3-h4-outside-titles-and-subtitles)
  - [The tag **ul** is used in **Unordered** lists. **ol** is used in **Ordered lists**.](#the-tag-ul-is-used-in-unordered-lists-ol-is-used-in-ordered-lists)
  - [Use the **main** tag to the main content of the page;](#use-the-main-tag-to-the-main-content-of-the-page)
  - [**Input** and **label** tags must be in the same wrapper;](#input-and-label-tags-must-be-in-the-same-wrapper)
  - [Always use double quotes for attributes;](#always-use-double-quotes-for-attributes)
  - [Single line comment must be placed before tag;](#single-line-comment-must-be-placed-before-tag)
  - [Headlines must be places in hierarchical order;](#headlines-must-be-places-in-hierarchical-order)
  - [Newline between tag name and content must be avoided;](#newline-between-tag-name-and-content-must-be-avoided)
  - [Don't omit optional closing tags;](#dont-omit-optional-closing-tags)
  - [Use HTML5;](#use-html5)
  - [Use HTTPS for embedded resources where possible..](#use-https-for-embedded-resources-where-possible)
  - [For navigation block, use **nav** structure with **ul** or **ol**, **li** and **a**;](#for-navigation-block-use-nav-structure-with-ul-or-ol-li-and-a)
  - [The `<br>` tag should be used only inside a `<p>` tag, and never more than one in a row;](#the-br-tag-should-be-used-only-inside-a-p-tag-and-never-more-than-one-in-a-row)
  - [The `<br>` tag should be always alone in a new line;](#the-br-tag-should-be-always-alone-in-a-new-line)
  - [Use **`<figure>`** tag and **`<figcaption>`** tag for figures with subtitles ;](#use-figure-tag-and-figcaption-tag-for-figures-with-subtitles-)
  - [Use **`alt`** attribute for **`<img>`** tag. The text should describe the image;](#use-alt-attribute-for-img-tag-the-text-should-describe-the-image)
  - [Block, list and table elements MUST start on a new line and their children MUST be indented.](#block-list-and-table-elements-must-start-on-a-new-line-and-their-children-must-be-indented)
  - [Use **`data-atributes`** to attribute **`Javascript`** actions.](#use-data-atributes-to-attribute-javascript-actions)

# Formatting and Spacing

## Use soft-tabs with a two space indent;
```html
<!-- Recommended -->
<main>
  <section>
    <p>Lorem ipsum</p>
  </section>
</main>

<!-- Not Recommended -->
<main>
	<section>
		<p>Lorem ipsum</p>
	</section>
</main>
```

## Use only lowercase;
```html
<!-- Recommended -->
<main>
  <section class="zygo">
    <p>Lorem ipsum</p>
  </section>
</main>

<!-- Not Recommended -->
<Main>
  <SECTION CLASS="zygo">
    <p>Lorem ipsum</p>
  </SECTION>
</Main>
```

* Never leave trailing whitespace;

* End each file with a newline.

# Tag use rules

## To bold text, use the **strong** tag;
```html
<!-- Recommended -->
<p><strong>Lorem ipsum</strong></p>

<!-- Not Recommended -->
<p class="font-weight-bold">Lorem ipsum</p>

<!-- Not Recommended -->
<p><b>Lorem ipsum</b></p>
```

## Use **span** tag only to apply styles inside from other text tag;
```html
<!-- Recommended -->
<p><span>Lorem ipsum</span> dolor sit amet..</p>

<!-- Not Recommended -->
<span>Lorem ipsum</span>
```

## Don't use tags **h(h1, h2, h3, h4..)** outside titles and subtitles;
```html
<!-- Recommended -->
<h1>Post Title</h1>
<div class="post-content">
  <p>First paragraph</p>
  <p>
    Lorem Ipsum is simply dummy text of the printing and typesetting industry.
  </p>
</div>

<!-- Not Recommended -->
<h1>Post Title</h1>
<div class="post-content">
  <p>First paragraph</p>
  <h2>
    Lorem Ipsum is simply dummy text of the printing and typesetting industry.
  </h2>
</div>
```


## The tag **ul** is used in **Unordered** lists. **ol** is used in **Ordered lists**.
```html
<!-- Recommended -->
<ul>
  <li class="row">
    <div class="col-6">
      user name
    </div>
    <div class="col-6">
      user email
    </div>
  </li>
</ul>

<ol>
  <li class="row">
    <div class="col-6">
      user purchase date
    </div>
    <div class="col-6">
      user purchase value
    </div>
  </li>
</ol>

<!-- Not Recommended -->

<div>
  <div class="row">
    <div class="col-6">
      user name
    </div>
    <div class="col-6">
      user email
    </div>
  </div>
</div>

<div>
  <div class="row">
    <div class="col-6">
      user purchase date
    </div>
    <div class="col-6">
      user purchase value
    </div>
  </div>
</div>

```

## Use the **main** tag to the main content of the page;
```html
<!-- Recommended -->
<html>
  <body>
    <main>
      <h1>Title</h1>
      <h2>Subtitle</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
    </main>
  </body>
</html>

<!-- Not Recommended-->
<html>
  <body>
    <h1>Title</h1>
    <h2>Subtitle</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
  <body>
</html>
```

## **Input** and **label** tags must be in the same wrapper;
```html
<!-- Recommended -->
<div>
  <label for="email">What's your e-mail?</label>
  <input type="text" id="email">
</div>

<!-- Recommended -->
<div class="form-group">
  <label for="email">What's your e-mail?</label>
  <div>
    <input type="text" id="email">
  </div>
</div>

<!-- Not Recommended -->
<div class="form-group">
  <label for="email">What's your e-mail?</label>
</div>
<div class="form-group">
  <input type="text" id="email">
</div>
```

## Always use double quotes for attributes;
```html
<!-- Recommended -->
<label for="email">What's your e-mail?</label>
<input type="text" id="email">

<!-- Not recommended -->
<label for='email'>What's your e-mail?</label>
<input type='text' id='email'>
```

## Single line comment must be placed before tag;
```html
<!-- Recommended -->
<!-- TODO: Trocar este icone para o correto -->
<i class="fab fa-accusoft"></i>

<!-- Not recommended -->
<i class="fab fa-accusoft"></i>
<!-- TODO: Trocar este icone para o correto -->
```

## Headlines must be places in hierarchical order;
```html
<!-- Recommended -->
<h1>Title</h1>
<h2>Subtitle</h2>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
<h3>Subtitle</h3>

<!-- Not recommended -->
<h3>Title</h3>
<h2>Subtitle</h2>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
<h1>Subtitle</h1>
```

## Newline between tag name and content must be avoided;
```html
<!-- Recommended -->
<div>
  <p> lorem ipsum </p>
</div>

<!-- Not recommended -->
<div>

  <p> lorem ipsum </p>
</div>
```

## Don't omit optional closing tags;
```html
<!-- Recommended -->
<!DOCTYPE html>
<html>
  <head>
    <title>Spending money, spending bytes</title>
  </head>
  <body>
    <p>Sic.</p>
  </body>
</html>

<!-- Not recommended -->
<!DOCTYPE html>
<title>Saving money, saving bytes</title>
<p>Qed.
```

## Use HTML5;
  * It’s recommended to use HTML, as text/html. Do not use XHTML. XHTML, as application/xhtml+xml, lacks both browser and infrastructure support and offers less room for optimization than HTML.

## Use HTTPS for embedded resources where possible..
```html
<!-- Recommended -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<!-- Not Recommended -->
<script src="//ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<!-- Not Recommended -->
<script src="http://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```

## For navigation block, use **nav** structure with **ul** or **ol**, **li** and **a**;
```html
<!-- Recommended -->
<nav>
  <ul>
    <li><a href="#">Item one</a></li>
    <li><a href="#">Item two</a></li>
    <li><a href="#">Item three</a></li>
  </ul>
<nav>

<!-- Recommended -->
<nav>
  <ol>
    <li><a href="item1">Item one</a></li>
    <li><a href="item1/subitem1">Subitem one</a></li>
    <li><a href="#">Item</a></li>
  </ol>
<nav>

<!-- Not Recommended -->
<nav>
  <ul>
    <li>Item one</li>
    <li>Item two</li>
    <li>Item three</li>
  </ul>
<nav>

<!-- Not Recommended -->
<nav>
  <a href="#">Item one</a>
  <a href="#">Item two</a>
  <a href="#">Item three</a>
<nav>
```

## The `<br>` tag should be used only inside a `<p>` tag, and never more than one in a row;
```html
<!-- Recommended -->
<div>
  <p>
    lorem ipsum
    <br>
    dolor
    <br>
    sit amet
  </p>
</div>

<!-- Not recommended -->
<div>
  <p>
    lorem ipsum
    <br><br><br>
    dolor
    <br><br>
    sit amet
  </p>
</div>

<!-- Not recommended -->
<div>
  <span>
    lorem ipsum
    <br>
    dolor
    <br>
    sit amet
  </span>
</div>
```

## The `<br>` tag should be always alone in a new line;
```html
<!-- Recommended -->
<div>
  <p>
    lorem ipsum
    <br>
    dolor
    <br>
    sit amet
  </p>
</div>

<!-- Not recommended -->
<div>
  <p>
    lorem ipsum <br> dolor <br> sit amet
  </p>
</div>
```

## Use **`<figure>`** tag and **`<figcaption>`** tag for figures with subtitles ;
```html
<!-- Recommended -->
<figure>
  <img src="pic_trulli.jpg" alt="Trulli">
  <figcaption>Fig.1 - Trulli, Puglia, Italy.</figcaption>
</figure>

<!-- Not recommended -->
<img src="pic_trulli.jpg" alt="Trulli">
<p>Fig.1 - Trulli, Puglia, Italy.</p>
```

## Use **`alt`** attribute for **`<img>`** tag. The text should describe the image;
```html
<!-- Recommended -->
<img src="smiley.gif" alt="Smiley face">

<!-- Not recommended -->
<img src="smiley.gif">
```

## Block, list and table elements MUST start on a new line and their children MUST be indented.
```html
<!-- Recommended Block -->
<div>
  <div>
    <div>
      Hello world
    </div>
  </div>
</div>

<!-- Not recommended Block -->
<div>
<div>
<div>
Hello World
</div>
</div>
</div>

<div><div><div>
Hello World
</div></div></div>

<!-- Recommended list -->
<ul>
  <li> 1 </li>
  <li> 2 </li>
  <li> 3 </li>
</ul>

<ul>
  <li>
    <div>
      1
    </div>
  </li>
  <li>
    <div>
      2
    </div>
  </li>
  <li>
    <div>
      3
    </div>
  </li>
</ul>

<!-- Not Recommended list -->
<ul>
<li>
1
</li>
<li>
2
</li>
<li>
3
</li>
</ul>

<ul><li>1</li>
<li>2</li>
<li>3</li></ul>


<!-- Recommended Table -->
<table>
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
</table>

<table>
  <tr>
    <th>
      <div>
        Month
      </div>
    </th>
    <th>
      <div>
        Savings
      </div>
    </th>
  </tr>
  <tr>
    <td>
      <div>
        January
      </div>
    </td>
    <td>
      <div>
        $100
      </div>
    </td>
  </tr>
</table>

<!-- Not Recommended Table -->

<table>
<tr>
<th>Month</th>
<th>Savings</th>
</tr>
<tr>
<td>January</td>
<td>$100</td>
</tr>
</table>

<table>
  <tr><th>Month</th><th>Savings</th></tr>
  <tr><td>January</td><td>$100</td></tr>
</table>

```

## Use **`data-atributes`** to attribute **`Javascript`** actions.
```html
<!-- Recommended -->
<button type="button" class="btn btn-primary" data-click-here> Clique Aqui </button>

<!-- Recommended -->
<button type="button" class="btn btn-primary" data-update-user="2"> Atualizar Usuário </button>

<!-- Not recommended -->
<button type="button" class="btn btn-primary js--click-here"> Clique Aqui </button>

<!-- Not recommended -->
<button type="button" class="btn btn-primary js--update-users" data-user="2"> Atualizar Usuário </button>
```
