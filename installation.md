---
layout: page
title: Dual markdown
description: When building a website it's helpful to see what the focus of your site is. This page is an example of how to show a website's focus.
sitemap:
    priority: 1.0
    lastmod: 2017-11-02
    changefreq: weekly
---



## Installation requirements

* LaTeX (distribution)[https://www.latex-project.org/get/#tex-distributions] (for PDF output with pandoc)

* [pandoc v1.19.x](https://github.com/jgm/pandoc/releases/tag/1.19.2.1)

* [panflute](https://github.com/sergiocorreia/panflute)

* [pandoc-crossref](https://github.com/lierdakil/pandoc-crossref)

* [Panbuild](https://github.com/jcsaezal/panbuild)

* A text editor to edit Markdown files
	- [Sublime Text 3](https://www.sublimetext.com/3) is possibly the best multi-platform editor for this. A [plugin to use Panbuild from Sublime Text](https://github.com/jcsaezal/SublimeText-Panbuild) is now available.

## Installation

Currently, the easiest way to install the Dual Markdown Framework is by using `pip`. The python package manager tool can be installed either running a python [script](https://pip.pypa.io/en/stable/installing/) or with the following command:

	apt-get install python-pip

	pip install git+https://github.com/dacya/dualmarkdown/dualmarkdown

More specific installation instructions can be found in the (official github repository)[https://github.com/dualmarkdown/dualmarkdown].

## Mac OS X installation notes

As for PDF output (LaTeX based), the Dual Markdown framework has been successfully tested with MacTex 2016 or Later. MacTeX versions earlier than 2013 are unreliable mostly due to outdated version of the `longtable` LaTeX package, which leads to build error when generating some PDF documents with `pandoc`. 	

## Windows installation notes

_Tests have been performed but no specific installation notes are provided since no issues became apparent so far._

## Linux installation notes

In order to build some slide templates on a Linux system you may need to have the Calibri font downloaded and installed in the ~/.fonts directory. You can do it with the following commands:
```
sudo apt-get install cabextract
mkdir ~/.fonts
wget -qO- http://plasmasturm.org/code/vistafonts-installer/vistafonts-installer | bash
```