HTML
====
### Regras básicas de formatação

* Utilizar de dois espaços para o recuo da indentação;
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

* Utilizar somente lowercase;
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

* Não deixar espaço em branco a direita;

* Finalizar cada arquivo html com uma linha em branco.

### Outras regras de formatação

* Para texto em negrito utilizar a tag **strong**;
```html
<!-- Recommended -->
<p><strong>Lorem ipsum</strong></p>

<!-- Not Recommended -->
<p class="font-weight-bold">Lorem ipsum</p>

<!-- Not Recommended -->
<p><b>Lorem ipsum</b></p>
```

* Utilizar da tag **span** somente em casos de estilização dentro de uma outra tag de texto;
```html
<!-- Recommended -->
<p><span>Lorem ipsum</span> dolor sit amet..</p>

<!-- Not Recommended -->
<span>Lorem ipsum</span>
```

* Não utilizar tags **h(h1, h2, h3, h4..)** fora de títulos e subtítulos;
```html
<!-- Recommended -->
<h1>Título do post</h1>
<div class="post-content">
  <p>Primeiro parágrafo</p>
  <p>
    Segundo parágrafo Segundo parágrafo Segundo parágrafo Segundo parágrafo
    Segundo parágrafo Segundo parágrafo Segundo parágrafo Segundo parágrafo
  </p>
</div>

<!-- Not Recommended -->
<h1>Título do post</h1>
<div class="post-content">
  <p>Primeiro parágrafo</p>
  <h2>
    Segundo parágrafo Segundo parágrafo Segundo parágrafo Segundo parágrafo
    Segundo parágrafo Segundo parágrafo Segundo parágrafo Segundo parágrafo
  </h2>
</div>
```

* Utilização da tag **ul** para listas não ordenadas e de **ol** para listas ordenadas;
  * **Lista Ordenada**: É usada para descrever uma coleção ordenada de dados. Os navegadores geralmente exibem uma lista ordenada como uma lista numerada. Crie uma lista ordenada usando a tag **ol**;
  * **Lista Não Ordenada**: É usada para descrever uma coleção não ordenada de dados. Os navegadores geralmente exibem uma lista não ordenada como uma lista com marcadores. Crie uma lista não ordenada usando a tag **ul**.

* Utilizar a tag **main** para o conteúdo principal da página;
```html
<!-- Recommended -->
<html>
  <body>
    <main>
      <h1>Título</h1>
      <h2>Subtítulo</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
    </main>
  </body>
</html>

<!-- Not Recommended-->
<html>
  <body>
    <h1>Título</h1>
    <h2>Subtítulo</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
  <body>
</html>
```

* As tags **input** e **label** devem estar no mesmo wrapper.
```html
<!-- Recommended -->
<div>
  <label for="email">Qual é o seu e-mail?</label>
  <input type="text" id="email">
</div>

<!-- Recommended -->
<div class="form-group">
  <label for="email">Qual é o seu e-mail?</label>
  <div>
    <input type="text" id="email">
  </div>
</div>

<!-- Not Recommended -->
<div class="form-group">
  <label for="email">Qual é o seu e-mail?</label>
</div>
<div class="form-group">
  <input type="text" id="email">
</div>
```

* Utilizar sempre aspas duplas para os atributos;
```html
<!-- Recommended -->
<label for="email">Qual é o seu e-mail?</label>
<input type="text" id="email">

<!-- Not recommended -->
<label for='email'>Qual é o seu e-mail?</label>
<input type='text' id='email'>
```

* O comentário de linha única deve ser colocado antes da tag;
```html
<!-- Recommended -->
<!-- TODO: Trocar este icone para o correto -->
<i class="fab fa-accusoft"></i>

<!-- Not recommended -->
<i class="fab fa-accusoft"></i>
<!-- TODO: Trocar este icone para o correto -->
```

* Os títulos devem ser colocados em ordem hierárquica;
```html
<!-- Recommended -->
<h1>Título</h1>
<h2>Subtítulo</h2>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
<h3>Subtítulo</h3>
  
<!-- Not recommended -->
<h3>Título</h3>
<h2>Subtítulo</h2>
<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
<h1>Subtítulo</h1>
```

* Novas linhas entre a tag e o conteúdo devem ser evitados;
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

* Não omitir tags opcionais;
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

* Utilizar o HTML5;
  * É recomendável utilizar o HTML, logo não use XHTML, XHTML. Não possui suporte a navegador, infraestrutura e oferece menos espaço para otimização que o HTML.

* Use HTTPS para recursos incorporados sempre que possível.
```html
<!-- Recommended -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<!-- Not Recommended -->
<script src="//ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>

<!-- Not Recommended -->
<script src="http://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```

