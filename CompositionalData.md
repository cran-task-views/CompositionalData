---
name: CompositionalData
topic: Compositional Data Analysis
maintainer: Karel Hron, Javier Palarea-Albaladejo, Matthias Templ, Alessandra Menafoglio
email: karel.hron@upol.cz
version: 2024-11-18
source: https://github.com/cran-task-views/CoDa/
---


In general terms, compositional data refers to multivariate, positive and scale 
invariant data that convey relative information. Although not necessarily, 
they are often closed or normalised to be expressed in proportions adding up to 
1, percentages adding up to 100, or the like; but the scale invariance property 
implies that the value of any normalisation
constant is in fact irrelevant. That is, compositional methods are applicable 
whenever the researcher recognises that the relevant information in the data is 
relative and there is an intrinsic
interdependence between the parts configuring the composition. These particular 
characteristics are missed by ordinary statistical methods generally designed 
for unconstrained real-valued data.

Awareness of the issues with compositional data dates back to the end of the 
19th century, when the renowned statistician Karl Pearson already identified 
the problem of spurious correlation between variables
representing ratios with respect to a common denominator caused by the scaling 
of the data. When closed, compositional data formally live on a simplex sample
space, and this can be a convenient representation in a practical setting. The 
simplex is a constrained space with its own internal operations and geometry.
However any coherent approach to analyse compositional data should not depend 
on any particular representation chosen nor require any preliminary 
normalisation.

The mainstream approach to analysing compositional data, as originally 
formulated by 
[Aitchison (1982)] (https://doi.org/10.1111/j.2517-6161.1982.tb01195.x),
involves the use of log-ratio transformations, or log-ratio coordinates using a 
more modern terminology, that project the data onto the real space. Nowadays, 
the literature offers a wide
range of methods and tools to tackle the analysis of compositional data within 
this methodological framework, many of which are implemented in R packages.

Compositional data are common in diverse scientific areas, including the 
chemical, biological and environmental sciences; typically representing portions 
of a total sample weight or volume and
expressed in units such as percentages, parts per million, mg/l, mmol/mol or 
similar. Some examples include chemical compositions of soil, water or air, 
food compositions, behavioural time-use profiles,
and species relative abundances. They are also common in social sciences like 
economics. For example, market shares, investment portfolios, or household 
budgets.

In recent years, the popularity of compositional methods has increased notably, 
with this meaning new methodological challenges and requiring new ways to 
transfer and formulate compositional knowledge
to meet the needs of diverse scientific fields.

Thus, this task view provides a curated collection of R packages aimed at 
supporting compositional data analysis, with the purpose of serving as guide 
for practitioners
interested in applying such methods. The packages can be broadly categorised 
into the following topics, although in fact many offer functionalities that 
span multiple categories:

### General purpose packages

This refers to packages that provide a general platform for compositional data 
analysis in R, implementing functions to conduct basic operations and 
calculations, log-ratio representations, 
data visualisation and some common statistical analyses. They, typically 
accompanying a published monograph, offer a platform compatible with the basic 
properties of compositional data to those approaching
the methodology from diverse domains. 

-   `r pkg("compositions", priority = "core")`: once the adequate class for the 
data is set, which corresponds
to the assumed underlying geometry (either compositional, `acomp` class, or 
multivariate positive data, `aplus` class), the package provides functions for 
their consistent analysis and modelling; including descriptive statistics, 
visualisation, statistical testing, and multivariate analysis (e.g. principal 
component analysis, clustering, MANOVA and regression). It supports the 
monograph 
[van den Boogaart and Tolosana-Delgado (2013)](https://link.springer.com/book/10.1007/978-3-642-36809-7) 
and allows to reproduce the analyses therein.

-   `r pkg("robCompositions", priority = "core")`: with a main focus on robust 
statistical methods, this package includes a wide range of tools for the 
manipulation and analysis of
compositional data within the log-ratio framework: transformations, dealings 
with irregular data, robust implementations of multivariate methods such as 
principal component analysis,
factor analysis and discriminant analysis, robust regression with compositional 
predictors, two-factorial compositions (compositional tables) and 
functional-compositional analysis of density data. 
The main reference monograph is 
[Filzmoser, Hron and Templ (2018) ](https://doi.org/10.1007/978-3-319-96422-5).

-   `r pkg("easyCODA", priority = "core")`: univariate and multivariate 
methods for compositional data analysis following the approach in 
[Greenacre (2018)](https://doi.org/10.1201/9780429455537), emphasising 
the use simple pairwise log-ratios. 
Particular features include procedures for selecting log-ratios that explain 
maximum log-ratio variance and conducting various multivariate analyses.

-   `r pkg("Compositional")`: regression, classification, contour plots, hypothesis 
testing and fitting of distributions for compositional data are some of the 
functions included in this package. Further some functions for percentages 
(or proportions) are included. The package deals, however, with compositional 
data mostly as with constrained data, thus avoiding the scale invariance 
property and, more generally, the principles of compositional data analysis 
characterizing the log-ratio approach 
(despite referring to the classical reference 
[Aitchison (1986)](https://doi.org/10.1002/bimj.4710300705)). This admits 
direct incorporation of zero components for the analysis, but leads to some 
conceptual inconsistencies with respect to the log-ratio approach. For these 
reasons, analyses run using this package may be incoherent with those run with 
the packages  `r pkg("composition", priority = "core")` or  
`r pkg("robCompositions", priority = "core")`.


### Compositional tables 

Compositional tables (i.e. ordinary contingency tables in their discrete version) represent frequencies or proportions structured across multiple categories. The compositional
nature of these tables, often constrained by row or column sums, requires specialised methods to analyse relationships, dependencies, and patterns while respecting their
relative nature. This section refers to packages implementing tools for their analysis, including log-ratio representation and selected multivariate methods.


-   `r pkg("robCompositions", priority = "core")`: log-ratio coordinate representation of compositional tables and methods for their statistical processing using principal component analysis and regression analysis with a real response and the compositional table as predictor.

<!-- -   `r pkg("lba")`: latent budget analysis for analysing two-way contingency tables with an exploratory and response variable, tailored for constant sum representation of compositional data. -->



### Density data analysis

Probability density functions are essentially scale invariant data objects which are commonly subject to a unit integral constraint. They can, therefore, be considered as
infinite dimensional compositional data and embedded into a Hilbert space, so-called a Bayes space. This section refers to packages implementing methods and tools for density data analysis
from this perspective.

Note that these methods differs from those included in the CRAN Task View on [CRAN Task View: Functional Data Analysis](https://cran.r-project.org/view=FunctionalData), 
in that they assume the Bayes space as sample space for density functions.

-   `r pkg("robCompositions", priority = "core")`: some methods for
representation of probability density functions using compositional smoothing splines, grounded on the theory of Bayes spaces.
Additionally, the package includes a functional version of the centered log-ratio transformation.

<!--
<span style="color: red;">
Comment from Matthias: what else? KH: I'm afraid that currently nothing. One can consider to add also the 'fdadensity' package from Petersen et al. but it could be quite misleading as it is based on another approach (mapping PDFs to(!) a Hilbert space). We therefore urgently need to build such a package.:-)
Alessandra: I agree with Karel. I'm wondering whether we should mention that after basis projection one could possibly resort to the 'fda' package for further processing - but this is not really ready-to-use, so work need to be done. In addition: should we include a reference to some work? It could be the paper on Bayes Hilbert spaces, or it could also be the entry on Bayes spaces in the encyclopedia.
</span>


<span style="color: red;">
Comment from KH: I removed the general section High dimensional data because there were only two packages and the package ccmm was very specific. I moved it to Other packages, where also a similar one purpose package CMMs is located.
</span>
-->

### Irregular data: zeros, censoring, missing and outliers

As with ordinary data sets, compositional data sets can be often affected by different issues in real-world applications, which might prevent for the immediate use of statistical methods and should be treated
in a data preprocessing stage. Of particular relevance for the application of the log-ratio methodology is the presence of zeros, which require careful handling to preserve the basic properties of the data and the
integrity of the subsequent analyses.

Traditionally, three types of zeros have been distinguished in the compositional data literature: _rounded zeros_, _count zeros_ and _essential zeros_. Briefly,
rounded zeros appear in continuous-valued compositions, and are commonly associated with small values that have been rounded off or have fallen below the detection limit of the
measuring device; count zeros refer to zeros that occurring in discrete compositions derived from a counting process, and are generally associated to limited sampling; and, finally,
essential zeros refer to genuine zero values, i.e. the case of parts of the composition that are truly absent. Rounded zeros is the case that has received the most attention in the literature
and represent a class of left-censored data.

Moreover, the presence of both missing values and outliers poses practical challenges, and a proper handling of them is required to
ensure consistency, validity and robustness of a compositional data analysis.

This section focuses on specialised packages including methods to address the above issues while respecting the compositional nature of the data.

-   `r pkg("zCompositions", priority = "core")`: integrated suite of data imputation methods applicable to zeros, nondetects, missing data, and combinations of them, following the
principles of the log-ratio approach as described in [Palarea-Albaladejo and Martín-Fernández (2015)](https://doi.org/10.1016/j.chemolab.2015.02.019). This includes a consistent treatment of closed and
non-closed compositions, unique or varying detection limits, parametric and nonparametric imputation, single and multiple imputation, maximum likelihood and robust estimation, as well as some tools for the exploration of zero patterns and statistical testing of grouping structure.

-   `r pkg("mvoutlier")`:	specific tools for visualising and identifying multivariate outliers in compositional data.

-   `r pkg("robCompositions", priority = "core")`: routines included to impute rounded zeros and missing data, as well as tools to detect outlying samples. 

-   `r pkg("compositions", priority = "core")`: routines included to detect, represent, and provide some analysis of irregular data, either missing values, zeros or outliers.



### Visualisation 

Visualisation is a crucial component of compositional data analysis, allowing researchers to explore patterns, relationships, and distributions within the constrained simplex geometry. This section includes
tools for creating ternary diagrams, biplots or pairwise log-ratio plots, among others. On top of overall visualisation functionality included in the general purpose packages above, some others particularly
devoted to such purpose are listed in the following.

-   `r pkg("ggtern")`: extends `ggplot2` to create ternary diagrams, supporting standard and 
additional custom geometries, including specialised ternary visualisations. 

-   `r pkg("Ternary")`: ternary diagrams and Holdridge life zone plots using base graphics. Features include custom annotation, interpolation, contouring, scaling, and a 
Shiny interface for interactive plotting.

-   `r pkg("isopleuros")`: tools for visualising data in ternary space, customising graphical elements, 
and displaying statistical summaries. Includes specialised diagrams for fields like archaeology (e.g., soil texture charts, ceramic phase diagrams).

-   `r pkg("provenance")`: tools for plotting compositional and count data on ternary diagrams and point-counting data on radial plots. Calculations of sample size required for specified levels of statistical precision,
and to assess the effects of hydraulic sorting on detrital compositions. Intuitive query-based user interface for users who are not proficient in R.

<!--
<span style="color: red;">
Comment from KH: I removed the robCompositions package from here so that it does not sound like overselling (and visualization tools are contained e.g. also in
compositions package), but I added a comment to description of the section. Javier: the same would apply to the previous section about
irregular data, particularly in relation to `compositions`. Some irregular data and also visualisation and also regression functionality (in relation
to the following section) are included in the general purpose packages, but should them be mentioned in all these specialised sections? I do not think so,
it can be just mentioned, as done in the first section, when they are described, and focus these sections in packages that are
specialised in a particular topic and have some distinctive feature. Alessandra: I agree with this strategy; however, should we say somewhere that the user can anyway also make reference to the basic packages although there are the specialized one? My idea would be that the user looking for a standard regression would first pass through the basic package and then through the advanced one.
</span>
-->

### Regression modelling

Specialised regression modelling with compositional data allows researchers to explore associations between compositions and other variables,
either acting as predictors/covariates or as response, and also between compositions on both sides of the regression model. Packages
specifically devoted to compositional regression analysis are listed in the following. It might be mentioned that `r pkg("complmrob")` and `r pkg("robregcc")` 
offering nothing essential beyond, e.g., `r pkg("robCompositional")`.
<!--
<span style="color: red;">
Javier: I have removed the subsequent text as I found it too redundant and referring to general things not specific of regression
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
any particular/special feature? Otherwise, from the current description it is not clear what they are offering
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


### High-dimensional compositional data: with applications to omics data

In recent years, compositional data analysis is having a notable impact on the omics sciences and bioinformatics, where types of data such as microbiome compositions, gene expression or metabolomic profiles
have been recognised as inherently compositional. Applications in this area require methods that address unique challenges, including high dimensionality, zero inflation, overdispersion or the integration of
phylogenetic information. This section highlights packages providing tools specifically designed for omics data, but certainly most of them could be equally considered for the statistical processing of
high-dimensional compositional data in general.  


-   `r pkg("FLORAL")`: log-ratio lasso regression for continuous, binary, and survival outcomes with compositional features as described in [Fei et al. (2023)](https://doi.org/10.1101/2023.05.02.538599).

-   `r pkg("BRACoD.R")`: Implements Bayesian regression to identify associations between 
microbiome compositional data and environmental variables. 
Corrects for compositional distortions by treating total abundance as an unknown variable. 
Integrates with Python via `reticulate`.

<!--
<span style="color: red;">
Comment from Matthias: Needs to be checked. KH: data are identified as compositional, but rather in sense of constrained data. Javier: it does not refer to any paper where the method is explained for more
details ... Not sure that this fits in.
</span>
-->

-   `r pkg("coda4microbiome")`: Provides tools for microbiome data analysis while accounting for its compositional nature. Includes penalised regression methods for variable selection in cross-sectional 
and longitudinal studies with binary or continuous outcomes.

-   `r pkg("codacore")`: identification of sparse log-ratios of a composition acting as predictor in regression problems. Scale-invariant log-ratios are derived optimised to account for
association with the response variable.

-   `r pkg("lnmCluster")`: logistic normal-multinomial clustering for microbiome compositional data, including extensions for factor analysis, bi-clustering, and sparse covariance estimation.

-   `r pkg("MicrobiomeStat")`: robust methods for analysing microbiome compositional data, addressing zero-inflation, phylogenetic structure, and compositional effects. 
Applicable to other high-dimensional compositional datasets from sequencing experiments.

-   `r pkg("QFASA")`: Implements quantitative fatty acid signature analysis to estimate predator diets, leveraging fatty acid diversity, biosynthesis limitations, and digestion properties in monogastric animals. Both methods for compositional and constrained data are used.



### Special applications in geostatistics and geochemistry

Compositional data analysis is integral to geostatistics and geochemistry, areas where the methodology found its early successful applications. Data sets here often represent proportions of elements,
minerals, or isotopes, and are subject to spatial dependencies. These applications require methods that respect the relative nature of compositions while addressing spatial structures and relationships. 
This section features packages which implement methods for specialised areas such as geostatistical modelling, spatial interpolation, variogram analysis, and compositional kriging; as well as techniques
for analysing geochemical compositions in the context of spatial data. In any case, some methods would be equally applicable to any data sets sharing analogous structures in any other application fields. 


-   `r pkg("provenance")`: statistical tools for sedimentary provenance analysis, 
including kernel density estimation, principal component analysis, correspondence analysis, and multidimensional scaling. Comparison of univariate proxies (e.g., single-grain ages, isotopic compositions) and 
categorical data are supported using distances like Kolmogorov-Smirnov, Wasserstein, Aitchison, and Bray-Curtis. Tools for visualising data on ternary and radial plots, calculating sample sizes, and 
assessing hydraulic sorting effects are included. Additionally, a user-friendly interface for non-R users is provided.

-   `r pkg("ArArRedux")`: data reduction and error propagation for 
Ar\(^\text{40}\)/Ar\(^\text{39}\) geochronology, processing isotopic compositions from noble 
gas mass spectrometer data. Methods for regression to $t=0$, blank and decay corrections, 
detector intercalibration, interference corrections, and age calculation. 
Argon isotope ratios are treated as compositional data for accurate statistical handling.

-   `r pkg("gmGeostats")`: geostatistical tools for multivariate data with restrictions, 
including compositions and positive amounts. Descriptive analysis and 
modelling using two-point Gaussian and multipoint perspectives. Compositional 
variograms and compositional kriging. <span style="color: red;">

-  `r pkg("compositions")`: includes a compositional variogram and kriging methods. <span style="color: red;">




### Other packages

<!--
Packages contained in this section are either of specific purpose or do not necessarily account 
for scale invariance of compositional data and consider them rather as constrained data.
Still methods contained in these packages can be useful in concrete applications, e.g. 
also for comparison to methods based on the log-ratio methodology.
-->

-   `r pkg("aIc")`: statistical tests for identifying compositional pathologies in datasets, 
including coherence of correlations, dominance of distance, perturbation invariance, 
and singularity of the covariation matrix. Supports multiple data transformations such as 
proportional, centred log-ratio (clr), and others from common R packages.

-   `r pkg("CMMs")`: compositional mediation models for continuous and binary outcomes, handling mediators represented as compositional data.

-   `r pkg("ccmm")`: compositional mediation models to estimate direct and indirect effects of a treatment on an outcome, designed for the case in which mediators are high-dimensional microbiome data.

-   `r pkg("coda.base")`: optimal implementation of friendly functions to compute log-ratio coordinate representations of various types,
including principal component and principal balance coordinates and coordinates from tailored orthonormal basis; as well as some basic compositional statistics.

-   `r pkg("countprop")`: model-based metrics of proportionality using the logit-normal multinomial model. It can also provide empirical and plugin estimates of these metrics. 

-   `r pkg("FlexDir")`: tools for using the flexible Dirichlet distribution, 
including maximum likelihood estimation via EM algorithm, variance-covariance matrix estimation, 
random data generation, and visualisation. Supports applications to compositional data.

<!--
-   `r pkg("SARP.compo")`: Offers tools for network-based interpretation of changes 
in compositional data, including computation of pairwise ratios, 
statistical testing between conditions, and network representation of results.
-->

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





### Links

-   [CRAN Task View: Functional Data Analysis](https://cran.r-project.org/view=FunctionalData)
-   [CRAN Task View: Bayesian](https://cran.r-project.org/view=Bayesian)
-   [CRAN Task View: Cluster](https://cran.r-project.org/view=Cluster)
-   [CRAN Task View: MachineLearning](https://cran.r-project.org/view=MachineLearning)
-   [CRAN Task View: Robust](https://cran.r-project.org/view=Robust)
-   [CRAN Task View: SpatioTemporal](https://cran.r-project.org/view=SpatioTemporal)

### References