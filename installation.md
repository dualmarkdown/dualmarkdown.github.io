---
layout: page
title: Dual markdown
description: When building a website it's helpful to see what the focus of your site is. This page is an example of how to show a website's focus.
sitemap:
    priority: 1.0
    lastmod: 2017-11-02
    changefreq: weekly
---

## Installation

### Using official installers

We are currently developing installers for Windows and Mac OS X. These installers will make it possible to automatically deploy on your system the various components of the Dual Markdown as well as the following dependencies:

* [pandoc v1.19.x](https://github.com/jgm/pandoc/releases/tag/1.19.2.1)
* [pandoc-crossref](https://github.com/lierdakil/pandoc-crossref)
* [Sublime Text 3](https://www.sublimetext.com/3)
* [A LaTeX distribution](https://www.latex-project.org/get/#tex-distributions) (for PDF output with pandoc)

The installers will be available shortly. In the meantime, users will have to resort to the [manual installation procedure](#manual-installation).

### Manual installation

The Dual Markdown framework relies on free multi-platform tools available for Windows, Mac OS X or Linux. To install the framework on your system just install the dependencies listed above, as well as the following three components that make up the framework, which are available on GitHub:   

1. **[Dual Markdown filters](https://github.com/dualmarkdown/dualmarkdown)**: A set of [pandoc filters](https://pandoc.org/filters.html) that extend Pandoc's Markdown with syntax for Dual Markdown files (i.e. documents in two languages) and with other constructions specifically designed to facilitate the creation of teaching materials. More information on these Markdown extensions can be found [here](/documentation).
2. **[Panbuild](https://github.com/jcsaezal/panbuild)**: Panbuild is a make-like builder for [pandoc](www.pandoc.org). It is a command-line tool that aims to simplify the construction of multiple output documents (in different formats, such as PDF, DOCX, EPUB, etc.) from a given source document (e.g. one or several Markdown files).
3. **[Panbuild plugin for Sublime Text](https://github.com/jcsaezal/SublimeText-Panbuild)**: This plugin makes it possible to use Panbuild seamlessly within the Sublime Text editor. <!--Essentially, the plugin removes the need to type panbuild or pandoc commands from a terminal window; all the interaction with panbuild and pandoc takes place from the graphical user interface of Sublime Text.-->

Note that the installation instructions for each component can be found on the associated GitHub repository page:
- [Installation of Dual Markdown filters](https://github.com/dualmarkdown/dualmarkdown/blob/master/README.md)
- [Installation of Panbuild](https://github.com/jcsaezal/panbuild/blob/master/README.md)
- [Installation Panbuild plugin](https://github.com/jcsaezal/SublimeText-Panbuild/blob/master/README.md)
