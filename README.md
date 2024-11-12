# Pandas Data Manipulation for Client and Sales Data

This Python program performs data manipulation tasks on a dataset containing client and sales information using the pandas library. The program filters the top clients, calculates totals for specific metrics, and generates summaries to support business analysis. It is designed to provide insights into key clients' purchase behavior, shipping costs, revenue, and profitability.

## Features

- **Filter Data by Client IDs**: Filter the dataset to focus on specific client IDs (top clients).
- **Aggregate Sales Metrics**: Calculate totals for `Units Purchased`, `Shipping Price`, `Revenue`, and `Profit` for each client.
- **Sort Data**: Optionally sort the summary data by specific metrics such as `Quantity` or `Revenue`.
- **Money-related Column Renaming**: Append "(millions)" to money-related columns for easier interpretation and reporting.

## Requirements

- Python 3.x
- pandas

To install pandas, run the following command:

```bash
pip install pandas
```

## Usage

1. **Load Data**: The program reads client and sales data from a CSV file with the following columns:
   - `first`, `last`, `job`, `phone`, `email`, `client_id`, `order_id`, `order_date`, `order_week`, `order_year`, `item_id`, `category`, `subcategory`, `unit_price`, `unit_cost`, `unit_weight`, `qty`, `line_number`.

2. **Filter by Top Clients**: Provide a list of top client IDs, and the program filters the data accordingly.

3. **Calculate and Summarize Metrics**:
   - Totals for `qty`, `shipping_price`, `line_cost`, and `line_profit` are calculated per client.
   - Optional: The program allows sorting by quantity or other metrics for further analysis.

4. **Money Column Formatting**: The program appends `"(millions)"` to columns like `shipping_price`, `line_cost`, and `line_profit` for clearer reporting.

### Example

```python
import pandas as pd

# Load the data
df = pd.read_csv('your_file.csv')


# Filter and summarize data
summary_df = (
    df[df['client_id'].isin(top_client_ids)]
    .groupby('client_id')
    .agg(
        qty=('qty', 'sum'),
        shipping_price=('shipping_price', 'sum'),
        line_cost=('line_cost', 'sum'),
        line_profit=('line_profit', 'sum')
    )
    .reset_index()
    .sort_values(by='qty', ascending=True)
)

# Rename columns to append "(millions)" for money columns
money_columns = ['shipping_price', 'line_cost', 'line_profit']
summary_df.rename(
    columns={col: f"{col} (millions)" for col in money_columns}, inplace=True
)

# Display the summary
print(summary_df)
```

## Output

The output will be a summary DataFrame showing totals for each client, with money-related columns labeled in millions:

```
   Client ID  UNITS  Shipping (millions)  Total Revenue (millions)  Total Profit (millions)
0      24741  100                       5.0                  3.0                    2.0
1      33615  200                       7.0                  4.0                    3.0
2      38378  150                       6.0                  3.5                    2.5
3      46820  250                      10.0                  5.0                    4.0
4      66037  300                       7.5                  4.0                    3.5
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

This project was developed with the assistance of ChatGPT, an AI language model created by OpenAI. The model helped in generating ideas, code snippets, and documentation to enhance the overall development process.
