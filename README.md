# Option Chain Data Analysis

## Overview
This project involves creating Python functions to retrieve and analyze option chain data for financial instruments using the Upstox API. The goal is to determine the highest bid or ask price for each strike price and calculate the margin required and premium earned for selling options. This work was completed as part of an assessment for the BreakoutAI internship.

## Code Structure
### Function 1 - `get_option_chain`
- **Purpose**: Retrieves the option chain data for a specified instrument and expiry date. It then identifies the highest bid price for put options (PE) or the highest ask price for call options (CE) for each strike price.
- **Key Columns**:
  - `instrument_name`: Name of the instrument (e.g., NIFTY).
  - `strike_price`: The strike price of the option.
  - `side`: "PE" for put options or "CE" for call options.
  - `bid_or_ask`: Highest bid price for PE or highest ask price for CE.
  - `instrument_key`: Unique identifier used to fetch margin details.
- **Output**: A DataFrame row containing the required columns.

### Function 2 - `calculate_margin_premium`
- **Purpose**: This function calculates the `margin_required` and `premium_earned` based on the retrieved data. Using `instrument_key` from Function 1, it calls the margin API to get the necessary margin for option selling.
- **Calculation**:
  - **Margin Required**: Uses the Upstox margin API, passing `instrument_key` and quantity (lot size) to determine the margin.
  - **Premium Earned**: Calculated by multiplying `bid_or_ask` price by the lot size.
- **Output**: Adds `margin_required` and `premium_earned` to the DataFrame.

## Approach
### Unique Aspects
- An additional `instrument_key` column was included to seamlessly use this data in margin calculations.
- Used two API calls effectively by breaking down the code into two separate functions for simplicity and clarity.

### Challenges
- Understanding and extracting only specific data parts from the API response (e.g., highest bid/ask prices and instrument keys) required careful handling of JSON data.
- Integrating multiple API calls to retrieve margin requirements in real-time and ensuring error-free data handling.

## Usage
1. Define `client_id`, `secret_key`, and `redirect_uri` for authentication.
2. Use `get_option_chain` to retrieve the required option data.
3. Pass the resulting DataFrame row to `calculate_margin_premium` with the correct lot size.

## AI Assistance
- Used AI tools like ChatGPT to clarify financial terms (e.g., options, premiums) and provide initial code structure for API data retrieval and JSON handling.
