# umiAnalyzer 1.0.0

Tools for analyzing sequencing data containing unique
molecular identifiers generated by UMIErrorCorrect 
(<https://github.com/stahlberggroup/umierrorcorrect>). The package 
allows merging of multiple samples into a single UMIexperiment object which 
can be easily manipulated using build-in functions to generate tabular and
graphical output. The package includes a shiny app with a graphical
user interface for data exploration and generating plots and report
documents.

This README serves as a basic introduction, for more detailed information and examples read
the wiki pages on GitHub (<https://github.com/sfilges/umiAnalyzer/wiki>) or
the R vignette using:

```r
browseVignettes('umiAnalyzer')
```

For a version history/changelog, please see the [NEWS](https://github.com/sfilges/umiAnalyzer/blob/master/NEWS.md) file.

Requirements
------------

- R (>= 4.1.0), which can be downloaded and installed via The Comprehensive R Archive Network [CRAN](https://cran.r-project.org/).
- Installation from R using install_github requires the devtools package

Installation 
------------

Install the current stable version from CRAN or GitHub or the latest
development version from GitHub.

```r
# from CRAN (not supported yet)
#install.packages('umiAnalyzer')

# Current stable version from github using the devtools package:
devtools::install_github('sfilges/umiAnalyzer')

# Latest development version from github:
devtools::install_github('sfilges/umiAnalyzer', ref = 'devel')
```

Running the visualization app
------------

Run the following command in the R console to start the app:

```r
umiAnalyzer::runUmiVisualizer()
```

# Using the R package in your own scripts

How to make build your own UMIexperiment object
---------------------

Define a variable containing the path to the directory with all the UMIErrorCorrect 
output folders belonging to your experiment. umiAnalyzer comes with raw test data 
generated with UMIErrorCorrect that you can import if you don't have any of your own.

Call the createUmiExperiment to create your UMIexperiment object.

The UMIexperiment object always maintains your raw data, however you can create 
as many filters as you like, which will be saved as separate objects to access. 
You can filter the consensus table of UMIexperiment object with filterUMIobject. 
The only mandatory arguments are the object to be filtered and a user defined name. 
You can use that name to retrieve a filtered table using getFilter. 

```r
library(umiAnalyzer)

main <- system.file('extdata', package = 'umiAnalyzer')

simsen <- createUmiExperiment(main)

reads <- parseBamFiles(main, consDepth = 10)

plotFamilyHistogram(reads)

simsen <- generateQCplots(simsen)

simsen <- filterUmiObject(simsen)

myfilter <- getFilteredData(simsen)
myfilter

simsen <- generateAmpliconPlots(simsen)
```