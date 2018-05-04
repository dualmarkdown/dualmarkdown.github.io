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

The extensions made on top of Pandoc's Markdown can be grouped into two categories. Those in the first category were designed for the creation of dual Markdown documents (i.e., documents written in two different languages). Default languages for dual documents are Spanish and English; nevertheless, other languages can be chosen by defining specific Pandoc variables. Extensions in the second category primarily encompass document constructions that are commonly used when creating teaching-related material, but which, unfortunately, are not currently supported by Pandoc's Markdown. Hence, the main goal of these extensions is to add missing key features to the language for the most widely used output formats in the context of academic writing.

For simplicity, we will refer to the extensions in the first category as _Dual Markdown_, and to those in the second category as _Teaching Markdown_. 


## Generic inline and block elements in Markdown

The vast majority of the enhancements made rely on the existence of generic inline and block elements in Markdown. Note that the `<span>` and `<div>` HTML elements can be included in any Markdown document, so they can be used as generic inline and block containers. For more information on these HTML elements, please have a look [here](https://www.w3schools.com/tags/tag_span.asp) and [here](https://www.w3schools.com/tags/tag_div.asp).

In Markdown, these generic inline and block elements may contain three types of attributes:   

* `class`: it is used primarily to specify the kind of inline or block element. Note that multiple classes can be specified by providing a space separated list of values, as in the following example:
  
    ```html
    <div class="myclass cool_class my_paragraph">
      ... Markdown code ...
    </div>
    ```

* `id`: for specifying unique identifiers in the document
* _generic attributes_: in addition to `class` and `id`, we may add any attribute we want. Note that when generating HTML and HTML-based output (e.g. EPUB or reveal.js) it only makes sense to include the so-called [Global HTML attributes](https://www.w3schools.com/tags/ref_standardattributes.asp). Nevertheless, for the implementation of Markdown extensions we may include arbitrary attributes to be processed by Pandoc itself or by Pandoc filters. 


Recently, a more markdownish syntax for generic inline elements was introduced in Pandoc's Markdown. It all comes down to including the markdown inline text in brackets; attributes must be specified next enclosed in braces. 

_Syntax_:

```
[... Markdown text ...]{.class1 .class2 #id attr1=val1 attr2=val2 ...}
```

Note that the `key=val` syntax within braces allows us to specify _generic attributes_. Class names and IDs, by contrast, must be prepended with `'.'` and `'#'` respectively.


_Example_:

```
[My underlined text]{.underline}
```

That is equivalent to:

```html
<span class="underline">My underlined text</span>
```

After a [very long discussion](https://github.com/jgm/pandoc/issues/168), which took over 6 years!!, a markdownish version of generic block elements --referred to as "fenced divs"-- was finally proposed (see [Pandoc's documentation](https://pandoc.org/MANUAL.html#extension-fenced_divs) for details) on October 24, 2017. The [associated changes](https://github.com/jgm/pandoc/commit/fda0c0119f415c6df95b20730650388c0471241d) have been included as part as the Pandoc v2.0 release, which just came out. Because the auxiliary tools used for the project, such as `panflute` or `pandoc-numbering`, have not yet been adapted to work with Pandoc v2.0, the new syntax for divs cannot be used in the context of the project yet.    


# Dual Markdown 

The Dual Markdown extensions enable the user to define Markdown elements (text, images, paragraphs, titles, etc.) associated with any of the two languages configured for the dual Markdown document. Henceforth, we will refer to the first language as _L1_, and to the second one as _L2_. 

Note that the two languages in a dual Markdown document have a _tag_ associated with them. By default _L1_ in Dual Markdown is Spanish, and _L2_ is English. The default tags for these two languages are `SP` and `EN`, respectively. Changing the language configuration entails overriding the `lang1` and `lang2` variables in Pandoc, which store the tags associated with L1 and L2 respectively. The value of these variables can be established either via the `-M` option in Pandoc's command line or by including the variable definition in the YAML header of the main Markdown file of the document. Note that language tags are not predefined;  it is totally up to the user to decide which tag to use for a particular language. 

When invoking `pandoc` to generate an output file from a dual Markdown document, just one of the two languages will be enabled. Unless explicitly noted, L1 --whose tag is defined in the `lang1` variable-- is the one enabled. To enable any specific language, the `lang_enabled` variable must be defined by assigning it the desired language's tag (e.g. `lang_enabled=EN` for English). 

The table below summarizes the language extensions for the creation of dual documents. These extensions are implemented in the  [`dual_md.py`](https://github.com/dacya/pimcd1718-jcsaezal/blob/master/common/dual_md.py) pandoc filter.  


|                       Extension                        | Supported output formats |               Example                |
| :----------------------------------------------------- | :----------------------: | :----------------------------------- |
| [Language-specific blocks](#lang-blocks)               |           All            | All                                  |
| [Dual spans](#dual-spans)                              |           All            | All                                  |
| [Dual titles](#dual-titles)                            |           All            | Slides and lab_assignment1.md        |
| [Dual inline table cells](#dual-tables)                |           All            | exercises_file_systems.md            |
| [Dual images](#dual-images)                            |           All            | Slides and exercises_file_systems.md |
| [Inclusion of Tikz diagrams as figures](#include-tikz) |       Latex-based        | Slides and exercises_file_systems.md |
| [Dual Tikz diagrams](#dual-tikz)                       |       Latex-based        | Slides and exercises_file_systems.md |
| [Dual Pandoc variables](#dual-vars)                    |           All            | Slides (files.md)                    |
| [Dual pandoc-crossref](#dual-crossref)                 |           All            | lab_assignment1.md                   |



## Language-specific blocks {#lang-blocks .unnumbered}     

This extension allows the user to specify Markdown blocks associated with L1 or L2. When the final document is generated, the block in question will be only displayed if the corresponding language is selected.

_Syntax for Language-specific block_:

```
BEGIN-<LANGUAGE_TAG>

... Markdown text block ...

END-<LANGUAGE_TAG>
```

_Example_:

```
BEGIN-SP

Días de la semana:

* lunes
* martes
* miércoles
...

END-SP

BEGIN-EN

Days of the week:

* Monday
* Tuesday
* Wednesday
...

END-EN
```

## Dual spans {#dual-spans .unnumbered}     

Dual spans make it possible to provide the "dual version" of an inline Markdown text: one for L1 and another for L2. As it happens for Language-specific blocks, the final document will only display the version of the inline text that corresponds to the language enabled when invoking `pandoc`.

_Syntax_:

```
[<Markdown Text for L1> ||| <Markdown Text for L2>]{.dual}
```

_Alternative Syntax_:

```
[<Markdown Text for L1> ;;; <Markdown Text for L2>]{.dual}
```


_Example_:

```
[Módulo 2: Sistemas de Ficheros ||| Unit 2: File Systems]{.dual}
```

## Dual titles {#dual-titles .unnumbered}     

Dual spans can be used in header titles as in the following example, which uses a level 3 header:

```
### [Título de sección ||| Section title]{.dual}
```

Dual titles constitutes a less verbose, simplified version of the dual span syntax just for header titles. With the dual title syntax, the previous example can be rewritten as follows:

```
### Título de sección ||| Section title
```

The `";;;"` string can be also used as a separator instead of `"|||"`:

```
### Título de sección ;;; Section title
```
              
## Dual inline table cells {#dual-tables .unnumbered}     

Dual inline table cells constitutes a less verbose version of the dual span syntax just for table cells that are made up of an inline Markdown element. Note that inline table cells are typically present in table header cells, as in the following example:

_Example:_ 


```
| **Nombre** ;;; **Name** | **Tipo** ;;; **Type** | **Fecha** ;;; **Date** |
| :---------------------: | :-------------------: | :--------------------: |
|          DATA1          |           F           |         8-2-05         |
|          DATA2          |           F           |         8-3-06         |
|                         |                       |                        |
```


In the example, a dual version of the table header is provided by employing dual inline table cells. Note that only the `";;;"` separator is allowed here to avoid syntactic ambiguity in the context of Pandoc's Markdown pipe tables.    
       
## Dual images {#dual-images .unnumbered}     

This extension constitutes a simple way of including the language-specific version of an image (e.g. English or Spanish version) in the final document with a single line of Markdown code. To use this feature, two versions of the figure (for L1 and L2) should be provided. Moreover, the figure file names must include the language tag, which will be omitted when using a dual image inclusion statement.

To illustrate this feature, let us consider the following example of a dual image statement:
```Markdown
![](images/figure.pdf){.dual}\
```   

As is evident, it is just like a regular image inclusion statement (without a caption) but with the `dual` class. In processing this statement, the Dual Markdown parser will include figure with name `images/figure-<LANG_TAG>.pdf`, where `<LANG_TAG>` denotes the tag of the language enabled when invoking `pandoc`. For example, if the Spanish language --with tag `SP`-- is enabled, the Markdown text above will be replaced with the following text:

```Markdown
![](images/figure-SP.pdf)\
```   

            
## Inclusion of Tikz diagrams as figures {#include-tikz .unnumbered}     

Pandoc's Markdown does not support the inclusion of figures created with the Tikz LaTeX package. Thanks to this new feature, figures with the `".tex"` extension will be treated as a Tikz figure and included appropriately in the final document, which must be PDF, LaTeX or Beamer. If the `standalone` class is specified in the image inclusion statement, the Dual Markdown parser will include the figure in the final document by using the `\includestandalone{...}` macro. Otherwise, the image will be included with a regular Latex `\input{...}` statement. 

It is also worth noting that this Markdown extension can be used along with the Dual image feature presented above.


## Dual Tikz diagrams {#dual-tikz .unnumbered}     

One interesting feature of the Dual Markdown framework is the ability to create _Dual Tikz diagrams_. Such a diagram is a Tikz figure that provides the translation (in L1 and L2) for each text snippet that appears in the figure. In other words, Dual Tikz diagrams constitute a way of defining two versions of the same diagram (for L1 and for L2) in a single file. These kind of diagrams must be created by using the `\dtext` built-in macro, which is automatically defined when processing a Dual Markdown file. This macro accepts two mandatory arguments: the first one is the version of the text in L1, the second one corresponds to the translation of the text in L2. 

Let us consider the following statement, included in a hypothetical Dual Tikz diagram:
```latex
\dtext{Texto en español}{Text in English}
```

When generating the final document for L1, it will display `"Texto en español"` on the corresponding diagram. Similarly, the  `"Text in English"` string will be displayed on the diagram when enabling L2 in building the document. 



## Dual Pandoc variables {#dual-vars .unnumbered}

Pandoc's Markdown enables the user to define some parts of the document, such as the title, subtitle or date, by means of variables passed as arguments on the command-line (-M option) or via YAML code snippets in Markdown files. Because the title and the subtitle of a document will likely be different in L1 and L2, it makes sense to define the corresponding variables differently based on the language enabled in the target document. To make this possible, Dual Mardown introduces a simple syntax enabling to define the two variants of the title and subtitle (for L1 and L2, respectively), by using the `"|||"` or `";;;"` separators, as in Dual titles.


For example, the following YAML sample snippet could be used in the YAML header of a dual markdown document:
```yaml
---
title: "Este es el título en español ||| This is the title in English"
subtitle: "Mi subtítulo ||| My subtitle"
...
```

## Dual pandoc-crossref {#dual-crossref .unnumbered}     

The [`pandoc-crossref` filter](https://github.com/lierdakil/pandoc-crossref) augments Pandoc's Markdown with statements for referencing images, equations and tables. This filter also enables the user to control how references and captions for the various elements are rendered in the final document. Customizing this aspect comes down to defining various pandoc variables (check out [this link](https://github.com/lierdakil/pandoc-crossref#customization) for details). For example, the `figureTitle` and `figPrefix` variables of `pandoc-crossref` allow us to define the label associated with image captions and image references, respectively. The default values for these variables are "Figure" and "fig." respectively.

Dual markdown relies on `pandoc-crossref` to support references to images or tables, and, more importantly, it extends the functionality of this pandoc filter with support for dual documents. Specifically, the Dual Markdown framework allows the user to provide the L1 and L2 version for the various customizable labels exposed by `pandoc-crossref`. To make this happen, the different label-related `pandoc-crossref` variables can now be assigned a value in exactly the same way as the dual pandoc variables discussed earlier.

_Example_:
```yaml
---
figureTitle: "Figura ||| Figure"
tableTitle: "Tabla ||| Table"
...
```

The Dual Markdown parser takes care of selecting the "right" value for the different variables, and passes them on to the `pandoc-crossref` filter. An important implication of this workflow is the fact that the `dual_md.py` filter should be specified before than the `pandoc-crossref` filter in Pandoc's command line. 

# Teaching extensions

The table below summarizes the Teaching Markdown extensions, which are implemented in the [`teaching_md.py`](https://github.com/dacya/pimcd1718-jcsaezal/blob/master/common/teaching_md.py) pandoc filter.   


|                            Extension                            | Supported output formats |                Example                |
| :-------------------------------------------------------------- | :----------------------: | :-----------------------------------: |
| [Multiformat images](#multiformat)                              |           All            |       exercises_file_systems.md       |
| [Latex blocks including Markdown](#latex-blocks)                |       Latex-based        |    DualSlides/FileSystems/files.md    |
| [Traditional Latex tables (no syntax extension)](#latex-tables) |       Latex-based        | Any document with tables (PDF output) |
| [Shaded and Framed blocks](#shaded-framed)                      |   HTML and Latex-based   |           lab_assignment1.md          |
| [Exercise delimiter and auto-numbering](#exercises)             |           All            |       exercises_file_systems.md       |
| [Multiple columns](#columns)                                    |  HTML, Latex and Docx*   |  Slides and exercises_file_systems.md |
| [Pagebreaks](#pagebreaks)                                       |   HTML, Latex and Docx   |           `## {.pagebreak}`           |
| [Custom spans (underline, alert, color)](#custom-spans)         |  HTML, Latex and Docx*   |                 Slides                |
| [Custom (Latex-style) fontsizes in Divs and Spans](#fontsize)   |   HTML and Latex-based   |     Slides and lab_assignment1.md     |
| [Block and figure alignment syntax](#alignment)                 |   HTML and Latex-based   |  Slides and exercises_file_systems.md |
| [Advanced beamer blocks](#beamer-blocks)                        |          Beamer          |                 Slides                |
| [Beamer transitions](#beamer-transitions)                       |          Beamer          |  None (Use spans with attribute only) |


<!--

|                            Extension                            | Supported output formats |                Example                |
| :-------------------------------------------------------------: | :----------------------: | :-----------------------------------: |
|              [Multiformat images (alt-ext attribute)             |           All            |       exercises_file_systems.md       |
|        [Latex blocks including Markdown (\\lbegin \\lend)        |       Latex-based        |    DualSlides/FileSystems/files.md    |
|          [Traditional Latex tables (no syntax extension)         |       Latex-based        | Any document with tables (PDF output) |
|                     Shaded and Framed blocks                    |   HTML and Latex-based   |           lab_assignment1.md          |
|    [Exercise delimiter and auto-numbering  (`### {.exercise}`)   |           All            |       exercises_file_systems.md       |
|                         [Multiple columns                        |  HTML, Latex and Docx*   |  Slides and exercises_file_systems.md |
|                            [Pagebreaks                           |   HTML, Latex and Docx   |           `## {.pagebreak}`           |
|              [Custom spans (underline, alert, color)             |  HTML, Latex and Docx*   |                 Slides                |
|              [Filter out notes (no syntax extension)             |           All            |       None (cleaning up feature)      |
|         [Custom (Latex-style) fontsizes in Divs and Spans        |   HTML and Latex-based   |     Slides and lab_assignment1.md     |
|           [Block alignment syntax (center, left, right)          |   HTML and Latex-based   |  Slides and exercises_file_systems.md |
| [Advanced beamer blocks (console, exampleblock, alertblock, ...) |          Beamer          |                 Slides                |
|                        [Beamer transitions                       |          Beamer          |  None (Use spans with attribute only) |

-->


## Multiformat images {#multiformat .unnumbered}     

Pandoc allows the creation of multiple output documents from a single Markdown source file. If such a source file includes images, we must guarantee that the image format is suitable for the output format. For example, if we want to generate HTML from Markdown, only SVG, jpeg or png figures are allowed. By contrast, PDF figures are more suitable when generating Docx o PDF (Latex-based) output. Unfortunately, Pandoc's Markdown lacks support for specifying multiple figure formats in the sources. This is in order to generate several types of output documents from the same Markdown document. 

Multiformat images allows the user to indicate which image format to use (such as *png* or *pdf*) for each figure, depending on the kind of output document being generated. 

_Syntax_:

```
(path to image){alt-ext=fig-format1/.doc-formatN,...,fig-formatN/.doc-formatN}
```

To illustrate how this extension works, let us consider the following example. Suppose that we have a Tikz figure (file *structure.tex*) --located in the *img* directory--, which we will use for generating the document in any format except for *html* and *docx*. In these two special cases, we will use figures *structure.png* and *structure.pdf* respectively, both located in the *img* directory as well.

```
![](img/structure.tex){alt-ext=html/.png,docx/.pdf align=center}\
```           

## Latex blocks including Markdown {#latex-blocks .unnumbered}     

Pandoc's Markdown allows the user to include LaTeX blocks enclosed in between `\begin{..}` and `\end{...}`. When generating a non-LaTeX based output, such as docx or HTML, these blocks are just removed from the document so that they do not appear in the output file. By contrast, for  LaTeX based output (e.g. PDF, Beamer, etc.) Pandoc dumps these LaTeX blocks directly onto the output document without further processing, so that they are handled by the LaTeX engine. That leads to an important limitation: it is not possible to add Markdown code inside `\begin{..}-\end{...}` blocks, as it will be treated as LaTeX code. [Several solutions](https://github.com/jgm/pandoc/issues/2453) have been proposed to address this issue via special LaTeX macros, but they all pose different shortcomings.

To fill this gap, Teaching Markdown allows to enclose Markdown code inside LaTeX blocks by using `\lbegin{..}` and `\lend{...}`, instead of `\begin{..}` and `\end{...}`. When the Teaching Markdown parser detects lines with `\lbegin{..}` and `\lend{...}` it transforms this into the corresponding `\begin{..}` and `\end{...}` LaTeX statements automatically. In doing so, the Markdown code inside  `\lbegin{..}` and `\lend{...}` is now effectively processed by Pandoc and transformed into the corresponding output format. 

As an interesting application of this Markdown extension, the following text snippet makes it possible to enlarge the page margins to use in an individual Beamer slide:
```Markdown
## Slide title

\lbegin{adjustwidth}{-2em}{-2em}

... MARKDOWN CODE GOES HERE...

\lend{adjustwidth}

```


## Traditional Latex tables (no syntax extension) {#latex-tables .unnumbered}     

This extension (enabled by default) just affects the way that tables are rendered in Latex-based or HTML based formats. It just takes care of displaying all tables as in a grid-like style: rows and columns are separated by horizontal and vertical rules. This stands in contrast with the default table-rendering style used by pandoc, which is [not always the most suitable choice](https://github.com/jgm/pandoc/issues/922). 



        
## Shaded and Framed blocks {#shaded-framed  .unnumbered}     

This extension enables the user to define a shaded or a framed block of text in Markdown, by using the a generic block element with the *shaded* or *framed* class respectively.

_Syntax_:

```html
<div class="shaded">
... Markdown text block goes here ...
</div>
```

_Example_:

```html
<div class="shaded">

What is the capital city of Spain?

a. Barcelona
b. Madrid
c. La Coruña
d. Sevilla

</div>
```

                 
## Exercise delimiter and auto-numbering {#exercises .unnumbered}     

<!-- **COMENTARIOS**: Se me ocurre que sería interesante poder incluir un texto antes del número de ejercicio o cuestión.-->

This extension enables the user to delimit and enumerate a set of exercises (*exercise* marker), questions (*question* marker) or a custom item in the document (via spans).

When we include a new *exercise* marker, the text of the previous exercise ends, and the text of the next exercise begins, preceded by the next integer number in sequential order. Similarly, the *question* marker delimits two questions and includes the next sequential integer. Resetting the numbering at some point is also possible by including ".reset" (class) in the exercise or question marker.  Note that exercises and questions are enumerated independently. 

_Syntax_ (exercise marker):

```
### {.exercise}
```
  
  


_Syntax_ (question marker):

```
### {.question}
```

   
----

_Example_:

```
# Exercises { .unnumbered }

### {.exercise}

Explain briefly *The French Revolution*.

# Questions { .unnumbered }

### {.question}

Who wrote *El Quijote*?

### {.question}

Which is the common root for Spanish, French and Italian languages?
```

----


To number other kind of things with a custom label in the document, the following kind of span can be used in the document.

```
[<Label> #]{}
```

where `<Label>` can be any string. The first time that a particular label is used in the document with that statement, a counter will be created and initialized to 1 in the filter code. Subsequent occurrences of the same span element (same label) will result in an increment of the counter. The span will be rendered in the final document as follows: `<Label> <CurrentCounterValue>`.  Notably, ".reset" can be used inside the span braces to reset the custom counter when needed. 

We should highlight that using the "`#`" symbol to create and increment custom counters was inspired by the syntax of the [pandoc-numbering filter](https://github.com/chdemko/pandoc-numbering), which provides a wider range of numbering formats.  

             
## Multiple columns {#columns  .unnumbered}     

<!--
TODO (See `exercises_file_systems.md:168`)
**COMENTARIOS**: Si no pongo el atributo width, no me pone el texto en columnas; sin embargo, según veo en el código de teaching_md.py, por defecto se inicializa width a un valor.
-->

This extension makes it possible to divide a specific region of the document into several columns. For that purpose, a generic block element must be used with the *columns* and *column* classes, as explained below.

The whole multi-column region must be enclosed in a `<div>` block with the *columns* class. Then, inside the multi-column region, the text belonging to each column must be included in a `<div>` block with the *column* class, used along with the *width* attribute, which indicates the column width. Note that columns may be assigned a different width.

Other attributes could be used as well. For example, the *colsep* attribute used with the *columns* class allows the user to specify a separation between the columns (by default, if the *colsep* attribute is not used, the separation is set to 0).

_Syntax_ (multiple columns):

```html
<div class="columns" colsep="Xcm">

<div class="column" width="Y%">
... Text of the first column goes here ...
</div>

<div class="column" width="Z%">
... Text of the second column goes here ...
</div>

...

<div class="column" width="K%">
... Text of the nth column goes here ...
</div>

</div>
```


_Example_:

```html
<div class="columns" colsep="0.3cm">

**Main sport per country:**

<div class="column" width="25%">
The main sport practised in Spain is soccer
</div>

<div class="column" width="30%">
The main sport practised in the USA is baseball
</div>

<div class="column" width="25%">
The main sport practised in India is cricket
</div>

</div>
```

**Important Note:** A very similar support has been recently introduced in Pandoc. Have a look at [this commit](https://github.com/jgm/pandoc/commit/892a4edeb1c9b9810c8386e639d8e457bbae7e86) for the details on the syntax, which is very similar to that in Teaching Markdown. There are two major differences between Pandoc's support and Teaching Markdown's:

- Teaching Markdown supports a `colsep` attribute, to indicate the separation between columns
- Teaching Markdown supports columns in regular LaTeX too via `minipage`
                  

## Pagebreaks {#pagebreaks  .unnumbered}     

Teaching Markdown allows the user to add pagebreaks in a document by using the following text snippet:

```
### {.pagebreak}
```


## Custom spans (underline, alert, color) {#custom-spans .unnumbered}    

<!--

TODO (subrayado, alert - texto en rojo-, color -texto en cualquier color-)
**COMENTARIOS**: No encuentro cómo hacer funcionar la opción color=<color_specification>.
-->

These extensions allows to highlight a given inline text in different ways. If the *underline* class is specified after the inline text, the whole text (included in brackets) will be underlined. Similarly, if we use *alert* class, the text will be displayed in red (in much the same way as with the Beamer `\alert` command). Finally, if we append `color=<color_specification>`, the text will be displayed in the specified color.


_Syntax_:

```
[... Highlighted markdown text goes here ...]{.underline}
[... Highlighted markdown text goes here ...]{.alert}
[... Highlighted markdown text goes here ...]{color=<color_specification>}
```


_Example_:

```
The computer can be divided into three main parts, according to [Von Neumann]{.alert} architecture:
[CPU]{.underline}, [Memory]{.underline} and [I/O]{.underline}.
```


              
## Custom (Latex-style) fontsizes in Divs and Spans {#fontsize .unnumbered}     

<!--TODO

See examples:
- `exercises_file_systems.md:17` (Span with fontsize)
- `exercises_file_systems.md:187` (Div with fontsize)
-->

This extension enables the user to establish the size of the text within a given region. For that purpose, generic block and inline elements must be used with the *fontsize* attribute.  Latex-style fontsize specifiers must be used (from smaller sizes to larger ones): `tiny`, `scriptsize`, `footnotesize`, `small`, `normalsize`, `large`, `Large`, `LARGE`, `huge` and `Huge`. 


_Syntax_ (spam element):

```html
[... Markdown text goes here ...]{fontsize=size}
```

_Syntax_ (div element):

```html
<div fontsize=[size_specifier]>
... Markdown text goes here ...
</div>
```

_Example_:

```html
[Section 1: Introduction to the C language]{fontsize=huge}
<div fontsize="normalsize">
In this Section we will introduce the main concepts of the C programming language.
</div>
```

         
## Block and figure alignment syntax {#alignment .unnumbered}     

This extension allows the user to specify the alignment of a text snippet enclosed in a div block, by using the *align* attribute. The text snippet can be left aligned, centered or right aligned. 


_Syntax_:

```html
<div align=aligment_type_spec>
... Markdown text block goes here ...
</div>
```


_Example_:

```html
<div align="left">
Dear sir,
</div>

<div align="center">
The purpose of this letter is to inform you that ...
</div>

<div align="right">
Madrid, 2017.
</div>
```


Note also that Teaching Markdown allows the *align* attribute to be used in figures as well.

## Advanced beamer blocks {#beamer-blocks .unnumbered}     

The `beamer` package allows the creation of slides in LaTeX. A very useful feature of this package is the fact that it allows the user to include blocks in each slide. Beamer blocks are just little slides that may be included within another beamer slide (aka frame).

Pandoc makes it possible to transform Markdown code into beamer, by using `-t beamer` in the command line. By default, level-3 headers (i.e. "`### Title`") are rendered as _regular_ beamer blocks with a title. Unfortunately, there is no way to tell Pandoc to render the text as another kind of beamer blocks commonly used in beamer, such as `alertblocks` or `exampleblocks`. 

To address this shortcoming, Teaching Markdown allows to specify the target block type by using a generic block container as follows:

```html
<div class="[block_type]" title="[title]">
... Markdown text block goes here ...
</div>
```

where `[title]` encodes the title of the beamer block (two languages can be used by using the [syntax for Dual Pandoc variables](#dual-vars)), and  `[block_type]` can be one of the following values:

* `alertblock`, for the inclusion of warnings in the slides.
* `exampleblock`, for the inclusion of examples in the slides.
* `block`, to add regular beamer blocks.
* `whiteblock`, to add regular beamer blocks with a white background.
* `console`, to add beamer blocks that emulate a terminal window (for the inclusion of examples with commands).

                   
## Beamer transitions {#beamer-transitions .unnumbered}     

The beamer LaTeX package allows the inclusion of simple animations in slides. For example, the `\pause` command allows us to reveal parts of the frame one after another. In a similar vein, the `\only<n>{text}` makes it possible to indicate at what step (`n`) of the rendering process of a slide a given text snippet will become visible. 

While  the `\pause` command can be used as is in our Markdown slides (to be transformed into beamer), pandoc does not support the inclusion of the `\only<n>{text}` command. To overcome this issue, Teaching Markdown allows the creation of markdown elements to be included in an "`only`" block or inline container. Essentially, the supported syntax is as follows:

```html
<div only="[step-spec]">
... Markdown text block goes here ...
</div>

[...Markdown text goes here ...]{only=[step-spec]}
```

_Example_

```html
[This will be displayed all the time in the current slide]{only="1-"}
[This will show up in the second step]{only="2"}
[This will show up in the third step]{only="3"}
```




