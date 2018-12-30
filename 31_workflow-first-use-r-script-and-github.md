# Render an R script {#r-test-drive}

An underappreciated fact is that much of what you can do with R Markdown, you can also do with an R script.

If you're in analysis mode and want a report as a side effect, write an R script. If you're writing a report with a lot of R code in it, write Rmd. In either case, render to markdown and/or HTML to communicate with other human beings.

  * In R markdown, prose is top-level and code is tucked into chunks.
  * In R scripts, code is top-level and prose is tucked into comments. You will use `#'` to request that certain comments appear as top-level prose in the rendered output.

You will continue to specify things like the output format via YAML at the top of the file. This will need to be commented with `#'`.

## Morph R Markdown into a renderable R script

Get yourself a working R Markdown file, such as the one you made in your [Rmd test drive](#rmd-test-drive). Or use the boilerplate Rmd document RStudio makes with *File > New File > R Markdown ...*.

Save the file as `foo.R`, as opposed to `foo.Rmd`. Yes, for a brief moment, you will have R Markdown saved as an R script, but that won't be true for long.

Transform the Rmd to R:

  * Anything that's not R code? Like the YAML and the English prose? Protect it with roxygen-style comments: start each line with `#'`.
  * Anything that's R code? Let it exist "as is" as top-level code. That means you'll need to change the syntax of R chunk headers like so:
  
    Before: ` ```{r setup, include = FALSE}`  
    After: `#+ r setup, include = FALSE`

    Replace the leading backticks and opening curly brace with `#+`.  
    Delete the trailing curly brace.  
    Delete the 3 backticks that end each chunk.

Render the R script through one of these methods:

  * Click on the "notebook" icon in RStudio to "Compile Report".
  * In RStudio, do *File > Knit Document*.
  * In R, do `rmarkdown::render("foo.R")`.

You'll get a markdown and/or HTML report, just as with R Markdown.

If you're having trouble making all the necessary changes and you're frustrated, see below for an example you can copy and paste.

All the workflow tips from the [Rmd test drive](#rmd-test-drive) apply here: when you script an analysis, render it to markdown, commit the `.R`, the `.md`, any associated figures, and push to GitHub. Collaborators can see your code but also browse the result without running it. This makes the current state of your analysis accessible to someone who does not even run R or who wants to take a quick look at things from a cell phone or while on vacation.

## Write a render-ready R script

Instead of morphing an R Markdown file, let's create a render-ready R script directly.

Create a new R script and copy/paste this code into it.







```r
#' Here's some prose in a very special comment. Let's summarize the built-in
#' dataset `VADeaths`.
## here is a regular code comment, that will remain as such
summary(VADeaths)

#' Here's some more prose. I can use usual markdown syntax to make things
#' **bold** or *italics*. Let's use an example from the `dotchart()` help to
#' make a Cleveland dot plot from the `VADeaths` data. I even bother to name
#' this chunk, so the resulting PNG has a decent name.
#+ dotchart
dotchart(VADeaths, main = "Death Rates in Virginia - 1940")
```

Render the R script through one of these methods:

  *  Click on the "notebook" icon in RStudio to "Compile Report".
  * In RStudio, do *File > Knit Document*.
  * In R, do `rmarkdown::render("YOURSCRIPT.R")`.

Revel in your attractive looking report with almost zero effort! Seriously, all you had to do was think about when to use special comments `#'` in order to promote that to nicely rendered text.

Drawing on the workflow tips in [Rmd test drive](#rmd-test-drive), let's add some YAML frontmatter, properly commented with `#'`, and request the `github_document`. Here's the whole script again:




```r
#' ---
#' title: "R scripts can be rendered!"
#' author: "Jenny Bryan"
#' date: "April 1, 2014"
#' output: github_document
#' ---
#'
#' Here's some prose in a very special comment. Let's summarize the built-in
#' dataset `VADeaths`.
## here is a regular code comment, that will remain as such
summary(VADeaths)

#' Here's some more prose. I can use usual markdown syntax to make things
#' **bold** or *italics*. Let's use an example from the `dotchart()` help to
#' make a Cleveland dot plot from the `VADeaths` data. I even bother to name
#' this chunk, so the resulting PNG has a decent name.
#+ dotchart
dotchart(VADeaths, main = "Death Rates in Virginia - 1940")
```

Behind the scenes here we have used `rmarkdown::render()` to render this script and you can go [visit it on GitHub](https://github.com/jennybc/happy-git-with-r/blob/master/render-r-script-demo.md).


