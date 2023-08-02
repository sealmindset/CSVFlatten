# Description
It allows a user to upload any standard format CSV file, process its data, flatten any nested JSON objects, remove duplicate rows, and download the processed CSV file.

Current version the output file is called `output.csv`

## How it works
Here's a breakdown of how the code works:

The code starts by importing required modules: React, useState from React, Papa for CSV parsing, and axios for HTTP requests.
The code defines two utility functions: flattenProperties and mergeRow. These functions are used to flatten nested JSON objects and merge the flattened properties into the original row data.
The CSVProcessor component is defined, which renders a simple user interface with an input element for file selection, a "Process CSV" button, and, upon processing, displays a message and a "Download Output CSV" button.
Inside the CSVProcessor component, it initializes two states using the useState hook: inputFile and outputFileLink. The inputFile state is used to store the selected CSV file, while outputFileLink holds the URL of the processed CSV file that the user can download.
The main processing logic occurs in the processCSV function. When the user clicks the "Process CSV" button, this function is executed. It reads the contents of the uploaded CSV file using FileReader and parses it using Papa.parse to get an array of rows.
For each row in the CSV data, it checks if the row has a 'PROPERTIES' column. If so, it attempts to parse the JSON data in that column and flatten the properties using the flattenProperties function.
After flattening the properties, it merges the flattened properties into the row using the mergeRow function and removes the 'PROPERTIES' column from the newRow.
The function checks for duplicates by comparing the string representation of the rows and keeps only unique rows in the outputRows array.
Once the processing is complete, it generates a new CSV string using Papa.unparse and creates a downloadable link for the processed CSV file using Blob and URL.createObjectURL. The link is then stored in the outputFileLink state.
The handleFileChange function is used to update the inputFile state whenever the user selects a file.
The downloadOutputCSV function is triggered when the user clicks the "Download Output CSV" button. It sends an HTTP GET request to the outputFileLink using axios, retrieves the processed CSV data, and generates a downloadable link for the user to download the file.

# Setup
To set up and run the code:

Ensure you have Node.js and npm (Node Package Manager) installed on your computer.
Create a new React project or use an existing one. If you don't have a project, you can create one using create-react-app by running the following command in your terminal:
```
npx create-react-app my-csv-processor
```
Navigate to the project directory:
```
cd my-csv-processor
```
Install the required packages (papaparse and axios):
```
npm install papaparse axios
```
Replace the default src/App.js content with the provided code.

# Run Test
Run the React development server:
```
npm start
```
Open your web browser and go to http://localhost:3000 to view the CSV Processor application.
Upload a CSV file, click "Process CSV," and once the processing is complete, the "Download Output CSV" button will appear. Click it to download the processed CSV file.

Note: Since this code uses some external libraries (papaparse and axios), make sure to install them before running the application. Also, be cautious while processing large CSV files, as the application might consume significant resources during the parsing and processing phases.