# ALLC

# Natural Gas Prices Data Processing and Web Scraping

## Overview

This project involves two main tasks:

1. **Daily Data Processing**: Downloading, processing, and saving natural gas price data from an Excel file provided by the EIA (U.S. Energy Information Administration).
2. **Monthly Data Scraping**: Scraping natural gas price data from a webpage and saving it to a CSV file.

## Libraries Used

- **pandas**: For data manipulation and analysis, including reading Excel files and HTML tables.
- **requests**: For downloading files from a URL.
- **beautifulsoup4**: For parsing HTML and extracting data when necessary.
- **lxml**: For parsing HTML content with BeautifulSoup.

## Daily Data Processing

### Step-by-Step Process

1. **Download the Excel File**:
   - The script uses the `requests` library to download the Excel file from the specified URL.
   - The file is saved locally as `natural_gas_prices.xlsx`.

2. **Read and Process the Excel File**:
   - The script reads the downloaded Excel file using `pandas`.
   - The `sheet_name` parameter specifies which sheet to read, and `skiprows=2` skips the header rows that are not needed.
   - Columns are renamed to `['Date', 'Price']`.
   - The `Date` column is converted to a datetime format for consistency.
   - Any rows with missing data are removed using `dropna()`.

3. **Save Data to CSV**:
   - The cleaned data is saved as a CSV file named `henry_hub_prices.csv` using `pandas`.

### Challenges Faced

- **Library Compatibility**:
  - Initially, there was an issue with the version of the `xlrd` library required by `pandas`. This was resolved by upgrading `xlrd` to version 2.0.1 or newer.

- **Dynamic Content and Table Extraction**:
  - The original plan involved web scraping, but the table data was not found. This led to a shift to directly downloading the Excel file, simplifying the process but requiring handling data extraction and cleaning in a different format.

- **Data Cleaning**:
  - Ensuring consistent date format and handling missing data required careful attention to avoid errors during the conversion process.

## Monthly Data Scraping

### Step-by-Step Process

1. **Send HTTP Request**:
   - The script uses the `requests` library to send a GET request to the target URL to retrieve the webpage content.

2. **Parse HTML Content**:
   - **Initial Parsing with Pandas**: The script attempts to use `pandas.read_html()` to extract tables directly from the HTML content. If tables are found, it prints the first few rows to help identify the correct table based on headers.
   - **Fallback Parsing with BeautifulSoup**: If Pandas fails to extract the correct table, the script uses `BeautifulSoup` to manually locate and parse the desired table.

3. **Extract Tables**:
   - **Using Pandas**:
     - Extract tables from the HTML content.
     - Inspect the first few rows of each table.
     - Identify and return the table with relevant headers (e.g., "Year").
   - **Using BeautifulSoup**:
     - Locate the table element in the HTML.
     - Extract data from rows and columns, clean the data, and convert it into a DataFrame.

4. **Clean and Save Data**:
   - Perform necessary data cleaning (e.g., removing missing or irrelevant rows).
   - Save the cleaned DataFrame to a CSV file using `pandas.to_csv()`.

### Challenges Faced

- **Identifying the Correct Table**:
  - The webpage's structure may vary, requiring careful inspection to ensure the correct table is identified and extracted.

- **Handling Different HTML Structures**:
  - Variations in HTML structure can complicate data extraction, necessitating adjustments in the parsing logic.

- **Data Cleaning**:
  - Post-extraction data often requires cleaning and formatting to ensure it is usable and accurate.

- **Error Handling**:
  - Robust error handling is essential to manage issues such as failed table extraction or changes in the webpage structure.

## Installation

Ensure you have the required libraries installed:

```bash
pip install requests pandas beautifulsoup4 lxml
