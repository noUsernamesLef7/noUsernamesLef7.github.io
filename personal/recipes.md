---
layout: default
date: 2020-08-03
author: Jason Brown
title: Recipes
---
These are some of the recipes that I've either written myself or adapted from other recipes.

{% for recipe in site.recipes %}
* [{{ recipe.title }}]({{ recipe.url }}) by {{recipe.author}}
{% endfor %}
