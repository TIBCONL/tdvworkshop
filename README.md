# Workshop
## TIBCO Data Virtualization

## Lab Guide
Version: 1.1

Authors	:	Machiel Jacobs, Alain Martens

### Table of Contents
[TOC]


1. Guided Lab: Getting started 

**Problem Statement**

You work as a data engineer for an retailer of electronic called UniTech. \
UniTech recently started a program which allows them to make data driven decision. To do so UniTech has hired business analysts and data scientists to help them find insights in data and construct predictive models.

The challenge however is that data is spread over various data sources, stored in various formats (tabular, flat files, etc.) and is located in various locations (cloud and on premise).

You've been asked to facilitate the business analysts and data scientists by preparing data such that it can be used for analytical purposes. Some key questions you're asked to find the answers to are:



*   Can you prepare a data source that combines data coming from various data sources? 
*   How can I trace the source of the data?
*   Can you make sure that the query performs quickly?
*   The data is confidential, can you enforce security policies?

In order to perform these tasks you've been given 2 things: 



1. Various Data Sources and 
2. TIBCO Data Virtualization. 

 \
During this workshop we'll take the following steps together: 



1. Connecting to data sources using TIBCO Data Virtualization
2. Creating data layers
3. Exposing data to the end user
4. Accessing data exposed by TIBCO Data Virtualization
5. Using the Business Directory

Along the way we'll explore TIBCO Data Virtualization and you'll get familiar with various powerful Data Integration features. \
 \
Feel free to ask any questions you might have along the way!

Working with TIBCO Data Virtualization

When working with data, oftentimes we have data coming from multiple different sources, causing data to get lost or ignored due to the complication of creating joins. In our lab today, we are going to take a couple different data sources and an xml file and expose that data to an end user using a single-entry point in TIBCO Data Virtualization. We will use TDV Studio to help us with these tasks.

We will then explore how we can view that data in multiple different ways as well as discover more about our data in the Business Directory tool. 



1. Connecting to Data Sources with TIBCO Data Virtualization
1. From the desktop of your virtual machine, select the Start Menu and click **Start TDV Studio8.5**.


<img src=images/image38.png width="80%"></image>


2. Enter **admin** as username and use **tdvadmin** as password and click **Connect**.



<p id="gdcalert2" ><span style="color: red; font-weight: bold"><img src=images/image19.png></image></span></p>


_When we enter the Studio, we see a few different sections. On the left, we have the **Modeler** tab, which is where we will do most of our creation, the **Manager** tab, which allows us to view the health of our system, and the **Discovery** tab, which is where we can learn more about how our environment is structured. We will spend our lab today in the **Modeler** tab. This tab composes of 2 parts. On the left, we have the **Resource Tree**, which allows us to see all of the information we have either imported or built. On the right we have the **Canvas**, which is where we will do our creating and manage the details of our environment._



<p id="gdcalert3" ><span style="color: red; font-weight: bold"><img src=images/image55.png></image></span></p>


3. Expand the **Desktop** and **Shared** folders.
4. Right Click on the **IntroDemoOven** folder under the **Shared** folder and rename it **IntroDemoOven[FIRST LETTER + YOUR LAST NAME]**. For example; **IntroDemoOvenAMARTENS** To create your first data source:
    1. Select **New > New Data Source**.



<p id="gdcalert4" ><span style="color: red; font-weight: bold"><img src=images/image57.png></image></span></p>




    2. Search for PostgreSQL in the find box and select **PostgreSQL 9.1**.
    3. Click **Next.**



<p id="gdcalert5" ><span style="color: red; font-weight: bold"><img src=images/image56.png></image></span></p>



    4. Enter the corresponding database information:
        1. **Name**: Order Data.
        2. **Host**: localhost.
        3. **Port**: 9508
        4. **Database Name**: orders
        5. **Login**: tutorial
        6. **Password**: tutorial
        7. Click **Create & Introspect**.



<p id="gdcalert6" ><span style="color: red; font-weight: bold"><img src=images/image43.png></image></span></p>


    5. Expand the **Order Data** and **tutorial** folders
    6. Select the **orderdetails** and **orders** tables
    7. Click **Next**and **Finish**.

_If the tables are not appearing, select **Order Data** and click **Refresh Resource List**to retrieve the list of objects currently in the database._



<p id="gdcalert7" ><span style="color: red; font-weight: bold"><img src=images/image58.png></image></span></p>


    8. At the introspection task window, verify the status of **SUCCESS** and click **OK**.



<p id="gdcalert8" ><span style="color: red; font-weight: bold"><img src=images/image59.png></image></span></p>


_At this moment you've successfully made a connection to 2 data tables in a Postgres Database._

_We'll now continue to make a connection to a data table located in a MSSQL database._



5. Right Click on the **IntroDemoOven**to add our Customer Data.
    9. Select **New > New Data Source**.



<p id="gdcalert9" ><span style="color: red; font-weight: bold"><img src=images/image57.png></image></span></p>


    10. Search for Microsoft in the find box and select **Microsoft SQL Server 2012**.
    11. Click **Next.**



<p id="gdcalert10" ><span style="color: red; font-weight: bold"><img src=images/image62.png></image></span></p>



    12. Enter the corresponding database information:
1. **Name**: Customer Data.
2. **Host**: localhost.
3. **Port**: 1433
4. **Database Name**: IntroDemoCustomer
5. **Login**: sa
6. **Password**: Tibco@123
7. Click **Create & Introspect**.



<p id="gdcalert11" ><span style="color: red; font-weight: bold"><img src=images/image60.png></image></span></p>



    13. Expand the **Customer Data>IntroDemoCustomer>dbo** folders
    14. Select the **Customer_Data** tables
    15. Click **Next**and **Finish**.

_If the tables are not appearing, select **Customer Data** and click **Refresh Resource List**to retrieve the list of objects currently in the database._



<p id="gdcalert12" ><span style="color: red; font-weight: bold"><img src=images/image61.png></image></span></p>

    16. In the **Introspection Task** **Status** window, verify the status of **SUCCESS** and click **OK** to close the window.



<p id="gdcalert13" ><span style="color: red; font-weight: bold"><img src=images/image63.png></image></span></p>

_At this point in time we've successfully added connections to 2 database. We have additional information about our product catalog, this information is stored in an XML file. Let’s bring this in to connect it with our databases._



6. Right Click on the **IntroDemoOven**to add our **Product Information**.
    17. Select **New > New Data Source**.
    18. Search for File in the find box and select **File-XML**.
    19. Click **Next.**



<p id="gdcalert14" ><span style="color: red; font-weight: bold"><img src=images/image64.png></image></span></p>


    20. Enter the corresponding information:
1. **Name**: Product Descriptions.
2. **Root Path**: C:\Program Files\TIBCO\TDV Server 8.5\docs\examples
3. Click **Create & Introspect**.



<p id="gdcalert15" ><span style="color: red; font-weight: bold"><img src=images/image65.png></image></span></p>


    21. Expand the **Product Descriptions** folder
    22. Select the **productCatalog.xml** file
    23. Click **Next**and **Finish**.



<p id="gdcalert16" ><span style="color: red; font-weight: bold"><img src=images/image66.png></image></span></p>


    24. In the **Introspection Task** **Status** window, verify the status of **SUCCESS** and click **OK** to close the window.



<p id="gdcalert17" ><span style="color: red; font-weight: bold"><img src=images/image67.png></image></span></p>

_You've successfully completed the chapter where you've made connections to 3 data sources. 2 databases and 1 xml file. In the next chapter we'll combine these data sources._



2. Creating Data Layers

_In order to expose data to our end users, we want to create an easily understood system in order to not only expose multiple data sets to our end user, but also create a manageable system to quickly and easily expand our data offerings. To do this we create layers. Each layer represents a level of abstraction from our original data, from the Meta Data Layer, which maps most closely to our original data, the Business Layer which contains our reusable data model, to our Application Layer which contains views created to most closely match our end users’ needs._



1. Right Click on the **IntroDemoOven** folder.
2. Select **New > New Folder**to create folders for our data layers



<p id="gdcalert18" ><span style="color: red; font-weight: bold"><img src=images/image68.png></image></span></p>


3. Create 3 folders named **L1_MetaLayer, L2_BusinessLayer, L3_ApplicationLayer**



<p id="gdcalert19" ><span style="color: red; font-weight: bold"><img src=images/image69.png></image></span></p>



<p id="gdcalert20" ><span style="color: red; font-weight: bold"><img src=images/image70.png></image></span></p>


_The first layer we are creating is the Meta Data Layer. This maps most closely to our data sources, bringing in the components of the sources that are of interest to our end users and preparing that data to be joined with other sources at a higher layer._



4. Right Click on the **L1_MetaLayer** folder.
    1. Select **New > New View**.



<p id="gdcalert21" ><span style="color: red; font-weight: bold"><img src=images/image45.png></image></span></p>



    2. Name your new view **L1_Order** and click **OK**.



<p id="gdcalert22" ><span style="color: red; font-weight: bold"><img src=images/image46.png></image></span></p>





    3. Expand the **Order Data** and **Tutorial**folders.
    4. Click and Drag **orders**onto the canvas on the right.
    5. Click **Save** (

<p id="gdcalert23" ><span style="color: red; font-weight: bold"><img src=images/image3.png width="5%"></image></span></p>

) at the top left of the screen.



<p id="gdcalert24" ><span style="color: red; font-weight: bold"><img src=images/image48.png></image></span></p>






5. Right Click on the **L1_MetaLayer** folder.
    1. Select **New > New View**.
    2. Name your new view **L1_OrderDetails** and click **OK**.
    3. Expand the **Order Data** and **Tutorial**folders.
    4. Click and Drag **orderdetails**onto the canvas on the right.
    5. Click **Save** (

<p id="gdcalert25" ><span style="color: red; font-weight: bold"><img src=images/image3.png width="5%"></image></span></p>

) at the top left of the screen.



<p id="gdcalert26" ><span style="color: red; font-weight: bold"><img src=images/image49.png></image></span></p>


6. Right Click on the **L1_MetaLayer** folder one last time.
    1. Select **New > New View**. 
    2. Name your new view **L1_Customer** and click **OK**.
    3. Expand the **Customer Data > IntroDemoCustomer > dbo**folders.
    4. Click and Drag **Customer_Data**onto the canvas on the right.
    5. Click **Save** (

<p id="gdcalert27" ><span style="color: red; font-weight: bold"><img src=images/image3.png width="5%"></image></span></p>


) at the top left of the screen.



<p id="gdcalert28" ><span style="color: red; font-weight: bold"><img src=images/image50.png></image></span></p>


_Now that we’ve setup our database views, we need to translate our XML product data into something that TIBCO Data Virtualization can understand, so we need to create data transformation to connect our product information with our other data_



7. Right Click on the **L1_MetaLayer** folder.
    1. Select **New > New Transformation**.



<p id="gdcalert29" ><span style="color: red; font-weight: bold"><img src=images/image51.png></image></span></p>


    2. Select XSLT Transformation and click **Next**.


<p id="gdcalert30" ><span style="color: red; font-weight: bold"><img src=images/image52.png></image></span></p>


    3. Name your Transformation **L1_Product**.
    4. Expand the **Shared > IntroDemoOven > ProductDescription**folders.
    5. Select **productCatalog.xml** for your transformation.
    6. Click **Finish**.



<p id="gdcalert31" ><span style="color: red; font-weight: bold"><img src=images/image11.png></image></span></p>


    7. In the new view that appears, select **outputs** under the target column on the right side of the window.
    8. select the **plus sign** (+) at the top middle to add a new target column.
        1. Select **Integer > INTEGER**.
        2. Enter **ProductID** and hit return.
        3. Repeat this step for **ProductName** (String > VARCHAR) and **ProductDescription** (String > VARCHAR). 



<p id="gdcalert32" ><span style="color: red; font-weight: bold"><img src=images/image13.png></image></span></p>


    9. Expand **catalog > category > products > product** on the left hand of the screen
    10. Drag **ProductID**, **ProductName** and **ProductDescription** from the left onto its counterpart on the right. 
    11. Click **Save** (

<p id="gdcalert33" ><span style="color: red; font-weight: bold"><img src=images/image3.png width="5%"></image></span></p>

) at the top left of the screen.



<p id="gdcalert34" ><span style="color: red; font-weight: bold"><img src=images/image14.png></image></span></p>


_Now that we have our physical layer set up, we want to expose data in a way that will be useful to our end users. To do this, we want to create views of commonly requested data as well as data that is connected but may not be in our database, such as a holistic view of our orders or a complete view of our customer activities._



8. In the Resource Tree on the left, right click on the **L2_BusinessLayer** folder.
    6. Select **New > New View**. 
    7. Name your new view **L2_OrderInfo**.



<p id="gdcalert35" ><span style="color: red; font-weight: bold"><img src=images/image5.png></image></span></p>



    8. Expand **L1_MetaLayer** and drag **L1_Order** and **L1_OrderDetails** onto the canvas.
    9. Drag **orderid** from **L1_Order**onto **orderid** in **L1_OrderDetails** to link the two tables based on **orderid**.
    10. Select the **Grid** tab at the bottom of the screen.



<p id="gdcalert36" ><span style="color: red; font-weight: bold"><img src=images/image15.png></image></span></p>


    11. On the **Grid Tab**, click **List Columns** (

<p id="gdcalert37" ><span style="color: red; font-weight: bold"><img src=images/image7.png></image></span></p>

) at the top of the screen.
    12. Select both **L1_Order**and **L1_OrderDetail** and click the right arrow to list all of the available columns.
    13. Click **OK**.

<p id="gdcalert38" ><span style="color: red; font-weight: bold"><img src=images/image17.png></image></span></p>

_When we look at all of the columns, we see a few that, while useful for customer service and our shipping department, aren’t very useful for order analyses, such as Shipping Method ID, so we need to cut down on some of these columns to make the data easier to digest._

    14. Select and delete all columns other than those appearing in the picture below by clicking the red X (

<p id="gdcalert39" ><span style="color: red; font-weight: bold"><img src=images/image9.png></image></span></p>

) at the top of the screen.
    15. Deselect **L1_OrderDetails.orderid** to remove it from the output.



<p id="gdcalert40" ><span style="color: red; font-weight: bold"><img src=images/image18.png></image></span></p>


_Now that we have our data selected, we want to add sorting to our data to make it more consumable by our end users. To do this, we’ll sort by Customer ID, Order ID and Product ID from the grid panel._



    16. Click **L1_Order.customerid** and press the up arrow at the top of the screen        (

<p id="gdcalert41" ><span style="color: red; font-weight: bold"><img src=images/image2.png></image></span></p>

) to move it into the first position.
    17. Select **L1_OrderDetails.productid** and press the up arrow to until it is in the third position.
    18. To the right of **L1_Order.customerid**, Select **Sort Order** and enter 1.
    19. To the right of **L1_Order.orderid**, Select **Sort Order**and enter 2.
    20. To the right of **L1_Order.productid**, Select **Sort Order** and enter 3.
    21. Click **Save** (

<p id="gdcalert42" ><span style="color: red; font-weight: bold"><img src=images/image3.png width="5%"></image></span></p>

) at the top left of the screen.



<p id="gdcalert43" ><span style="color: red; font-weight: bold"><img src=images/image4.png></image></span></p>

9. In the Resource Tree on the left, right click on the **L2_BusinessLayer** folder to add a view for our Customer Activity Data.
    1. Select **New > New View**. 
    2. Name your new view **L2_CustomerActivity**.

<p id="gdcalert44" ><span style="color: red; font-weight: bold"><img src=images/image5.png></image></span></p>


    3. Expand **L1_MetaLayer** and drag **L1_Customer, L1_Product** and **L2_OrderInfo** onto the canvas.
    4. Drag **customerid** from **L1_Order**onto **customerid** in **L2_OrderInfo** and **productid** in **L2_OrderInfo** onto **productid** in **L2_Product** to link the tables.
    5. Select the **Grid** tab at the bottom of the screen.



<p id="gdcalert45" ><span style="color: red; font-weight: bold"><img src=images/image6.png></image></span></p>


    6. On the **Grid Tab**, click **List Columns** (

<p id="gdcalert46" ><span style="color: red; font-weight: bold"><img src=images/image7.png></image></span></p>

) at the top of the screen.
    7. Select all three tables and click the right arrow to list all of the available columns.
    8. Click **OK**.



<p id="gdcalert47" ><span style="color: red; font-weight: bold"><img src=images/image8.png></image></span></p>

_Similar to our last table, there is more information here than we’d like to expose. Let’s remove some of those tables to make our data a bit cleaner._



    9. Select and delete all columns other than those appearing in the picture below by clicking the red X (

<p id="gdcalert48" ><span style="color: red; font-weight: bold"><img src=images/image9.png></image></span></p>


47.png "image_tooltip")
) at the top of the screen.
    10. Deselect **L2_OrderInfo.customerid** and **L1_Product.ProductID** to remove them from the output.
    11. Click **Save** (

<p id="gdcalert49" ><span style="color: red; font-weight: bold"><img src=images/image3.png width="5%"></image></span></p>

) at the top left of the screen.



<p id="gdcalert50" ><span style="color: red; font-weight: bold"><img src=images/image10.png></image></span></p>


_Now that we’ve exposed our data, one of our teams is building an application that needs a slightly different data set than what we have exposed. Let’s build a view that allows them to use the data that they need and creates a new column._



10. Right click on **L3_ApplicationLayer** and navigate to **New > New View** .
    22. Name your View **L3_CustomerActivityCustomized**.
    23. Expand **L2_BusinessLayer**and drag **L2_CustomerActivity** into the canvas.
    24. Select the **Grid** tab.



<p id="gdcalert51" ><span style="color: red; font-weight: bold"><img src=images/image31.png></image></span></p>


    25. On the **Grid** **Tab**, click **List Columns** (

<p id="gdcalert52" ><span style="color: red; font-weight: bold"><img src=images/image7.png></image></span></p>

) at the top of the screen.
        1. Select **L2_CustomerActivity** and click the right arrow to list all of the available columns.
        2. Click **OK**.
    26. Deselect the columns under Output as shown below.
    27. Select the row below **L2_CustomerActivity.ProductDescription** under the **Column** column and enter **L2_CustomerActivity.unitprice * L2_CustomerActivity.quantity**.
    28. Select the alias for your new column and enter **totalprice**.
    29. Click the **up arrow** twice to move your column to the third from last position.
    30. Click **Save** (

<p id="gdcalert53" ><span style="color: red; font-weight: bold"><img src=images/image3.png width="5%"></image></span></p>

) at the top left of the screen.



<p id="gdcalert54" ><span style="color: red; font-weight: bold"><img src=images/image32.png></image></span></p>


_Once we’ve created our views, we want to limit the access our end users have to the data based on criteria they enter. To do this, let’s create a new procedure that limits our data by **Company Name**._



11. Right Click on **L3_ApplicationLayer**and select **New > New SQL Script** .
    31. Name your script **L3_SelectiveCustomerActivityCustomized**.
    32. Replace the **SQL code** with the code below.
    33. To copy this code from the machine, open the **Lab Files** folder on the **Desktop**.
        3. Open the Data Virtualization Intro Demo file
        4. Right Click **SelectiveCustomerActivityReplace.sql** and select open with **Notepad++**.
        5. Return to TIBCO Data Virtualization and paste the SQL code into the window. 
    34. Click **Save** (

<p id="gdcalert55" ><span style="color: red; font-weight: bold"><img src=images/image3.png width="5%"></image></span></p>


<p id="gdcalert55" ><span style="color: red; font-weight: bold"><img src=images/image12.png></image></span></p>

) at the top left of the screen.



### Data lineage?





## Exposing Data to the End User

_Now that we’ve created the views that our end user wants to see, we want to expose that data to our end user. This can be done either by querying the data using methods such as JDBC or as a SOAP or REST Service. The first thing we need to do is publish our data._



1. Right Click on **L3_CustomerActivityCustomized** and select **Publish**.



<p id="gdcalert57" ><span style="color: red; font-weight: bold"><img src=images/image34.png></image></span></p>



2. In the window that appears, expand to **Desktop > Composite Data Services > Databases > IntroDemo > IntroDemoCat.**
3. Select **IntroDemoSchema**to publish your view to that schema.
4. Name your view **CustomerActivityCustomized**.
5. Click **OK**.


<p id="gdcalert58" ><span style="color: red; font-weight: bold"><img src=images/image35.png></image></span></p>


6. Right Click on **L3_SelectiveCustomerActivityCustomized** and select **Publish**.



<p id="gdcalert59" ><span style="color: red; font-weight: bold"><img src=images/image34.png></image></span></p>



7. In the window that appears, expand to **Desktop > Composite Data Services > WebServices > IntroDemo**
8. Select **IntroDemo**to publish your procedure to that schema.
9. Name your procedure **SelectiveCustomerActivityCustomized**.
10. Click **OK**.



<p id="gdcalert60" ><span style="color: red; font-weight: bold"><img src=images/image36.png></image></span></p>


## Accessing Data Exposed by TIBCO Data Virtualization

_The first way we want to access our data is through a database visualization tool, such as SQuirreL SQL Client. In doing this, we’ll be able to access our data similar to if it was in a database._



    1. From the desktop, double click the **SQuirreL SQL Client** icon.



<p id="gdcalert61" ><span style="color: red; font-weight: bold"><img src=images/image37.png></image></span></p>




        1. Double Click **TDV Local** on the left of the screen and click **Connect**using the username/password **admin/tdvadmin**.



<p id="gdcalert62" ><span style="color: red; font-weight: bold"><img src=images/image30.png></image></span></p>





        2. Click to expand **TDV Local > IntroDemoCat > IntroDemoSchema > Table**.
        3. Select the **CustomerActivityCustomized**table**.**
        4. Click **Content**to view the data within our table.



<p id="gdcalert63" ><span style="color: red; font-weight: bold"><img src=images/image21.png></image></span></p>



_Now that we’ve seen our data from a data visualization tool, we want to expose it as a service so our developers have the ability to access our data from their applications._



    2. In TIBCO Data Virtualization Studio, right click **IntroDemo** and select **Open**.
        5. On the bottom of the screen, click the **REST** tab.
        6. Select your **SelectiveCustomerActivityCustomized** we published earlier.
        7. In the center section, double click the **HTTP/XML** value at the bottom of the screen to copy the URL to your clipboard.
    3. Open Google Chrome at the bottom of the screen.



<p id="gdcalert64" ><span style="color: red; font-weight: bold"><img src=images/image22.png></image></span></p>



    4. Paste in the link you just copied into the address bar, replacing **{company_name_starts_with}**with any letter.
    5. Enter the username/password **admin/tdvadmin** when requested.



<p id="gdcalert65" ><span style="color: red; font-weight: bold"><img src=images/image24.png></image></span></p>





## Using the Business Directory

_Now that we’ve exposed our data to our end users, they can take advantage of multiple different data sources without need to create joins or manipulate the data. Oftentimes, though, end users have access to a large amount of data and do not know what all is available to them or they need to solve a problem and haven’t interacted with the data they need. By using the Business Directory, our end users can learn more about the data they have available to them and find the information they need to be successful._



    6. In Google Chrome, navigate https://localhost:9602/directory/#browse.
    7. Enter the username/password admin/tdvadmin 
    and click **Login**.



<p id="gdcalert66" ><span style="color: red; font-weight: bold"><img src=images/image25.png></image></span></p>



_In this view, we can explore the available databases and web services that have been published on this machine. Let’s search for a column to find which tables make that information available to us._



<p id="gdcalert67" ><span style="color: red; font-weight: bold"><img src=images/image26.png></image></span></p>


    8. In the search bar, enter **Company Name** and hit **Return**
    9. Select **CustomerActivityCustomized**to view information on this table. 



<p id="gdcalert68" ><span style="color: red; font-weight: bold"><img src=images/image27.png></image></span></p>


This concludes our TIBCO Data Virtualization Introductory Lab. Feel free to continue looking around the Business Directory to view all of the information available to end users. In this lab we were able to connect data from multiple data source types using the TIBCO Data Virtualization Studio, expose that data to our end user through web services and database calls, and discover more about our data using the Business Directory.
