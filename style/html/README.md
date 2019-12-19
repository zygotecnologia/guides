HTML
====
### Basic formatting rules

* Use soft-tabs with a two space indent;
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

* Use only lowercase;
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

### Other formatting rules

* To bold text, use the **strong** tag;
```html
<!-- Recommended -->
<p><strong>Lorem ipsum</strong></p>

<!-- Not Recommended -->
<p class="font-weight-bold">Lorem ipsum</p>

<!-- Not Recommended -->
<p><b>Lorem ipsum</b></p>
```

* Use **span** tag only to apply styles inside from other text tag;
```html
<!-- Recommended -->
<p><span>Lorem ipsum</span> dolor sit amet..</p>

<!-- Not Recommended -->
<span>Lorem ipsum</span>
```

* Don't use tags **h(h1, h2, h3, h4..)** outside titles and subtitles;
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
  <p>Primeiro parágrafo</p>
  <h2>
    Lorem Ipsum is simply dummy text of the printing and typesetting industry.
  </h2>
</div>
```

* The tag **ul** is used in to Unordered lists. **ol** is used in **Ordered lists**.

* Use the **main** tag to the main content of the page;
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

* **Input** and **label** tags must be in the same wrapper;
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

* Always use double quotes for attributes;
```html
<!-- Recommended -->
<label for="email">What's your e-mail?</label>
<input type="text" id="email">

<!-- Not recommended -->
<label for='email'>What's your e-mail?</label>
<input type='text' id='email'>
```

* Single line comment must be placed before tag;
```html
<!-- Recommended -->
<!-- TODO: Trocar este icone para o correto -->
<i class="fab fa-accusoft"></i>

<!-- Not recommended -->
<i class="fab fa-accusoft"></i>
<!-- TODO: Trocar este icone para o correto -->
```

* Headlines must be places in hierarchical order;
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

* Newline between tag name and content must be avoided;
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

* Don't omit optional closing tags;
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

* Use HTML5;
  * It’s recommended to use HTML, as text/html. Do not use XHTML. XHTML, as application/xhtml+xml, lacks both browser and infrastructure support and offers less room for optimization than HTML.

* Use HTTPS for embedded resources where possible..
```html
<!-- Recommended -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<!-- Not Recommended -->
<script src="//ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<!-- Not Recommended -->
<script src="http://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```

* For navigation block, use **nav** structure with **ul** ou **ol**, **li** and **a**;
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
