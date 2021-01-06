# Project 05: US Census Bureau Web Scraper
> A python script that extracts web links from the _Population and Housing Unit Estimates_ web page of the U.S. Census Bureau and outputs those links in a CSV file in an absolute and non-duplicated format. 

General Information
---
The project is part of a graduate course (_Programming in Python_) at Western Governor's University. 

Summary
---
A web scraper is created by using Python and scraped 227 links from the [Population and Housing Unit Estimates web page](https://www.census.gov/programs-surveys/popest.html). In order to get only unique links, a for loop is created which resulted in 119 unique links.

Tech Stack
---
* Python (requests, csv, BeautifulSoup)

Code
---
```myset = set()
for link in raw_links:
    hrefs = link.get('href')
    if hrefs.startswith('None'):
        continue
    elif hrefs.startswith('#'):
        continue
    elif hrefs.startswith('/'):
        myset.add('https://www.census.gov' + hrefs)
    else:
        myset.add(hrefs)

print('Total URLs in myset: ', len(myset))

with open('links.csv', 'w') as f:
    writer = csv.writer(f)
    for links in myset:
        writer.writerow([links])
    f.close()```
