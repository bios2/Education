---
title: Contributing to Lessons
layout: generic
---

# Guidelines for contributors and content editors

This document details our recommended processes to [update current content](#update), [suggest changes to content](#suggest), and [fork content for your own use](#fork), as well as an introduction to [how the content is organized](#structure) and the [tools we use to display content](#tools).

This repository was developed by the DataONE Community Engagement and Outreach Working Group and continues to be maintained by members of this team. Thank you for your interest in contributing to these educational materials.

---

## Update current content <a id="update"></a>
Want to update a link or method? See a spelling error? Changes can be easily proposed by opening the [GitHub Education page](http://github.com/DataONEorg/Education) and editing content directly. For help, try this brief [GitHub tutorial](https://guides.github.com/activities/forking/) on forking and editing content.

### Edit content

1. Create a fork of the [lessons](https://github.com/DataONEorg/Education/tree/master/_lessons) or [best practices](https://github.com/DataONEorg/Education/tree/master/_bestpractices) repository into your github account, depending on which content you wish to edit.
2. Modify the files that you want to change ([See "Structure" below for tips on making changes](#structure)).
3. Submit a pull-request against the `master` branch of this repository.
4. Your changes will be reviewed by the repository admins.

### Page not rendering?

Check that the `title` field of the YAML header (the first line of each
lesson) is in quotes.

## Suggest changes to content <a id="suggest"></a>

1. Open an [*Issue*][issue] on this repository.
2. Provide your suggested changes with as much detail and guidance as possible. Be specific.
3. Your suggestions will be reviewed by the repository admins.
4. Changes will be pushed to the repository by the repository admins regularly/as needed.

[issue]: https://github.com/DataONEorg/Education/issues

## Fork content for your own use <a id="fork"></a>

Fork and edit content through GitHub, rather than editing privately, to enable others to use your edited content and to track how these materials are used.

1. Create a fork of the  [lessons](https://github.com/DataONEorg/hub_lessons/tree/23581c038ba70cf727ea2c31a6332fc57e49bccc/lessons) or [best practices](https://github.com/DataONEorg/hub_bestpractices/tree/b10d396c32d34385d2f5a7cfe5b2fdc1e4130352/bestpractices) repository into your github account
2. Modify the files that you want to change ([See "Structure" below for tips on making changes](#structure))

___

## Structure of the education materials <a id="structure"></a>

All of the content is generated from markdown documents. These guidelines will walk you through the repository organization, the markdown basics, and any additional information.

### Repository organization

The content linked to each tile on the home page is held within a single folder in the `best practices` or `lessons` directory.

## For Best Practices:
Each best practice can be found in the _bestpractices folder. `best practices` are named for the first three words of their title, separated by hyphens. Instructions for creating new best practices can be found in the [How to Write](_bestpractices/bestpractices/how-to-write.md) best practice example.

## For Teaching Modules:
Teaching module are found in the folder called [lessons](_lessons), and each teaching module `lessons` folder is called `XX_keyword`, where `XX` is the order content is displayed via tiles on the home page, and `keyword` is
a brief description of the content. Edits can be made to the descriptive information contained in the `lesson_cover.md` (the page that opens when a tile is selected on the home page).  If education materials include slides, these slides are in a file called `slides.md`. Do not use another filename. For example, the [demonstration lesson][demolessonhtml] markdown file can be [viewed here][demolessonmd]. This demonstration lesson showcases most of the features you can use if publishing slides.

[demolessonhtml]: https://dataoneorg.github.io/Education/lessons/00_markdown/index.html "Rendered demonstration lesson"
[demolessonmd]: https://github.com/DataONEorg/Education/blob/master/lessons/00_markdown/index.md "Raw markdown file for the demonstration lesson"

You are free to add other directories to your lesson. Images go in `images`, and PDF files in `pdf`. For example, a lesson repository could look like:

~~~
01_management/
  index.md
  index.png
  images/
    image1.png
    image3.jpg
  pdf/
    one-pager.pdf
~~~

## Information about the tools used <a id="tools"></a>

The markdown documents are rendered into a website using [*Jekyll*][jekyll]. When sharing presentations, slides
themselves are rendered using [*remarkjs*][remark]. The rendering is done using GitHub
pages, which builds the site from the `master` branch. You can build the site
locally with `jekyll serve -w`, and it will be available at
[`http://localhost:4000`][local] for you to review.

[jekyll]: https://jekyllrb.com/ "Jekyll website"
[remark]: https://remarkjs.com/#1 "RemarkJS website"
[local]: http://localhost:4000

The stylesheets are defined in `resources/styles`, and rendered to
`resources/dataone.css` using `lessc` (just type `make` from the root).


## Working with the liquid tags

A few hints for working with Liquid tags, which are the tags using in the
templates.

Whitespace can be controlled by adding a `-` to the opening and/or closing
liquid tag. e.g.

```
{% assign blah="foo" %}
```

Would result in a newline being output, whereas:

```
{%- assign blah="foo" %}
```

would not.


List the available collections:

```
{%- for collection in site.collections %}
  {{ collection.label }}
{%- endfor %}
```

The lesson collection is a bit odd because we need to treat each folder as an
item, but Jekyll treats each file as an item. Metadata from both the
`slides.md` and `index.md` is used in rendering, but it takes a bit of extra
work to get those metadata attributes when rendering a page.

From the context of the index page, the slides page can be accessed as follows:

```
{%- assign slides_id = page.id | split: "/" | slice: 0,3 | join: "/" | append: "/slides" %}
{%- assign slides = site[ page.collection ] | where: 'id', slides_id | first %}
{{ slides.title }}
```

Similarly, from the slides page, the index can be accessed:

```
{%- assign index_id = page.id | split: "/" | slice: 0,3 | join: "/" | append: "/index" %}
{%- assign index = site[ page.collection ] | where: 'id', index_id | first %}
{{ index.tags }}
```

To get a list of tags used in a collection, include the `collection_tags.html`
file using a liquid tag like:

```
{% include collection_tags.html the_collection="bestpractices" %}
```
where the value of the `the_collection` property is the name of the collection
to evaluate. The list of tags will then be available as the `tags` liquid
variable.


Thank you for your interest in making these data management education modules more useful!
