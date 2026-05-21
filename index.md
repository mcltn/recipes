---
layout: default
title: Recipes
---

# Welcome to Recipes

Add your favorite recipes by creating markdown files in the `recipes/` folder.

## All Recipes

{% assign recipes = site.pages | where_exp: "page", "page.path contains 'recipes'" | sort: "title" %}

{% if recipes.size > 0 %}
<div class="recipes-grid">
    {% assign categories = "" | split: "" %}
    {% for recipe in recipes %}
        {% if recipe.category %}
            {% assign categories = categories | push: recipe.category | uniq %}
        {% endif %}
    {% endfor %}

    {% for category in categories | sort %}
        <h3 class="category-title">{{ category }}</h3>
        <div class="recipes-list">
            {% for recipe in recipes %}
                {% if recipe.category == category %}
                    <div class="recipe-card-home">
                        <h4><a href="{{ recipe.url | relative_url }}">{{ recipe.title }}</a></h4>
                        {% if recipe.servings %}<p class="recipe-meta-small">Servings: {{ recipe.servings }}</p>{% endif %}
                        {% if recipe.prep_time or recipe.cook_time %}
                            <p class="recipe-meta-small">
                                {% if recipe.prep_time %}Prep: {{ recipe.prep_time }}{% endif %}
                                {% if recipe.cook_time %} | Cook: {{ recipe.cook_time }}{% endif %}
                            </p>
                        {% endif %}
                    </div>
                {% endif %}
            {% endfor %}
        </div>
    {% endfor %}
{% else %}
    <p class="empty-message">No recipes yet. Create a markdown file in the `recipes/` folder to get started!</p>
{% endif %}
