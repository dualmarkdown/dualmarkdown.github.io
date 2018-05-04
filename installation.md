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

* [pandoc v1.19.x](https://github.com/jgm/pandoc/releases/tag/1.19.2.1)

* Python v2.7

* pip for Python v2.7
	- On Mac OS X, it typically comes installed with your Python distribution.
	- On Windows, make sure you choose to install `pip` during the installation of Python (latest Python installers provide such an option).
	- On a Debian-based system (including Ubuntu), you can install `pip` (as root) as follows:

			apt-get install python-pip

* LaTeX distribution (for PDF output with pandoc)

* [panflute](https://github.com/sergiocorreia/panflute) Python library
	- Note that it gets installed automatically with `pip` when installing the Dual Markdown Framework

* [pandoc-crossref](https://github.com/lierdakil/pandoc-crossref) (use the OS-specific tarball found [here](https://github.com/lierdakil/pandoc-crossref/releases/tag/v0.2.6.0))
	- Simply copy the executable file in the same folder where the pandoc executable file was installed 

* [Panbuild](https://github.com/jcsaezal/panbuild), a make-like builder for Pandoc
 	- Installation: `pip install git+https://github.com/jcsaezal/panbuild`

* A text editor to edit Markdown files
	- [Sublime Text 3](https://www.sublimetext.com/3) is possibly the best multi-platform editor for this. A [plugin to use Panbuild from Sublime Text](https://github.com/jcsaezal/SublimeText-Panbuild) is now available.

## Installation

Currently, the easiest way to install the Dual Markdown Framework is by using `pip` as follows:

	pip install git+https://github.com/dacya/pimcd1718-jcsaezal

Because the repository is currently a private one, you should have your git environment properly configured on your machine in order for pip to be able to download it. This requirement will be removed eventually as the repository will be publicly available soon.

In the meantime, if the one-command installation shown above does not work (e.g., git is not installed on your system) you can follow this two-step  process:

1. Download a copy of the repository in [ZIP format](https://github.com/dacya/pimcd1718-jcsaezal/archive/master.zip) and extract it on your computer.

2. Install the Dual Markdown Framework on your system by running `pip` as follows:

		pip install <path_to_your_local_copy_of_repository>

## Mac OS X installation notes

As for PDF output (LaTeX based), the Dual Markdown framework has been successfully tested with MacTex 2016 or Later. MacTeX versions earlier than 2013 are unreliable mostly due to outdated version of the `longtable` LaTeX package, which leads to build error when generating some PDF documents with `pandoc`. 	

## Windows installation notes

_Tests have been performed but no specific installation notes are provided since no issues became apparent so far._

## Linux installation notes

_Tests have been performed but no specific installation notes are provided since no issues became apparent so far._
