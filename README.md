**Project Name: Wikipedia Web Scraper for Largest Companies in the United States**

---

## Description:

This Python script scrapes data from a Wikipedia page listing the largest companies in the United States by revenue. It utilizes the BeautifulSoup library for parsing HTML and the Requests library for making HTTP requests. The scraped data is then processed and stored in a Pandas DataFrame, which is subsequently saved as a CSV file.

## Installation:

To run this script, you need to have Python installed on your system. You can install the required libraries using pip:

```bash
pip install beautifulsoup4
pip install requests
pip install pandas
```

## Usage:

1. Import necessary libraries:

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```

2. Define the URL to scrape:

```python
url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
```

3. Send a GET request to the URL:

```python
page = requests.get(url)
```

4. Parse the HTML content:

```python
soup = BeautifulSoup(page.text, features="html.parser")
```

5. Find and extract data from the HTML elements:

```python
table = soup.find_all('table')[1]
world_titles = table.find_all('th')
world_table_titles = [title.text.strip() for title in world_titles]
column_data = table.find_all('tr')
```

6. Create a Pandas DataFrame and populate it with the extracted data:

```python
df = pd.DataFrame(columns=world_table_titles)
for row in column_data[1:]:
    row_data = row.find_all('td')
    individ_row_data = [data.text.strip() for data in row_data]
    length = len(df)
    df.loc[length] = individ_row_data
```

7. Save the DataFrame as a CSV file:

```python
df.to_csv(r'path/to/save/companies_by_revenue.csv', index=False)
```

## Example:

Here's a brief example of how to use the script:

```python
# Run the script
python wiki_scraper.py
```

## Contributors:

- William Hellems-Moody
