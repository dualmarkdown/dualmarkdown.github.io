---
layout: page
title: Dual markdown
description: Every great website starts with a great homepage. The homepage tells your viewers what your site is all about and gives your viewers a place to come back to.
sitemap:
    priority: 1.0
    lastmod: 2017-11-02
    changefreq: weekly
---

## F.A.Q.

### Getting the Calibri font on Linux

In order to build some slide templates on a Linux system you may need to have the Calibri font downloaded and installed in the ~/.fonts directory. You can do it with the following commands:
```
mkdir ~/.fonts
wget -qO- http://plasmasturm.org/code/vistafonts-installer/vistafonts-installer | bash
```
If the script fails on Debian you may need to install this library first:
```
sudo apt-get install cabextract
```
