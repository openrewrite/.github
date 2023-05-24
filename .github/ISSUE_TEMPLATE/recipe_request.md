---
name: Recipe request
about: Suggest a new recipe for this project
title: ''
labels: 'recipe'
assignees: ''
---
<!--
Thank you for suggesting a new recipe for OpenRewrite!
Feel free to delete any sections that don't apply to your request.
-->

## What problem are you trying to solve?

<!-- A description of a problem you encounter that you hope to resolve with a recipe. -->

## What precondition(s) should be checked before applying this recipe?

<!-- Should we limit execution to certain versions of languages or libraries for instance? -->

## Describe the situation before applying the recipe

<!-- Ideally as a self-contained code example, as a start to the recipe unit tests. -->

```java
class A {
    void foo(String bar) {
        int i = Integer.valueOf(bar);
    }
}
```

## Describe the situation after applying the recipe

<!-- Ideally as a self-contained code example, as a start to the recipe unit tests. -->

```java
class A {
    void foo(String bar) {
        int i = Integer.parseInt(bar);
    }
}
```

## Have you considered any alternatives or workarounds?

<!-- Any other ways to solve the problem, or ways to work around the problem. -->

## Any additional context

<!-- Any thoughts such as considerations and limitations when applying this recipe, or hints on the implementation. -->

## Are you interested in [contributing this recipe to OpenRewrite](https://github.com/openrewrite/.github/blob/main/CONTRIBUTING.md#adding-new-recipes)?

<!-- Indicate if this is something you would like to work on, and how we can best support you in doing so. -->
