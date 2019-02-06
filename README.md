## A look at US Government Shutdowns
## Introduction
We are in the midst of the 21st and the record-long US government shutdown. So we asked the question, why is there a government shutdown? We decided to dig a little deeper, and answer few questions that arose: <br>
-Does government unification play a role in government shutting down? <br>
-Historically, what happens to Presidents' Job Approval Ratings as they go in and exit out of a shutdown?<br>
-Similarly, What happens to Congressional Approval Ratings as the government exits a shut down?<br>
-Finally, What is the impact of a shutdown on the "economy" (Using S&P 500 stock Prices)?

## Getting The Data Ready

-**S&P 500 Historical Data**. Source: *Yahoo Finance*.[Link](https://finance.yahoo.com/quote/%5EGSPC/history?p=%5EGSPC) <br>
-**US Party Control 1933-2010** from Southeast Missouri State University. [Link](http://cstl-cla.semo.edu/rdrenka/ui320-75/presandcongress.asp) <br>
-**Shutdowns Dates and Lengths**. [Link](https://www.vox.com/policy-and-politics/2018/1/19/16905584/government-shutdown-history-clinton-obama-explained) <br>
-**Former Presidents' Approval Ratings**. Source: *The American Presidency Project*. [Link](https://www.presidency.ucsb.edu/statistics/data/presidential-job-approval) <br>
-**President Trump's Approval Ratings**. Source: *Gallup*. [Link](https://news.gallup.com/poll/203198/presidential-approval-ratings-donald-trump.aspx) <br>

## Data Cleanup
### S&P 500 Cleanup
The S&P 500 data we loaded covered daily openings and closings from the date of 1976-07-12 up until 2019-01-11. Only skipping, what we have assumed to be (holidays, weekends and/or other dates stock market was closed). 

However, we were only interested in the few days **ahead** of historical governemnt shutdowns and the few days **afterwards**, depending on the length of a shutdown and the availability of stock market data for those particular dates. <br>

Therefore a loop over both dataset is necessary to match the dates of interest. 


```
# csv of s&p 500 data from yahoo finance
filepath = "../Input/^GSPC.csv" 

# read stock csv
stock_prices_unclean = pd.read_csv(filepath)

# make the index the date to help with cleaning
stock_prices_unclean = stock_prices_unclean.set_index(['Date']

# print first 3 records of stock market dataframe
stock_prices_unclean.head(3)
```


| Date       | Open       | High       | Low        | Close      | Adj. Close |   Volume |
|------------|------------|------------|------------|------------|------------|---------:|
| 1976-07-12 | 104.980003 | 106.300003 | 104.739998 | 105.900002 | 105.900002 | 23750000 |
| 1976-07-13 | 105.900002 | 106.779999 | 105.150002 | 105.669998 | 105.669998 | 27550000 |
| 1976-07-14 | 105.669998 | 106.610001 | 105.050003 | 105.949997 | 105.949997 | 23840000 | 

----
----
As for the government shutdowns data would look something like this:

![Image description](file:///Users/ahmedacheikh/Desktop/shutdown_data.png)


  