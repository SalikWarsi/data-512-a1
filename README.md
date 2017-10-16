# data-512-a1
Assignment 1 template. See: https://wiki.communitydata.cc/HCDS_(Fall_2017)/Assignments#A1:_Data_curation

# English Wikipedia page views, 2008 - 2017

The aim of the project is to count the page views for english wikipedia, total as well as split by web and mobile.

## Data Source
We use wikipedia APIs to get page views from July 2008 to September 2017. 
1. The legacy PageCounts API provides desktop and mobile data from January 2008 till July 2016 : [Legacy PageCounts API](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts). This data icludes web crawler traffic. Mobile data is only included from October 2014. [Documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts)
2. The PageViews API provides desktop, mobile web, and mobile app traffic data from July 2015 through September 2017.  : [PageView API](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews) This new API lets us filter out web spiders and crawlers. [Documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews)

I used API Version 1.0 to get this data

[Terms for use for WikiMedia](https://wikimediafoundation.org/wiki/Terms_of_Use/en)

Wikimedia licensed under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/)

## Data Acquisition
We call the PageCounts API twice (once for desktop and once for mobile) and the PageViews API thrice (for desktop, mobile web and mobile app) and write each data in JSON file. For PageViews API we filter out web crawler traffic by passing user-agent = user. This is why we later see that there is a drop in total page visits between the 2 APIs. 

All data is collected at monthly granularity.

The JSON files are as follows:
1. pagecounts_desktop-site_200801-201607.json: Desktop page counts (legacy) from January 2008 to July 2016
2. pagecounts_mobile-site_200801-201607.json: Mobile site page counts (legacy) from January 2008 to July 2016. Note mobile data is only available from October 2014
3. pageviews_desktop_201507-201709.json: Desktop Page Views from July 2015 to September 2017
4. pageviews_mobile-web_201507-201709.json: Mobile Web Page Views from July 2015 to September 2017
5. pageviews_mobile-app_201507-201709.json: Mobile App Page Views from July 2015 to September 2017

## Data Processing
We process the data from all 5 and combine it into a csv file: en-wikipedia_traffic_200801-201709.csv . For both PageCounts(Legacy) and Page Views we count total Page Views and for PageView we also combine the Mobile web and Mobile App data to calculate total mobile page views.
The CSV file has the following Columns:

| Column                  | Values                                 |
|-------------------------|----------------------------------------|
| year                    | YYYY                                   |
| month                   | mm                                     |
| pagecount_all_views     | Total Views from PageCount API         |
| pagecount_desktop_views | Total Desktop Views from PageCount API |
| pagecount_mobile_views  | Total Mobile Views from PageCount API  |
| pageview_all_views      | Total Views from PageView API          |
| pageview_desktop_views  | Total Desktop Views from PageView API  |
| pageview_mobile_views   | Total Mobile Views from PageView API   |

Note: If data doesn't exist for a particular date, I replaced it with 0

## Data Analysis

I read from the CSV and plot the values using Matplotlib. The jupyter notebook contains an inline image and also produces a png file: PageViewsWikipediaEn.png

## Tools
The entire analysis was done using Python 3.5.3 :: Anaconda custom (64-bit)

Libraries used:
1. requests
2. json
3. pandas
4. matplotlib.pyplot