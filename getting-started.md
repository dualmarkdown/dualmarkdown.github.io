---
layout: page
title: Dual markdown
description: When building a website it's helpful to see what the focus of your site is. This page is an example of how to show a website's focus.
sitemap:
    priority: 1.0
    lastmod: 2017-11-02
    changefreq: weekly
---

## Getting started

This open source project facilitates the creation of teaching content in multiple languages by editing a single markdown file. Devoloping this project entailed creating different extensions for existing frameworks and programs, that were released in github as independent tools.

The main components of this project are the following:

* [Dual Markdown](https://github.com/dualmarkdown/dualmarkdown): This repository contains the main extensions and filters created for Pandoc Markdown.
* [Panbuild](https://github.com/jcsaezal/panbuild): Panbuild is a make-like builder for pandoc. It is a command-line tool that aims to simplify the construction of multiple output documents (in different formats, such as PDF, DOCX, EPUB, etc.) from a given source document (e.g. one or several Markdown files).
* [Panbuild-Sublime](https://github.com/jcsaezal/SublimeText-Panbuild): This plugin makes it possible to use panbuild --a make-like builder for pandoc-- within the Sublime Text editor. Essentially, the plugin removes the need to type panbuild or pandoc commands from a terminal window; all the interaction with panbuild and pandoc takes place from the graphical user interface of Sublime Text.