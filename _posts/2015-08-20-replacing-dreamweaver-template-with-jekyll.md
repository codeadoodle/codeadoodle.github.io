---
layout: post
date: "2015-08-20 00:00:00"
categories: 
  - "tutorials"
published: true
title: Replacing Dreamweaver Template with Jekyll
---

One of Dreamweaver's [indispensable timesaving feature](http://www.onlamp.com/pub/a/web-development/excerpts/0636920001393/templates-ch19.html) is "Templates" to help you quickly build similar-looking pages and update every page in your site with the click of a button. Despite powerful text editor feature like Sublime Text, it is still not as practical as Dreamweaver Site Template feature to manage multiple pages. Now, I can achieve similar functionality using [Jekyll static page](http://jekyllrb.com/docs/pages/) and take advantage of much more powerful [Shopify Liquid](https://docs.shopify.com/themes/liquid-documentation/basics), an open-source Ruby-based template language, to load dynamic content.

To  start, update jekyll `_config.yml` with

```
include:
  - "_pages"
```

Create your global main page template, called _main.html_ at `_layouts` and include `{{content}}` tag to indicate editable region:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <title>{% if page.title %}{{ page.title }} &#8211; {% endif %}{{ site.name }} &#8211; {{ site.description }}</title>
  <meta name="description" content="{% if page.summary %}{{ page.summary }}{% else %}{{ site.meta_description }}{% endif %}" />
  <meta name="author" content="{{ site.author }}"> {% if page.categories %}
  <meta name="keywords" content="{{ page.categories | join: ', ' }}">{% endif %}
  <link rel="canonical" href="{{ page.url | replace:'index.html','' | prepend: site.baseurl | prepend: site.url }}">
  <meta name="HandheldFriendly" content="True" />
  <meta name="MobileOptimized" content="320" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
  <!-- Optional theme -->
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap-theme.min.css">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css">
  <!-- Customisation  -->
  <link rel="stylesheet" type="text/css" href="/assets/css/site.css" />
  <meta property="og:locale" content="en_US">
  <meta property="og:type" content="article">
  <meta property="og:title" content="{% if page.title %}{{ page.title }}{% else %}{{ site.title }}{% endif %}">
  <meta property="og:description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
  <meta property="og:url" content="{{ site.url }}{{ page.url }}">
  <meta property="og:site_name" content="{{ site.title }}"> </head>

<body> {{ content }}
  <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
  <!-- Latest compiled and minified JavaScript -->
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
</body>
</html>
```

To accommodate common UI components across some of the pages, you can create sub-template called _bootstrap.html_ with `layout` key value referring to parent template's file name (e.g. _main_). 

```html
---
layout: main
---
<div id="container"> 
    <div class="row">
      <div class="page-header clearfix">
        <h1 class="pull-left">{{ page.title }}</h1> </div> {{content}} </div>
    <!-- /.row-->
    <div class="row">
      <footer>
        <div id="footer">
          <hr/> <small>
            <p class="text-muted"><a href="{{ site.baseurl }}">{{ site.name }}</a> &copy; {{date format="YYYY"}} &bull; All rights reserved.</p>
            </small> </div>
      </footer>
    </div>
    <!-- /.row -->
</div>
<!-- /#container -->

```

You can also include another _html_ files as part of the template if they are placed in jekyll's `includes` folder, e.g.  _navbar.html_. This is useful to make your template code more readable and manageable using following `{\% include navbar.html \%}`: 
      

```html
<nav class="navbar navbar-default navbar-fixed-top" role="navigation">
  <div class="navbar-header"> <a class="navbar-brand" href="{{site.baseurl}}">{{ site.name }}</a>
    <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".sidebar-collapse"> <span class="sr-only">Toggle navigation</span> <i class="fa fa-bars"></i> </button>
    <button type="button" id="nav-toggle" class="navbar-toggle" data-toggle="collapse" data-target="#main-nav"> <span class="sr-only">Toggle navigation</span> <i class="fa fa-ellipsis-h"></i> </button>
  </div>
  <!-- /.navbar-header -->
  <div id="main-nav" class="collapse navbar-collapse">
    <ul class="nav navbar-nav">
      <li><a href="#">Page 1</a></li>
      <li><a href="#">Page 2</a></li>
      <!-- /.dropdown -->
    </ul>
  </div>
  <!--/#main-nav .navbar-collapse-->
</nav>
<!-- /.navbar-fixed-top -->
```

Create your actual page called _hello.html_ in jekyll's `_pages` folder which refer to specific page template to apply.

```html
---
layout: bootstrap
title: "Hello World"
permalink: /hello-world/
---
<main id="content" class="content" role="main">
  <div class="panel panel-default">
    <div class="panel-heading">Panel Title</div>
    <div class="panel-body"> Some content </div>
  </div>
</main>
```

The page is available @ _http://localhost:4000/hello-world/_ after Jekyll build. Note that you can set relevant page and site level parameters for the templates to render, thus making your template more flexible and reusable.
