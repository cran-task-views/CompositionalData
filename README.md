# coda-ctv-draft

This is an intitial github repo for the CRAN Task View (CTV) on Compositional Data Analysis. 

Afterwards we put this CTV as an issue (assigned to Achim Zeileis) to the CRAN Task View 
GitHub repository.

To compile the Markdown file:

```{r}
library("ctv")
ctv2html("CoDa.md", cran = TRUE)
browseURL("CoDa.html")
```

Check for errors:

```{r}
check_ctv_packages("CoDa.md")
```
