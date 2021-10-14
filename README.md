# Data 512 Assignment 2 


This project is to analyze Wikipedia articles on political figures from countries in the world, including the ratio of total number of relavent articles to the country's population and relative proportion of high quality articles.

### Data Sources
Two data sources (provided in .csv format in this repo) used in this project are:
* page_data.csv
  * [Wikipedia politicians by country dataset](https://figshare.com/articles/dataset/Untitled_Item/5513449)
  * The data contains most English-language Wikipedia articles within the category "Category: Politicians by nationality" and subcategories, along with the code used to generate that data. "country" column indicates the country of the politician; "page" column indicates the title of that Wikipedia page; and "rev_id" is the edit ID of the last edit to the page.
* WPDS_2020_data.csv
  * [World Population Data sheet](https://www.prb.org/international/indicator/population/table/)
  * The data is published by the Population Reference Bureau. It contains the population of all the countries as in 2019 and also provides regional information. "Name" column provides the name of the country or the region ("FIP" column is the short for the country's name); "Type" column indicates if the entry is a country or a region (countries belong to a specific region is ordered after the row for that region); "TimeFrame" is set to be 2019 to specify the population record in the year os 2019; "Population" column provides the total population for that country or region and the "Data(M)" column is the population in million.

Additionally, the article quality estimation is generated using the [ORES REST API](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model) based on the revision ID (rev_id) and the model is set to be "articlequality".

### Output files 
Two csv files are generated by this poject:
* wp_wpds_politicians_by_country.csv
  * It contains all articles analyzed in this project and its corresponding country and population, and their predicted quality score.
* wp_wpds_countries-no_match.csv
  * It contains rows from either page_data.csv or WPDS_2020_data.csv that does not have a matching recording in another. 

### Reflection

This project is a good practice for me to learn more about data cleaning process in data science, since the WPDS data comes in a format that the hierarchical relationship between countries and regions are indicated by ordering of the rows. 
One thing I found surprising to me is that the total number of article count for Europe, which is 14,444 is over twice of the article counts for all America (Northern America, South America, and Latin America and the Caribean), which is 6,818. The number for America is also much lower than in Asia. Another interesting finding is that for the bottom 10 countries ranked by coverage (article count per population), most of them are countries with large populations in Asia. 

1. What (potential) sources of bias did you discover in the course of your data processing and analysis?

There are two potential biases in this analysis. First is the bias involved in creating the article quality estimation. How the REST API generates the quality estimation is unclear and the data is used to train the model is also unclear. If the model is only trained on articles from a certain region or a certain subject, it might not produce an accurate estimation for the articles included in this project. The second bias is the project only focuses on the English Wikipedia page, but for most of the countries, its official language is not English so there can be articles on politicians in those countries but not included in this project. 


2. What might your results suggest about (English) Wikipedia as a data source?

The results do provide some confirmation of the second bias mentioned earlier. When looking at the table for ranking of geographic regions in terms of the relative quality, Northern America has a much greater ratio of high-quality articles per article, following by Asia, Europe, and Oceania. Given that the two major countries in Northern America are the USA and Canada, and the official language for both countries is English, this result might suggest some biases in the data source. 

![image](https://user-images.githubusercontent.com/33292688/137208609-4d049b5a-78bb-4a3f-b7b1-69e6c46a14c9.png)


3. Can you think of a realistic data science research situation where using these data (to train a model, perform hypothesis-driven research, or make business decisions) might still be appropriate and useful, despite its inherent limitations and biases?

I think these data can be biases or misleading when trying to create an analysis for all the countries in the world, including both English-speaking and non-English-speaking countries. Since it is less likely for non-English-speaking countries to have a full list of articles on their politicians translated to English. Meanwhile, these data can be useful if the analysis is only focused on a specific region (Northern America) or only English-speaking countries. 

