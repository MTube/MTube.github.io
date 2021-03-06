# MTube
- an example user profile

## how it works
- static pages for profile and upload are in the root folder. 
- home pages for each course/module which have topics as a series. have 2 modules pre-loaded, so let's just populate those.

## how to change the site title and default layouts
- go to `_config.yml` and you can see the site settings, it's basically in YAML markup, which is just another form of markup [DOCS](http://jekyllrb.com/docs/configuration/), you can set global site variables here
- there are layouts that you can choose from in the `_layouts` folder, this is pretty straightforward and to make sure they all share the same `head`, `footer` and `header` HTML content, those are stored (and can be edited in the files) in `_includes`
- CSS is written using SASS, that can be installed using ruby gems, but you don't really need it as jekyll builds it for you (i think). [basic sass is here](http://sass-lang.com/guide) - it's like CSS but with variables and more awesome basically, and it's not too different

## course home pages
Take the comp module for example
- in `_comp`, this stores all topic pages in the module/course
- in `comp`, this stores the module home page as `index.html` - the home page should be edited here

## refer to topics in this module in your code 
- use a for loop or if or some loop, documentation is [here](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)

e.g. for the math collection, I want to generate a link to every topic that I have created:
```
{% for math in site.math %}
    <li>
	    <h2>
	      <a class="post-link" href="{{ math.url | prepend: site.baseurl }}">{{ math.title }}</a>
	    </h2>
	{% endfor %}
    </li>
```


### How to create a new course/module 
1. go to `config.yml` 
2. add a new collection following the `comp` and `math` presets
i.e.:

```
collections:
- newmodule

collections:
  newmodule:
    output: true

defaults:
  -
    scope:
      path: ""
      type: newmodule
    values:
      layout: (choose a layout)
```

3. create two new folders:
- `_newmodule` - this will store all topic pages
- `newmodule` - only create an `index.html` page in this file, and any "lecturer pages", basically, anything that is not a recurring series can be stored in this file as a static page