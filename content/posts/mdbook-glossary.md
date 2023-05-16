---
title: "Glossary webpage with yaml and mdBook"
date: 2023-05-16T22:00:00+01:00
draft: false
---

# Introduction 

Today I finished my work on a glossary page. My goal was to have a single source of truth, 
for wording which is used in my company and definition and translations to it.

So I decided to use a *.yaml file to save source strings of the wordings, definitions and 
their translations. I made a basic iterable structure with key/value pairs for the term, an 
abstract and a description. See the following example to get a notion:

```yaml
glossary:
  - term-de: Haus
    term-en: House
    abstract-de: Gebäude mit Wänden und einem Dach.
    abstract-en: Building with walls and a roof.
    description-de: Meistens eine Gebäude das Schutz vor Wind und Wetter bietet.
    description-en: Often a building which offers protection from wind and weather.
  - term-de: Keller
    term-en: Cellar
    [...]
```

Because the file is written in YAML it is possible to use Node.js and parsers like 
[js-yaml](https://www.npmjs.org/package/js-yaml) to transform the file into different formats.

# mdBook

[mdBook](https://rust-lang.github.io/mdbook) is easy to use static site generator to create simple
sites based from markdown files. You can generate an overview file called SUMMARY.md which describes
the basic structure of the "book". You can add a landing page and links to files which represents single
chapters.

Based on this structure I created a Node.js script which creates a landing page with a table having
all words and their translations.
There is also, a chapter page create out of every term with all information about it including translation
and definition of the term in differnt languages.

# Convenience and quality

To hold the quality of the source file high I added Prettier as code formatter. 

Also, there is a script which sorts all terms in the yaml file, this has two advantages: First 
finding terms in the yaml file is easier and also, the terms are sorted in the generated mdBook Page.

Last tool is a linting tool, to check the basic structure of the yaml file so the script does not 
fail generating the mdBook page.

