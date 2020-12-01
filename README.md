# A3-hcds-hcc-bias
Assignment 3 for HCDS

## 1. Project Description
This is a assignment organised under the framework of FUB:HCDS course for the topic "Bias". 

The goal of this project is to determine prediction scores and to analyze them afterwards.

## 2. Project Structure
The project is structured in three parts:

### 2.1. Data Source
Two data sources in the project are used: (1) Wikipedia articles of politicians and (2) world population data.
Both of the original datasets can be found in data_raw folder.

(1) Wikipedia articles - The Wikipedia articles can be found [here](https://figshare.com/articles/Untitled_Item/5513449).  The file `page_data.csv` is the data source used in this project and can be found in data_raw folder.
This data inclused unnecessary entries and need to be processed.
This dataset is published by [Os Keyes](https://figshare.com/authors/Os_Keyes/660514) under license [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

(2) Population data - The preprocessed population data named export_2019.csv is provided by the instructor in the _data folder. The dataset is drawn from the world population datasheet published by the [PRB (Population Reference Bureu)](https://www.prb.org/international/indicator/population/table/). This dataset is also found in data_raw folder. This population data is being used directly without any processing.

### 2.2 Data Acquisition

Step 1. clean data base (filter out unwilling data entries)

>Unwilling entries (which include "Template" are not wikipedia articles) are filtered out.

Step 2. ORES request

> In the second step, the articles found on wikipedia page need to be rated by its quality through ORES ("Objective Revision Evaluation Service") API. This API is based on a machine learning system and will rate the articles into 6 different categories -- the two best of them are "FA" (featured article) and "GA" (good article). These two categories are relevant for our analysis.

Step 3. Assign quality assessment to each article 

>Each article (the original dataset are read as DataFrame and renamed into politician_data) is rated through ORES REST API  and given a quality catogory. Cleaned and processed database should contain essential information of each article (including country, revision_id, prediction etc.)

>The data is retrieved through multiple chunks, since the retrieval is taking a few hours. The result can be found in `data clean/chunks/`. These chunks are being used to create later on a single csv.

>Articles which cannot be processed are also extracted and stored in `result/countries_no_match.csv`.


### 2.3. Data Processing and Cleaning

> In this step, cleaned dataset are combined with population data and generates an complete dataset in `result/politician_by_country.csv`.

> The data contains following structure:

|article_name|country|region|revision_id|article_quality|    population|
|------------|:-----:|-----:|----------:|--------------:|---------:|
| xxxxxx | xxxxxxx | xxxx | xxxxxxxxx | xxx | xxx |


### 2.4. Data Analysis

>The aim of this project is to compare the number of articles (with/without good quality) in proportion to national/regional population. Therefore, 6 comparison tables are generated showing the results.

> They are: 
> Table 1&2: Top/Bottom 10 countries by coverage
> Table 3&4: Top/Bottom 10 countries by relative quality
> Table 5&6: Regions by coverage (total articles/good quality articles)

All 6 tables can be found in the notebook.

## 3. External Resource: ORES REST API endpoint 

The [ORES REST API](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model) contains three parameters project, redid and model ([Documentation](https://www.mediawiki.org/wiki/ORES#API_usage),[Usage](https://www.mediawiki.org/wiki/ORES#API_usage)). 

## 4. Notes for reproduction

### Prerequisites:
peotry for dependency management, Jupyter Notebook, Python 3.8

## 5. License

The project is licensed under [MIT.license](https://github.com/mvrcx/A3-hcds-hcc-bias/blob/main/LICENSE).






