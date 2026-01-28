***This travel price analysis tool evaluates prior flight pricing trends and generates best-time-to-book recommendations for global destinations:

- Analyzes average flight prices by city and month
- Identifies lower cost and higher cost travel periods
- Provides simple booking recommendations based on observed price trends.




# Files in this Project

Flight Prices - Resume Project - Sheet2.csv   -   Raw flight price data (City, Month, Avg_Price)
flight_analysis.py	                          -   Python script that cleans the data and finds the cheapest month per city
setup_database.sql                            -   SQL file to create a table structure for flight prices
flight_prices.db                              -   SQLite database (for storing flight prices)
README.md                                     -   Project documentation


# Technologies Used

Python 3.x
pandas (data manipulation)
SQLite (database integration)
CSV    (data source)


# How to Run

Clone the repository.
Install dependencies:

pip install pandas

Place Flight Prices - Resume Project - Sheet2.csv in the same folder as flight_analysis.py.

Run the script:
python flight_analysis.py

Results will print the cheapest month and price for each city.


# Data Cleaning Steps

- Removed $ symbols and commas from the Avg_Price column.
- Converted the Avg_Price column from string to numeric (float) for calculations.
- Filtered the data by city and identified minimum prices.

Removes $ and commas, convert to float
df['Avg_Price'] = df['Avg_Price'].str.replace('$','', regex=False)
df['Avg_Price'] = df['Avg_Price'].str.replace(',','', regex=False)
df['Avg_Price'] = df['Avg_Price'].astype(float)


# Manual Approach

For each city, the script:
Filters the data for that city.
Finds the minimum price using min().
Selects the row corresponding to the minimum price to identify the month.

Palermo_df = df[df['City'] == 'Palermo']
Palermo_min_price = Palermo_df['Avg_Price'].min()
Palermo_min_month = Palermo_df[Palermo_df['Avg_Price'] == Palermo_min_price]
print(Palermo_min_month)


# Advanced / Vectorized Approach

To scale for any number of cities, the script uses pandas grouping and indexing.

- Find the index of the lowest price in each city
idx = df.groupby('City')['Avg_Price'].idxmin()

- Pull the corresponding rows from the original dataframe
cheapest_months = df.loc[idx]


# Optional Database Integration

The project includes setup_database.sql and flight_prices.db.
You can store the cleaned CSV in SQLite and query it with Python using sqlite3.


# Skills Demonstrated

- Python data manipulation
- Pandas filtering, aggregation, and grouping
- Problem-solving and stepwise reasoning
- Ability to optimize manual approaches into scalable code
- Preparing data for database storage


