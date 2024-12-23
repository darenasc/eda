# Exploratory Data Analysis

- 12.10.2024. Slides CorrelCon 2024 available [here](https://docs.google.com/presentation/d/18An6Y9cGu1lSO2enbFsOwY-xxaPBPh12tw7MJAZluOk/edit?usp=sharing).
- 11.12.2023. Slides DataKindUK SDS available [here](https://docs.google.com/presentation/d/1KWrMbF5Q-gffoc5sXn0B31lyiACdFHiiPWay0MI5Vdw/edit?usp=sharing).
- 11.11.2023. Slides CorrelCon 2023 available [here](https://docs.google.com/presentation/d/1mYtzt5Tfk_xbYSWUBRgiNH5TumJNUWlRVDMeyntee_w/edit?usp=sharing).

## How to use this repository

You can clone this repository and use it locally as follows.

```bash
git clone https://github.com/darenasc/eda.git
cd eda
pip install pipenv
pipenv install Pipfile
```

Or you can go to the [eda.ipynb](notebooks/eda_dkuk_sds.ipynb) notebook and open it in Colab.

# EDA Mindmap

Mindmap created with [freeplane](https://docs.freeplane.org).
![](eda.png)

# Linux commands
Some useful commands for the terminal.

```bash
# Explore directories
ls
# Explore content of files
cat
more
less
head
tail 
# Count number of lines
wc -l
# Search in files
grep
# Get documentation of commands
man
# Download data or files
wget
curl
# Monitor resources
htop
btop
# Modify files
vim
sed
```

# Python libraries

Some python libraries to explore data.

- [pandas](https://github.com/pandas-dev/pandas)
- [ydata-profiling](https://github.com/ydataai/ydata-profiling) (former pandas-profiling)
- [sweetviz](https://github.com/fbdesignpro/sweetviz)
- [pygwalker](https://github.com/Kanaries/pygwalker)
- [facets](https://github.com/pair-code/facets)
- [datapane](https://github.com/datapane/datapane)
- [streamlit](https://github.com/streamlit/streamlit)
- [gradio](https://github.com/gradio-app/gradio)
- [geopandas](https://github.com/geopandas/geopandas)
- [pysal](https://github.com/pysal/pysal)
- [networkx](https://github.com/networkx/networkx)
- [word_cloud](https://github.com/amueller/word_cloud)
- [great_expectations](https://github.com/great-expectations/great_expectations)
- [featuretools](https://github.com/alteryx/featuretools)
- [superset](https://github.com/apache/superset)
- [metabase](https://github.com/metabase/metabase)
- [openml-python](https://github.com/openml/openml-python)

# EDA Checklist

- What are the formats?
- Are there files with problems? (can't be opened)
- How many files, tables, databases?
- Per item: How many columns and rows?
- Are there any encoding issues?
- Verify data types of columns: Discrete, Continuous, Dates, GIS, network, other.
- Univariate analysis
  - Histogram
  - Bar plot
  - Boxplot
- Multivariate analysis
  - Correlations
  - Use target variable to visualize other features