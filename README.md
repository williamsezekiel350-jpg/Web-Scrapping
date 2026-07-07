# Web-Scrapping Project
## Project Description  This project is an automated web scraper designed to extract, clean, and structure financial data from public web resources. Specifically, it targets the **List of Largest Companies in Nigeria** from Wikipedia, extracting key business performance indicators such as company rank, revenue, profits, and industry sectors.   

import requests
from bs4 import BeautifulSoup

url = "https://en.wikipedia.org/wiki/List_of_largest_companies_in_Nigeria"

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
}

try:

    response = requests.get(url, headers=headers)

    
    if response.status_code == 200:
        
        soup = BeautifulSoup(response.text, 'html.parser')

        print(soup.prettify()[:2000])

    else:
        print(f"Failed to fetch page. Status Code: {response.status_code}")

except Exception as e:
    print(f"An error occurred: {e}")

#%%
soup.find_all('table')
#%%
soup.find_all('table')[0]
#%%
soup.find('table', class_ = 'wikitable sortable')
#%%
table = soup.find_all('table')[0]
#%%
print(table)
#%%
world_titles = table.find_all('th')
#%%
world_titles
#%%
world_table_titles = [title.text for title in world_titles]
print(world_table_titles)
#%%
world_table_titles = [title.text.strip() for title in world_titles]
print(world_table_titles)
#%%
import pandas as pd
#%%
df = pd.DataFrame(columns = world_table_titles)
df
#%%
Column_data = table.find_all('tr')
#%%
table = soup.find('table', class_='wikitable')

column_data = table.find_all('tr')[1:]

for row in column_data[0:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    print(individual_row_data)

    length = len(df)
    df.loc[length] = individual_row_data
#%%
df
#%%
df.to_csv(r'C:\Users\user pc\PycharmProjects\JupyterProject4\companies.csv', index=False)

#%%

#%%
