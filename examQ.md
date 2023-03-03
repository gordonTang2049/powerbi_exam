Power BI services
Power BI report
Power BI dashboard

Q:  (Update won't add new column)
    Get Data to connect to an Excel table - columns: 
        Date, CustomerID, Product, Price, Qty
    remove the ***Product column*** by selecting the other columns and clicking Remove Other Columns. 
    create a data model and report from the data.
    The Excel table 
        is later ***updated*** and now has these columns: 
            Date, CustomerID, Product, Price, Qty, Store
    You click the refresh button in Power BI
    Which columns is available in your data model for reporting?
        
    A:
        Date
        CustomerID
        Price
        QTY

    Explan:
    1. Product col has been removed 
    2. Excel table has new Column "Store", but update ***wont add Column*** 

    Remove Other Columns 
        removes all columns other than the ones 
        that 
        was originally selected 
        ***even if the source data is updated with new columns.***
    https://docs.microsoft.com/en-us/powerquery-m/table-selectcolumns

Q:
    Scenario
    - Get Data to connect to a data source containing rainfall data.
    - edit the query revealing the data table as in the exhibit. 
    Goal
    - want to prepare the data so that there are three columns, namely: 
        City, Year and Rainfall

    Table
    |City|      2010|2011|2012|
    |Johnsburg|   50|55  |58  |
    |Pretoria |   60|61  |40  |
    |Cape Town|   90|16  |12  |


    A:
        UnPivot Column

    Explanation
    Converting from columns to rows - use Unpivot (as is the case for the question). 
    Converting from rows to columns - use Pivot. 

    Changing the orientation of the table without rearranging the values - use Transpose. 
    Duplicating values into empty rows - use Fill Down (or Up). 
    Reversing the order of rows (top to bottom and bottom to top) without sorting - use Reverse Rows.
    
    https://radacad.com/pivot-and-unpivot-with-power-bi

    
***Pivot Column***

    |City|      2010|2011|2012|
    |Johnsburg|   50|55  |58  |
    |Pretoria |   60|61  |40  |
    |Cape Town|90   |16  |12  |

***unpivot Column***

    |City     |Year |Rainfall|
    |Johnsburg|2010 |50|
    |Johnsburg|2011 |55|
    |Johnsburg|2012 |58|
    |Pretoria |2010 |60|
    |Pretoria |2011 |61|
    |Pretoria |2012 |40|
    |Cape Town|2010 |90|
    |Cape Town|2011 |16|
    |Cape Town|2012 |12|

***fill down*** 

    Query editor - From Column drop down fill

    The fill down operation takes a column and traverses through the values in it to 
        fill any null values in the next rows 
        until it finds a new value. This process continues on a row-by-row basis until there are no more values in that column.

***Reverse row***

    Query editor -> Transform -> Reverse Rows

Q:
    Which of the following could represent a ***valid hierarchy***?

    A:
        Product Category > Product Brand > Product
        Tree > Fruit > Juice

    Explan:
    Peach > Pear > Plum  Incorrect, same kind of things, no obvious hierarchy.   
    Country > City > State  Incorrect order.   
    Day > Month > Year  Incorrect order; hierarchies must descend.   
    ZipCode > State > Department  Incorrect, departments is not geo.   
    Product Category > Product Brand > Product  Correct, same kind, descending order.   
    Tree > Fruit > Juice  Correct, same kind, descending order.


Q: (Power BI Service feature)
  Which of the following is ***true*** regarding ***Power BI Dashboards***?

    A: 
        - Can be set as a favourite

    Explan:
        Dashboards is a Power BI Service feature and is limited to a single page (although you could scroll down nearly infinity).
    They are not designed in Power BI Desktop, 
    but rather 
        you can pin visuals as tiles to dashboards from reports published to the Power BI Service.  
    You can set a dashboard or a report as a favourite in the Power BI Service.  
    Dashboards can use multiple data sets. 
    You can mash several data sources together in Power Query, 
        but once it is loaded into the Power BI model, 
        it is considered a single data set.

    https://docs.microsoft.com/en-us/power-bi/service-dashboards        

    Power BI Dashboards -> 
        - is a ***Power BI Service feature***
        - is limited to a single page(although you could scroll down nearly infinity)
        - not designed in Power BI Desktop    
        - pin visuals as tiles to dashboards from reports published to the Power BI Service.  
        - set a dashboard or a report as a favourite in the Power BI Service.  
        - mash several data sources together in ***Power Query***

    Power BI model
        Once loaded, it considered a ***single data set***
        
Q:
    What functionality does creating a hierarchy provide in Power BI reports?

    A:
        Drill-up
        Drill-down

    Explan:

    Drill-down and drill-up uses hierarchies, the others don't. 
    Don't confuse drill-down with drillthrough.  
    Drill-down uses (requires) a hierarchy to traverse the level of detail in a visual.  
    Drillthrough passes the filters from the visual (and page) where it was activated to another report page for usually for further detailed analysis.  
    Drill-down happens within a visual; drillthrough happens between report pages. 
    https://docs.microsoft.com/en-us/power-bi/consumer/end-user-drill#drill-requires-a-hierarchy
    https://docs.microsoft.com/en-us/power-bi/desktop-drillthrough

Hierarchies
    -Drill-down
    -drill-up

drill-down (traverse the level)
Drillthrough (filter)

Don't confuse ***drill-down*** with ***drillthrough***
    - Drill-down - requires a ***hierarchy*** to traverse the level of detail in a visual.
        - >> happens within a visual
    - Drillthrough - passes ***the filters from the visual*** (and page) 
        where it was ***activated to another report page*** for usually for further detailed analysis.  
        
Q:
    What is the Power BI Desktop feature that allows for ***what-if analysis***?

    A:
        New Parameter
    
    Explain:
        New Parameter (What If) is used to create what-if analysis.
        Creating a new parameter automatically 
        creates a new measure, slicer and table used in the what-if analysis. 
        There is no feature called New KPI.
        New column is not used in what-if analysis.
    https://docs.microsoft.com/en-us/power-bi/desktop-what-if


New Parameter (create what-if analysis) 
    -Creating a new parameter automatically 
    -creates a new measure, slicer and table used in the what-if analysis. 
    -New column is not used in what-if analysis.


Q: (Slicer)
    How do you change 
        - the slider to only control changing the lower (left) value 
        - not the higher (right) value, as in the exhibit?

    A:
        Use the down arrow menu on the 
            - slicer and 
            - choose greater than or equal to.

    Explan:
    The appearance of the slider control can be adjusted at run-time by changing it on the slicer visual itself.  
    To only manipulate the lower (left) value, one must choose greater than.

(Slicer)
slider control
    - adjusted at run-time
    - only manipulate the lower (left) value, one must choose greater than

Q:
    How do you configure a push notification on data in a ***Power BI Dashboard***? 

    A:
        - Available only for card, gauge or the KPI tiles
        - Click the elipses (...) button on the tile, then click manage alerts

    Explan:
    Push notifications are known in the Power BI Service as alerts.  
    They are available only for 
    KPI 
    and 
    card tiles 
    and is configured using the manage alerts menu item on the tile's ellipses (...) menu.

(Alerts) - Power BI Service feature
    available only for
        - Power BI Service
        - KPI
        - card tiles 
        - Open menu item on the tile's ellipses (...) menu

Q:
    You have pinned a card visual from one of your reports to a dashboard 
        in the Power BI Service as in the exhibit.
    Your dashboard users want an alert to be sent 
        when fewer than 50% of apps are games.
    Select the actions you must perform from the list. Each action represents part of the solution. (Choose 6)

    A:
        - Choose Manage alerts from move options on the card
        - Click + add alert rule
        - Choose below in the condition field
        - Set the threshold value to 0.5
        - check Send me email too checkbox
        - click Save and close 

    Explain:
        -configure alerts on the card in a dashboard, 
        not on the dashboard itself
        Values formatted as percentage must be specified as absolute value on the alert (0.5 instead of 50%)

        The Send me email too checkbox must be 
            selected - this is the only way an email will be sent.
             Users must configure their own alerts - you can't configure this on their behalf.
        https://docs.microsoft.com/en-us/power-bi/create-reports/service-set-data-alerts


Power BI Service - pinned a card visual - one of your reports to a dashboard 
    (configure alerts on the card Only, not on the dashboard, when fewer than 50% of apps)
    - Users must ***configure their own alerts*** - ***you can't configure this on their behalf***.

Q: 
    created a report ->  sales department
        -> help them to analyse sales across sales teams in the organisation. 
        -> users complain > the visuals contain ***too much granularity***
    some 
        - require scrolling left to right and up and down 
        - number of data elements make discerning similar sizes impossible.
    Exhibit
        - A treemap showing sales by department for all 100 departments
        - A clustered bar chart showing sales by product for all 1000 products
        - A column chart showing sales by customer city for all 300 retail stores worldwide
        Solution
        - You group departments using ***a bin size of 10 and replace the department field*** with the bin on the treemap
        - You add the product category above product in the Axis fieldwell of the clustered bar chart
        - You replace the customer city field with the country field in the column chart
    
    A:
        No
    - NOT This one (Can not bin text, Can group )
    (Adding product category in the bar chart -> craete Drill down chart -> show first product category -> allow user drill down)
    (replace customer region by COUNTRY FIELD reduce scrolling)

    Explan:
    Grouping categorical data is a viable solution in this case, 
    however, 
    you cannot bin a text field, 
    you can group text fields using list instead.

    Adding the product category field above the product field in the bar chart 
    will effectively create a drill-down chart 
    showing first the product categories 
    and 
    allowing the user to drill down into specific categories. This solution will work for the scenario.

    Replacing the customer region field with the country field will also work to alliviate the scrolling, 
    but the analysis is limited to country level of granularity.

    https://docs.microsoft.com/en-us/power-bi/consumer/end-user-drill

Q:
    How many days of question history is stored for questions typed into the ***Q&A fields***?

    A:
        28 days
    
Q:
    While following the principal of least privilege, 
    select the appropriate workspace permission level that 
        allows a user 
        - add new members
        - assign the contributor role
    
    A:
        Member

    Explan
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-new-workspaces#roles-in-the-new-workspaces


Q : 
    Pre-condition
    1. created and published a report you have created for your organisation's data analytics team.
    2. team members (including you) are ***only permitted to publish updated reports*** if you request the change through your organisation's change control system.
    3. Your team ***only has Viewer role*** on the workspace in question.
    intend to do
    1. want to ***allow your team the flexibility to make changes to visuals*** like swap out a ***measures and dimensions*** without going through the change control process.
    2. ***allow this without republishing the report?***
    
    A: 
        Change the report settings to allow Personalize visuals

    Explain :
        - Allowing Personalize visuals allows users to make changes to report visuals without needing edit permissions or republishing the report. 
        - You will need contributor access to the workspace to change this setting.

        Q&A (Viewer Role does not allow change visual in Q&A)
            - Pinning visuals to a dashboard and allowing Q&A will achieve the goal in concept, but does not allow changing the visuals as is requested by the question. 
            - You can use Q&A to create new visuals (and then pin them to the dashboard), but since the team has only viewer role, they won't be able to do this.



    You work for an electric engine manufacturer as a Power BI admin. You have two colleagues, Ray and Jane, who need access to your workspace. Ray will need to publish, unpublish, and change permissions for the apps. Jane needs to be able to publish reports to the workspace and delete content.

    Admin 
        Creating a report
            --->>> another workspace depending upon the dataset of this workspace

        -Create and manage users & groups
        -Reset User passwords

    Admin, Member, or Contributor 
        -lineage view only available

    Contributor (The lowest lvl can)
        - publish reports and delete dashboards within a workspace

    Member
        - assign viewer, contributor, and member roles?

    A Billing Admin 
        -manage subscriptions.

    A Power Platform admin
        -enable and disable Power BI features.

    
Q:
    Your organisation's governance department has published a new policy governing the use of information assets. 
    - implementing the corporate policy in ***Power BI***
    Which of the following must be done to achieve your goal?

    - Enable information protection in the Power bi tenant
    - Create and publish sensitivity labels in the M365 tenant
    - Select the applicable sensitivity labels in the report settings

    Explan:
    https://docs.microsoft.com/en-us/power-bi/admin/service-security-enable-data-sensitivity-labels


Q: (incremental refresh Power BI dataset - require Power BI premium)
    (RangeStart and RangeEnd) - NOT StartRange and EndRange
    Which of the following are mandatory for 
        ***configuring incremental refresh*** for your 
        ***Power BI dataset***?

    A:
        - Define the incremental refresh policy
        - Define the refresh ranges
     
    Explan:
    - require Power BI premium capacity to use incremental refresh
    - should (highly recommended) use a data source that supports ***query folding***, 
        but this is not mandatory
    (No need date)- need a column that contains dates, it doesn't have to be a table marked as the date table
    - need RangeStart and RangeEnd parameters (not StartRange and EndRange)
    - must configure the ***incremental refresh policy and define the refresh ranges in the policy***

    https://docs.microsoft.com/en-us/power-bi/admin/service-premium-incremental-refresh

Q:
    Which of the following report visuals uses ***AI capabilities of Power BI***?

    A:
        - Q&A
        - Key Influencers
        - Decomposition Tree

     AI visuals 
        -> Decomposition Tree 
        -> Key Influencers
    - Q&A visual -> AI visual -> you can add to your reports.  
    - (Not) - Quick Insights -> (not a visual add to your report)  capability in Power BI Service
    
    The Python visual allows you to add your own Python code to create the visual, 
    but does not necessarily include AI.
    https://docs.microsoft.com/en-za/learn/modules/ai-visuals-power-bi/1-introduction
    https://docs.microsoft.com/en-us/power-bi/create-reports/service-insights


AI visuals 
        -> Decomposition Tree 
        -> Key Influencers
        -> Q&A visual, can add to your reports.  
    - (Not) - Quick Insights -> (not a visual add to your report) AI capability in Power BI Service

Q:
    You are ***troubleshooting poor performance*** of visuals in Power BI. 
    You need to use the ***Performance Analyzer*** to troubleshoot performance. 
    Which of the following steps are required?
    
    A:
        - Add a blank report page
        - Restart Power BI Desktop
        - Start recording
        - Refresh visuals
        - Stop recording
        - Review results

    Explan
    ***Performance analyzer*** runs in Power BI and evaluates DAX,
    visual rendering and other aspects of report performance.
    ***Query diagnostics*** runs in Power Query and analyses query (source data interaction) performance
    https://docs.microsoft.com/en-za/power-bi/create-reports/desktop-performance-analyzer
    https://docs.microsoft.com/en-za/power-query/recordingquerydiagnostics

Q:
    - performing long-term trend analysis on the financial transactions of your web retail organisation. 
    - transaction database is extensive and is scoped at a very high level of granularity. 
    - experiencing slow performance and need to optimise the report for performance. 
    -->> perform in the order it is listed?
    
    A:
        - Create an aggregation table named Aggregate
        - Select the transactions table and select Manage aggregations
        - Specify the Aggregate table for aggregation
        - Specify the summarization
        - Specify the transactions table for detail

    Explanation
    -first create an aggregation table containing the columns you want to aggregate
    -select Manage aggregations on the source table
    -specify the target table for aggregation
    -select the summarization (method)
    -select the source table for the detail field

    https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-aggregations

Go -> Manage Aggregations    


Q: 
    |TABLE|Column     |Data Type|
    |Sales|Order ID   |Whole Number|
    |     |Order Date |Date|
    |     |Customer ID|Whole Number|
    |     |Product ID |Whole Number|
    |     |Amount     |Decimal number|
    Total Sales = SUM( Sales[Amount])
    - create a matrix visual
    - shows monthly sales as compared to the previous period.
    Which measure will you use to achieve your goal?

    A:
        Calculate(
            [Total Sales],
            DateDD(Sales[Order Date], -1, Month)
        )
    
    Explan
    - matrix with the ***current month*** compared to ***last month***.
    - SAMEPERIODLASTYEAR shows last year's total, not last month's total
    - PARALLELPERIOD shows the calculation for the follow month, we need the previous month
    - DATEADD is the correct calculation
    - PREVIOUSYEAR also shows the current month from the previous year - not correct
    https://docs.microsoft.com/en-us/learn/modules/dax-power-bi-time-intelligence/
    

SAMEPERIODLASTYEAR - last year's total, not last month's total
PARALLELPERIOD - the calculation for the follow month
PREVIOUSYEAR - the current month from the previous year
(compared to the previous period data)

Q: (Slicer toggle turn on / off)
- creating a collapsible slicer panel on one of your report pages
- Users ***click on a button*** to ***reveal the slicer panel*** from where they can adjust the slicers for your report page. 
- Clicking the button again removes the slicer panel.

When designing the report, 
    which item from the list below will you use to 
        - toggle between the collapsed 
        - revealed state of the panel?

    A:
        Selection Pane > Show
    
    Explan
    configured using the ***selection pane*** at design time -> 
        Showing 
        hiding visuals on your report page is . 
    To create a slicer panel you will be using a combination of buttons (or images), bookmarks, the selection pane, and slicers.
    https://www.youtube.com/watch?v=xy9nmSQeUWg

Selection pane
Slicer Toggle
    -> configured using the selection pane at design time
    -> To create a slicer panel you will be 
        - combination of buttons (or images), 
        - bookmarks, 
        - the selection pane, 
        - slicers
['ODBC Driver 18 for SQL Server']

Q:
    You are investigating ***query performance*** issues for a Power BI dataset. 
    Part of your investigation reveals the information in the exhibit.

    A:
        The data source does not support query folding

    Explan
    https://docs.microsoft.com/en-us/power-query/power-query-folding#determine-when-a-query-can-be-folded

Q:
    ***connection modes*** are available to you 
    when connecting to source data stored in ***Azure Analysis Services***?

    A:
        - Import
        - Connect Live

    Explain:    
    You can specify an MDX or DAX query as part of the connection, 
    however, 
    this is not a connection mode as is asked by the question.
    https://docs.microsoft.com/en-za/learn/modules/get-data/7-azure-analysis-services


Connecting Azure Analysis Services - (Yes for direct query but MDX or DAX query) 
    -MDX or DAX query
    -Import
    -Connect live

Q:
    created & published 
        -> reports & dashboards for your organisation's sales team.
    Data updates frequently, 



    often on an hourly basis and the sales teem needs to keep up to date with the latest developments. 
    One of the dashboards you created has a KPI visual that is particularly important for your sales team. 
    They want to receive a notification when the value of this visual exceeds a threshold.
    What options do your sales team have for receiving notifications?

    A:
        Power bi Moblie App
        Email
        PowerAutomate flow
    
    Explan
    https://docs.microsoft.com/en-us/power-bi/consumer/end-user-alerts
    https://tools.ietf.org/html/rfc1149

Q:
    You have created and published reports and dashboards for your organisation's sales team. Data updates frequently, often on an hourly basis and the sales teem needs to keep up to date with the latest developments. One of the dashboards you created has a KPI visual that is particularly important for your sales team. They want to receive a notification when the value of this visual changes or remains unchanged.
    Which of the following will you configure?

    A:
        - Add a subscription

    Explanation
    You need the notification even if the data doesn't change - this is a subscription. 
    If you need a notification if the data goes over or under a threshold, you need an alert.
    https://docs.microsoft.com/en-us/power-bi/consumer/end-user-subscribe
    https://docs.microsoft.com/en-us/power-bi/consumer/end-user-alerts

Q:  
    Data Source
    |||||
    You create a Power BI report and individual visuals referring to each of the tables individually and save the .pbix file to OneDrive. A few weeks later, you open the .pbix file from a different machine.
    How up to date are you expecting the data to be for each of the following visuals? (Choose 3)


    A:
        (Azure SQL Database) - Sales viusals have up-to-date data as per the data source 
        (Excel) - Product visuals have data from when the data source was connected
        (Excel - OneDrive) - Customer viusals have data from when the refresh button was las activated 

    Explanation
    Dual storage mode is a Direct Query storage mode plus allowing Power BI to cache data at its discretion. Direct Query will refresh the data source when the file is opened and ensure up-to-date data is displayed.
    Since there is no more access to the local Excel file for the Product table and we are using import mode as the storage mode (naturally, it can't be anything else for Excel), the Product table cannot be refreshed and will stay as up to data as when it was imported. Pressing the refresh button will fail because the data source cannot be found.
    The Customer table will be accessible from the new location since it is shared from OneDrive. It will refresh when you click the refresh button. However, since it is in import mode, it won't be up-to-date as is the case with Direct Query (or dual) sources.
    https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-storage-mode

Q:
    Data Source
    |||||
    You need to create a matrix visualisation that shows each year and month in a column and an accumulating sales total for the year - example in the exhibit.
    Matrix with Year & Months Revenue figure
    How can you use a quick measure to accomplish your task?  (Choose 3)

    A:
        Calculation = Year-to-date total
        Base Value = Sales[Sales amount]
        Extended field = CalendarDim[Date]    

    Explanation
    https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-quick-measures

Q:
    You are creating a dataflow in Power BI. How is data stored? (Choose 3)

    A:
        - Plaform: Azure Data Lake storage Gen2
        - Container: Common Data Model Folders
        - Data : Entity

    Explan
    https://docs.microsoft.com/en-us/power-bi/transform-model/dataflows/dataflows-introduction-self-service
    https://docs.microsoft.com/en-us/powerapps/maker/data-platform/data-platform-powerbi-connector

###### Automatic page refresh / scheduled daily refresh database
-----------------------------------------------------------------------
Daily refresh database
    (No premium) - 4 times per day
    (normal)- 8 times per day for a normal workspace
    (premium)- 48 times for a workspace backed by premium capacity.

Daily refresh database (No Power BI Premium)
Q: 
    You are configuring a scheduled daily data refresh for your dataset in the Power BI Service. 
    How many times per day can you refresh your dataset? 
        (You do not yet have Power BI Premium capacity allocated to the workspace where the dataset is located.)

    A:
        4 times per day

    Explain:
        8 times per day for a normal workspace; 
        48 times for a workspace backed by premium capacity.
        License level is irrelevant for scheduled data refresh; 
        Pro license is required for access to a shared workspace.
        https://docs.microsoft.com/en-za/learn/modules/manage-datasets-power-bi/5-dataset-refresh

    Configure Power BI report page

    https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-automatic-page-refresh


Queries refresh setting 
Q: prevent certain queries from refreshing when you click the Refresh button from the Home tab in Power BI Desktop?

    A:
        In Power Query, right click the query, un-check include in report refresh.

    Explain:
        There is no drop-down menu under the refresh button in Power BI Desktop, nor is there a Allow data refreshes check-box.
        The refresh button in Power BI Desktop 
            refreshes all queries that have Include in report refresh enabled in Power Query - it doesn't care about what visuals are on the page. 
        All visuals are also refreshed once the queries are refreshed.
        https://docs.microsoft.com/en-us/power-bi/refresh-data


Q : table storage mode should you choose?
    - Optimise query performance
    - Large data set
    - Near-realtime source telemetry

    A:
        Dual

    Explain :
        -Import is best for query performance due to caching
        -DirectQuery is best for ***large data set and Near-realtime***
        =Dual is best when all three requirements is needed

        There is no cached storage mode. Import and Dual will cache, but not DirectQuery

        https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-storage-mode


Q : following features are ***available*** to you when using the ***filter panel***?

    A:
    - Disallow users to change a filter you added
    - Make a filter you added invisible to users
    - Adjust the appearance of the filter pane
    - Use a single apply filters button for all filters

    Explain :
        Filter pane guide : https://docs.microsoft.com/en-us/power-bi/create-reports/power-bi-report-filter


Q: available connection modes -> connecting to source data stored in ***Azure Analysis Services***?

    A: 
        Import 
        Connect live
    
    https://docs.microsoft.com/en-za/learn/modules/get-data/7-azure-analysis-services


How to go power query?
    -> Transform data

How to create a manual table? / How to edit an existing table?
    -> Enter data / -> click the table you want to edit -> click the gear

Q: Power Query to connect to a new data source
    - no check on Type detection
    -  data type of the ***Product ID column*** (Product ID is number) after transformation 
        - all columns and select Transform > Format > Trim
        - the Date column and change the data type to Date.
        - Transform > Detect Data Type

    A: Product ID column - > Text data type 


Q: Power Query Connect new data?
    What is the data type of the Product ID column after you apply the following transformations:
        - You select all columns and select Transform > Format > Trim
        - You select the Date column and change the data type to Date.
        - You select Transform > Detect Data Type

    ProductID  -> 
    1
    2
    3
    1
    1
    3

    A: TEXT data type

    The Detect Data Type button only detects data types for the currently selected columns. 
    Since at the time of clicking the Detect Data Type button, only the date column is selected, 
    Power Query is not going to detect the data type of the Product ID column. 
    If all columns were selected, the detected data type will be Whole number, especially after trim was performed.


Q:
    You are sent an Excel file containing data by a colleague.  
    You want to analyse the data in Power BI Desktop.  
    Reviewing the content in Excel reveals that substantial data cleanup would be required.

    A:
        Normalise, clean and load the data in Power Query
    
    Explan:
        Data normalisation is the practice of arranging unstructured or semi-structured data in to structured tables 
        where columns contain the same data types and data is arranged rows of attributes. 
        Data cleansing refers to changing the data types or item contents to fit with the columns created during data normalisation.
        You would typically perform cleansing after normalisation.
        It is not considered best practice to any data manipulation (normalise and/or clean) in Excel,
        because it would require the same manual process each time data is updated.
        There is no automatic data normalisation or cleanup in the Power BI Service.
        Power Query is the preferred tool used for data manipulation; 
        some data manipulation can also be done in the data model, 
        but this is to be avoided and therefore not the best answer. 


###### Import / dual / direct query
Q: 
    - Using Power Query to connect to a data source in SQL Server. 
    - don't want to load the data from the server into the Power BI Desktop data model,
    - but would rather like Power BI to query data on the server in real-time. 
    Which of the following options do you select?

    A:
        Direct Query

    Explan
    DirectQuery is the correct response. 

    - ActiveSync 
        is mobile device data synchronisation tool. 
    - Live connection 
        is similar to DirectQuery and is used with SSAS, not SQL.
    
    SQL Server and Azure SQL Database supports DirectQuery.
    https://docs.microsoft.com/en-us/power-bi/desktop-directquery-about


Q:  (Connect Dataverse)
---------------------------
    Strip out 
        1. https:// 
        2. trailing /
You are connecting to data that is stored in your organisation's Common Data Service. 
You retrieve the Instance url from your Power Apps environment as shown in the exhibit.
    https://org077bbf3e.crm4.dynamics.com/
Configure the Dataverse connector in Power BI to connect to this environment?

    A:
        org077bbf3e.crm4.dynamics.com

    Explain:
        You should strip out 
            the https:// and the trailing / from the Instance url 
            when configuring the connector
        https://docs.microsoft.com/en-us/powerapps/maker/data-platform/data-platform-powerbi-connector


Q : Where do you enable Top-N statistical analysis?

    A: Filter Pane

    Explain:
        https://powerbidocs.com/2020/01/21/power-bi-top-n-filters/


#### Dashboard / Matrix / reporting / format cell

Sort Matrix by SubCategories
----------------------------------------------------
    Go -> ... -> Sort by (Choose the value)
    https://community.powerbi.com/t5/Desktop/How-to-Change-Sort-in-Sub-Categories/td-p/2244861


Q: Table visual is using Color1 in its Values fieldwell.
    - How to conditional formating configured?

    Table
    
    |Color1|Color2|Color Code|
    |RED| White|#80080|
    |Orange| black|#ffff00|

    A:
        - Background Color > Format by = Field value
        - Background Color > Based on field = First Color1

        - Font color > Format by = Field value
        - Font color > Based on field = First Color Code

    Explain:
        Background + Font 

        ***Based on field*** option for conditional formatting in the table visual.
        
        Based on field will interpret the field value being 
            displayed and 
            apply the color name or 
            color code 
            in the field to either the background color or font color respectively. 

        Color1 column is used for background colors based on the field value
        Color2 column is used for the font color based on the field value
        Color Code is not used in our example, but would be honoured if chosen as the based on field.

Q:  
    troubleshooting poor performance of visuals in Power BI. 
     ***evaluate*** your report's interaction with the data source to troubleshoot performance.
     Which of the following steps are required?

    A:
        - Options > Diagnostics > Query Diagnostics > Enable in Query Editor 
        - Start Diagnostics
        - Refresh data
        - Stop diagnostics
        - Review Results


    Explan:
    Performance analyzer runs in Power BI and evaluates DAX, 
    visual rendering and other aspects of report performance.
    Query diagnostics runs in Power Query and analyses query (source data interaction) performance
    https://docs.microsoft.com/en-za/power-bi/create-reports/desktop-performance-analyzer
    https://docs.microsoft.com/en-za/power-query/recordingquerydiagnostics

Q:
    - performing long-term trend analysis on the financial transactions of your web retail organisation. 
    - The transaction database is extensive and is scoped at a very high level of granularity. 
    - experiencing ***slow performance*** and need to optimise the report for performance.
    Which of the following actions should you perform?

    A: 
    - Adjust the data query to include aggregation at the month-level
    - Adjust the table storage mode to Dual

    Explanation
    For very large datasets one should try to 
    ==> ***reduce the granularity of the data (reduce the number of rows)*** 
    Moving to 
    ==> DirectQuery (or dual) storage mode 
        will offload the workload to the data source system 
        that is presumably optimised for the dataset.
        
    Reducing the number of visuals per page will ***not*** have a significant impact on performance in this scenario because of the very large dataset.
    ===> Hiding columns in the model has ***no performance*** impact and is done for ease-of-use reasons
    https://docs.microsoft.com/en-us/power-bi/guidance/power-bi-optimization

    Not improve performance 
        -Reducing the number of visuals per page
        -Hiding columns in the model

Q:
    You are exploring a new dataset you have connected to and using 
        column profiling to get a better sense of column statistics and value distributions.
    The column profile is based on a subset of the rows in the column.
    How can you configure the column profiling in this regard?

    A:
    - Base on the first 1000 rows
    - Base on the entire dataset
    
    Explain:
    First 1000 or entire dataset is available
    https://docs.microsoft.com/en-us/learn/modules/clean-data-power-bi/6-profile-data


Q:
    - configuring Row-Level Security in Power BI.
    - need to define which rows of the dataset will be available to the role.
    Which of the following will you create?

    A:
        DAX expression
    
    Explanation
    https://docs.microsoft.com/en-za/power-bi/guidance/rls-guidance

Q:
    |Table  |Column       |Data type   |
    |Sales  |Date         |Date        |
    |       |Sales OrderID|Whole number|
    |       |Quantity|Whole number|
    |       |Product ID|Whole number|
    |       |Sale amount|Decimal number|
    |       |Cost code|Text|
    |       |Sales Person ID|Whole number|
    |Product|Product ID|Whole number|
    |       |Product Name|Text|
    |       |Product unit cost|Decimal number|

 configure the default summarisation mechanism for implicit measures that uses the columns.
    Which would you choose for the listed columns?  (Choose 5)

    A:
    -Date = Don't Summarize
    -Sales Order ID = Count
    -Quantity = Sum 
    -Sale amount = Sum
    -Product unit cost = Average

    Explanation
    - Don't summarize dates.
    - Count IDs (or rows).
    - Sum quantities and amounts in fact tables.
    - Average amounts in dimension tables.

    https://docs.microsoft.com/en-za/power-bi/create-reports/service-aggregates


Q: 
    Which of the following visuals 
        ***allows you*** to ***change*** the ***source data*** used in a Power BI report?

    A:
        Power Apps
    
    Explanation
    https://docs.microsoft.com/en-za/power-bi/visuals/power-bi-visualization-powerapp        


(Coloring Table)
Q:
    |State|Weather|Affordability|Overall rank|
    |Hawaii|1     |45   (Red)   |10         |
    |Florida|1    |25   (Red)   |5          |
    |Louisiana|1  |29   (Red)   |36         |
    |Hawaii|1     |24  (Yellow) |17         |
    |Hawaii|1     |19  (Blue)   |28         |
    |Hawaii|1     |6   (Blue)   |19         |

    How to color the cell base on value

    A:
    - Conditional formatting = Background
    - Format by = Rules

    Explan
    https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-conditional-table-formatting


Q:
    While following the principal of ***least privilege***, 
    select the appropriate workspace permission level that 
        1. allows a user to create content
        2. publish an app that contains the content
    
    A:
    Member

    Explanation
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-new-workspaces#roles-in-the-new-workspaces


Q:
    Which options are available to you for the ***promotion of datasets*** for your organisation in Power BI?

    A:
        1. Promoted
        2. Certified

    Explanation
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-endorse-content


Q:
    You are the ***administrator*** for your organisation's Power BI adoption project. 
    Your organisation wants to prevent a specific list of users from creating workspaces. 
    - use as few as possible steps from the list below.
    1) Open the M365 admin centre
    2) Select authorised users
    3) Select unauthorised users
    4) Add the security group
    5) Select the specific option
    6) Navigate to tenant settings > Workspace settings
    7) Select enabled
    8) Open the Power BI admin centre
    9) Create a security group
    10) Select the entire organisation option
    11) Select the except specific option
    12) Select Apply

    A:
        1,9,2,8,6,7,5,4,12

    Explanation

    The workspace settings in the 
        ---> Power BI Admin centre allows you to select who is allowed or prevented from creating workspaces. 
        By default everyone in the organisation (license permitting) can create workspaces.
    - only specify the entire organisation or a specify a specific security group.  
    - do this from either an allow or a prevent perspective, the latter using the except specification. 
    - ***cannot*** specify individual users in this area, so you have to do the group creation steps.
    Using the preventative approach (users not allowed) requires more steps in this scenario than to use the users allowed list of steps.

    https://docs.microsoft.com/en-us/power-bi/admin/service-admin-portal#create-the-new-workspaces

Q:
    Which of the following measures will increase data model performance?

    A:
    - Summarise and aggregate data on a query-level
    - Remove unused columns using data view in power bi
    - Remove unused columns using Power Query

    Explanation
    Removing unused columns from the data view in Power BI has the same effect as doing it from Power Query.
    Hiding columns doesn't improve performance, it just makes the model easier to use for report developers.
    (Not optimise the data model)Reducing the number of visuals on a page will have an overall positive effect on report responsiveness, 
        but doesn't optimise the data model in any way as per the question
    https://docs.microsoft.com/en-za/learn/modules/optimize-model-power-bi/1-introduction

(Q&A feature -> Power BI dashboard)
Q&A visual and Q&A feature is different
Q:
    Which of the following measures would contribute positively to being able to ***successfully use the Q&A feature*** on your Power BI dashboard?

    A:
        - Add Synonyms to the tables in the model 
        - Configure the row label for fact tables in the model
        - Define nouns adjectives

    incorrect --> adding a (Q&A visual) to the report 
        NOT affect the use or training of the ***Q&A feature***

    Explan
    Q&A feature
    - Use in Power BI Service dashboards
    - Q&A visual -> can use in reports
    train the system in the same way & the data model changes is universal -> Q&A visual or Q&A feature on the dashboard
    dashboard -> 
    adding a Q&A visual to the report will not affect the use or training of the Q&A feature and is therefore the only incorrect answer.
    https://docs.microsoft.com/en-za/power-bi/natural-language/q-and-a-intro
    https://docs.microsoft.com/en-za/power-bi/natural-language/q-and-a-tooling-teach-q-and-a

Q:

Scenario
have a Sales table that 
    contains two date columns: [Order Date] and [Ship Date], 
    each with a relationship to a ['Calendar'] table, as shown in the exhibit. 
    The active relationship is on the [Order Date] column.


Calendar                                Sales
--------------------                  ------------------------
- Calendar Year                              - Customer ID          
- Date              Active relationship -->  - Order Date
- Fiscal Month Number                        - Order ID
- Month Number                               - Product ID
                                                - Qty
                Inactive relationship --->   - Ship Date
                                                - Total deliveries
                                                - Total sales

create a visualisation that displays 
    1. the quantities ordered 
    2. delivered per day 

(Don't know either Sales date contains all date of each of the column)

- 'calendar'[date] -> presumably contains the entire date range from the sales table
- CAN NOT use two date columns in the 'sales' table -> don't know if there are orders or deliveries on all days.
Q1  
    Which field will you choose for the ***Axis*** of you area chart?    
        
        A:
            Calendar[Date]

        Explan
        1. use the 'calendar'[date] column -> presumably contains the entire date range from the sales table
        cannot use 
            either of the two date columns in the sales table 
                ---> since you don't know if there are orders or deliveries on all days.

Q2
    Which field well will you use for the [Total Deliveries] measure in the area chart?
    (don't need to place the deliveries on a secondary values)

    A:
        Values

    
    Explain
    add both the [Total Sales] and [Total Deliveries] measures in the Values filed well of the area chart. 
    don't need to place the deliveries on a secondary values 
    because 
        ---> both measures use the same scale and is summing the same column.


Q:
    How would you resolve the error ?
        !! Sheet1 
        Could Not find file [Path].xlsx

    A:
        - Click Data source settings
        - Choose Scoresheet.xlsx
        - Click Change source
        - Specify the correct path to the source file
        - Click OK
    
    Explanation
    Two ways will work: 
    1. Transform data > Sheet1 > Source settings > Path > OK > Close
    2. Apply Data source settings > Scoresheet.xlsx > Change source > Path > OK
    The second option has fewer steps


Tips :
    AVERAGE 
    - take zeros as valid data points to consider in the calculation.
    - ignore null values.


Q: 
    In which of the following areas can you NOT use natural language analytics?

    A:
        - None of the options


    Explain
    Natural language analytics is the Q&A feature. 
    Can 
    - (unpublished) Power BI Desktop
    - (published) Power BI Service ***reports***.  
    It can be used on a dashboard in Power BI Service and also in Power BI embedded.
    https://docs.microsoft.com/en-za/learn/modules/ai-visuals-power-bi/1-introduction

(apply ML - text analytics)
Q:
    Where would you 
        ***apply pretrained machine learning models*** -> ***text analytics*** to your data as part of data analytics in Power BI?

    A:
        Power Query
    
    Explan
    https://docs.microsoft.com/en-za/learn/modules/perform-analytics-power-bi/10-ai-insights


(Use Histogram -> need to bin data first)
Q:
    Which Power BI Desktop feature will you use to show a histogram of a data point using a standard column chart?

    A:
    New Group

    (Binning - Grouping)
    Explain:
    The Histogram chart in AppSource does it's own binning (Grouping).

    To create a histogram by column chart
    --> create your own bins using the new group feature
    https://docs.microsoft.com/en-za/learn/modules/perform-analytics-power-bi/2-statistical-summary

Q:
    T/F: Workspace contributors can configure data refreshes?

    A:
    True

    Explain
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-new-workspaces#roles-in-the-new-workspaces


Q:
    Which of the following custom visuals are supported in Power BI Desktop?

    A:
        -R
        -Python
        -NodeJs
    
    Explain
    Custom visuals in Power BI is created using the SDK which is based on NodeJS. You can also use custom R and Python visuals.
    https://docs.microsoft.com/en-us/power-bi/developer/visuals/power-bi-custom-visuals
    https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-python-visuals
    https://docs.microsoft.com/en-za/power-bi/create-reports/desktop-r-powered-custom-visuals?toc=/powerbi-docs/developer/TOC.json&bc=/powerbi-docs/breadcrumb/toc.json
        

Q:
    data analyst for an online retail company
    - connected to the company's transactions database 
    - several other related dimensions 
    - created a data model in Power BI.
    --> Analyse the possible reasons for the apparent rise in revenue after the decline shown for Oct 1998.    
    Solution
    - You right-click the last marker on the visual
    - You select Analyse > Explain the increase
    - You select Add to page

    A:
        No

    Explanation
    The steps are correct, however, 
    you would want to analyse the second-last data point on the chart to explain the increase.
    Although the last data point might reveal some important insights for the continued increase,
    the analysis calls for 
        explaining the ***increase right after the decrease***.

    https://docs.microsoft.com/en-us/power-bi/consumer/end-user-analyze-visuals

Q2) :
    Solution
    - You select the Q&A visual from the Visualizations pane
    - You type the following question into the Ask a question about your data field: "analyze total revenue by calendar year and calendar month"
    - You review the results

    A:
        No
    
    Explan
    Adding the Q&A visual.
        - Q&A visual don't understand the "analyze" verb
        - Q&A visual cant be taught VERBS
        - Q&A visual NOT provide the analysis & using the analyze feature of Power BI Desktop
    
    https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-q-and-a


    Explan
    There is a possibility that Quick insights may pick up on the anomaly and explain it as is the case with the Analyze > Explain the increase feature in Power BI Desktop.  
    However, in our testing, Quick insights did not even reveal the increase, let alone the reasons for the increase.  
    Depending on the data model, your experience may differ. 

    It is important to note, however, that Quick insights is analysing the entire dataset to find correlations and anomalies - 
    it is not trying to explain specific data points as is the case with Analyze > Explain.  
    So regardless of the results, the idea here is to understand that Analyze > Explain is a highly targeted AI analysis, whereas Quick insights is a more general interpretation.
    https://docs.microsoft.com/en-us/power-bi/create-reports/service-insights


Q:
    |Table name |Column Name    |Data type   |
    |Employee   |Name           |Text
    |           |Department ID  |Whole Number
    |           |Manager        |Text
    |Department |Department ID  |Whole Number
    |           |Department Name|Text
    |           |Cost Centre    |Text

Data model information
There is an ***active relationship*** between 
     Department ID - both tables. 
     There can be multiple employees in a single department.

RLS for Own Departments

Objective
Your goal is to implement Row-Level Security (RLS) for the report 
- managers can only see department information for their own departments.

configure the data model to achieve your goal?
  
    A:
        - Set the relationship cardinality to one-to-one
        - Set the cross filter direction to both
        - Set the security filter direction to both

    Explain:
        In this scenario the relationship between the tables are one-to-many, 
        with department on the one side and employee on the many side. 
        This is because the department table has unique department IDs and the same column in the employee table will have duplicate department IDs.

        By default the cross filter direction is from the one side to the many side - from department to employee.
        You want to configure RLS on the employee table - therefor on the many side.

        Since the filter direction is one to many, 
        any filters applied to the many side (employee table) will not propagate to the one side (department table). 
        RLS will filter the employee table, 
        but the unfiltered department table will still be visible.

        To fix this problem, 
        you have to change the cross filter direction to both and also check the apply security filter in 
        both directions checkbox.

        https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-create-and-manage-relationships
        https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-relationships-understand
        https://docs.microsoft.com/en-us/power-bi/guidance/rls-guidance

Q:
    Analysing sales data for a customer and have created a report with two report pages, 
    each with different sales perspectives. 
    When select a sales person on one of the pages, 
    want the other page to also only display sales related to the selected sales person.
    How can you accomplish your goal? (Choose 2)

    A:
        - Add a slicer for the sales person on both pages and configure sync
        - Add a report-level filter in the filter panel for the sales person field

    Explain:
    Sync slicers is the obvious answer. Get the sync slicers panel from the View menu.

    To get all visuals on both pages to respect the filter panel setting, you have to apply it using the report-level (all report pages) filter in the filter panel. Page-level filters only affect the current page - if you add the filter to both pages, they won't be synched.

    Bookmarks snapshots of a current view of a page. Bookmarks are created per page (not per report) and will not affect slicers or visuals on other pages.

    Edit interactions only works on the current page, not across pages.

    https://docs.microsoft.com/en-za/power-bi/visuals/power-bi-visualization-slicers#sync-and-use-slicers-on-other-pages
    https://docs.microsoft.com/en-us/power-bi/consumer/end-user-report-filter

Q1:
Scenario
    - Connect to a data source in Power BI Desktop
    - (Table)Customers -> two columns -> [Customer Name] and [Birthdate]
Exhibits
    Power Query add a column using the M code -> close and apply the transformation
        
        = Table.AddColumn(#"Changed Type", "BirthYear", each Date.Year([BirthDate]), Int64.Type)

From the data view in Power BI Desktop, add a column using DAX code as in the exhibit.
        
        BirthYearCC = Customers[BirthDate].[Year]
        
Action
    - delete the [BirthDate] column.
(Is this True/False)Statement
    1. Deleting [BirthDate] column
    2. [BirthYear] column (contains the ***year component*** of the [BirthDate] field)
        
    A: 
        True
    
    Explain:
    Transformations made in Power Query is applied in serial (one after the other) & 
    no dependencies are created on the columns the transformation derives from. 

    TRUE --> even if the transformations are made from within Power BI 
    (see previous point regarding Power BI adding applied steps to the Power Query applied steps for transformations made in the data view in Power BI).
    
Q2:
    (Is this True/False)Statement
        BirthYearCC = Customers[BirthDate].[Year]
        [BirthYearCC] column contains only the year component of the [BirthDate] field

    A:
        False
    
    Explanation
    Since [BirthDate] has been deleted, the calculated [BirthYearCC] column - error will be displayed
    Unlike Power Query applied steps, DAX calculated columns retain their dependency on deriving data columns.
    
***Power Query applied steps*** -> retain their dependency on deriving data columns

Q:
    -Exploring the data in a new data source you want to use in an analysis. 
    -Review statistical information about the data in each column. 
    interested in the ***percentages of valid***, error and empty cells in the columns.
    Which of the following tools would you use to accomplish your goal?
    - statistical information 
    - percentages of valid, error & empty

    A: 
        View > Column quality

    Explain
    https://docs.microsoft.com/en-us/power-query/data-profiling-tools

Q:    
    techniques -> Power Query use to improve performance of interacting with data sources that uses DirectQuery?

    A:
        Query folding
    
    Explanation
    https://docs.microsoft.com/en-za/learn/modules/get-data/8-performance-issues


Q:  (query languages -> Azure Analysis Services -> MDX & DAX)
    query languages -> interact with -> ***Azure Analysis Services*** from Power BI?

    A:
        Muti-Dimensional Expression (MDX)
        Data Analysis Expression

    Power Query NOT a query language

    To query
    -MDX
    -DAX 
    https://docs.microsoft.com/en-za/learn/modules/get-data/7-azure-analysis-services
    https://docs.microsoft.com/en-us/azure/analysis-services/analysis-services-connect-pbi

Q:
    DirectQuery access your source data
        - ensure always up-to-date data
        - time-sensitive report
    Problem
        -lag time for accessing data
        -simple visuals severely hampers the performance of your report

improve the performance of your report?

    A:
        Change the storage mode of the table to dual
    
    Explain
    (Query folding) always used (if available), cannot be disabled or enabled if the data source doesn't support it.
    
    storage mode -> import will improve report performance
        - expense of refresh interval
        - not the best option for maintaining the always up-to-date requirement for the time-sensitive report.
        - NO cached mode for storage mode
        (SQL Server Analysis Services only Live connection)- Live connection (and import) is only available for SQL Server Analysis Services, Azure Analysis Services or Power BI Dataset.  
        DirectQuery and Live connection is mutually exclusive.  

        Depending on the source data system, 
    you can choose between DirectQuery and Import or Live connection and Import, 
    but you cannot select between DirectQuery and Live connection.
        
    Storage mode of dual is the best answer 
        because it allows ***Power BI to cache certain parts*** of the data depending on context.
    This will effectively improve performance as described in the scenario
    https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-storage-mode
    https://docs.microsoft.com/en-us/power-bi/guidance/power-query-folding
    https://docs.microsoft.com/en-za/learn/modules/get-data/6-storage-mode


Q:
    Scenario
        workspace 
            - add several of the members of your analysis team to the workspace.
            - Your team uses Power BI Desktop to connect to data sources in your organisation 
            - data sources in Power BI that have been (certified).
            - Your team publishes several reports to the workspace 
            - configure ***scheduled data refresh*** for the data sources that uses ***the import table storage mode***.
            - create a dashboard by ***pinning visuals from the reports***.
            - publish an app that 
                a. includes only the dashboard element from the workspace 
                b. configure the permissions as in the exhibit.    

POWER BI App
    Setup       Navigation      *Permission(Selected)
-
    Access
        ( )- Entire organization
        (X)- Specific individual group
            [SalesAgents]
Q
***
Event
    The source data is update
***
    A:
        The app is automatically updated

    Explan
        https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-create-distribute-apps

Q
***
Event
    The data source is updated in a report
***

    A:
        The app must be updated manually by selecting the Update app button
    
    Explanation
    workspace -> staging area for changes made to the components (datasets, reports and/or dashboards)
    
    - Updating a data source(different database or file path)
        a. change to the report in the workspace
        b. require an app update to push the change to users
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-create-distribute-apps


Q
***
Event
    A visual in a report is updated
***

    A:
        The app must be updated manually by selecting the Update app button

    Explanation
    workspace -> staging area for changes made to the components (datasets, reports and/or dashboards)
    - Updating a visual in a report 
        a. make the change to the report in the workspace
        b. require an app update to push the change to users
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-create-distribute-apps


Q
***
Event
    The SalesAgents group has been changed to include more users
***

    A:
        The app is automatically updated

    Explanation
    Any changes to the group membership(app has been published)
        - does not require republishing of the app
        - app will simply become available to the new users
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-create-distribute-apps
    

Q
***
Event
    One of your pinned visuals are changed from a pie chart to a ***treemap***. 
Additional instructions
    Select all the update actions you have to perform so that the members of the SalesAgents group will see the change.
***

    A:
        - Delete the tile that containsthe pie chart from the dashboard
        - pin the treemap to the dashboard
        - update app

    Explan
    underlying data of a pinned visual changes
        - the visual on the dashboard is automatically updated (how else will dashboard alters function).  

    Pinned visual on the dashboard remains unchanged
        - if the visual on the report -> tile was pinned from changes
        - will still continue to be updated provided that the data source keeps refreshing.
    https://docs.microsoft.com/en-us/power-bi/create-reports/service-dashboard-tiles
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-create-distribute-apps

Q:
    Which of the following actions are required 
    to create a visual tooltip for a visual (Bar chart) in your Power BI report page (Analysis)?

    A:
        - Insert > New page > Blank page > Page 2
        - Page2 > Format > Page size > Tooltip
        - Page2 > Format > Page size > Tooltip > On
        - Page2 > Insert > New visual
        - Analysis > Bar chart > Format > Tooltip > Page > Page2

    Explanation
    https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-tooltips


Q:
    senior data analyst (Jedi Master) in your organisation. 
    number of analyst interns -> 
        a. started with your department
        b. mentor them in the ways of the force (Power BI).
    Give A file
        1. use in Power BI desktop
        2. connect to a sample data set
        3. specify their own credentials when connecting to the data source
        4. create their own data models and visualisations

What type of file will you give them?  

    A:
        .pbids

    Explanation
    .pbix -> default file format as Power BI Desktop report
        - contains the connection strings, data model, visualisations and any imported data.
        - save a Power BI report -> template file 
            - include the connection strings, 
            - data model 
            - visualisations
            - NOT the actual source data.

    .pbiviz
        - save a custom visual you created in a development environment.
    .pbids
        - the connection strings
        - NOT the data models
        - visualisations or source data. 
    
    https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-data-sources#how-to-create-a-pbids-connection-file
    https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-templates
    https://docs.microsoft.com/en-us/power-bi/developer/visuals/environment-setup



Q:
     analytics for the sales department in your organisation. created the chart including a forecast
    (End 3 months has shade of forecast)

    A: 
        Forecast lenght > 3 month(s)
        Ignore las > 3

    Explain:
        Forecast lenght - 3
        Ignore last - 3 
        Confidence Interval 95%
        Seasonlity (Auto) Points


    https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-analytics-pane#apply-forecasting

Q:
    You are performing time-series analysis of your organisation's sales data. 
    You sales team asks you to help then compare 
        ***quantities of products sold ***
            and 
        *** returned over time. ***
    You have already created the visual as shown in the exhibit.
        
    A:
        - Legend > product_brand
        - X Axis > Quantity Sold
        - Y Axis > Quantity Returned
        - Size > Total Revenue
        - Play Axis > Start of Month (Play axis - Date)

    Explain:
        Use the displayed tooltip and the scale of the axis to determine which measure is on which axis.
        In our case Quantity Sold is on X and Quantity Returned is on Y. 
        Since there are different coloured data points displayed, we must have a legend configured.  
        This is again revealed by the tooltip - product_brand is the legend.
        The bubbles differ in size, therefore needs a numeric field - looking at the tooltip, this must be Total Revenue. 
        Lastly, Play axis needs a date.  
        The only date in the tooltip is Start of Month, so we'll go with that. 
        Below is the configuration of the visual as confirmation.  
        
        https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-scatter
        https://docs.microsoft.com/en-us/learn/modules/perform-analytics-power-bi/6-time-series-analysis

Q: 
    - Pattern & trend analysis. 
    - use ***animation*** to show changes over time

    A: 
        - Add the Play Axis (Dynamic Slicer) visual from AppSource
        - Add a Scatter chart & set the Play Axis option 

    Explain:
        - scatter chart has a built-in play axis,  
            you can step through a time series using the Play Axis (Dynamic Slicer) visual from App Source.

        - (Play Axis - slicer to achieve the animation) Adding the date to the X-axis will work (continuous or not) 
            but you'll also need the Play Axis to step through the slicer to achieve the animation.

        - Adding ***relative date slicer*** does ***not*** do automatic ***animations***

        - Adding a series of bookmarks will be impractical for a large date range. 
            Also, the bookmarks do not automatically animate in view mode, you have to advance them manually.

Question :
    sales data by day in a time series chart
    --->produce-> a **25 day forecast** with a **90% confidence interval** as per the below exhibit. 
    --->ignore-> data anomalies in the last 5 days of data that you want to ignore for the forecast.

    Ans : analytics pane and under forecast select ‘+ Add’

        -Go to analytics pane & under Select '+Add'
        -Set forcast length to 25 points & ignore last 5 points
        -Set the confidence interval to 90% and click on apply

Question : 
    1.have a time series chart
    2. need to display a line to show the direction the data has moved over your selected period.
    --> add this black dotted line? 

    Ans: add a Trend line in Analytics pane

    Power BI provides options to draw a trend line for visualizations 
        -scatter plot charts
        -line charts. 
            --->> add a Trend line
                    --> Analytics pane --> add a Trend line

    NOT :
        -average line --> give a horizontal line that averages the data values
        -forecast line --> historical data and estimates future values using a "triple exponential smoothing algorithm".
        -add a PlayAxis --> create an animation of a scatter chart across time
    
Q: 
    Which term best describes the process of transforming a table 
        ->> from a horizontal orientation 
            to 
            a vertical orientation 
            by 
            turning distinct column values into rows?

    A: 
        Unpivot

    Explan
    Pivot 
        rows into columns by splitting unique values 
            from the selected column into additional columns. 

    Unpivot 
        columns into rows by repeating the row 
            for each of the selected columns.

    Transpose 
        changes the orientation of the table without rearranging the values. 

    https://docs.microsoft.com/en-us/power-query/unpivot-column


###### Power Query Editor-> Column quality vs profile vs distribution / cardinality
###### column distributions / Data Profile /  profiling source data 
--------------------------------------------------------------

    In transformation / power query -> view ->
    - Column Distribution
        -number of distinct
        -number of unique

    - Column profile
        -Column statistics 
            - Count, Error, Empty, Distinct, Unique, Min, Max, Avg
            - Value distribution

    - Column Quality
        - (Percentage of)
            1. Valid
            2. Error
            3. Empty

Q:
    - exploring new dataset, understand how many empty and error rows vs. valid rows

    A:  
        - Column profile
            gives you a quick view of empty, error and valid.

        - Column Quality
            gives you a ***more extensive view*** of empty, error, valid and other detail for the currently selected column

Q:
    Which column in the exhibit has the highest cardinality?
    - ***Add distinct and unique counts together***. ***High answer = high cardinality*** and vice versa.
    - Lower cardinality increases performance.
        https://docs.microsoft.com/en-za/learn/modules/optimize-model-power-bi/4-reduce-cardinality

    e.g. 
        1 Distinct 0 unique| 4 Distinct 4 unique| 2 Distinct 0 unique
        Col 1              | Col 2              |  Col 3
        1                   a                    a
        1                   b                    a
        1                   c                    b
        1                   d                    b

Q:     
    distinct value vs unique value 

    “Distinct”
        - total number of different values regardless how many times it appears in the dataset.
        - A name appears in the list multiple times is counted as 1 distinct count. 
    
    "Unique"
        - “Unique” value is total number of values that only appear once.

    -Column Quality    
    -Column distribution

    -Column profile 
        -> Default base on 1000 rows
        are data profiling functionalities under the View tab in Data Preview Section. 
        These functionalities help in understanding the data anomalies and statistics. 
        Out of these three functionalities, Column quality is the one that can be used to show the percentages of data that is in error, empty and valid.
     
    Column profile -> (in-depth look, column statistics)
        provides a deeper look into the statistics within the column. 
        This column can be used to provide many different values like the count of rows
        but it does not help in identifying the percentage of empty cells in the column.

    Column Quality -> ( percentage of empty cells in each column)
        Column quality is the data preview option that is used to show the percentages of data that is in error, empty and valid.        

    Column distribution -> (frequency and distribution of the values)
        
        Distinct -> total number of different values 
        Unique -> total number of values that only appear once
        
        “Distinct” means total number of different values regardless how many times it appears in the dataset. 
        A name appears in the list multiple times is counted as 1 distinct count. 
        Whereas, the “Unique” value is total number of values that only appear once.

        -Check unique and distinct values for each
        displays the data distribution within the column and the counts of unique and distinct values. It is not the right choice for the target goal.

Question

     1. checking your data for errors 
     2. want to see the average and standard deviation for a column.

Ans -> Column Profile -> give you a column distribution chart as well as key column statistics including average, standard deviation, min and max.


###### RLS / Table relationship / Data modelling / Data Classification / Sensitivity Labels / PDF option / foregin related table

Q:
    How can you include a column from a foregin related table in ***data hierarchy*** ?

    A:
        Add a calculated column using the related() function 

    Explan:
    Hierarchies can not contain columns from any other tables.

    You can add the column from the foreign related table into your table using the RELATED() function 
        and then add the column to your hierarchy
    https://docs.microsoft.com/en-za/learn/modules/dax-power-bi-models/1-introduction

Q:
    Which of the following options best describes a tabular data model in PowerBi?

    A:
        Contains related tables
    
    Explan:
    https://docs.microsoft.com/en-za/learn/modules/dax-power-bi-models/1-introduction

********************************************************************************************************************
********************************************************************************************************************
Q: 
    (Only in Power BI Desktop)
    (associate users/groups with the defined roles in the Power BI Service)
    T/F: Row-level security configurations 
        can be ***defined using DAX filters*** in both Power BI Desktop and Power BI Service.
    
    A:
        False
    
    Explain:
        - You define the roles and set up the DAX filter in ***Power BI Desktop.***
        - associate users/groups with the defined roles in the Power BI Service 
            after publishing from Power BI Desktop.
        https://docs.microsoft.com/en-za/learn/modules/row-level-security-power-bi/

Q:
    - already created a workspace in Power BI service
    - want to to store temporary source data files (OneDrive) for analysis. 
    - not yet added the members of your team to the workspace & want to ensure that all members of your team can collaborate in the workspace (and OneDrive)
    - must minimise ongoing access control administrative effort
    -->***NOT*** do to accomplish your goals

        A:
            - Add the members of your team to the workspace
            - Add the workspace to the office 365 group

    Explain:
        1. In the past when you created 
        a workspace in Power BI Service, 
        an Office 365 group was automatically created. 

        --> With modern workspaces, this is no longer the case. 
        If you want to take advantage of a shared OneDrive for the workspace,
        you must add an Office 365 group to the workspace. 
        This can be an existing or a newly created Office 365 group.

        To minimise ongoing access control administrative effort you would 
        not 
        want to manage access for both the workspace and Office 365 group separately. 

        So you want to add members to the group and add the group to the workspace. 
        Access control to your workspace is then managed through O365 group membership 
        and 
        not 
        directly on the workspace as you would normally do.

        ***You cannot add a workspace to the O365 group configuration.***
        https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-create-the-new-workspaces#set-a-workspace-onedrive
        https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-connect-to-files-in-app-workspace-onedrive-for-business



Q: - student age and other data. 
   - creating a visualisation showing the age distribution of students enrolled.
   - The marketing department wants to use the data for targeted adds for 
>> certain demographics and they have supplied you with an additional spreadsheet containing the same as in the exhibit. 
>> They have confirmed to you that this data is set and will not change.

    A:
        - Set the group type to bin
        - Right click the Age field of your data & select new group, named [Age group]
        - Use the [age group] field as the axis in a clustered column chart


        Explain :
            - first strategy is to connect to the spreadsheet as source data and create a ***relationship to the existing data for slicing***.
            (Cannot use Age group to create relationship, because the dash between the ages)
            - data in the demographics table shows the age bins, but this is ***a text field***
                    - cannot be used to create a relationship with the student age field.
                    
              In its current form and since no mention is made of additional transformations, we can assume that this strategy won't work.


               In this case we are going to need an alternative approach so,
               we are not going to connect to the demographics sheet as a data source 
                and we'll have to use (hardcoded) grouping instead.
               Since the data will not change, this hardcoding is not necessarily a problem. 

            The alternative approach of 
                -> using grouping (AKA binning) will work here. 
                This approach does however, 
                    come with the drawback of hardcoding the bins into the report 
                        as opposed to getting the bins from the source file as discussed above. 

            Bins are used for numerical, continuous data points; list is used for categorical data. 

            In addition, If the bins as provided in the spreadsheet were irregularly sized and specific,
                 one will have to use the data import method with additional transformations 
                    instead of uniform bins provided by the group feature.


Q: ***dependencies and relationships*** between datasets, reports, and data sources in Power BI?

    A : View Lineage

    https://docs.microsoft.com/en-za/learn/modules/create-manage-workspaces-power-bi/5-troubleshoot-data

-Table relationship

    Q: Create visual that companies Sales & budget amounts by "MONTH" Accomplish with minimum Step

    Tables

    Budget              Sales           Calendar
    -Budget Amount      -Amount         -Date
    -Month              -Country
    -Value              -etc ....
    -Year

    Steps
    1. Concatenate the budget[Year], budget[Month]
    2. Change to date fomat 
    3. Create relationship between "the Calendar[Date] field" & Budget[Date] field

    RLS 
    -------------------------------------
    -Do not use Row-level Security (RLS) for PDF exports. 
    -restrict data access for given users by filtering the rows they see. 
    -does nothing to encrypt reports that are printed to PDF.
    

    RLS roles that use the DAX functions 
        USERNAME and 
        USERPRINCIPALNAME are examples of dynamic RLS roles

    B. 1-2-3-5-4-6
    1. Create a report in Microsoft Power BI Desktop that involves import the data, 
        confirm the data model between both tables, 
            and create the report visuals.
    2. Create RLS roles in Power BI Desktop by using DAX.
    3. Test the roles in Power BI Desktop.
    4. Add members to the role in the Power BI service.
    5. Deploy the report to Microsoft Power BI service.
    6. Test the roles in the Power BI service.

Q:
        two tables named 
            -Invoice  
            -Geo 
            "active relationship" using the GeoID field. 
        --> need to be able to filter data from 
            ->> both Geo Table and Invoice Table
                - need the Invoice table filtered by Geo
                - Geo table filtered by Invoice type
        RLS -> Geographic leaders can only see the invoices from their region.
        *** You are having difficulty getting RLS working 
            *** for the relationship between the Geo and Invoices.
            
    A : 1. In the relationship view, check apply security filter in both directions
          2. In the relationship view, set the cross filter direction to Both

    - In the relationship view, set the cross filter direction to Single
        --> Setting to Single will restrict the filtering in a single direction.

    - In the relationship view, uncheck make this relationship active
        --> If you make the relationship inactive, the two tables will not be able to join together.    

    PDF option
    -------------------------------------
    no PDF options in the tenant settings.

    Data Classification
    -------------------------------------
    Admin Portal -> Tenant Settings -> dashboard settings -> Data Classification

    In dashboard Tab -> Data classification (Select a Class)

        -Precaution about data
        -Awareness
        -Apply to only *dashbaord*
        - minimize the configuration efforts and effect on the dashboard design.
        -optionally add a URL with more information about your organization’s classification guidelines and usage requirements.   

    -ON -> tenant settings, all dashboards are given a default classification type. 
    -OFF -> none of the tags are remembered if you decided to switch on data classifications later.

    What data to share to who, data Sensitivity 

    -> Go to the dashboard itself -> setting

    Sensitivity Labels (all exported reports need to be encrypted, data can remain protected, even when it leaves Power BI.)
    ---------------------------------------
    -> the exported file and protects it according to the label's file encryption settings.

    -Protection of data
    -Prevent Unauthorized Access Data
    -Apply to *Dashboard, Reports, DataSets & DataFlow* 

