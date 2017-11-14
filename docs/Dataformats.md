# Data Formats

The type of files involved in this package can be divided into two categories: input files and output file. The summary of different files are listed as

| Name       | Category           | Extension  | Description |
| ------------- |:-------------:|:-----:|-------------|
| Kernel distance matrix file      | Input | .csv | Csv file that contains the information of microbiome count and phylogenetic relationship|
| Kernel name list file      | Input | .csv | Csv file that contains the file names of the multiple kernel distance matrix files |
| Covariates file      | Input      |  .csv | Csv file that contains the values of covariates|
| Phenotype file | Input     |    .csv | Csv file that contains the values of phenotypes |
| Output file | Output     |    .out | Flat file that contains p-value for each group of OTUs under certain testing shceme|

# Kernel Distance Matrix file

UniFrac is a distance metric used for comparing biological communities. More information about the UniFrac distance is [here](https://en.wikipedia.org/wiki/UniFrac). UniFrac distance can be calculated using julia package [_PhylogeneticDistance.jl_](https://github.com/JingZhai63/PhylogeneticDistance.jl). Microbiome count file and phylogenetic tree file are needed. The distance matrix need be transformed to positive-definite kernel matrix. 


# Multiple Kernel Name List file
It's a csv file that contains the file names of the multiple kernel distance matrix to be tested.
```csv
"x"
```

# Covariates file

Covariates file is a csv file that contains the values of covariates. In covariates file, each line represents one measurement for one subject. The format of covariates file is: the first three fields is Subject ID, Measurement ID and Time Point, the rest fields are the covariates/predictors (e.g. sex, age, weight and etc). The intercept should NOT be included. Fields are separated by a comma. A typical covariates file look like

If a specific covariate value is missing, please use "NA" to indicate that missing value

If no covariates file is provided, the covariates matrix **X** will be automatically set to a _n_-by-1 matrix with all elements equal to 1, where n is the number of individuals.

```csv
"subjectID" "microbiomeID" "age" "sex" "smoker"
```

# Phenotype file

Phenotype file is a csv file that contains the values of phenotypes. In phenotype file, each line represents one measurement at one time point. One subject may have several repeated measurements. The format of phenotype file is the same as covariate file. The fields in phenotype file are

* Subject ID
* Measurement ID
* Time Point
* Phenotypes

```csv
"subjectID" "microbiomeID	" "y1" "y2" "y3" "y4" "y5"
```

# Output file

Output file is a flat file that contains p-values and other information for each phenotypes under certain testing scheme. In output file, each line represents for one phenotype in phenotypes file(the first line is the header).