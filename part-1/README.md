
# Unleash the Power of Data Visualization with Power BI

<img src="/part-1/pics/pic-51.png" width="500" />

#### Even though I've provided high-level step-by-step instructions, you should still be comfortable with Power BI or at least be able to navigate around. If not, consider using some tutorial videos on YouTube instead.

Here's a short agenda that outlines the key topics to be covered:

## Agenda

1. **Connecting Power BI to MySQL Database**
   - Importing data from MySQL
   - Selecting relevant tables

2. **Power Query Transformations**
   - Cleaning and shaping data
   - Removing unnecessary columns
   - Handling missing values

3. **Data Modeling in Power BI**
   - Creating relationships between tables
   - Defining fact and dimension tables
   - Optimizing the data model

4. **Introduction to DAX (Data Analysis Expressions)**
   - Creating calculated columns
   - Defining measures
   - Applying filters and slicers

5. **Visualizing Data with Charts**
   - Selecting appropriate chart types
   - Configuring chart elements (axes, legends, colors)
   - Customizing chart formatting

6. **Insights and Reporting**
   - Generating meaningful insights from the data
   - Creating interactive reports and dashboards
   - Sharing and publishing reports




The picture below represents the relationships between tables in our sample database. This diagram was obtained by using the Reverse Engineering feature of MySQL Workbench, which allows you to visualize the structure and relationships of an existing database. When importing this data into Power BI, we need to verify that these relationships are correctly established. If the relationships are not accurately represented, we will have to make the necessary corrections within Power BI to ensure data integrity and accurate analysis.

<img src="/part-1/pics/pic-50.png" width="500" />

### Connecting To MySql Database:


To connect Power BI to a MySQL database like the one from https://github.com/ramandcpu/SQL/tree/main/mysql, follow these steps:

1. Launch Power BI Desktop and navigate to the Home ribbon. From there, click on 'Get Data'. Alternatively, if you landed on the Welcome screen, you can click on 'Get data from other sources' as shown in the picture below.

<img src="/part-1/pics/pic-5.png" width="500" />

3. In the Get Data window, select "MySQL Database" from the "Database" categories.
<img src="/part-1/pics/pic-6.png" width="500" />

You might encounter the following error when attempting to connect to the MySQL database. If you do, simply click on 'Learn More' and follow the provided link to install the required connector. The image below shows what the error might look like.

<img src="/part-1/pics/pic-1.png" width="500" />

For the Windows version, the connector you need to download is shown in the picture below

<img src="/part-1/pics/pic-2.png" width="500" />

   

4. In the MySQL Database window, enter the Server and Database name for your MySQL instance. You can also specify the Data Connectivity mode (Import or DirectQuery) based on your needs.

<img src="/part-1/pics/pic-3.png" width="500" />

6. Click "OK" and enter your credentials (username and password) to authenticate with the MySQL server.

<img src="/part-1/pics/pic-4.png" width="500" />

8. If the connection is successful, you'll see the Navigator window listing all the available tables and views in the database. Select the ones you want to import and click "Load" or "Transform Data" if you need to apply any transformations.

9. Let's Select all the tables for now. The selected tables will now load into Power BI Desktop as separate queries. You can start building visualizations and reports using this data.
<img src="/part-1/pics/pic-8.png" width="500" />

A few important points:

- Make sure the MySQL server is accessible from the machine running Power BI Desktop. You may need to configure firewall rules or use an on-premises data gateway if the database is not publicly accessible.

- For large datasets, it's recommended to use DirectQuery mode to avoid loading all data into Power BI Desktop's memory.

- You can also connect using a connection string by selecting "Advanced options" in the MySQL Database window.

- Power BI supports MySQL versions 5.7 and above.


# Power Bi Power Query:

After connecting to the database, you will be taken to the Power Query Editor within Power BI. This is the stage where you can tidy up and make modifications to the data. We are going to perform a few tasks here. 

First, let's remove any unnecessary columns. If you select the 'employees titles' table, you will notice a column named 'employees.employees'. This column was automatically added by Power BI. To remove it, right-click on the column and select 'Remove' from the context menu. 


<img src="/part-1/pics/pic-9.png" width="500" />

<img src="/part-1/pics/pic-11.png" width="500" />


Following the same process, remove the 'employee.dept_emp', 'employees.dept_manager', 'employees salaries', and 'employees titles' columns from the 'employees employees' table. Since you're familiar with the structure of our database from the MySQL tutorial, you can identify and remove any extra columns that were automatically added by Power BI. You understand the process now, so continue cleaning up the tables by removing unnecessary columns.


<img src="/part-1/pics/pic-12.png" width="500" />

## Adding A Column 'full_name':

In the 'employees employees' table, we will create a new column by combining the 'first_name' and 'last_name' columns. To do this, select both columns by clicking on one and then pressing the 'Ctrl' key while clicking on the other. 

Next, navigate to the 'Add Column' ribbon and click on 'Merge Columns'. You should see options similar to the ones shown in the picture below. Adjust your settings to match the options in the picture, and then click 'OK'. You should now have a new column named 'full_name' added to the end of the table.

<img src="/part-1/pics/pic-13.png" width="500" />

## Adding A Column 'Age':

In the 'employees employees' table, we will add another column based on the 'birth_date' column. Select the 'birth_date' column, then go to the 'Add Column' ribbon and click on the down arrow next to 'Date'. From the options, choose 'Age'. This will add a new column called 'Age'. However, you might notice that the values in this column are displayed as long numbers with decimals. We will address this formatting issue in the next step.


<img src="/part-1/pics/pic-21.png" width="500" />


Let's now utilize the 'Transform' ribbon. Select the 'Age' column, then navigate to the 'Transform' ribbon. Click on 'Duration' and choose 'Total Year'. This will transform the values in the 'Age' column to display the age in years without decimals. While you could have achieved the same result by right-clicking and using the context menu, I wanted to demonstrate how to leverage the 'Transform' ribbon for such operations.


<img src="/part-1/pics/pic-23.png" width="500" />

To display the age values as whole numbers without decimals, click on the left-most corner of the 'Age' column. This will reveal a dropdown menu. From the options, select 'Whole Number' as shown in the picture.

<img src="/part-1/pics/pic-24.png" width="500" />

## Adding Two More Columns 'to_year' & 'emp_status':

"In the 'employees dept_emp_latest_date' table, we will add a new column called 'to_year'. Subsequently, we will create another column based on the 'to_year' column, which will indicate whether an employee is currently working or has left the company.

steps:

1. In Power Query Editor, select the date column you want to extract the year from (e.g. "to_year").

2. Go to Add Column > Custom Column on the ribbon.

<img src="/part-1/pics/pic-16.png" width="500" />

4. In the new column formula dialog, provide a name for the new column like "to_year".

5. Enter the following formula:

```
= Date.Year([to_date])
```



This will create a new "to_year" column containing just the year values extracted directly from the "to_date" column.For the 'emp_status' column, follow the same steps as before. However, this time, use the following formula:

```
= if [to_year] = 9999 then "still working" else "not working"
```

<img src="/part-1/pics/pic-17.png" width="500" />



Before finalizing our work in the Power Query Editor, let's modify the query names listed in the left column labeled 'Queries'. Power BI has prefixed the word 'employees' to each query name. We will remove this prefix from all the queries. After making these changes, the query names should match the ones shown in the picture below.

<img src="/part-1/pics/pic-27.png" width="500" />


With all the necessary modifications and transformations completed in the Power Query Editor, click on 'Close & Apply' in the Home ribbon.

<img src="/part-1/pics/pic-26.png" width="500" />


# Model View

Apart from one minor change, Power BI has correctly identified the relationships between the tables, as evident when comparing it to the figure from MySQL Workbench shown at the beginning of the tutorial.


<img src="/part-1/pics/pic-28.png" width="500" />

To fix this minor issue, double-click on the highlighted line and choose 'Single' in the 'Cross-filter direction' section at the bottom, as shown in the provided image.


<img src="/part-1/pics/pic-29.png" width="500" />

# DAX (Data Analysis Expressions) 

###  DAX: total employees

Let's navigate to the Table view to create a couple of DAX Measures. Right-click on the 'employees' table and select 'New Measure'. When the input bar appears, enter the following formula: total employees = COUNTROWS(employees).

Steps to create a new DAX Measure in the Table view:

1. In Power BI Desktop, switch to the "Data" view by clicking on the "Data" icon in the left-hand pane.

2. Locate the "Tables" section, which lists all the tables you have imported or created.

3. Right-click on the "employees" table, and from the context menu, select "New Measure".

4. A new formula bar will appear, allowing you to enter a DAX expression.

5. In the formula bar, type the following expression:

```
total employees = COUNTROWS(employees)
```

6. Press Enter or click the checkmark icon to commit the new measure.

The measure "total employees" will now be listed under the "employees" table in the "Fields" pane. You can use this measure in your reports and visualizations to display the total count of employees in the dataset.

Here's a breakdown of the formula:

- `total employees` is the name you're giving to the new measure.
- `COUNTROWS(employees)` is the DAX function that counts the number of rows in the "employees" table.

By following these step-by-step instructions, you can create a new DAX Measure called "total employees" that calculates the total number of employees in your dataset.

<img src="/part-1/pics/pic-34.png" width="500" />

## DAX: Employees by Department

Following the same process, let's create another Measure called 'Employees by Department'. However, this time, use the following formula:

```
Employees by Department = 
CALCULATE(
    COUNTROWS('employees'),
    FILTER(
        'dept_emp',
        'dept_emp'[dept_no] = MAX('departments'[dept_no])
    )
)
```
# Report View: Creating Different Charts


By following the general high-level instructions I'm about to provide, I will show you how to create a chart. The steps and options are very intuitive for our examples. Therefore, I'm only going to show you my pictures with the important options filled in.

Here are the step-by-step instructions to create a stacked bar chart for employees using the 2024 version of Power BI:

## Creating a Stacked Bar Chart for Employees

1. Launch Power BI Desktop and import the employees dataset into Power BI. 

2. Once the data is loaded, switch to the "Report" view by clicking on the "Report" icon in the left-hand pane.

3. From the "Visualizations" pane, click on the "Stacked Bar Chart" icon to add a new stacked bar chart visual to the report canvas.

4. In the "Fields" pane, locate the table containing employee information (e.g., "employees" table).

5. Drag and drop the field representing the employee categories (e.g., "department" or "job_title") into the "Y-axis" area of the visualizations pane. 

6. Next, drag and drop the field containing the numerical data you want to visualize (e.g., "salary" or "hours_worked") into the "X-axis" area of the visualizations pane. This will determine the height or length of the bars.

7. If you want to break down the bars into subcategories, drag and drop another field (e.g., "gender" or "age_group") into the "Stack by" area of the visualizations pane. This will create stacked segments within each bar, representing the subcategories.

8. Optionally, you can customize the appearance of the stacked bar chart by using the formatting options available in the "Visualizations" pane. This includes changing colors, adding data labels, adjusting axis titles, and more.


By following these steps, you can create an insightful stacked bar chart that visualizes employee data, such as salaries, hours worked, or other relevant metrics, broken down by categories like department, job title, gender, or age group. The stacked bar chart will help you identify patterns, compare values across categories, and make data-driven decisions related to your workforce.

Below is the picture for the 'Number of Employees by Department' chart.

<img src="/part-1/pics/pic-52.png" width="500" />

Below is the picture for the '"No of Employees by Department & Gender"' chart.

<img src="/part-1/pics/pic-53.png" width="500" />

Below is the picture for the 'Total Employees by Gender' chart. *Bender  --error :)

<img src="/part-1/pics/pic-54.png" width="500" />

Below is the picture for the Slicer called 'Timeframe' chart.

<img src="/part-1/pics/pic-55.png" width="500" />



#### Once you're satisfied with the stacked bar chart, you can save the report and share it with others or incorporate it into a larger dashboard or report.






