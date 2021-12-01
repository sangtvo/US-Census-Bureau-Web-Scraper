# US Census Bureau Web Scraper
> A python script that extracts web links from the _Population and Housing Unit Estimates_ web page of the U.S. Census Bureau and outputs those links in a CSV file in an absolute and non-duplicated format. 

Table of Contents
---
1. [General Information](#general-information)
2. [Summary](#summary)
3. [Tech Stack](#tech-stack)
4. [Code Examples](#code-examples)

<a name="https://github.com/sangtvo/US-Census-Bureau-Web-Scraper#general-information"/>
<a name="https://github.com/sangtvo/US-Census-Bureau-Web-Scraper#summary"/>
<a name="https://github.com/sangtvo/US-Census-Bureau-Web-Scraper#tech-stack"/>
<a name="https://github.com/sangtvo/US-Census-Bureau-Web-Scraper#code-examples"/>

General Information
---
A project on web scraping.

Summary
---
A web scraper is created by using Python and scraped 227 links from the [Population and Housing Unit Estimates web page](https://www.census.gov/programs-surveys/popest.html). In order to get only unique links, a for loop is created which resulted in 119 unique links.

Tech Stack
---
* Python
    * BeautifulSoup
    * csv
    * requests
* Jupyter Notebook
* Visual Studio Code 

Code Examples
---
```
r = requests.get("https://www.census.gov/programs-surveys/popest.html")
page = r.text
soup = BeautifulSoup(page, 'html.parser')
raw_links = soup.find_all("a", href = True)

myset = set()
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
    f.close()
```
There is a total of 227 URLs from the web page. An unordered and unindexed set is created called myset. The ```link.get(‘href’)``` function extracts all links contained within each identified href tag and goes through a for loop. For all relative links that starts with “/,” it is being concatenated with a domain website and added to the set. Otherwise, all unique links are added to the set and no duplicates are added. In total, there are 119 URLs in the set.

To see the full code, check out US Census Bureau Web Scraper.ipynb.
