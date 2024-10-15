# Covid Report NYC Dashboard

https://covidreportnyc.netlify.app/

This website fetches recent Covid-19 data from [NYC Health Department](https://github.com/nychealth/coronavirus-data), displays key statistics for the last few days (cases, hospitalizations, deaths), and plots a scatter chart to visualize the trend of cases over the last 30 days. All functionality is on the client-side.

### Architecture
1. **Fetch and Parse CSV Data:**
- The `getDataCSV` function is responsible for fetching a CSV file from a remote URL: `https://raw.githubusercontent.com/nychealth/coronavirus-data/master/trends/data-by-day.csv`.
- An `XMLHttpRequest` is used to send an asynchronous HTTP GET request to retrieve the CSV data.
- Once the request is successful (HTTP status 200), the function verifies if the response is of type `text/csv`.
- The CSV data is parsed by splitting the response into lines and using a helper function (`getCsvValuesFromLine`) to break each line into individual values (CSV columns).
- The parsed data is stored in a global variable `days`.

2. **Display Latest Data:**
- The function retrieves the 7-day average of cases, hospitalizations, and deaths, from the parsed CSV data.
- It extracts the most recent three entries: one for each metric—cases, hospitalizations, and deaths.
- These values are then inserted into HTML elements (with IDs `cases`, `hosp`, and `deaths`) to display the data on a web page.

3. **Generate a Scatter Plot:**
- The `scatterPlot` function takes the most recent 30 days of case count data (7-day averages) and creates an array of objects with `x` (representing days relative to today) and `y` (representing case count averages).
- This data is then plotted as a scatter chart using Chart.js. The x-axis represents the days (from -30 to 0), and the y-axis shows the number of cases.
- The chart is rendered on an HTML canvas element with the ID `myChart`.

4. **Helper Function for CSV Parsing:**
- `getCsvValuesFromLine`: This helper function splits a CSV line by commas and removes any quotation marks (`"`) around the values.