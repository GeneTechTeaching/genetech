# Setup

This is some instructions for TAs how to setup the labs on Posit Cloud.

## Install required packages

**Packages required**

``` 
airway
DESeq2 # CD2040 only
dplyr
ggplot2
gprofiler2
magrittr
pheatmap
R.utils # CD2040 only
RColorBrewer
rjson
Seurat
STutility
SummarizedExperiment
```

Most can be installed directly using:

```{r}
install.packages(c("RColorBrewer", "Seurat", "dplyr", "ggplot2", "gprofiler2", "magrittr", "pheatmap", "rjson"))
```

For CD2040 you also need to install these packages for the bulk RNA-seq lab

```{r}
install.packages(c("DESeq2", "R.utils",))
```

To install `STUtility` see: https://github.com/jbergenstrahle/STUtility#installation or run

```{r}
install.packages("remotes")
remotes::install_github("jbergenstrahle/STUtility")
```

To install `SummarizedExperiment` and `airway` run:

```{r}
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install(c("SummarizedExperiment", "airway"))
```
