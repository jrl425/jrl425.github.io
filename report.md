# Report File

## Summary

The question that I had entering this project was whether or not 10k’s contain any value-relevant information in the sentiment of the text. I wanted to understand if certain negative or positive words or specific topics talked about in the 10k’s could lead to any significant stock return in a number of different return windows. I began by using a list of all of the S&P 500 companies to download each company’s 10k from SEC Edgar.  Next, the process involved organizing these files within a zip folder, parsing their titles, and opening each to extract data like CIK and Accession No.. This data extraction enabled me to programmatically navigate and scrape information from 500 SEC filing  webpages to locate the filing dates. I then downloaded historical stock return data, allowing me to correlate these filing dates with corresponding stock returns, as well as examining stock performance over a specified window around these dates. A key aspect of the project was conducting sentiment analysis on the 10-K filings, where I created sentiment lists from provided files. Using these lists, I analyzed the filings to calculate the underlying sentiment, trying to join quantitative data with qualitative insights to uncover the impact of corporate sentiment on stock performance.

Unfortunately, I struggled with merging my outputs and I was unable to calculate the actual correlation or causation between sentiment and stock returns. This was most likely due to the format of my outputs. I was able to calculate the returns for Version 1, 2 and 3 and the sentiment scores for all 10 variables. 


## Data

### What’s the sample?
In this project, the sample was the list of 2022 S&P 500 Stocks and this came from Wikipedia. The other part of my sample was the CRSP 2022 Stock returns dataset, which only contains stock returns on days the market was open. 


### How are the return variables built and modified? 
- Version 1, I went for a simple approach and used a merge because I had all of the data in the two data frames that I needed in order to satisfy version 1. I merged left on symbol and filing date and right on ticker and date.
- 
For Version 2,  I initialized results_df by extracting the 'Symbol', 'CIK', and 'Filing Date' columns from merged_df . Then, I iterated over each row in results_df, using a loop to search stock_rets for stock returns that matched each company's ticker symbol and filing date, extending to two days post-filing to capture a short-term return window. In cases where matching return data was found, I inserted these values into newly created columns within results_df. Then, I calculated the cumulative returns for the period from the filing date to two days after. Last, I refined results_df to only include essential columns—'Symbol', 'CIK', 'Filing Date', and the newly computed 'Cumulative Return t to t+2'
.- 
Version 3 was much simpler because I already built a very strong foundation in V2. For Version 3, I practically used the same code from2V@, but this time I edited the range to start at day 3 and end at day 10. For this, I used the range (3, 11), as 3 is inclusive and 11 is exclusive. After this, I needed to change the newly computed result to ‘Cumulative Return t to t+2.’


### How are the sentiment variables are built and modified?

- I began with creating the list of words from the ML and LM files. I followed the guideline from the build sample file posted in the midterm sandbox. For the ML negative words, I first created a variable for the file path. I then created a dataframe from reading this csv file and named this column ‘BHR_Negative_Word. Next, I switched this df to a list and named it ‘BHR_negative. 
I did the same steps for ML Positiv
- 
For LM Negative,  I first loaded the Dictionary from a CSV file into a DataFrame called df using pandas' read_csv function. Then, I filtered this DataFrame to include only the words categorized as negative, identified by the 'Negative' column not being equal to 0, and I stored the result in filtered_df. Last, I converted all of the words in the 'Word' column of filtered_df to lowercase and converted them into a list named  ‘LM_negative ’
I did the same steps for LM Positi- ve
To measure the sentiment of the first four lists of words I first opened the zip file containing the 10-K HTML documents and filtered out the primary document files for analysis. Then, I iterated through each, using BeautifulSoup to parse the HTML content and clean it by removing hidden div elements, converting it to lowercase, and removing non-word characters and excess whitespace. In each document, I calculated the total word count and then analyzed the text against my predefined sentiment word sets (BHR_negative, BHR_positive, LM_negative, LM_positive). I then computed the frequency of sentiment words as a fraction of the total word count. Last, I added these results into the data frame ‘sent_an’, which includes the CIK, word set label, and sentiment score for each document.


### Why did you choose the three topics you did for the “contextual sentiment” measures?

I chose these three topics because I believe that they can be very controversial and deterministic topics in a 10k filing report. For the most part, these words are unique enough that they will not be mentioned aggressively, but they should be at least mentioned in most of the 10k’s. 

### Do your “contextual sentiment” measures pass some basic smell tests?


### Do you have variation in the measures (i.e a variable is not all the same value)?


One observation that I had is that BHR_positive has 75 words while BHR_negative has 94 words. This is not extremely significant. 
However, LM positive has 354 words, while LM negative has 2355 words. This is significant and could be a reason why 10k’s have a stronger negative score than positive score. 


## Results


```python

```

## Disclaimer

### I copied and pasted the words in this file from a google doc and there were some formatting errors that I just could not figure out. I apologize for those errors


