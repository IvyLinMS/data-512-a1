# data-512-a1

This is our first project of Data512 Human-Centered Data Science. Our goal is to construct, analyze, and publish a dataset of monthly traffic on English Wikipedia from January 2008 through August 2021. All analysis are performed in a single Jupyter notebook, named hcds-a1-data-curation.ipynb.

# Data source:
Wikipedia traffic from 2008-2021

# Data acquisition:
+ Wikimedia Foundation REST API terms of use: https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions
+ The Legacy Pagecounts API (https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts) provides access to desktop and mobile traffic data from December 2007 through July 2016.
+ The Pageviews API (https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month.

5 Data files we get:
+ pagecounts_desktop_file = 'pagecounts_desktop-site_200712-202108.json'
+ pagecounts_mobile_file = 'pagecounts_mobile-site_200712-202108.json'
+ pageview_desktop_file = 'pageviews_desktop_200712-202108.json'
+ pageview_mobile_app_file = 'pageviews_mobile-app_200712-202108.json'
+ pageview_mobile_web_file = 'pageviews_mobile-web_200712-202108.json'

# Data processing:
+ Load data from json file into a data frame and do extra process for combination
   + For legacy page count API data, keep 'access-site', 'timestamp', 'count' column, rename access-site and count column name to make it consistent with page view API data, also update the access type with expected name
   + For page view API data, keep 'access', 'timestamp', 'views' column, update the access type with expected name
   
+ Sum the two mobile app and mobile web data from page view API into a single acess type pageview_mobile_views
+ Combine all data frame into a single data frame
+ Pivot the combined data to make different access type has separate column
+ Replace not available data with 0
+ Extra year and month column from timestamp column
+ Create pagecount_all_views and pageview_all_views by sum the desktop view and mobile view from pagecount and pageview API respectively
+ Reorder the data frame and save to final CSV output 'en-wikipedia_traffic_200712-202108.csv'
+ Final data file includes the fields: 'year','month','pagecount_all_views', 'pagecount_desktop_views', 'pagecount_mobile_views', 'pageview_all_views', 'pageview_desktop_views','pageview_mobile_views

# Data analysis:
Based on the final data csv file from previous step, I plotted the graph using Seaborn Lineplot, the 6 lines display the trending by 'PageCount - All traffic', 'PageCount - Desktop traffic', 'PageCount - Mobile traffic', 'PageView - All traffic', 'PageView - Desktop traffic', and 'PageView - Mobile traffic'.

# Observation:
As we can see from the graph, PageView - Destop traffic is going down in the trending, PageView - Mobile traffic keeps going up in the trending, then the overall traffic PageView stays almost the same since July 2015, with a Spike between 2020-03 to 2020-06. 

# Known issues:
+ The Legacy Pagecounts API provides traffic data from December 2007 through July 2016, then the Pageviews API provides data to desktop, mobile web, and mobile app traffic data from July 2015 through last month.
+ Pageview API excludes spiders/crawlers, while data from the Pagecounts API does not.

