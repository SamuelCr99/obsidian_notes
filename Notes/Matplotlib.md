20231101 - 08:38

Status: #idea

Tags:

# Matplotlib
A plotting library for drawing plots, histograms, scatter plots etc. 

Example creating a histogram. 
```Python
import pandas
import pandas.pyplot as plt
df = pandas.read_csv("GDP-2015.csv")
gdp = df["GDP per capita"]
plt.hist(gdp, bins=50)
plt.xlabel("GDP per capita")
plt.ylabel("Count")
plt.show()
```

Violon plot:

![[violin_plot.png]]

In scatter plots we usually plot 2-3 variables from a dataset using dots. Can reveal correlations between variables. 

Developing a visulization aesthetic. 
* Maximizing data-ink ratio 
* Minimizing the lie factor
* Minimizing chart junk
* Using proper scales and clear labeling 
* Making effective use of color
* Exploit the power of repetition

Be careful when drawing conclusions based statistics, plot the data to make sure that what we are looking at is indeed correct. Here is an example:

![[anscombes_quartet.png]]

\-\-\-
# References