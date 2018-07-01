---
layout: page
title: Dual markdown
description: When building a website it's helpful to see what the focus of your site is. This page is an example of how to show a website's focus.
sitemap:
    priority: 1.0
    lastmod: 2017-11-02
    changefreq: weekly
---

# Getting Started

After installing the Dual Markdown Framework (check out the [Installation instructions](./installation)) you may now begin to create Dual Markdown documents and transform them into a variety of output documents (PDF, docx, HTML, EPUB, etc.).

Two tutorials can be found below. The first one describes how to use and build the Dual Markdown sample documents [available on Github](https://github.com/dualmarkdown/examples). The second tutorial explains how to create a Dual markdown document from scratch, and what to do to transform it into any of the available output formats. 

## How to use and build the examples

To illustrate the basics and the potential of the Dual Markdown Framework we created a set of sample documents, which can be downloaded as [a single ZIP file](https://github.com/dualmarkdown/examples/archive/master.zip). After extracting the archive on your computer, various folders will be created; each folder contains the source code and related material for a particular example. Specifically, each folder includes at least three things:

* `README.md`: Markdown file with a brief description of the example. This information will not be used to generate the final documents.
* `build.yaml`: file with the build rules that will be used by [Panbuild](https://github.com/jcsaezal/panbuild), a key component of our framework. Panbuild makes it easier to automatically generate the various output documents with pandoc from dual markdown files. It can be used from the [Sublime Text](https://www.sublimetext.com/) editor— thanks to the [Panbuild plugin](https://github.com/jcsaezal/SublimeText-Panbuild)— as well as via the command line.
* Markdown files with the source code of the example

To illustrate how to build any of the examples, we will use the one found in the _hello_ folder.

### Working with Sublime Text

Open the *hello* directory in *Sublime Text* by dragging it onto the *Sublime* window, and then open the *hello.md* file. Now, enable the "Panbuild" build system by clicking on the following menu entry: *Tools*– *Build System*– *Panbuild*.

![](../images/gs/scr-000-f.png)

To tell *pandoc* to transform your document into one of the output formats defined in the *build.yaml* file, just type CTRL+B (On Windows or Linux) or CMD+B (on Mac OS X). In doing so, a list with the available output formats -in this case, PDF, DOCX, TXT and HTML- and available languages -spanish [SP] and English [EN] in the example will be displayed, as in the figure below:

![](../images/gs/scr-001-f.png)

​		
Clicking on the desired format's list entry will initiate the build process with pandoc. When done, the output document will be automatically opened with the default application for viewing that kind of file (e.g., Adobe Reader for PDF files):

![](../images/gs/scr-003-f.png)

Note that the generated output file -a different one for each available format and language- will be placed in the same folder where the `build.yaml` was located:

![](../images/gs/scr-002-f.png)	

## Using the console to build the examples

You can also transform your document into the different output formats from the command line. For that purpose, open a shell window in your operating system and switch to the `hello` directory. Once there, you can use the panbuild program with different options:

1.  By simply typing `panbuild` in the command line without any options, all the possible output documents will be generated: *hello.docx*, *hello.html*, *hello.pdf*, *hello.txt*, *hola.docx*, *hola.html*, *hola.pdf* and *hola.txt*.

2. By typing panbuild followed by a specific output `format/language`, you will only obtain the document in that format and language. For example, typing the following command will create the *hello.docx* file (English version of the document in the Microsoft Word's DOCX format):

      `panbuild DOCX/EN`			


​			
## How to create and build a Dual Markdown document from scratch with Sublime Text

<div class="resp-container">
	<iframe class="resp-iframe" align="center" src="https://drive.google.com/file/d/1dgSBe3DsIWQTmpCFrC8YgJoTCMettfTK/preview" gesture="media"  allow="encrypted-media" allowfullscreen></iframe>​
</div>

