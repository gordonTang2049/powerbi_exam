###### Priority
Learn 
    - Try RLS / try parameter
    - 
    Color cell
    conditional formatting
    base on field
    background color
    - Paginated report
    
    RLS / Workspace 
    Bookmark
    drill through -> Master and Product page
    pinning visuals from the reports

    Ext -> .pbix / pbit / pbiviz / pbids

    report navgation
    https://docs.microsoft.com/en-za/learn/modules/data-driven-story-power-bi/4-report-navigation


###### Tips 
    For groupby Count / Sum values in table, no need to groupby

        Just use 
            1. CountX
            2. SumX
    
    Use Data groups to Categorise data

###### virtual table

    It creates from Dax, not physical table from Database or excel

###### Data groups
    
    Column tools -> Data groups  

    Group by 
        - value interval
        - Number of bins

###### Create dimension and Fact Table
    1. Duplicate a table and rename it as the Dim table
    2. Remove Rows, Remove Duplicate 
    3. Add Column -> index Column 
    4. Home -> Merge query -> dropdown pick dim table -> select the column in dim and fact table
    5. In fact table -> that column drop down box pick DimID

    To remove steps in power query -> select the step to remove
        left click "Delete Until End"

###### table vs Matrix
    1. Matrix has drop down box
    2. table does not have drop down box

Q: switch from using a table visualisation to using a matrix?
    
    A: When you have more than one dimension you want to analyse

    Explain:
        Matrix -> multiple dimensions similar to an Excel PivotTable


###### Create Dimension time
    VAR HourTbl = 
        SELECTCOLUMNS(GenerateSeries((0), (23)), "Hour", [Value])

    VAR MinuteTbl = 
        SELECTCOLUMNS(GenerateSeries((0), (59)), "Minute", [Value])

    VAR SecondTbl = 
        SELECTCOLUMNS(GenerateSeries((0), (59)), "Second", [Value])
    Return
    AddColumns(
        CrossJoin(HourTbl, MinuteTbl, SecondTbl), 
        "Time", Time([Hour], [Minute], [Second])
    )
        

###### R Viusal / R base
-R visuals for plotting are limited to ***150,000 rows***
-R visuals are all displayed at a 72 DPI resolution.
-version of the plotly will not affect the number of rows

###### Parameter
    Query Parameter

        Click Edit Query -> Manage parameters / new parameters 

        List of Value -> need to have current value
        
    Use Query Parameter in a table -> go to column -> Drop down -> filter -> dropdown (ABC icon) -> select parameter

Only Modified by PowerBi Desktop

    Param only use by Power BI Model Authors, not users

###### Query editor / Live Connection vs DirectQuery vs m Code vs Power Query vs Dax vs Advance Editor / refresh import excel / Advance Options(connecting SQL Database) / Import size 
###### Direct query / import / filter panel / Dual / Performance Analyse / refresh database


###### Steps

    Sources -> Dataset -> reports -> dashboard

###### Synonyms (Q&A)
    
    define Synonyms (Words) in Q&A  for the data table
    
    Insert -> Q & A -> Gear(Setting) -> Field Synonyms -> With the data fields

    Insert -> Q & A -> Gear(Setting) -> teach Q&A
    
    I can Synonyms in Data modelling -> click the fields -> Properties -> General -> Synonyms


###### Dashboard Display / Display in Published report -> Tab order and Layer Order  / Bookmark

    logical way. =>    View -> Selection -> Layer or Tab order
    Bookmark => save the current filters and slicers, cross-highlighted visuals, sort order.
    layer order => The layer order is used to control the order in which visuals are shown and is used if you have visuals that overlap. 

How to add youtube video in dashboard

    add a video title

Image title 

    Do not use an image tile. An image tile is used for a static image such as a logo.

Streaming Data title 

    Do not add a custom streaming data tile. A streaming data tile is used for sensor data or feeds like Twitter.

Question:
    1. management wants you to make quick changes to 
        both content and layout 
        that they can see *immediately* on the dashboard.
    2. Management is only comfortable using a dashboard.

    Ans : Pin the report as a live page 
        
        When you pin an entire page, the tiles are live. 
        You can interact with the visuals directly on the dashboard. 
        Changes are reflected in the dashboard tile.
    
    Refresh schedule 
    ----------------------------------------
    management wants to see updates *immediately* in the dashboard.

    add management to the workspace. 
    ----------------------------------------
     1.not help them see an up to date dashboard. 
     2.Management only interested in accessing a dashboard 
     3.not want to access the underlying workspace.

    create an app
    ----------------------------------------
    Any layout changes will not be reflected in the app.

What should you do to achieve this goal?



###### decomposition tree & key influencer

decomposition tree
---------------------------------
    Useful
        -Conduct root cause analysis
        -Visualize data across multiple dimensions
        -understand and explore the potential causes 

    Option -> preview feature -> enable decomposition tree

        -> Visualiation has 3 icons in the bottom

                Select Explained by -> 
        
        can rename the attribute names

key influencer
--------------------------
    creates segments 
        ->contribute to a selected metric value
        ->contrasts the relative importance of factors.
     
###### M code vs Dax Function 
    M code is for Data processing Manuplation 
    Dax Function is for Viusalize data


Q : 
    You build a report to show sales by country.  
    The list of cities is ***too long*** for how you want to show the data so you decide to rather show sales by region.  
    Your company ***has a nonstandard way of representing regions*** that is ***not included*** in your dataset.
    How can you ***show sales by region without editing the query or using DAX***?
    
    A : 
        Use the group function to create regions;
        add countries to the appropriate group

    Explain:
        The group function (AKA binning) in Power BI Desktop is suitable for this task as 
        per this article: https://docs.microsoft.com/en-us/power-bi/desktop-grouping-and-binning

        New Parameter, new hierarchy and Power Query Group-by is not appropriate for this task.




##### FILTER - SUMMARIZE (create a virtual table)
    -----------------------------------------------------------------------

##### TOPN - SUMMARIZE (create a virtual table)
    -----------------------------------------------------------------------

**Tips**
    Use Column Tools -> Sort by Column -> To Sort with right order


###### Look up table & data table
    - Look up table -> Dimension Table
    - Data Table -> Fact Table


###### Key Influencer
    
Q 1. You are interested in creating a measure that will always calculate the total sales for 2020, 
irrespective of the year selected in any other visual in Power BI. Which of the following is the right way to create such a measure?

A. Total Sales for 2020= CALCULATE(SUM(‘Sales OrderDetails'[Total Price]), YEAR(‘Sales OrderDetails'[orderdate]) = 2020)

B. FORMAT([Date],”MMMM DD, YYYY”)


data model has an impact on the time consumed in the refreshing of a model but once the model is loaded in the memory,
no impact on the performance of the reports

measures still affect performance

    False
the measures need to iterate over more data and therefore the evaluation is likely to consume more time that will certainly affect the performance of the reports. Therefore, reducing the size of the data model by removing the unnecessary rows or columns will help in improving the performance of the reports.


2019 Salary_Cost = CALCULATE([Total Salary_cost], Filter (Date, Date[Year]=2019))
    C. Blank. It will return no records.


C. CROSSFILTER -> DAX function that takes the two columns and set the cross filter relationship between these columns.
    DAX function to modify a single directional relationship to a bi-directional relationship on the fly (within the measure)



Salary_Cost having Q&A enabled on it.
 When a user tries to get the count of Employees, 
 the query gets failed. 
 On the other hand, when the user asks for the count of workers

C. Editing synonyms from the Power BI Desktop

When you are interested in improving the Q&A experience, it is always a good practice to add synonyms from the Power BI Desktop Model view.

###### resources
    https://www.whizlabs.com/blog/da-100-exam-questions/

    **Scrope**
    https://www.mssqltips.com/sqlservertip/7285/microsoft-exam-pl-300-microsoft-power-bi-data-analyst-prep-guide/

    **Dataset Settings**
    Dataset Settings 
        -> Schedule refresh 
        -> Data Source credentials

    https://www.velosio.com/blog/getting-started-with-scheduled-refresh-in-power-bi/#:~:text=Configuration%20in%20Dataset%20Settings&text=You%20can%20also%20get%20to,to%20configure%20your%20refresh%20plan.
        Can't check B. Check the cardinality for the columns in the dataset

Able to 
    A. Modify query editor parameter values
    C. Mark the dataset as certified or promoted
    D. Change the credentials used for connecting to the underlying data source
    E. Define the sensitivity label for the dataset


<!-- ============================================================================== -->

###### Alert
-------------------------------------------------------------------------------------------------------
    Send an email
    MS power Automate 

Q: 
    You set up an ***alert*** on a visual on a dashboard you have configured in the Power BI Service. 
    You add the alert, ***configure the threshold value and click Save and Close.*** 
    Where do you ***expect to receive the alert*** when the threshold is crossed?

    A:
        (By default)
        - Notification center in Power BI
        - On your mobile device where you have power BI mobile installed
    
    (also has)
        -alert delivered as an email
        -a PowerAutomate flow to trigger in the alert
    (no option)
        -no option for text message.


    Explanation:
    (not all the available options)
    The question is quite specific in the steps taken.  
    ***It does not ask you to specify all the available options, ***
    but rather the outcome of the configuration as presented. 


    By default the alert is fired in the Power BI notification center.  
    And, if you have Power BI mobile installed on your mobile device, 
    you will also receive the alert via push-notification there.  

    The other options available to you,
     but not configured in this question is as follows: 
     As part of configuring the alert you can optionally also have 

     the alert delivered as an email,
     
      but this was not mentioned in the question.  
      There is no option for text message.
    You can also configure a PowerAutomate flow to trigger in the alert, 
    but this again was not mentioned as part of the alert configuration in the question.
    https://docs.microsoft.com/en-us/power-bi/service-set-data-alerts


Q: 34
    the following is the best approach to ***share a set of reports*** with ***everyone in the company***?

    A:
        Publish an app

    Explain:
        Company-wide sharing of multiple reports and/or dashboards is best achieved by creating a Power BI Service app.

        All the other options will also work, but has drawbacks.

        Since .pbix files usually contain the dataset being 
        -> analysed these emails can potentially be too large to effectively send.
        -> Sharing content with everyone after publishing to My Workspace creates a problem if for example you leave the organisation.

        Creating a workspace and adding everyone to the workspace could be confusing if multiple reports for different purposes are all shared in the same way.  
        (Azure AD, Hard to manage users)Also, it becomes quite hard to manage user permissions for many users and would require group management via Azure AD.
        There are certain scenarios where this is a viable solution, but for a generalised question like this, publishing an app is a better answer.
        
        (Web security concern) Publish to web creates anonymous access to the reports which is a security concern.

        https://docs.microsoft.com/en-us/power-bi/service-create-distribute-apps
    
Set custom URL Location 

Q:
    dashboard - pinning a visual from a report. 
    You click the ellipses (...) menu on ***the tile*** and ***select Edit details.***
    You ***check Set custom link***, ***enter a URL into the field provided and click Apply***.
    What is the effect of this setting on the functioning of the dashboard?    

    A: When clicking on the tile your browser will redirect to URL entered 

    Explain:

    You can set a custom URL location for when a user clicks on a visual in a dashboard.
    https://docs.microsoft.com/en-us/power-bi/service-dashboard-edit-tile#hyperlink



Q: You are performing a time-series analysis of your organisation's sales data. 
    You sales team asks you to help them compare quantities of products sold and returned over time. 
    You have already created the visual as shown in the exhibit.

    A: Add the [Start of Month] field of the play axis field
    
    Explain: 

        Since the applied steps are identical and the data sources for each of the queries all point to the same folder, 

        - it would be optimal to change the data source to folder (new source) and 
        combine the files before applying transformations. 

        The transformations can be applied only once, as opposed to several times,
         once for each file. This also allows for additional files that are added to the folder to be incorporated into the dataset when data is refreshed.

        Get from folder and combine only works if the transformations doesn't apply structural transformations like unpivot and transpose. 
        Getting files from a folder applies combine before transformations. 
        If this was the case you should add an append as new to combine the queries into a single table and deselect enable load on the intermediate tables.

        - ***Merging*** is not appropriate since the transformations are identical, 
            meaning that the files have the same structure (columns).
            Merge is used when there is a common id and different meta-data that you want to combine into a wider table.

        - ***Reference*** is when you want to start a new query from where another one left off - not appropriate for the scenario.

        - ***Parameter*** is used to change some variable in the query on a global basis. 
            You don't need to create parameters for data source since this is built-in to Power BI. 
            Parameters are often used to change the month end of a fiscal calendar etc. Not appropriate for this scenario.

        https://docs.microsoft.com/en-us/power-bi/connect-data/service-get-data-from-files
        https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-shape-and-combine-data

Modern Power Bi Workspace / One drive space
--------------------------------------------

Q : Q18
    open the .pbix file and select Transform data. 
    see several queries to a series of files in a file share accessible in your organisation. 
    review the applied steps in the each of the queries and notice 
        that the ***applied steps*** are ***identical for all queries*** 
        and ***does not apply table restructuring transformations like unpivot or transpose.*** 
    - 2 Action optimise the dataset


    A: -Combine  -New source

    Explain: 

Q:
     - combine a newly created modern Power BI workspace with 
     - a shared OneDrive space that the ***users of your workspace*** can use as a working area. 
        Which of the following should you not do?

    A: 
        Specify the path to the Office 365 OneDrive in the workspace settings

    Share OneDrive Space to users of your workspace, 
    Should
    - Specifying the Office 365 group name -> workspace settings
    - Create an Office 365 Group
    - Assign the Office 365 Group to your workspace

    NOT to do
    - NOT Specify the path

    Explan
    - should be specifying the Office 365 group name in the workspace settings, 
    - not the path.  
    Everything else must be done to accomplish the task.
    https://docs.microsoft.com/en-us/power-bi/collaborate-share/service-create-the-new-workspaces#set-a-workspace-onedrive


(Pinned to a dashboard)
Q:  You create a dashboard in Power BI Service by ***pinning a bar chart*** visual from a report.
    - You click one of the bars on the visual. 
    How does the visual react by default?

    A: 
        None of the above

    No:
        - The visual highlights the selected bar
        - The visual highlights the selected bar and 
            filters the other visuals on the page
        - The visual highlights the selected bar and 
            highlights the relevant data on other visuals on the page
        - The visual highlights the selected bar and 
            uses the configured interaction mode to either highlight or filter other visuals on the page

    (configure in interactivity mode, not case with dashboards)

    Explain:
    - When any part of a visual pinned to a dashboard is clicked, 
    the underlying report where the visual was pinned from opens. 

    The interactivity between visuals on a report is governed by the 
    >>>> configured interaction mode, 
    but this is not the case with dashboards.  

    You can 
        >>> also specify a URL for the dashboard tile 
        that will redirect the user to that URL when the tile is clicked.

    https://docs.microsoft.com/en-us/power-bi/create-reports/service-dashboards


Personalize Visuals in report
https://learn.microsoft.com/en-us/power-bi/consumer/end-user-personalize-visuals
---------------------------------------------------------------------------------------------------------------


Q:
    Situation
        - grouped into a security group called DA100Workspace
        - User cannot create new workspaces.
        
    3 actions to Fix
        1. Navigate to Power BI admin portal and select Tenant settings
        2. Click on Workspace settings and then click on create workspaces
        3. Choose specific security groups to apply to and add DA100Workspace


only for admin ->  Adding or removing the other users from the workspace
Workspace level
-----------------------------------
    Private 
    Public
    Organization


Share dashboard
----------------------------------
Question : Display - share with your suppliers to help with the data communications between your organizations
     Power BI Pro license and uses Power BI within their own organization as well
     Prior to share, what do you first need to do

    -> In the tenant settings, enable share content with external users
        ->Your supplier has Power BI Pro and *does not need Power BI Premium* to view your reports.

    Question : share a dashboard with external guest users from another business

        Invite external guests through the 
        *Azure Active Directory B2B*

         By default, external guests can only view reports and dashboards. 
        Additionally, you can allow guest users outside your organization to edit and manage content within your organization.
    
    Not
        -share a dashboard directly.
        -add external user emails in the tenant setting.
        -modify workspace permissions to allow for external users.

Organizational Custom Visual
--------------------------------------------

    - management wants no custom visuals
        -> custom visuals are easily accessed by the Power BI users within the organization 
            With --> while still respecting **the external restriction** for custom visuals.




###### chart Choice

    1. Show progress of conversion rates against a target -> KPI
    2. Identify outliers in sentiment scores -> Scatter
    3. Show the factors that influence sentiment scores -> Key influencers

    Key influencers -> show the factors that drive a metric you're interested in.

    scatter chart -> visually identify outliers 
        -How category sales have **changed** over time with an animation. 
        -You decide that a chart with an animation to **show changes across months** would help visualize the data.
            Category over time 
            Scatter chart & add month to the play axis well 

    Treemap chart ->  displays hierarchical data as a set of nested rectangles.
    Funnel chart -> helps you visualize a linear process that has sequential connected stages.
    Card -> visual shows a single number such as a total.
    waterfall chart -> is used to understand how an initial value is affected by a series of positive and negative changes.
    ribbon charts -> discover which data category has the highest rank /rank change

    KPI Chart -> 
            (Question)  
            KPI wells: Indicator, Trend Axis and Target Goals?
                    -> total units this year
                    -> the historic values at a **monthly level**
                    -> comparison use **total** units last year
            (Awnser)
                Indicator -> Sales Units This Year
                Trend Axis -> Fiscal Month
                Target Goals -> Sales Units Last Year

###### mobile visualize

    -Set slicers to be reposive
    -Add the most important visuals to the mobile canvas
    -Resize the visuals to fit the mobile canvas


###### Power BI report server  / Paginated reports / pixel perfect

    are designed to be printed or shared. 
    They are called paginated because they are formatted to fit well on a page 
    and are sometimes called ‘pixel perfect.’


Question : Power Bi Service not available in *Power BI Report Server*. 
    
    Not available in Power Bi report server
    1. Dashboards
    2. Q & A
    3. Quick insights 


###### Quick Insights(only for datasets in the Power BI Service)
--------------------------------------------------------------------------------
Quick insights 
        - available only datasets in the Power BI Service
        - Power BI Service
        - pin visuals discovered by Quick insights to a dashboard
        - will try to find outliers by using scatter chart 
             & automatically highlight outliers
    not 
        report
        desktop

    Quick Insights doesn't work with DirectQuery, streaming, and PUSH datasets.

    
Q:
    Which of the following statements regarding the Quick insights feature of Power BI are ***true***?

    A:
        The Quick insights feature produces reusable visuals
        The Quick insights feature will automatically identify outliers in your data

    Explain:
        - Quick insights is available only for ***datasets*** in the Power BI Service, ***not reports***
        - Quick insights is only available in Power BI Service, not in the desktop
        - You can pin the visuals discovered by Quick insights to a dashboard - reusable
        - Quick insights will try to find outliers by using scatter chart and automatically highlight outliers
        https://docs.microsoft.com/en-us/power-bi/create-reports/service-insights
        
###### Azure Active Directory / Azure Active Directory security group 

Azure Security group
----------------------------------------

    -Manage member & computer access
    -Create specific secuirty policies -> for different group
    -Allows you to set permission for all members of a group
    -Managing user join & leave

    situation -> RLS has been created

    with Azure Active Directory security group, 
        add the user to Azure Active Directory for France

    Azure -> identity and access management service.


###### Merge & Append
    Append query -> the same structure and headings

Merge Queries
----------------------------------------------

    Left anti
    Right anti
        
    Left Anti means if identifier does not exist in Left Table, 

It will not join into ***new merged table***

    https://learn.microsoft.com/en-us/power-query/merge-queries-left-outer

After Append Queries

The original table can be ***disable*** loading from 

    query editor -> right click the table -> uncheck enable loading

    https://community.powerbi.com/t5/Desktop/Getting-rid-of-source-tables-after-append/m-p/154745

###### custom developed 'pbiviz' in powerBi 

    The answer is B. To develop pbiviz files, you need to install node.js, a framework designed to build scalable applications based on the Javascript language. The steps to set up an environment for a custom visual are:

    1. Install nodes.js

    2. Install pbiviz

    3. Create and install a certificate

    4. Set up Power BI service for developing a visual

    5. Install additional libraries (required for developing a visual, e.g. D3)

###### Development pipeline / LifeCycle of Dashboard - Feedback from your team & testing (prior to release)

Question:
    Some of the feedback from your team is that it is hard to test Power BI Service dashboards fully prior to release. 
    Is there a better way to handle the lifecycle of your Power BI report and dashboard creation?

    1. feedback from your team
    2. test dashboards prior to release
     
    Ans : 
        Create Development pipeline across development, test and production stages

    *deployment pipelines tool* ->enables BI creators to manage the lifecycle of organizational content

    NOT:
        -Power BI Report Server, Not enable report lifecycle management.
        -Creating separate workspaces, Not an efficient way to manage a deployment lifecycle
        -Paginated reports, --> used for ‘pixel perfect’ reporting  
                            --> will not assist in report lifecycle management.
    

###### Visual Setting / Chart setting / Chart coloring / Chart conditional formatting
    
    Question : calculate a measure of the sales percentage within each category.
        
        ans -> In conditional formatting select 'Sales % Category' and turn on "data bars"
    
        ‘Sales % Category’  -->> the dropdown -->> turn on data bars.


    Question : Sales % of Categories & conditional formatting ->  low values are red, center values are orange and high values are green
            conditional formatting -> LOW / CENTER / HIGH VAL
    
        ans -> 
            Conditional Formatting ‘Color scale' -> Diverging Setting ->  three color options: Minimum, Center and Maximum. Set the Minimum color to red, the Center color to orange and the Maximum to green.

    default settings
    ----------------------------------------
         only two color settings, one color for Minimum and one color for Maximum.
    
    rules-based 
    ----------------------------------------
        specific numeric range for each color and you will not be able to see a diverging color scheme as per the exhibit.


    field values
    ----------------------------------------
    relies on a column with color names or color codes.

###### Pivot & unPivot

    From Table 1
    |TransactionID|Product1    |Product2 |Product3  |Product4|Product5|
    |0            |citrus fruit|rye bread|eggs      |milk    |UHT-milk|
    |1            |yogurt      |banans   |whole milk|beer    |potatoes|

    To Table 2
    |TransactionID|Attribute|Value       |
    |0            |Product 1|Citrus fruit|
    |1            |Product 1|beer        |
    |2            |Product 2|cat food    |


    Select TransactionID -> Select Unpivot other columns

###### Hierachy / drill Down

    Hierachy
                                Year
                                  V
        Q1              Q2               Q3             Q4
        V               V                V               V
    Jan Feb Mar     Apr May Jun     Jul Aug Sep     Oct Nov Dec


    To create hierachy
        just drag the higher hierachy column to lower hierachy column

The Arrows up down - Drill Down

In Legend
    Divison
    Department
    Team

    - Single arrow Down - Drill down

    - Double arrow Down - Go to next level in the hierachy 
        It will split the figure to next level
            e.g.  Year -> quarter
                It will display all quarters
    
    -Double split arrow Down - Expand all down one level in the hierachy 
            Drill further down the level 

    Date Hierachy is pre created
        Year 
        Quarter
        Month
        Day
        
    just drag date in Legend 
        It has YEAR QUARTER MONTH DAY





###### Use DataFlow / Store DataFlow 
    
    Can Store
        Azure Data Lake Gen2.
        Common Data Model folders
            ->cannot store the dataflow itself in a Common Data Model folder

    Can Not store 
        SharePoint 
        Azure SQL Server

###### DateTime Setting 

     Question : 
        the first row is 2022-03-20 0831 EST. 
        - Want to extract Date only


    Ans : Add a Column by example and type 2022-03-20, then set the data type to Date

    Power Query Editor -> Add Column > Column
        type in the date component of the first row you see 
            e.g. 2022-03-20. After Power BI applies to all rows, set the data type of the column to Date.

    NOT:
        Value() -> converts a string to a number.
        TRIM() -> TRIM is used to remove whitespaces in strings.


###### Anomaly detection (line charts)

    Applies to.Power BI service for designers & developers 
    Applies to.Power BI Desktop 
    
    Does not apply to.Power BI service for consumers 
    Does not apply to.Requires Pro or Premium license

    line charts by automatically detecting anomalies in your time series data.

    https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-anomaly-detection

    -Anomaly detection requires at least four data points.

###### smart narrative summaries

     -Power BI Desktop 
     -Power BI service

    https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-smart-narrative

    number of summaries -> up to four summaries per visual and up to 16 per page.

    The smart narrative feature doesn't support the following functionality:

-Limitation

    -Using dynamic values and conditional formatting (for example, data bound title)
    -Pinning to a dashboard
    -Publish to Web
    -Power BI Report Server
    -On-premises Analysis Services
    -Live Connection to Azure Analysis Services or SQL Server Analysis Services
    -MultiDimensional Analysis Services data sources
    -Key influencers visual with a categorical metric or unsummarized numerical field as 'Analyze' field from a table:
    -that contains more than one primary key
    -without a primary key, and measures or aggregates as 'Explain by' fields
    -Map visual with non-aggregated latitude or longitude
    -Multi-row card with more than three categorical fields
    -Cards with non-numeric measures
    -Tables, matrices, R visuals or Python visuals, custom visuals
    -Summaries of visuals whose columns are grouped by other columns and for visuals that are built on a data group field 
    -Cross-filtering out of a visual
    -Renaming dynamic values or editing automatically generated dynamic values
    -Summaries of visuals that contain on-the-fly calculations like QnA arithmetic, complex measures such as percentage of grand total and measures from extension schemas.
    -Calculation groups



###### Case Study 

Overview
You are the newly appointed data analyst for a web-based retail company with operations worldwide. You are responsible for improving sales reporting.


Existing Environment

    - The organisation has selected and adopted Power BI as the data analysis platform
    - All users belonging to the 
        sales department 
            have been allocated a Power BI Pro license
    - You are the 
        a. only user with Power BI Desktop installed 
        b. and Power BI Pro license

Data Sources

    The organisation's sales data is 

        -stored in Azure SQL Database 
            and is used by the company's financial system. 

        The financial system 
            a. uses online processing and 
            b. is constantly updating the data in the database. 

    Sales data includes 
        a sales fact table 
            - sales of products to customers 
            - financial transaction data. 
        It also includes 
            - a customer information table, 
            = a product category table 
    
     
    product table with details about 
            - the product like country of manufacture and 
            - cost price.

    The organisation has recently 
        - grouped their international sales territories based on 
            a. where sales take place 
            b. provided you with an Excel spreadsheet showing this breakdown.


    Technical Requirements

        - data model is optimised for ***best performance***
        - Corporate policy 
            a. sales team members must 
                --> only be able to analyse sales data >>> their own territory.

Reporting Requirements

    The sales team require 
        a. reporting quality be improved 
        b. standard naming conventions be applied across all reporting. 
            c1 Country names, 
            c2 territory names
            c3 sales data aggregations should be named consistently, 

    d. use proper capitalisation 
    d. not use abbreviations or special characters.

    The sales team 
        able to analyse sales by product category.

    |Table Name| C|


Q1:

You add a ***bar chart*** visual to your report. 
    You drag 
        - PrdCat[Product Category Name] to the Axis fieldwell 
        - Sales[Sales Amnt] to the Values fieldwell. 
        However you visualisation does not seem to provide the correct results. 
        With due consideration of all the requirements, 
        what should you do first?
        
    A: 
        Change the Product[Prd_Cat] data type to whole number

    The visual is probably not working because there 
        ==> may not be a relationship between the Product and PrdCat tables. 
        ==> ***before you create a relationship between the Product and PrdCat tables***
        you must ensure that 
            ==> the key filed have a common data type 
            to meet 
            =>the technical requirement of having an ***optimised data model.***

        https://docs.microsoft.com/en-za/learn/modules/optimize-model-power-bi/2-performance        

Q2:
    You want to include the ***Territory data source*** as textual information into the data model 
    so you connect to the data source using Power Query. 
    What should you do to prepare the data for inclusion in the data model? 
    Each answer represents part of the solution and is performed in the order as listed below.

    A:
        -Select Remove top rows from ribbon, Specify 2
        -Select Choose columns from the ribbon, specify 2,3,4
        -Select Use first row as headers from ribbon
        -Select Column 1 then select Remove empty
        -Add the following M code:
            = Table.TransformColumnTypes(
                #'Remove empty',
                {
                {"Territory", type text},
                {"Country", type text},
                {"Team Lead", type text}
                }
            )

    Explain:
    Remove the top 2 (not 3) rows of header information so that Territory is the first row of column 2
    Choose columns and select columns 2, 3 and 4 to keep. 
    This action will discard column 1.  
    We want to do this since the data in this column doesn't follow a logical structure and will not be useful in the model.
    You should not be unpivoting since the data is not pivoted.
    Promote the first row as headers so that the columns names are Territory, Country and Team Lead.
    Apply a text filter (remove empty) to column one to remove the first empty row.
    Apply the data type transformations - all columns must be text.
    Since the manual data type transformations answer 
    is correct (all text) it is a better answer than to use detect; 
    Detect data type will only detect the data type for the currently selected column which isn't specified as part of the answer option.

    https://docs.microsoft.com/en-za/learn/modules/clean-data-power-bi/2-shape-data

Q3:
    You must create a relationship for the newly imported Territory table in the data model. 
    Select the ***correct relationship characteristics*** from the list of options below 
    that will satisfy the requirements related to territories.  (Choose 3)

    A:
        - Create relationship between Territory & Customer (1)
        - Configure the Cardinality as one-to-many (2)
        - Configure the cross filter direction as single

    Explan:

    This question requires that you imagine the table 
        after it has been transformed as in the previous question; 
        it contains a list of countries and team leader names.  

    >>>> The question checks if you understand the purpose of the table 
        - in this case it is about where sales are taking place.

    The Products table 
        -has a country field, 
            but this has nothing to do with where sales are taking place, 
            but rather where the product is manufactured.  

    (1)
    ->connect Territory to customer 
        as this is where the sale is taking place.  
        
    We will also have to 
        extract the country from the address column 
        in the customer table first though to make this work, 
        but this is not part of the question. 

    (2) One-to-many for 
            Territory to Customer 
            as the territory table has unique countries 
            with more than one country belonging to the same territory. 

    We presumably have 
        more than one customer per country 
        so the country (to be created from address) column will have duplicates - therefore the many side of the relationship

    (3) Cross filter can be single, since we do not need the customer table to filter the territory table in this requirement.

    *** Security filter is automatically applied in the cross-filter direction. 
        And this satisfies the security requirement. 

    ***Tips
    (if bi-directional cross filter)

    (you may also want the security filter (RLS) to propagate in both directions)
    and will in that case have to switch on Apply security filter in both directions. 
    
    
    But that is not needed or available in this scenario.
    https://docs.microsoft.com/en-za/learn/modules/design-model-power-bi/


Q4:
    You must improve quality as per the requirements, which of the following should you ***not*** do?

    A:
        Rename Product[Prd_Cat] to Product[Product Category Identification]

    Explan
    (don't have to rename the Product[Prd_Cat])

    because 

    (this column will only be used as a key column for the relationship) 
    and 
    will not be used as a heading in the report - in fact, you will probably hide this column from the data for this same reason.

    All the other column renaming is consistent with the naming conventions requirement.



##### Qualified table / Column and measure references

qualified table -> TableName[Column]

column -> table-level object, and column names must be unique within a table. 
A measure -> model-level object, measure names must be unique within the model


- Always use fully qualified column references
- Never use fully qualified measure references

##### Columns 
------------------------------------------------------
    -> DAX will ***not force*** using a ***fully qualified reference*** to a column. A fully qualified reference means that the table name precedes the column name.


A column is a table-level object, and column names must be unique within a table. 
So it's possible that the same column name is used multiple times in your model—providing they belong to different tables. 
There's one more rule: a column name cannot have the same name as a measure name or hierarchy name that exists in the same table.

In general, DAX will not force using a fully qualified reference to a column. A fully qualified reference means that the table name precedes the column name.

(Profit = [Sales] - [Cost])  same as (Profit = Orders[Sales] - Orders[Cost])

Column 
    -> When you need to use fully qualified column
=====================================================
 when Power BI detects ambiguity. 
 When entering a formula, a red squiggly and error message will alert you.
    Also, some DAX functions like the LOOKUPVALUE DAX function, require the use of fully qualified columns.

=====================================================

##### Measures / implicit measures
------------------------------------------------------




###### Case Study 2

Sceneria
creating a Power BI report for your organisation's factory operation.
The factory is equipped with IoT sensors that monitor robotic performance telemetry.
The factory's quality assurance department assesses 
    each product coming off the assembly line and makes a determination 
    as to 
        - the product's readiness for delivery 
        and 
        - records the decision in the database.
    Your report must ***highlight the telemetry responsible for quality***.

Q:  Which of the following visualisations will you choose for your report?

    A:
        Key Influencers (identify the factors that influenced that decision)


    Explan:
    Visual that identifies the factors that influence 
        -->>>> the ***outcome of an observation*** is the key influencers visual.
    The QA team makes a decision (determination) on readiness.
    You have to identify the factors that influenced that decision.
    The best visual for this is the key influencers visual. 

    You should know which visuals should be used in different scenarios.
    You can expect questions to not use the name of the visual in the question or scenario.
    https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-influencers


Q: Which fields would you add to the Analyze fieldwell of the visual?

    A:
        Quality
    
    Explain:
        The field in this scenario that describes the ***outcome is the quality field***.
        https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-influencers


Q: Which fields would you add to the Explain by fieldwell of the visual?

    A: 
        Telemetry

    Explan
    The factors influencing the outcome (quality) are the telemetry fields
    https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-influencers


###### Case Study 3

Scenario

You are the BI analyst for a multinational organisation. You create a report that analyses the revenue streams for your organisation.

Goal

Your analysis must allow for showing data for different countries separately.


Solution

- From Power Query add a parameter for country with a default value

- Create a row-level filter referencing the parameter

- Apply the query changes

- Publish the report to the Power BI Service

- Specify the country in the dataset settings of the report


    A:
        



Solution

- From Power BI add a parameter and specify the country field

- Publish the report to the Power BI Service

- Specify the country in the dataset settings of the report    


- Add the country field to the Filters on all pages area of the Filters pane

- Publish the report to the Power BI Service

- Share the report and select Share report with current filters and slicers



==================================================================================
Use app then app workspace

app -> can be use by free user
depend on viewer role 