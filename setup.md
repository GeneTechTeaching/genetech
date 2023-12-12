# Setup

This is some instructions for TAs how to setup the labs on Posit Cloud.

## 1. Setup a new Workspace

Click "+ New Space" in the pannel to right. A popup should appear where you can fill in the name and specify which project to create it under. This should be the same project you ordered for the course. 

## 2. Invite TAs to the workspace

In the workspace overview, select the Members tab and click the "Add Member" button. Add all TAs with the appropriate roles, usually "Admin" or "Moderator". 

## 3. Setup RStudio project

Create a new Posit Cloud project in your by clicking `New Project` -> `New RStudio Project`. 

Adjust the resources for the project to set the allocated RAM memory to 6GB. This can be done by clicking the :gear: (gear) icon in the upper right corner, then select the "Resources" tab and change the allocation there.

Also change the access for the project. This can be done by clicking the :gear: (gear) icon in the upper right corner, then select the "Access" tab and change the "GENERAL ACCESS" to "Space Members" and select "Make this project an assignment". 

## 4. Add course material

In the terminal, go to the `/cloud/project` dir and clone the Github repo for the course

```bash
cd /cloud/project
git clone https://github.com/GeneTechTeaching/genetech.git
```

This will create a folder `/cloud/project/genetech`.

```bash
cd genetech
```

It should containing all the required material ... but actually two files are missing. The files for ex3 `labs/ex3/data/bc` and `labs/ex3/data/se` are to large to store on Github so they need to be added separately. They are posted in the TA slack for now, search for "scRNAseq_extra_files.zip". Maybe we need a more permanent solution for this.

## 5. Install required packages

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
Seurat # Version must be <5 for STutility to work
STutility
SummarizedExperiment
viridis # CD2040 only
```

Most can be installed directly using:

```r
install.packages(c("RColorBrewer", "Seurat", "dplyr", "ggplot2", "gprofiler2", "magrittr", "pheatmap", "rjson"))
```

For Seurat we will specify version 4.4 as 5 does not work with STutility. We also need a specific version of SeuratObject. 

```r
packageurl <- "https://cran.r-project.org/src/contrib/Archive/Seurat/Seurat_4.4.0.tar.gz"
install.packages(packageurl, repos=NULL, type="source")
packageurl2 <- "https://cran.r-project.org/src/contrib/Archive/SeuratObject/SeuratObject_4.1.4.tar.gz"
install.packages(packageurl2, repos=NULL, type="source")
```

For CD2040 you also need to install these packages for the bulk RNA-seq lab

```r
install.packages(c("R.utils", "viridis"))
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("DESeq2")
```

To install `STUtility` see: https://github.com/jbergenstrahle/STUtility#installation or run

```r
install.packages("remotes")
remotes::install_github("jbergenstrahle/STUtility")
```

To install `SummarizedExperiment` and `airway` run:

```r
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install(c("SummarizedExperiment", "airway"))
```

## 6. Test the labs

Testrun all labs to check that all the checks pass and that they Rmarkdown files are able to be knitted. 

Remember to remove any solutions added to the `main.Rmd` files and any knitted files e.g. `main.html` once you are done. You can use the code below 

```bash
cd /cloud/project/genetech
git restore labs/*/main.Rmd
rm -i labs/*/main.html
```

## 7. Invite students to Workspace

In the workspace overview, select the Members tab and click the "Add Member" button. Add all students with the appropriate role, usually "Contributor". 
