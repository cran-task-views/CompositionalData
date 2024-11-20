---
name: CoDa
topic: Compositional Data Analysis
maintainer: Karel Hron, Javier Palarea-Albaladejo, Matthias Templ
email: karel.hron@upol.cz
version: 2024-11-18
source: https://github.com/matthias-da/coda-ctv-draft
---

Compositional data are positive multivariate data where the sum of the values in 
each vector equals a constant, sometimes normalized to unity for convenience. 
These data reside in the standard simplex, a constrained sample space. 
A popular approach for analyzing compositional data involves log-ratio transformations, 
originally introduced by [Aitchison  (1982)](https://doi.org/10.1111/j.2517-6161.1982.tb01195.x). 
The compositional data analysis literature now offers a wide range of methodologies, 
many of which are implemented in publicly available software packages, as listed below.




This task view provides a collection of R packages designed to support compositional data analysis. The packages can be broadly categorized into the following topics, 
although many offer functionalities that span multiple categories:

---

<span style="color: red;">
INTERNAL COMMENTS:
</span>

<span style="color: red;">
Comment from Matthias: Should we outline the properties of a compositional analysis (subcompositional coherence, scale invariance, ...) and 
comment on those methods/packages that violates these basic properties?
</span>

<span style="color: red;">
Comment from Matthias regarding the outline: I am not sure about the structure. I see several possibilities. 
</span>

- <span style="color: red;">One may list packages according to the type of methods 
(such as regression methods, compositional tables, robust methods, visualization, high-dimensional data, ...), </span>

- <span style="color: red;">and the other one lists packages (also) based on applicational fields 
(such as omics science and bioinformatics, chemometrics, ecology, ...). </span>

<span style="color: red;">Personally, I think the main categories should be built based on the kind of methods 
and there could be some extra sections with very specialized fields 
(or even subsubmit them in the previous sections and have 8) High-dimensional data as the last section).


<span style="color: red;">
Maybe something like this?
</span>

<span style="color: red;">
1. General purpose packages
2. Rounded zeros, structural zeros, count zeros, and missing values
3. Multivariate analysis
3. Regression modelling
4. Functional data analysis and probability density functions
5. Robust methods (?)
6. High-dimensional data
7. Contingency tables and compositional tables 
8. Visualization 
9. Special applications in Omics science and bioinformatics (?)
10. Special applications in geo-statistics and geochemistry (? or two points?)
11. Other packages
</span>

<span style="color: red;">
Comment from Matthias: Another idea is to have a similar structure on sections like the sections in the books of CoDa:
</span>

- <span style="color: red;">https://link.springer.com/book/10.1007/978-3-642-36809-7#toc (a bit too less sections, but anyhow good to look at it).</span>
- <span style="color: red;">https://link.springer.com/book/10.1007/978-3-319-96422-5#toc (this would be my choice (but I am biased here) because of a bit more sections, thus maybe a good start)</span>
- <span style="color: red;">https://www.routledge.com/Compositional-Data-Analysis-in-Practice/Greenacre/p/book/9781138316430 </span>


---

### General purpose packages

General purpose packages provide a broad range of tools for compositional data analysis, offering foundational methods that address key challenges such as data transformation, 
visualization, regression, and multivariate analysis. These packages are versatile and applicable across diverse domains, 
making them ideal starting points for compositional data exploration. They often include functionalities for log-ratio transformations, 
principal component analysis, distance-based methods, and hypothesis testing, 
while maintaining compatibility with the simplex geometry of compositional data. 
This section highlights comprehensive packages that form the backbone 
of compositional data analysis, supporting both basic and advanced applications.  







-   `r pkg("easyCODA", priority = "core")`: Provides univariate and multivariate 
methods for compositional data analysis, emphasizing simple pairwise log-ratios. 
Features include selecting log-ratios that explain maximum log-ratio variance 
and conducting multivariate analyses. The package follows the approach detailed 
in [Greenacre (2018)](https://doi.org/10.1201/9780429455537).<span style="color: red;">
Comment from Matthias: easyCODA and coda.base under misc or under general purpose?
</span>

-   `r pkg("coda.base")`: A minimum set of functions to perform compositional 
data analysis using the log-ratio approach introduced by 
[Aitchison (1982)](https://doi.org/10.1111/j.2517-6161.1982.tb01195.x). 
<span style="color: red;">
Comment from Matthias: coda.base rather to "other packages"?
</span>

-  `r pkg("compositions", priority = "core")`: Provides tools for consistent analysis of compositional data (e.g., substance proportions) and positive numbers (e.g., concentrations). Implements methods for univariate and multivariate analysis, including principal component analysis (PCA), cluster analysis, and regression models adapted to compositional data. 
Main reference is [van den Boogaart. and Tolosana-Delgado (2008)](https://doi.org/10.1016/j.cageo.2006.11.017).

-   `r pkg("robCompositions", priority = "core")`: Methods for analysis of compositional data including robust methods, imputation of missing values, methods to replace rounded zeros, count zeros, 
methods to deal with essential (true) zeros, (robust) outlier detection for compositional data, (robust) principal component analysis for compositional data, 
(robust) factor analysis for compositional data, 
(robust) discriminant analysis for compositional data (Fisher rule), 
robust regression with compositional predictors, 
functional data analysis and p-splines, contingency and compositional tables and (robust) Anderson-Darling normality tests for compositional data as well as popular log-ratio transformations. 
References include [Filzmoser, Hron and Templ (2018) ](https://doi.org/10.1007/978-3-319-96422-5) and [Hron et al. (2016)](https://doi.org/10.1016/j.csda.2015.07.007).
<span style="color: red;">
Comment from Matthias: anybody experience with the Compositions package? Should it be core? I rather to intend it for a non-core package
</span>


### Rounded zeros, structural zeros, count zeros, and missing values

Compositional data analysis often involves datasets containing zeros and missing values, 
which require careful handling to preserve the integrity of analyses. 
**Rounded zeros** occur due to detection limits, while **structural zeros** represent true absence. 
**Count zeros** arise in discrete compositional datasets, such as those from sequencing experiments.
Additionally, missing values can pose challenges in maintaining the compositional nature of the data. 

This section focuses on methods to address these issues, including imputation techniques, zero-replacement strategies, 
and approaches tailored to specific types of zeros or missingness. 
Proper handling of zeros and missing values ensures valid, interpretable, 
and robust compositional data analyses across various fields.  

-   `r pkg("zCompositions", priority = "core")`: Principled methods for the imputation of zeros, left-censored and missing data in compositional data sets as descibed in [Palarea-Albaladejo and Martin-Fernandez (2015)](hhttps://doi.org/10.1016/j.chemolab.2015.02.019).

-   `r pkg("robCompositions", priority = "core")`: Amongs others (see general purpose packages) it includes methods to impute of missing values, to replace rounded zeros, 
count zeros, methods to deal with essential (true) zeros.


<span style="color: red;">
Comment from Matthias: are there other packages?
</span>


### Multivariate Analysis

Multivariate analysis is fundamental in compositional data analysis, providing tools to uncover patterns, reduce dimensionality,  
and explore relationships between variables within the constraints of the simplex. 
These methods address the unique challenges posed by the relative nature of compositional data, 
ensuring meaningful interpretation of variation and structure. 
Techniques such as principal component analysis (PCA), correspondence analysis, 
and cluster analysis are adapted to handle the geometry of the simplex, 
while newer approaches like sparse log-ratio methods and canonical correlation analysis 
offer additional insights for complex datasets. 
This section highlights tools designed to extract and visualize meaningful multivariate patterns in compositional data across various domains.  


<span style="color: red;">
Comment from Matthias: which topics to be listed here? Sometimes its evident, just to make a log-ratio
transformation and then apply a standard method. Sometimes it is more complicated. How to deal with this?
</span>

While CoDa is a subfield of multivariate analysis, we list special packages that implements multivariate methods for compositional data in the 
field of principal component analysis, cluster analysis, discriminant analysis, correspondence analysis, correlation analysis, etc.

-   `r pkg("robCompositions", priority = "core")` includes (robust) principal component analysis for compositional data, 
(robust) factor analysis for compositional data, (robust) discriminant analysis for compositional data 
(Fisher rule), robust regression with compositional predictors, see also [Filzmoser, Hron and Templ (2018) ](https://doi.org/10.1007/978-3-319-96422-5).


-   `r pkg("ToolsForCoDa")`: Provides multivariate analysis tools for compositional data, 
including compositional canonical correlation analysis, log-ratio principal component analysis with 
condition number computations, and log-ratio discriminant analysis.

-   `r pkg("lnmCluster")`: Performs logistic normal multinomial clustering for compositional data, 
including extensions for 
factor analysis, biclustering, and sparse covariance estimation.


### Regression Modelling

Regression modelling plays a pivotal role in compositional data analysis, allowing 
researchers to explore relationships between compositional predictors, compositional outcomes, 
or both, while addressing the unique constraints of compositional data. 
These models are essential for understanding associations in fields such as microbiome research, 
geochemistry, and ecology, where the data reside in a simplex and require specialized approaches 
to avoid spurious correlations and preserve meaningful interpretation. 
Tools in this section mostly include methods for handling compositional covariates.

-   `r pkg("complmrob")`: The package provides robust linear regression models for compositional data, 
where the response variable is a real-valued vector and the covariates are compositional data. 
See also [Hron, Filzmoser and Thompson (2012)](https://doi.org/10.1080/02664763.2011.644268). 

-   `r pkg("robregcc")`: The package implements an algorithm estimating the parameters of the robust 
regression model with compositional covariates. 
The model simultaneously treats outliers and parameter estimates. 
The algorithm is described in [Mishra and Mueller (2019)](https://doi.org/10.48550/arXiv.1909.04990).

-   `r pkg("robCompositions", priority = "core")`: Classical and robust regression of 
non-compositional (real) response on compositional and non-compositional predictors

-   `r pkg("codalm")`: Implements the expectation-maximization algorithm for transformation-free linear regression for compositional outcomes and 
predictors of [Fiksel, Zeger and Datta (2021)](https://doi.org/10.1111/biom.13465). <span style="color: red;">
Comment from Matthias: not reviewed or touched yet.
</span>

-   `r pkg("codaredistlm")`: Fits linear regression models with isometric log-ratio (ilr) transformed compositional 
predictors, providing predictions and confidence intervals 
for outcome changes based on reallocations of compositional values, see [Dumuid et al. (2017a)](https://doi.org/10.1177/0962280217710835) and 
[Dumuid et al. (2017b)](https://doi.org/10.1177/0962280217737805). <span style="color: red;">
Comment from Matthias: not reviewed or touched yet.
</span>

-   `r pkg("DirichletReg")`: The package implements Dirichlet regression models. 
While this method is not specifically designed for compositional data and violates the properties of a compositional analysis, 
it can be used to model compositional data. 

-   `r pkg("multilevelcoda")`: Provides Bayesian multilevel modeling for compositional data, including decomposition of Isometric Log Ratios (ILR) at within- and between-person levels, model fitting for compositional 
predictors and outcomes, and post-hoc analyses such as isotemporal substitution models.




### Functional data analysis and probability density functions

Functional data analysis and probability density functions extend compositional data analysis 
to contexts where data are functions or continuous distributions rather than discrete points. 
In compositional settings, functional data arise in scenarios such as time-series compositions 
or compositional curves, requiring specialized tools to analyze their structure 
while respecting the simplex geometry. 
Similarly, the analysis of probability density functions focuses on distributions 
as compositional data, enabling comparisons and modeling of complex systems 
where the sum constraint applies to densities. This section introduces methods and tools designed to address these advanced scenarios,  
allowing researchers to explore functional and distributional compositional data effectively.  
Note that these methods differs from them in the CRAN Task View on [CRAN Task View: Functional Data Analysis](https://cran.r-project.org/view=FunctionalData), 
because most of these methods assume the Bayes space as sample space for density functions.

-   `r pkg("robCompositions", priority = "core")` includes methods for
functional data analysis and compositional smoothing splines grounded on the theory of Bayes spaces.
Additionally, it includes a functional version of the centered log-ratio transformation.

<span style="color: red;">
Comment from Matthias: what else?
</span>


### Robust methods 

<span style="color: red;">
Comment from Matthias: I rather would like to tend to have no section on robust methods.
</span>


### High-dimensional data

High-dimensional compositional data present unique challenges due to the high number of variables 
relative to the number of observations, often leading to issues such as overfitting, 
spurious correlations, and computational inefficiency. 
These challenges are compounded by the constraints of the simplex, 
requiring specialized methods to ensure valid and interpretable results.
This section focuses on tools designed for high-dimensional compositional data, 
including penalized regression, sparse log-ratio methods, dimensionality reduction techniques, and Bayesian approaches. 
These methods enable robust analysis, variable selection, and pattern identification in high-dimensional compositional datasets across fields such as genomics, microbiomics, 
and geochemistry.  <span style="color: red;">
Comment from Matthias: we have microbinomics as seperate point. Not sure how to deal with this. 
</span>

-   `r pkg("robCompositions", priority = "core")` includes methods for the replacement of zeros of 
high-dimensional data sets.

-   `r pkg("ccmm")`: Implements compositional mediation models to estimate 
direct and indirect effects of a 
treatment on an outcome when mediators are high-dimensional and compositional.

<span style="color: red;">
Comment from Matthias: what else?
</span>


### Contingency tables and compositional tables 


Contingency tables and compositional tables are common in compositional data analysis, 
representing frequencies or proportions structured across multiple categories. 
The compositional nature of these tables, often constrained by row or column sums, 
requires specialized methods to analyze relationships, dependencies, and patterns 
while respecting the simplex geometry. 
This section highlights tools for the analysis of contingency and compositional tables, including methods for log-ratio transformations, correspondence analysis, 
association testing, and graphical visualization.  


-   `r pkg("robCompositions", priority = "core")` includes methods for contingency and 
compositional tables, like principal component analysis of compositional tables 
based on backwards pivot coordinates, coordinate representation of compositional tables.

-   `r pkg("lba")`: Implements latent budget analysis for analyzing two-way contingency tables 
with an exploratory and response variable, tailored for compositional data.

<span style="color: red;">
Comment from Matthias: what else?
</span>

### Visualization 

Visualization is a crucial component of compositional data analysis, allowing researchers to intuitively explore patterns, relationships, 
and distributions within the constrained simplex geometry. 
This section includes tools for creating ternary diagrams, biplots, 
pairwise log-ratio plots, among others. 

-   `r pkg("robCompositions", priority = "core")`: Provides, amongst others, basic ternary diagrams and 
compositional biplots and missing and zero patterns plots.

-   `r pkg("robCompositions", priority = "core")`: Provides, amongst others, barplots, biplots (also 
in 3D), boxplots, outlier plots, multiple scatterplots, plots of pairwise log-ratios, QQ-plots, 

-   `r pkg("mvoutlier")`:	The package includes tools for visualizing multivariate outliers in compositional data.

-   `r pkg("Ternary")`: Creates ternary diagrams and Holdridge life zone plots using base graphics. Features include custom annotation, interpolation, contouring, scaling, and a 
Shiny interface for interactive plotting. An alternative to `ggtern` for ternary visualizations.

-   `r pkg("ggtern")`: Extends `ggplot2` to create ternary diagrams, supporting standard and 
additional custom geometries. Provides a range of specialized tools for ternary visualizations. 
Comprehensive examples and documentation are available on the `ggtern` website.

-   `r pkg("isopleuros")`: Simplifies the creation of ternary plots using base graphics. 
Offers tools for visualizing data in ternary space, customizing graphical elements, 
and displaying statistical summaries. Includes specialized diagrams for fields like 
archaeology (e.g., soil texture charts, ceramic phase diagrams).

-   `r pkg("provenance")`: The package includes tools to plot compositional and count data on ternary diagrams and point-counting data on radial plots, to calculate the sample size required for specified levels of statistical precision, and to assess the effects of hydraulic sorting on detrital compositions. Includes an intuitive query-based user interface for users who are not proficient in R.



### Special applications in Omics science and bioinformatics (?)

Compositional data analysis is essential in omics sciences and bioinformatics, 
where datasets, such as microbiome compositions, gene expression profiles, 
and metabolomic measurements, are inherently compositional. 
These applications require methods that address unique challenges, 
including high dimensionality, zero inflation, and the integration of phylogenetic structures.
This section highlights tools specifically designed for omics data.  


-   `r pkg("FLORAL")`: Log-ratio lasso regression for continuous, binary, and survival outcomes with compositional features by 
[Fei et al. (2023)](https://doi.org/10.1101/2023.05.02.538599).

-   `r pkg("ampir")`: Predicts antimicrobial peptides from protein sequences on a genome-wide scale using support vector machine models trained on physico-chemical and compositional sequence properties. Optimized for high-throughput analyses,
it supports any protein input for large-scale predictions.
<span style="color: red;">
Comment from Matthias: Is it a CoDa package?
</span>

-   `r pkg("BRACoD.R")`: Implements Bayesian regression to identify associations between 
microbiome compositional data and environmental variables. 
Corrects for compositional distortions by treating total abundance as an unknown variable. 
Integrates with Python via `reticulate`.<span style="color: red;">
Comment from Matthias: Needs to be checked.
</span>

-   `r pkg("coda4microbiome")`: Provides tools for microbiome data analysis, accounting for its 
compositional nature. Includes penalized regression methods for variable selection in cross-sectional 
and longitudinal studies with binary or continuous outcomes.

-   `r pkg("codacore")`: Identifies sparse log-ratios predictive of a response variable in 
compositional data. Applicable to regression problems, it derives 
scale-invariant log-ratios (ILR or SLR) 
optimized for association with the dependent variable.

-   `r pkg("MicrobiomeStat")`: Provides robust methods for analyzing microbiome compositional data, addressing zero-inflation, phylogenetic structure, and compositional effects. 
Applicable to other high-dimensional compositional datasets from sequencing experiments.<span style="color: red;">
Comment from Matthias: Needs to be checked.
</span>

-   `r pkg("QFASA")`: Implements quantitative fatty acid signature analysis to estimate 
predator diets accurately, leveraging fatty acid diversity, 
biosynthesis limitations, and digestion properties in monogastric animals.<span style="color: red;">
Comment from Matthias: Needs to be checked.
</span>


### Special applications in geo-statistics and geochemistry

Compositional data analysis is integral to geostatistics and geochemistry, 
where datasets often represent proportions of elements, minerals, or isotopes, 
and are subject to spatial dependencies. 
These applications require methods that respect the simplex constraints 
while addressing spatial structures and relationships. 
This section features tools for geostatistical modeling, spatial interpolation, 
variogram analysis, and compositional kriging, as well as techniques 
for analyzing geochemical compositions in the context of spatial data.  


-   `r pkg("provenance")`: Offers statistical tools for sedimentary provenance analysis, 
including kernel density estimation, PCA, correspondence analysis, and multidimensional scaling. 
Supports comparison of univariate proxies (e.g., single-grain ages, isotopic compositions) and 
categorical data using distances like Kolmogorov-Smirnov, Wasserstein, Aitchison, and Bray-Curtis. 
Features tools for visualizing data on ternary and radial plots, calculating sample sizes, and 
assessing hydraulic sorting effects. 
Includes a user-friendly interface for non-R users.

-   `r pkg("ArArRedux")`: Facilitates rigorous data reduction and error propagation for 
Ar\(^\text{40}\)/Ar\(^\text{39}\) geochronology, processing isotopic compositions from noble 
gas mass spectrometer data. Includes methods for regression to t=0, blank and decay corrections, 
detector intercalibration, interference corrections, and age calculation. 
Treats argon isotope ratios as compositional data for accurate statistical handling.

-   `r pkg("gmGeostats")`: Provides geostatistical tools for multivariate data with restrictions, 
including compositions and positive amounts. Features include descriptive analysis and 
modeling using two-point Gaussian and multipoint perspectives. It also contains compositional 
variograms and compositional kriging. <span style="color: red;">
Comment from Matthias: Compositional Variogram to Visualization?
</span>

<span style="color: red;">
Comment from Matthias: Which packages are missing for geo?
</span>


### Other packages


-   `r pkg("aIc")`: Provides tests for identifying compositional pathologies in datasets, 
including coherence of correlations, dominance of distance, perturbation invariance, 
and singularity of the covariation matrix. Supports multiple data transformations such as 
proportional, centered log-ratio (clr), and others from common R packages.

-   `r pkg("CMMs")`: Provides compositional mediation models for continuous and binary outcomes, 
handling mediators represented as compositional data.


-   `r pkg("countprop")`: The package calculates metrics of proportionality using the logit-normal multinomial model. It can also provide empirical and plugin estimates of these metrics. 
<span style="color: red;">
Comment from Matthias: Needs to be checked if it is a CoDa package.
</span>


-   `r pkg("FlexDir")`: Offers tools for the Flexible Dirichlet distribution, 
including maximum likelihood estimation via E-M algorithm, variance-covariance matrix estimation, 
random data generation, and visualization. Supports applications to compositional data.
<span style="color: red;">
Comment from Matthias: Exclude FlexDir?
</span>



-   `r pkg("SARP.compo")`: Offers tools for network-based interpretation of changes 
in compositional data, including computation of pairwise ratios, 
statistical testing between conditions, and network representation of results.

<!--
-   `r pkg("NBDdirichlet")`: Implements NBD-Dirichlet Model of Consumer Buying Behavior for Marketing
Research. The relevant paper is [Goodhardt, Ehrenberg and Chatfield (1984)](https://doi.org/10.2307/2981696).

-   `r pkg("rBeta2009")`: The packate contains a function for generating Dirichlet random vectors using a C translation. The relevant paper is [Hung, Balakrishnan and Cheng (2011)](https://doi.org/10.1080/00949650903409999).

-->

-   `r pkg("zetadiv")`: Provides tools for analyzing compositional turnover using zeta-diversity, including calculations for single or multiple assemblages and modeling its variation with distance or 
environmental differences using methods like GLMs, GAMs, and I-splines.
<span style="color: red;">
Comment from Matthias: Needs to be checked if it is a CoDa package.
</span>





### Links

-   [CRAN Task View: Functional Data Analysis](https://cran.r-project.org/view=FunctionalData)
-   [CRAN Task View: Bayesian](https://cran.r-project.org/view=Bayesian)
-   [CRAN Task View: Cluster](https://cran.r-project.org/view=Cluster)
-   [CRAN Task View: MachineLearning](https://cran.r-project.org/view=MachineLearning)
-   [CRAN Task View: Robust](https://cran.r-project.org/view=Robust)
-   [CRAN Task View: SpatioTemporal](https://cran.r-project.org/view=SpatioTemporal)

