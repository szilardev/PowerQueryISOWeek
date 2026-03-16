# Power Query ISO 8601 Week Calculator

A custom Power Query (M) function to accurately calculate the ISO 8601 week number from any date or datetime. By implementing an ordinal date-based algorithm, it perfectly handles complex year-end edge cases for seamless use in Power BI and Excel.

## The Algorithm

The function calculates the week of the year (`woy`) based on the ordinal date (day of the year, `doy`) and the day of the week (`dow`). The mathematical model applied in this code is:

$$y = \text{year}(date)$$
$$w = \left\lfloor \frac{10 + \text{doy}(date) - \text{dow}(date)}{7} \right\rfloor$$
$$\text{woy}(date) = \begin{cases} \text{weeks}(y - 1), & \text{if } w < 1 \\ 1, & \text{if } w > \text{weeks}(y) \\ w, & \text{otherwise.} \end{cases}$$

Where:
* `doy` $\in [1, 366]$
* `dow` $\in [1, 7]$ (Monday = 1, Sunday = 7)
* `weeks(year)` returns the total number of ISO weeks in a given year (either 52 or 53).

Source: https://en.wikipedia.org/wiki/ISO_week_date#Calculating_the_week_number_from_an_ordinal_date

## How to Use (Installation)

1. Open the **Power Query Editor** in Power BI or Excel.
2. Right-click in the Queries pane and select **New Query > Blank Query**.
3. Open the **Advanced Editor** from the Home or View tab.
4. Replace all existing text with the M code below.
5. Click **Done** and rename the query to `GetISOWeek`.

## Usage Example

Once saved, you can use this function in your datasets by adding a Custom Column with the following formula:

```powerquery
= GetISOWeek([YourDateColumn])
