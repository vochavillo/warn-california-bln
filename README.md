# warn-bln

BigLocal News, a journalism initiative run out of Stanford University, has pulled federal WARN notice data across multiple states. The majority of the data on the BigLocal News Project was scraped or manually inputed from tables on government websites. The process for one dataset in the project -- called "California_warn_expanded_2020-03-16.csv" --  was created differently. 

"California_warn_expanded_2020-03-16.csv" is a dataset built from extracting the data from individual WARN reports that were requested from California's Employment Development Department, rather than table data published on the government website. 

The difference between individual WARN reports and the table data released on the EDD's website are: 

1. Individul WARN reports: (California_warn_expanded)

-Fields: Company Name and Address, Employees Affected, Layoff Date, Local Workforce Investment Area, Contact Name and Telephone Number, Date Notice Received, Layoff or Closure, Severance, Bumping Rights, Union Representation, Union(s) Name and Address(es) representing Employees, Job Title(s) and Number of Layoffs for each

-Updated: After processing (as described below) and only as far as EDD provided reports for (this date ends the file name: e.g. California_warn_expanded_2020-03-16.csv.

-Native format: Excel (.xlsx) files.

2. EDD website table data: (California_warn_processed)

-Fields: Company Name, City, County, No. Of Employees, Layoff/Closure, Notice Date, Effective Date, Received Date

-Updated: Biweekly, on website.

-Native format: HTML table. 

The individual WARN reports came as Excel (.xlsx) files. Data processing was done with Python and relied primarily on the openpyxl package which allowed for necessary manipulation across Excel cells. Thee position of data headers and their corresponding data fields were not uniformly formatted. (For example: the number of affected employees would be one cell below the header, while the date of notice received would be in the cell on the right of the header.) Additionally, each report was a worksheet within a workbook; data for any given year was broken into multiple workbooks, alphabetically.

The script iterates over all workbooks in a folder, then iterates over every work sheet in a workbook. Luckily the layout of the data fields is largely uniform across all sheets and workbooks. The only exceptions are: 1) the first sheet in each workbook has a header field not found in other sheets within the same workbook, and 2) the itemized lists of layoffs ('Job Title(s)' and '# of Layoffs' per job type) is obviously variable across companies. But the script accounts for this. 

Currently, the most unique element to the 'California_warn_expanded.csv' is the last field in the csv file labeled "jobs." This column stores the number of layoffs itemized by job type ("Job Title(s)") as a dictionary. 

The Jupyter Notebook, california-warn-cleaning.ipynb contains the code used to clean the California's WARN reports from Excel workbooks on a local computer. 

###
