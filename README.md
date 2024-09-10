# ALLC

# Natural Gas Prices Data Processing

This project involves downloading, processing, and saving natural gas price data from the EIA (U.S. Energy Information Administration). The data is initially provided in an Excel file format and is processed to be saved as a CSV file.

## Libraries Used

- `pandas`: For data manipulation and analysis.
- `requests`: For downloading files from a URL.
   `BeautifulSoup`: For web scraping files from a URL. 

## Step-by-Step Process

1. **Download the Excel File**:
   - The script uses the `requests` library to download the Excel file from the specified URL.
   - The file is saved locally as `natural_gas_prices.xlsx`.

2. **Read and Process the Excel File**:
   - The script reads the downloaded Excel file using `pandas`.
   - The `sheet_name` parameter specifies which sheet to read, and `skiprows=2` skips the header rows that are not needed.
   - The columns are renamed to `['Date', 'Price']`.
   - The `Date` column is converted to a `datetime` format for consistency.
   - Any rows with missing data are removed using `dropna()`.

3. **Save Data to CSV**:
   - The cleaned data is saved as a CSV file named `henry_hub_prices.csv` using `pandas`.

4. **Run the Script**:
   - Execute the script using Python. The script will automatically download the data, process it, and save it as a CSV file.

## Challenges Faced

- **Library Compatibility**:
  - Initially, there was an issue with the version of the `xlrd` library, which is required by `pandas` to read Excel files. This was resolved by upgrading `xlrd` to version 2.0.1 or newer.

- **Dynamic Content and Table Extraction**:
  - The original plan involved web scraping, but the table data was not found. This led to a shift to directly downloading the Excel file, which simplified the process but required handling data extraction and cleaning in a different format.

- **Data Cleaning**:
  - Ensuring that the date format is consistent and handling missing data required careful attention to avoid errors during the conversion process.

## Running the Script

To run the script, follow these steps:

1. Ensure you have Python installed on your machine.
2. Install the required libraries using pip:

   ```bash
   pip install pandas requests
