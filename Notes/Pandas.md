20231101 - 08:29

Status: #idea

Tags: [[Python]]

# Pandas
Provides data structures for working with data. 

Series: 1D, labelled, homogeneously-typed array. 
DataFrame: General 2D, labelled, size-mutable tabular structure with potentially hetrogeneously-types columns. 

CSV, comma-separated values is a common way of storing data. 
![[gdp_csv.png]]

``` Python
import pandas
df = pandas.read_csv("GDP-2015.csv")
gdp = df['GDP per capita']
```

pandas.DataFrame.descibe()
* Summarizes the central tendency, dispersion and shape of a dataset's distribution.
* Analyzes both numberic and object series, as well as DataFrame column sets of mixed data types. 
* The output will vary depending on what is provided.


\-\-\-
# References