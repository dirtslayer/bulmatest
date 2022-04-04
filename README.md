# Sample project using bulma.io and showdown.js together

Bulma.io is a scss framework for making web pages look nice. It adds things like spacing and rounded borders - the look is similar to bootstrap.

If you are new to node, the first thing you will want to look at here is package.json

```json
"scripts": {
    "start": "http-server -o -c-1 -p 8081",
    "scss": "node-sass scss/ -o css --include-path node_modules/bulma",
    "postscss": "postcss --use autoprefixer --output css/index.css css/index.css"
  }
```
So one would use npm run with start and scss (postscsss runs automatically).
```
$npm run scss
```
What is interesting here is the --include-path part. In line 1 of index.scss there is an incantation 
```css
@import "bulma"
```
So, our main index.html file does not have any bulma stylesheets imported, and all the classes and mixins from bulma are available here now.

Showdown.js did not add any classes to the output, so we extend the bulma base class into the default class:
```css
table {
  @extend .table;
}
```
the alternative is commented out in ./md/showdown.html, which is
use js to apply the table class (not as cool)

So, the final result of our markdown slid into our html, transformed with showdown and styled with bulma looks like this:

https://dirtslayer.github.io/bulmatest/md/showdown.html

So this is one way, but, i'd rather not have my page additionally load the showdown library when we can do this work as a build step.

Enter phtml. We can run showdown on an md file, and use a phtml include to insert it into a page.

```json
"scripts": {
    "start": "http-server -o -c-1 -p 8081",
    "md2html": "showdown makehtml -i md/logic\\ symbols.md -c tables github > html/logic\\ symbols.html",
    "phtml2html": "phtml html/bulma\\ logic.phtml html/output.html -p @phtml/include",
    "scss": "node-sass scss/ -o css --include-path node_modules/bulma",
    "postscss": "postcss --use autoprefixer --output css/index.css css/index.css"
  }
```




