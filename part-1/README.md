
<img src="/part-1/pics/pic-1.png" width="500" />


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


### Power Bi:























