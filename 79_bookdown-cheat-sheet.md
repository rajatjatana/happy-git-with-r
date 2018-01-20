# Bookdown cheat sheet

Here's where I park _little_ *examples* **for myself** about bookdown mechanics that I keep forgetting.

## Heading blah blah

## About labelling things {#id-example}

You can label chapter and section titles using `{#label}` after them, e.g., we can reference Section \@ref(id-example). If you do not manually label them, there will be automatic labels anyway, e.g., this reference to the unlabelled heading \@ref(heading-blah-blah) uses the automatically generated label `\@ref(heading-blah-blah)`.

## Cross-references

Add an explicit label by adding `{#label}` to the end of the section header. If you know you're going to refer to something, this is probably a good idea.

To refer to in a chapter- or section-number-y way, use `\@ref(label)`.

  * `\@ref(install-git)` example: In chapter \@ref(install-git) we explain how to install Git.

If you are happy with the section header as the link text, use it inside a single set of square brackets:

  * `[A picture is worth a thousand words]`: example "A picture is worth a thousand words" via [A picture is worth a thousand words]

There are two ways to specify custom link text:

  * `[link text][Section header text]`, e.g., "pic = 1000 words" via [pic = 1000 words][A picture is worth a thousand words]
  * `[link text](#label)`, e.g., "RStudio, meet Git" via [RStudio, meet Git](#rstudio-see-git)
  
The Pandoc documentation provides more details on automatic section IDs and implicit header references.

## Figures, tables, citations

Figures and tables with captions will be placed in `figure` and `table` environments, respectively.


```r
par(mar = c(4, 4, .1, .1))
plot(pressure, type = 'b', pch = 19)
```

<div class="figure" style="text-align: center">
<img src="79_bookdown-cheat-sheet_files/figure-html/nice-fig-1.png" alt="Here is a nice figure!" width="80%" />
<p class="caption">(\#fig:nice-fig)Here is a nice figure!</p>
</div>

Reference a figure by its code chunk label with the `fig:` prefix, e.g., see Figure \@ref(fig:nice-fig). Similarly, you can reference tables generated from `knitr::kable()`, e.g., see Table \@ref(tab:nice-tab).


```r
knitr::kable(
  head(iris, 20), caption = 'Here is a nice table!',
  booktabs = TRUE
)
```



Table: (\#tab:nice-tab)Here is a nice table!

 Sepal.Length   Sepal.Width   Petal.Length   Petal.Width  Species 
-------------  ------------  -------------  ------------  --------
          5.1           3.5            1.4           0.2  setosa  
          4.9           3.0            1.4           0.2  setosa  
          4.7           3.2            1.3           0.2  setosa  
          4.6           3.1            1.5           0.2  setosa  
          5.0           3.6            1.4           0.2  setosa  
          5.4           3.9            1.7           0.4  setosa  
          4.6           3.4            1.4           0.3  setosa  
          5.0           3.4            1.5           0.2  setosa  
          4.4           2.9            1.4           0.2  setosa  
          4.9           3.1            1.5           0.1  setosa  
          5.4           3.7            1.5           0.2  setosa  
          4.8           3.4            1.6           0.2  setosa  
          4.8           3.0            1.4           0.1  setosa  
          4.3           3.0            1.1           0.1  setosa  
          5.8           4.0            1.2           0.2  setosa  
          5.7           4.4            1.5           0.4  setosa  
          5.4           3.9            1.3           0.4  setosa  
          5.1           3.5            1.4           0.3  setosa  
          5.7           3.8            1.7           0.3  setosa  
          5.1           3.8            1.5           0.3  setosa  

You can write citations, too. For example, we are using the **bookdown** package [@R-bookdown] in this sample book, which was built on top of R Markdown and **knitr** [@xie2015].
