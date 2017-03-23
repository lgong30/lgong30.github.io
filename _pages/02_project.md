---
layout: default
title: Project
permalink: /project/
---

{% assign projKeys = "projects, gadgets" | split: ", " %}
{% assign isProjectPage = true %}

<div class="row">
    {% for pk in projKeys %}
        {% assign pkh = pk %}
        <div class="col-md-10 col-md-offset-1">
        <h1>{{ pkh | capitalize }}</h1>
        <hr/>
            {% if pk == "projects" %}
            {% assign posts = site.categories.projects %}
            {% else %}
            {% assign posts = site.categories.gadgets %}
            {% endif %}
            {% for post in posts %}
            {% include projects.html %}
            {% endfor %}
        </div>
    {% endfor %}
</div>
