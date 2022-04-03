# Sample project using bulma.io and showdown.js together

Bulma.io is a scss framework for making web pages look nice. It adds things like spacing and rounded borders - the look is similar to bootstrap.

If you are new to node, the first thing you will want to look at here is package.json

```
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
What is interesting here is the --include-path part. In line 1 of index.scss there is an incantation @import "bulma"

So, our main index.html file does not have any bulma stylesheets imported, and all the classes and mixins from bulma are available here now.

One thing about showdown.js, is the output did not add any classes to the output, so we extend the bulma base class into the default class:
```
table {
  @extend .table;
}
```
the alternative is commented out in ./md/showdown.html, which is
use js to apply the table class (not as cool)

