# UKFSR Guidance

This is part of the UKFSR infrastructure, which comprises a number of elements.
The public elements are listed below:

- **this repo**, and associated [website](https://foodchainstats.github.io/ukfsr-docs/)
. Here we keep the style guide and all other guidance for the team producing the
UKFSR, current and future.
- the [ukfsr](https://github.com/FoodchainStats/ukfsr) package. This R package is intended to contain helper functions to assist in the production of the report, mostly to ensure graphics are consistent.
- the [UKFSR2024](https://github.com/Defra-Data-Science-Centre-of-Excellence/UKFSR2024) repo. Here you will find mostly the code used to produce the graphics in the UKFSR, alongside some supporting code.


## Updating the guide

The site is built with `bookdown`. Most of the content is in standard Rmarkdown
Rmd files which can be edited as necessary. They can include R code which runs
when the site is rendered, although currently there is little, if any, of this
so they are effectively just markdown files.

The text style guide section is a bit different. Because the policy team are
more comfortable with Sharepoint and Word, we let them edit that bit of the
guide in Word and incorporate it into this site by periodically converting the
Word doc into a Markdown md file using pandoc. The instructions for doing that
are basically the same as in the web publishing section of this guide. Firstly,
we convert the docx (make sure you have removed any track changes from it
first):

```
library(rmarkdown)
pandoc_convert(input = 'style-guide.docx',
               to="markdown_mmd",
               output = "01-text-style-guide.md", 
               options = c("--wrap=none",
                           "--reference-links"))
```

Then check the md output. The file 01-text-style-guide.Rmd pulls this md file in
when the site is built. You must remove any level 1 headings, else it will 
mess up the website structure. If there is any fancy formatting it might also
mess up the output, so check before pushing the output to Github.

To update the guidance you need to render the site using the code below. Make
sure to copy the docx thats generated into the /docs folder, if you need to.
Github Actions will do the rest!

```
rmarkdown::render_site(output_format = 'bookdown::gitbook', encoding = 'UTF-8')
# docx download
rmarkdown::render_site(output_format = "bookdown::word_document2")

```