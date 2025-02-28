---
name: CompositionalData
topic: Compositional Data Analysis
maintainer: Karel Hron, Javier Palarea-Albaladejo, Matthias Templ, Alessandra Menafoglio
email: karel.hron@upol.cz
version: 2024-11-18
source: https://github.com/cran-task-views/CompositionalData/
---


In general, compositional data refers to multivariate, positive and scale-invariant data that convey relative information. Although not necessarily, they are often closed or normalized to be expressed in proportions adding up to 1, percentages adding to 100, or the like; but the scale-invariance property implies that the normalization constant used is actually irrelevant. That is, compositional methods are applicable whenever the researcher recognizes that the relevant information in the data is relative and, thus, there is an intrinsic interdependence between the parts that make up the composition. These particularities are not considered by ordinary statistical methods, which are generally designed for unconstrained real-valued data.

This task view provides a curated collection of R packages to 
support compositional data analysis within the log-ratio coordinate framework. The main goal is serving as a guide to practitioners interested in applying such methods. The packages can be broadly categorized into the following topics, although many provide functionalities spanning multiple categories, as detailed below.

**Table of Contents**


- [General purpose packages](#general-purpose-packages)
- [Irregular data: zeros, censoring, missing and outliers](#irregular-data-zeros-censoring-missing-and-outliers)
- [Visualization](#visualization)
- [Compositional tables](#compositional-tables)
- [Density data analysis](#density-data-analysis)
- [Regression modelling](#regression-modelling)
- [High-dimensional compositional data with applications to omics data](#high-dimensional-compositional-data-with-applications-to-omics-data)
- [Special applications in geostatistics and geochemistry](#special-applications-in-geostatistics-and-geochemistry)
- [Other packages](#other-packages)
- [Background](#background)
- [References](#references)





### General purpose packages 

This section refers to packages that provide a general platform for compositional data 
analysis in R, implementing functions to conduct basic operations and 
calculations, log-ratio representations, 
data visualization and some common statistical analyses. They, typically 
accompany a published monograph and provide an environment for analysis compatible with the basic 
properties of compositional data for those approaching the methodology from diverse domains. 

-   `r pkg("compositions", priority = "core")`: once a class for the 
data is set, which corresponds
to the assumed underlying geometry (either compositional, `acomp` class, or 
multivariate positive data, `aplus` class), the package operates through functions for 
their consistent analysis and modelling; including descriptive statistics, 
visualization, statistical testing, and multivariate analysis (e.g. principal 
component analysis, clustering, MANOVA and regression). It also implements some geostatistical tools such a variogram for compositions and compositional ordinary kriging.
This package is linked to the monograph 
[van den Boogaart and Tolosana-Delgado (2013)](https://link.springer.com/book/10.1007/978-3-642-36809-7) 
and supports the analyses and examples therein.

-   `r pkg("robCompositions", priority = "core")`: with a main focus on robust 
statistical methods (see `r view("Robust")` for an overview of other robust statistical methods available in R). The package includes a wide range of tools for the 
manipulation and analysis of
compositional data within the log-ratio framework. This includes ordinary transformations, dealings 
with irregular data, and robust versions of methods such as 
principal component analysis, factor analysis and discriminant analysis and regression with compositional 
predictors. Additionally, it implements specialized methods for two-factorial compositions (a.k.a compositional tables) and 
functional-compositional analysis of density data. 
The main reference monograph is 
[Filzmoser, Hron and Templ (2018) ](https://doi.org/10.1007/978-3-319-96422-5).

-   `r pkg("easyCODA", priority = "core")`: provides methods and graphics for univariate and multivariate 
analysis of compositional data in the spirit of [Greenacre (2018)](https://doi.org/10.1201/9780429455537), emphasizing 
the use of basic pairwise log-ratios. Particular features include procedures for stepwise selecting log-ratios,
correspondence analysis and redundance analysis.

<!--
-   `r pkg("Compositional")`: regression, classification, contour plots, hypothesis 
testing and fitting of distributions for compositional data are some of the 
functions included in this package. Furthermore, some functions to deal with for percentages 
(or proportions) are included. Distinctly, the package deals with compositional 
data mostly as constrained data, thus ignoring the scale invariance 
property and, more generally, the principles of compositional data analysis 
characterizing the log-ratio framework originally established in the classical reference 
[Aitchison (1986)](https://doi.org/10.1002/bimj.4710300705)). Such approach allows for 
zero components in the analysis, but leads to some 
conceptual inconsistencies that the log-ratio approach on the other hand aims to avoid. Thus, analyses based on this package may be incoherent with those based on 
`r pkg("compositions", priority = "core")`,  `r pkg("robCompositions", priority = "core")` and other packages below.
-->

### Irregular data: zeros, censoring, missing and outliers

As with ordinary data sets, compositional data are often affected by issues
which may prevent from straightforward application of statistical methods in real-world applications.

Of particular relevance for the log-ratio approach is the treatment zeros, which requires careful handling
to not distorting basic properties of the data and preserve the consistency of subsequent analyses. Traditionally,
three types of zeros have been distinguished: _rounded zeros_, _count zeros_ and
_essential zeros_. Briefly, rounded zeros occur in continuous-valued compositions, and are generally
associated with small values that have been rounded or have fallen below the detection limit of
the measuring device; count zeros refer to zeros that occur in discrete compositions derived from a
counting processes, generally associated with limited sampling; and, finally, essential zeros
refer to truly zero values, i.e. parts of the composition that are genuinely absent.
Rounded zeros, which essentially correspond to a class of left-censored data, have received the most
attention in the literature.

Moreover, analogously to ordinary statistical methods, the presence of either missing values or outliers poses practical challenges.
Again, coherent handling is required for consistent data analysis within the compositional
framework.

The following are specialized packages focused on addressing these issues while respecting the compositional nature of the data.

-   `r pkg("zCompositions", priority = "core")`: a suite of data imputation methods applicable to zeros, nondetects, missing data, and combinations of them, following the
principles of the log-ratio approach ([Palarea-Albaladejo and Martín-Fernández (2015)](https://doi.org/10.1016/j.chemolab.2015.02.019)). This includes a consistent treatment of closed and
non-closed compositions, unique or varying detection limits, parametric and nonparametric imputation, single and multiple imputation, maximum likelihood and robust estimation, as well as some tools for the exploration of zero patterns and statistical testing of grouping structures.

-   `r pkg("mvoutlier")`:	specific tools for visualizing and identifying multivariate outliers in compositional data.

<!--
-   `r pkg("robCompositions", priority = "core")`: routines included to impute rounded zeros and missing data, as well as tools to detect outlying samples. 

-   `r pkg("compositions", priority = "core")`: routines included to detect, represent, and provide some analysis of irregular data, either missing values, zeros or outliers.
-->


### Visualization 

Visualization is a critical component of compositional data analysis, allowing researchers to explore patterns, relationships, and distributions within the constrained simplicial geometry.

On top of the functionality provided with the *general purpose packages* cited above, this section compiles
specialized tools for producing ternary plots, compositional biplots, or pairwise log-ratio plots, among others.

-   `r pkg("ggtern")`: enables plotting and managing ternary diagrams following the style and syntax of the
graphical package `ggplot2`; supporting both standard and additional geometries with a high level of customization. 

-   `r pkg("Ternary")`: produces ternary diagrams and Holdridge life zone plots using base graphics. Particular features include custom annotation, interpolation, contouring, scaling, and a 
Shiny interface for interactive plotting.

-   `r pkg("isopleuros")`: visualisation of data in ternary space, customising graphical elements, 
and displaying statistical summaries. Includes specialized diagrams in archaeology, e.g. soil texture charts and ceramic phase diagrams.

-   `r pkg("provenance")`: representation of compositional and count data on ternary diagrams and point-counting data on radial plots. Allows to compute sample size required for specified levels of statistical precision,
and to assess the effects of hydraulic sorting on detrital compositions. Provides an intuitive query-based user interface for users who are not proficient in R.

<!--
<span style="color: red;">
Comment from KH: I removed the robCompositions package from here so that it does not sound like overselling (and visualization tools are contained e.g. also in
compositions package), but I added a comment to description of the section. Javier: Agree, and the same would apply to the previous section about
irregular data, particularly in relation to `compositions`. Some irregular data and also visualisation and also regression functionality (in relation
to the following section) are included in the general purpose packages, but should them be mentioned in all these specialised sections? I do not think so,
it can be just mentioned, as done in the first section, when they are described, and focus these sections in packages that are
specialised in a particular topic and have some distinctive feature. Alessandra: I agree with this strategy; however, should we say somewhere that the user can anyway also make reference to the basic packages although there are the specialized one? My idea would be that the user looking for a standard regression would first pass through the basic package and then through the advanced one.
</span>
-->

### Compositional tables 

Compositional tables (i.e., ordinary contingency tables in their discrete version) represent frequencies or proportions structured across multiple categories. The compositional nature of these tables, often constrained by row or column sums,
requires specialized methods to analyze relationships, dependencies, and patterns while respecting their
relative nature. This section refers to tools for their analysis,
including log-ratio representation and selected multivariate methods.


-   `r pkg("robCompositions", priority = "core")`: log-ratio coordinate representation of compositional tables and methods for their statistical processing using principal component analysis and regression analysis with a real response and the compositional table as predictor. See [Filzmoser, Hron and Templ (2018)
](https://doi.org/10.1007/978-3-319-96422-5) (Chapter 12) and [Nesrstová et al. (2023)](https://doi.org/10.57645/20.8080.02.9) for more details.

<!-- -   `r pkg("lba")`: latent budget analysis for analysing two-way contingency tables with an exploratory and response variable, tailored for constant sum representation of compositional data. -->



### Density data analysis

Probability density functions are essentially scale invariant data objects, usually subject to a unit integral constraint. Therefore, they can be considered as infinite dimensional compositional
data and embedded in a Hilbert space, so-called a Bayes space (see [van den Boogaart, Egozcue and Pawlowsky-Glahn (2014)](https://doi.org/10.1111/anzs.12074) for details).

The packages listed below implement methods for density data analysis from this perspective.
Unlike the methods in the `r view("FunctionalData")` task view, here it is assumed that the sample space for density functions is the Bayes space. 

-   `r pkg("robCompositions", priority = "core")`: methods for
representation of probability density functions using compositional smoothing splines, grounded on the theory of Bayes spaces.
Additionally, a functional version of the centered log-ratio transformation is included.

<!--
<span style="color: red;">
Comment from Matthias: what else? KH: I'm afraid that currently nothing. One can also consider to add the 'fdadensity' package from Petersen et al. but it could be quite misleading as it is based on another approach (mapping PDFs to(!) a Hilbert space). We therefore urgently need to build such a package.:-)
Alessandra: I agree with Karel. I'm wondering whether we should mention that after basis projection one could possibly resort to the 'fda' package for further processing - but this is not really ready-to-use, so work needs to be done. In addition: should we include a reference to some work? It could be the paper on Bayes Hilbert spaces, or it could also be the entry on Bayes spaces in the encyclopedia.
</span>


<span style="color: red;">
Comment from KH: I removed the general section High dimensional data because there were only two packages and the package ccmm was very specific. I moved it to Other packages, where also a similar one-purpose package CMMs is located.
</span>
-->

### Regression modelling

Regression modelling with compositional data allows researchers to explore associations between compositions
and other variables, either as predictors/covariates or response; and also between compositions on both
sides of the regression model. Packages specifically devoted to compositional regression analysis are listed below. It should be noted that `r pkg("complmrob")` and `r pkg("robregcc")` do not offer anything essential beyond, for example, `r pkg("robCompositions")`.
<!--
<span style="color: red;">
Javier: I have removed the subsequent text as I found it too redundant and referring to general things not specific to regression
analysis. I have instead added some general comments about "why CoDa analysis" in the general introduction at the beginning.
</span>
<span style="color: red;">
Alessandra: I would rephrase the last sentence as: "Although compositional regression can be generally performed using the *general purpose packages*, packages specifically devoted to compositional regression analysis are listed in the following.
</span>
-->

-   `r pkg("complmrob")`: robust linear regression models for compositional data, 
where the response variable is a real-valued vector and the covariates are compositional data. 
See also [Hron, Filzmoser and Thompson (2012)](https://doi.org/10.1080/02664763.2011.644268). 

-   `r pkg("robregcc")`: algorithm estimating the parameters of the robust regression model with compositional covariates. 
The model simultaneously treats outliers and parameter estimates as described in [Mishra and Mueller (2019)](https://doi.org/10.48550/arXiv.1909.04990).

<!--
<span style="color: red;">
Javier: it would be worth highlighting what is the added value of the above packages, particularly the first, 
any particular/special feature? Otherwise, from the current description, it is not clear what they are offering
beyond e.g. `robCompositions`.
</span>
-->

<!--
-   `r pkg("codalm")`: Implements the expectation-maximization algorithm for transformation-free linear regression for compositional outcomes and 
predictors of [Fiksel, Zeger and Datta (2021)](https://doi.org/10.1111/biom.13465). <span style="color: red;">
Comment from Matthias: not reviewed or touched yet. KH: then I would remove it, Javier: agree. Alessandra: What do you mean that it was not reviewed? 
</span>
-->

-   `r pkg("codaredistlm")`: linear regression models with compositional predictors, providing predictions
and confidence intervals for outcome changes based on reallocations of compositional values, see [Dumuid et al. (2017a)](https://doi.org/10.1177/0962280217710835) and 
[Dumuid et al. (2017b)](https://doi.org/10.1177/0962280217737805). 


-   `r pkg("DirichletReg")`: functions to analyse compositional data using Dirichlet regression models. 

-   `r pkg("multilevelcoda")`: Bayesian multilevel modelling with compositional data, both as predictors and outcomes, and _post hoc_ isotemporal substitution analysis.


### High-dimensional compositional data with applications to the omics sciences

In recent years, compositional data analysis has had a notable impact on the omics sciences and bioinformatics,
where data types such as microbiome compositions, gene expression, or metabolomic profiles have been
recognized as inherently compositional. Applications in this area require methods that address unique
challenges such as high dimensionality, zero inflation, overdispersion or the integration of phylogenetic
information.

This section highlights packages that provide compositional tools designed for omics data, but certainly most of
them could also be considered for the statistical processing of high-dimensional compositional data in general.  

-   `r pkg("FLORAL")`: log-ratio lasso regression for continuous, binary, and survival outcomes with compositional features as described in [Fei et al. (2023)](https://doi.org/10.1101/2023.05.02.538599).

<!--
-   `r pkg("BRACoD.R")`: Implements Bayesian regression to identify associations between 
microbiome compositional data and environmental variables. 
Corrects for compositional distortions by treating total abundance as an unknown variable. 
Integrates with Python via `reticulate`.
-->

<!--
<span style="color: red;">
Comment from Matthias: Needs to be checked. KH: data are identified as compositional, but rather in sense of constrained data. Javier: it does not refer to any paper where the method is explained for more
details ... Not sure that this fits in.
</span>
-->

-   `r pkg("coda4microbiome")`: tools for microbiome data analysis while accounting for its compositional nature. Includes penalized regression methods for variable selection in cross-sectional 
and longitudinal studies with binary or continuous outcomes.

-   `r pkg("codacore")`: identification of sparse log-ratios of a composition acting as predictor in regression problems. Scale invariant log-ratios are derived which are optimized to account for
association with the response variable.

-   `r pkg("lnmCluster")`: logistic normal-multinomial clustering for microbiome compositional data, including extensions for factor analysis, bi-clustering, and sparse covariance estimation.

-   `r pkg("MicrobiomeStat")`: robust methods for analysing microbiome compositional data, addressing zero inflation, phylogenetic structure, and compositional effects. 
Applicable to other high-dimensional compositional data sets from sequencing experiments.

-   `r pkg("QFASA")`: quantitative fatty acid signature analysis to estimate predator diets, leveraging fatty acid diversity, biosynthesis limitations, and digestion properties
in monogastric animals. Both methods for compositional and constrained data are used.



### Special applications in geostatistics and geochemistry

Compositional data analysis is an integral part of geostatistics and geochemistry, areas where the
methodology found its first successful applications. Data sets here often represent proportions of elements,
minerals, or isotopes, and are subject to spatial dependencies (see `r view("SpatioTemporal")` for a task view focused on spatiotemporal methods). In the case of compositional data, these
applications require methods that
respect their relative nature while taking into account any spatial structures and relationships.

Thus, this section refers to packages for geostatistical modelling,
spatial interpolation, variogram analysis, and compositional kriging; as well as techniques for analyzing spatial
geochemical compositions. Note that some methods would be equally applicable to any data set with analogous
structures in any other application area.

-   `r pkg("provenance")`: statistical tools for sedimentary provenance analysis, 
including kernel density estimation, principal component analysis, correspondence analysis, and multidimensional scaling. Comparison of univariate proxies (e.g., single-grain ages, isotopic compositions) and 
categorical data are supported using distances like Kolmogorov-Smirnov, Wasserstein, Aitchison, and Bray-Curtis. Tools for visualizing data on ternary and radial plots, calculating sample sizes, and 
assessing hydraulic sorting effects are included. Additionally, a user-friendly interface is provided for R beginners.

-   `r pkg("ArArRedux")`: data reduction and error propagation for 
$Ar\^\text{40}\/Ar\^\text{39}\$ geochronology, processing isotopic compositions from noble 
gas mass spectrometer data. Methods for regression, blank and decay corrections, 
detector intercalibration, interference corrections, and age calculation. 
Argon isotope ratios are treated as compositional data for accurate statistical handling.

-   `r pkg("gmGeostats")`: tools for multivariate data with restrictions, 
including compositions and positive amounts. Descriptive analysis and 
modelling using two-point Gaussian and multipoint perspectives. Compositional 
variograms and compositional kriging. <span style="color: red;">

<!--
Javier: I have commented this when describing the compositions package above.
-  `r pkg("compositions")`: includes a compositional variogram and kriging methods. <span style="color: red;">
-->



### Other packages

This collection is meant to include other useful small packages, typically having a fairly specific purpose.
In accordance with the log-ratio framework considered here, the condition for inclusion is that the scale invariance property of compositional data is, at least partially, respected.

<!--
Packages contained in this section are either of specific purpose or do not necessarily account 
for scale invariance of compositional data and consider them rather as constrained data.
Still methods contained in these packages can be useful in concrete applications, e.g. 
also for comparison to methods based on the log-ratio methodology.
-->

-   `r pkg("coda.base")`: provides optimized and user-friendly implementations of functions to compute log-ratio coordinate representations of various types,
including principal component and principal balance coordinates, as well as log-ratio coordinates from tailored orthonormal basis. It also allows to compute some basic compositional statistics.

-   `r pkg("aIc")`: statistical tests to identify compositional _pathologies_ in data. Namely, coherence of
correlations, dominance of distances, perturbation invariance, and singularity of the covariation matrix. Supports
multiple data transformations such as proportional, centred log-ratio (clr), and others from common R packages.

<!--
-   `r pkg("CMMs")`: compositional mediation models for continuous and binary outcomes, handling mediators represented as compositional data.

-   `r pkg("ccmm")`: compositional mediation models to estimate direct and indirect effects of a treatment on an outcome, designed for the case in which mediators are high-dimensional microbiome data.
-->

<!--
-   `r pkg("countprop")`: model-based metrics of proportionality using the logit-normal multinomial model. It can also provide empirical and plugin estimates of these metrics. 

-   `r pkg("FlexDir")`: tools for using the flexible Dirichlet distribution, 
including maximum likelihood estimation via EM algorithm, variance-covariance matrix estimation, 
random data generation, and visualisation. Supports applications to compositional data.
-->

-   `r pkg("SARP.compo")`: tools for network-based interpretation of changes 
in compositional data, including computation of pairwise ratios, 
statistical testing between conditions, and network representation of results.


<!--
<span style="color: red;">
Comment from Karel: If we would accept the disclaimer in the general description of the package we could also add
further packages which are currently removed.
</span>
-->

<!--
-   `r pkg("NBDdirichlet")`: Implements NBD-Dirichlet Model of Consumer Buying Behavior for Marketing
Research. The relevant paper is [Goodhardt, Ehrenberg and Chatfield (1984)](https://doi.org/10.2307/2981696).

-   `r pkg("rBeta2009")`: The packate contains a function for generating Dirichlet random vectors using a C translation. The relevant paper is [Hung, Balakrishnan and Cheng (2011)](https://doi.org/10.1080/00949650903409999).

-->

-   `r pkg("ToolsForCoDa")`: selected multivariate analysis tools for compositional data, including compositional canonical correlation analysis, log-ratio principal component analysis with condition number computations, and log-ratio discriminant analysis.

<!--
-   `r pkg("zetadiv")`: tools for analysing compositional turnover using zeta-diversity, including calculations for single or multiple assemblages and modelling its variation with distance or 
environmental differences using methods like GLMs, GAMs, and I-splines.
<span style="color: red;">
Comment from Matthias: Needs to be checked if it is a CoDa package. KH: I added a disclaimer instead at the beginning of the section.
Javier: I'm  not very convinced with the disclaimer that would apply to several packages above and others, if we are stating the "Compositional Data Analysis"
framework at the beginning, particularly that CoDa are scale invariant, I think we should stick to packages
aiming to respect this one way or another; otherwise it somehow loses its sense and almost any package referring to "compositions" should be
included, which would also make the maintaining of this task view more complicated ... 
we are at least r
Alessandra: I agree with Javier's viewpoint, we should put a boundary to say who are the packages in scope with this. However, with respect to this, it is not easy then to decide who's inside and who's outside, and probably someone will sit on the boundary. Should we then also exclude the package "Compositional", based on this reasoning?
</span>
-->

### Background
Awareness of the problems with compositional data dates back to the end of the 19th century, when the renowned statistician Karl Pearson recognized the problem of spurious correlations between variables scaled with respect to a common denominator. When closed to add up to constant value, compositional data are formally projected on a simplex sample space, and this is often a convenient representation in a practical setting. The simplex is a constrained space with its own internal operations and geometry. However, any coherent approach to analyzing compositional data should not depend on the chosen representation, nor require any preliminary normalization. 

The mainstream approach to compositional data analysis, as originally formulated by 
[Aitchison (1982)](https://doi.org/10.1111/j.2517-6161.1982.tb01195.x), involves the use of log-ratio transformations (or log-ratio coordinates to use a more more modern terminology) which project the data into real space. Nowadays, the compositional literature offers a wide range of methods within this methodological framework, many of which are implemented in R packages.

Compositional data are common in diverse scientific fields, including the chemical, biological, and environmental sciences; where they typically represent portions of a total sample weight or volume and are expressed in units such as percent, parts per million, mg/l, mmol/mol, or similar. Some examples include chemical compositions of soil, water, or air, 
food compositions, behavioral or time-use profiles, and relative abundances of species. They are also common in socio-economical sciences; for example when dealing with market shares, investment portfolios, or household budgets.

In recent years, the popularity of compositional methods has grown significantly. Simultaneously, new methodological challenges have arisen requiring novel ways to transfer and formulate compositional knowledge to meet the needs of different scientific fields.

### References
