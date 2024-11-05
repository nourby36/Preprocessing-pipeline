# Project Overview

This project involves a comprehensive data preprocessing pipeline that takes an input in the form of a dictionary and processes it through several steps to obtain a clean, preprocessed output. The pipeline is designed to handle multilingual text data, extract relevant information, standardize prices to USD, and enrich data with location and keyword details.

## Input Structure

The input to the notebook is expected to be a list of dictionaries, where each dictionary represents a product with attributes such as:
- `id`: Unique identifier for the product
- `content`: Description or textual content of the product
- `updated_at`: The last update date of the product (ISO 8601 format)
- `price`: The price of the product (including currency symbol)
- `product_url`: The URL associated with the product for location extraction
- Other attributes as needed for the analysis

## Processing Steps

### 1. **Duplicate Removal**
- **Function**: `process_json_files`
- **Purpose**: Ensures the input data does not contain duplicate entries by hashing each dictionary and comparing it to a set of existing hashes.
- **Output**: A list of unique product dictionaries.

### 2. **Keyword Extraction**
- **Function**: `extract_keywords`, `keywords_extraction` after detecting the language and applying some preprocessing
- **Purpose**: Extracts the most common keywords from the preprocessed content and adds them as a new field (`keywords`) in each product dictionary.
- **Output**: A list of products enriched with extracted keywords.

### 3. **Inactive Product Detection**
- **Function**: `detect_inactive_products`
- **Purpose**: Identifies products that have not been updated within a specified number of months and flags them as inactive.
- **Output**: Adds an `inactive_product` boolean field to indicate inactivity.

### 4. **Currency Standardization to USD**
- **Function**: `convert_to_usd`, `process_products_for_usd`, `standardize_prices_to_usd`
- **Purpose**:
  - Retrieves the latest currency conversion rates using an API.
  - Converts the `price` of each product to USD and adds `price_in_USD` as a new field.
- **Output**: A list of products with standardized USD pricing.

### 5. **Location Enrichment**
- **Function**: `get_country_from_tld`, `get_country_and_region_from_whois`, `update_json_with_location`
- **Purpose**:
  - Extracts country and region information from the `product_url` using TLD and WHOIS lookups.
  - Updates each product dictionary with `country` and `region` fields.
- **Output**: A list of products enriched with location information.
-  
### 6. **Seller information Extraction**
- **Function**: `extract_seller_information`, `scrape_seller_info`,`add_seller_info_to_json`
- **Purpose**:
  - Extracts seller information from the profided URL, using web scrapping

## Final Output

The final output is a list of dictionaries representing products, each containing:
- Preprocessed content with removed stop words
- Extracted keywords
- A standardized price in USD
- An `inactive_product` flag if applicable
- `country` and `region` fields based on the `product_url`
- eller information
- a freshness score
- min/max prices

## How to Run

1. **Install Dependencies**:
   Ensure all required libraries are installed:
   ```bash
   pip install spacy transformers pycountry tldextract python-whois ipinfo requests matplotlib seaborn numpy pandas nltk pytz dateparser langdetect lingua-language-detector
    ```
   The provided data folder represents just a part of the whole data, change the path accordingly
   
