
###### Loading Data 
=======================================================================================================
###### Performance tricks / performance analyzer / Query Diagnostics

###### For data souring performance
-----------------------------------------
    (fastest)1. Direct Query 
             2. Dual 
             3. import

###### Dual
-----------------------------------
    In table relationship session, the top bar of the table, Indicator which mode
        - Blue Bar, Direct query
        - Yellow & Blue Bar, Dual

    Click right bar Properties, go to the bottom - Advanced 

    View -> Performance Analyse -> right bar -> start analyse -> copy query from the bottom

    Dax studio -> Similar to Data viualisal studio

    if it is calculated table, it is imported


Sql Server Database import/DirectQuery Option
------------------------------------------------------------------------------
    
    Navigate using full hierachy
        -> if checked, means Schema become a Folder and then file is the tables

        -> if not checked, it will show as  Schema.tables   


Dual -either cached or not cached, depend on context of the query
------------------------------------------------------------------------------
        You should not use the dual storage mode. 
    -> Tables with dual setting can act as either cached or not cached, 
        depending on the context of the query that's submitted to the Power BI dataset.
        There is not a need for dual storage on this data set.

    -Composite Model
        Mix and Match

    Issue
        Microsoft SQL Server database and has over 15 million rows, 
        before you use database, want to import "sample of the credit card data".
        
        In advanced options, add Where Clauses to SQL statement

    -> no option HEAD in the advanced settings
    -> HEAD is a function used in R scripts.

    F5 -> refresh the local Excel file

    import Table
        -Cached
        -static or low volume
        -small Size (less than 1m)
    
    -> Import smaller size dataset, less than million 
    DirectQuery 
        -Large size (More tahn 1m)
        -shown immediately in report

Add Column or Edit Query
------------------
Go View tap -> Advanced Editor 
Custom Column

Advance Option - Import Large dataset from MS SQL Server database
---------------------------------------------    
    Question : credit card transactions 15 million rows, want to import a sample of the credit card data.
    
    Ans : Add a WHERE clause to SQL statement in the advanced options

            a SQL Server Database, expand the advanced options.
            you can add a SQL statement. 
            Write a filter using the WHERE clause to import a sample of the data.

        NOT :
        1.TOPN functionality
            TOPN is a DAX filter used to create measures once the data has already been imported.

        2. Check HEAD to sample data from the advanced option
            -no option HEAD in the advanced settings to automatically sample the data. 
            -HEAD is a function used in R scripts.

Advance Editor / Connection string
------------------------------------------------------------------------------------------

let 
    Source = Sql.Database("", "PSMPowerBi"),
    dbo_CTCReport = Source{[Schema="dbo",Item="CTCReport"]}[Data],
    #"Renamed Columns" = Table.RenameColumns(dbo_CTCReport, {{"monthyear", "Year"}})
in
    #"Renamed Columns"

    where the query at the beignning of importing the ds

    There are steps of queries, if I want to split your query into two parts,
    I right click "Extract previous"

    resharpe transform and then load data into data model


Import file size limitation 
---------------------------------------------    
- json & txt are allowed
- There is a 1-GB limit for datasets stored in shared capacities in the Power BI service. Only the json and txt files are under 1 GB.


Calculated Table / Import Data (Rarely Change & Calculated table)
---------------------------------------------    
    -Import Data -> cache Data -> fast & less space use


    -Calculated Table -> is to copy a table with filter of rows


    -You should use the import mode for a calculated table and for the countries table. 
    -Since these tables will rarely change, import is the best option.

DirectQuery -> (Does not Cache data, suit for) Pull Schema not data itself
---------------------------------------------
     DirectQuery does not cache the data and is useful when using large amounts of data.

        DirectQuery limitation
            from power query and DAX


The database is updated on a frequent basis.
    Some data sources have the option of connecting directly to the data source using DirectQuery. 
    With the DirectQuery option, 
    no data is imported or copied to Power BI Desktop. For relational sources,
the chosen columns and tables appear in the Fields list. 
In multi-dimensional sources such as SAP Business Warehouse, 
the dimensions and measures for the chosen cube appear in the Fields list. As you interact with the visualization,
you always view the current data.

     Azure SQL database -> connect with  -> By setting the data connectivity mode to DirectQuery
            While connecting to a data source in Power BI Desktop, it is always possible to import a copy of the data in Power BI Desktop.
             Some data sources have the option of connecting directly to the data source using DirectQuery. 
             With the DirectQuery option, no data is imported or copied to Power BI Desktop. 
             For relational sources, the chosen columns and tables appear in the Fields list.
              In multi-dimensional sources such as SAP Business Warehouse, 
              the dimensions and measures for the chosen cube appear in the Fields list. 
              As you interact with the visualization, Power BI queries the underlying data source and you always view the current data.

-Live Connection
-----------------------------
        - Only available for 
            a. SQL Server Analysis Services
            b. Allowed Azure Analysis Services
            c. Power BI Dataset
        ->mutually exclusive ***DirectQuery*** and ***Live connection***

        Analysis Services -> powerBI -> powerBI Dataset
            No change with model

        You should not use a Live Connection. 
        A live connection is used for streaming data such as Analysis services from IoT devices.



Query diagnostics
--------------------------------------------
To go Query diagnostics 
    Go transform data (Power Query) -> Tools 
    
    1. Diagnose Step - if you just want to record one Step / action, e.g. remove one column 
    2. Start Diagnostics - Record every steps

    - Diagnostic Options (open Diagnostic data)
        Enable tracing
        Bypass geocoding cache
        - Open Crash dump/traces folder -> where the Diagnostic data store
            open -> diagnostic table
    
    - Visualise Diagnostic Data
        1. Open it in Open Crash dump/traces folder
        e.g. Axis - Category 


    After Stop record Steps, it will show you a table 

    Diagnostics Detail
        1. Operation Column - is most important, it shows you what have been performed 
        2. Exclusive Duration - How long does it perform
        3. Data Source Query 

    Diagnostics Aggregated - Top Level view

    Diagnostics partition
        - Expression -> check power query

    -Time spent on different actions 
        
Q: What tool should you use in Power Query to discover and investigate and improve performance issues?

    A: Query Diagnostics

    Explan:
    Query diagnostics is the performance analysis tool in Power Query. Performance analyzer is the performance analysis tool in Power BI Desktop.


performance analyzer
--------------------------------------------------
    View -> performance analyzer
    
    - Click start recording, 
        it shows the query when you click different visualised on the dashboard.

        Other -> means time spend on for other chart filter viuslize

         - (Dax query)Copy Query -> can copy that query 


Q : Power Query Editor seems to be taking a lot longer to refresh, 
            Power Query is doing at authoring and at refresh time.

    Ans: Run Query Diagnostics
            -> Query Diagnostics tells you what Power Query is doing at authoring and refresh time in Power BI Desktop.

    Performance analyzer (performance issues of visuals)
    -----------------------------------------
     identify performance issues of visuals and is not used in Power Query Editor.
     
    ALM toolkit (Power BI dataset)
    -----------------------------------------
    is a tool to manage Microsoft Power BI dataset and cannot be used to analyze queries.

Performance tricks 
        1.management wants no custom Visuals
        2.Enable consultant visual maintaining the default requirement
            Solution-> Add custom visuals to organizational store

                Custom Power BI visuals created privately for your organization can be uploaded to the organizational store.
                 Uploading the private files into your organizational store saves overhead and management time. 
                 The custom visuals are easily accessed by the Power BI users 
                 within the organization while still respecting the external restriction for custom visuals.

   1. Create a blank report page
   2. Restart Power BI
   3. Open performance analyzer and press start recording
   4. Interact with the visuals
   5. Press stop and review results

improve the performance while getting the data in Power BI?
            Calculation in Powerquery -> C. Performing some calculations in the original data source 


###### diagnostic logging
    diagnostic logging like Sql profiler to check process of data coming from and steps
        trace info, analytics

        Log Analytics


Question
------------------------------------------------------
Which storage model should you use for each of the three requirements from top to bottom?

    Import -> Date is a date table created in DAX
    Import -> Countries is a geographic table that is rarely updated
    DirectoryQuery -> Sales has the software sales to retailers and has many new records added every day


==================================================================================================================================================

###### M code / Transform Data / Advance Query

ActiveSync -> mobile device data synchronisation tool. 
Live connection -> similar to DirectQuery and is used with SSAS, not SQL.
DirectQuery-> SQL Server and Azure SQL Database, also real time


Advance Editor -> see Detail of M code
-----------------------------------------------------------------------------------------
1. let : the definition of all Variable
2. in : the output of your query
3. #Variable Name -> This is steps

let 
    Source = Csv.Document(File.Contents("./Path.csv").[Delimiter=",", Columns=10, Encoding=65001, QuoteStyle=QuoteStyle.None]),
// Function param1 -> Step from  "Source" Variable
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Change Type" = Table.TransformColumnTypes(#"Promoted Headers", {{"Transaction", type data}, {"Stock_ Date", type date},
    {"Invoice_ID", type text} }
    ),
    #"Reordered Columns" = Table.ReorderColumns(#"Change Type", {"Transaction_Date", "Product Key", "Stock_ Date"}),
    #"Sorted Rows" = Table.Sort(#"Reordered Columns", {{"Product Key", Order.Ascending}})
in 
// Final Output
    #"Sorted Rows"

(Function Name)                         (Argument - a Filter condition (quantity sold = 2))
Table.SelectRows(#"Reordered Columns", each([Quantity_Sold]=2))
                 (Reordered Column Step)

M code Categories
-----------------------------------------------------------------------------------------
Table                  |  List          | Text                  | Date |

//Table Construction    
Table.FromList          List.Select      Text.Length             Date.EndOfMonth
Table.ToList            List.Contains    Text.From               Date.EndOfQuarter
Table.isEmpty           List.Unions      Text.Middle             Date.Day
Table.FindText          List.Median      Text.Contains           Date.StartOfWeek
Table.RemoveColumns     List.Numbers     Text.Remove             Date.StartOfMonth
Table.Contains                           Text.BeforeDelimiter

-Table construction     Selection        Information
-Conversion             Membership       Text.comparisons
-information            Set operations   Extraction
-Row operations         Ordering         Membership
-Column operations      Generators       Modification
-Membership                              Transformations

e.g. Filter Customer by 2
= Table.SelectRows(#'Reordered Columns', each([Quatity_Sold]=2))


###### Table.TransformColumnNames()  Currency.Type / Data Type
-----------------------------------------------------------------------------------------
Convert the standard Cost Column from a a decimal Number

decimal Number -> standard Cost  (Type)

= Table.TransformColumnNames(#"Promoted Headers",{ {"ProductKey", Int64.Type}, {"Product", type text}, {"Standard Cost", Currency.Type} })

Currency.Type (Currency)
type number (decimal)
Int64.Type (integer)
type text (text)
Percentage.Type (percentage)

no USD type

###### Transform 

Change Number to date format

    https://www.youtube.com/watch?v=TRL6ZYMKd48&ab_channel=MITutorials

   
transformation -> power query -> view -> Advanced Editor

cardinality
--------------------------------
What is cardinality?
Cardinality is a term that is used to describe the ***uniqueness of the values*** in a column.

- Lower cardinality increases performance.
- low level of cardinality - distinct count is low -> has a lot of repeated values
- high level of cardinality - a lot of unique values

relationships between two tables, where it describes the direction of the relationship.

    - Remove too many unique values, higher performance

###### the dataset settings
    it has user Q&A comment session enable

    no -> Check the cardinality for the columns in the dataset

###### data modelling / Relationship

    https://www.youtube.com/watch?v=-4ybWQSRcOY&ab_channel=Curbal


###### bidirecttional ambigutiy

https://www.sqlbi.com/articles/bidirectional-relationships-and-ambiguity-in-dax/#:~:text=Activating%20bidirectional%20cross%2Dfilter%20in,models%20as%20numbers%20become%20unpredictable.


###### Large datasets in (Only Power BI Premium)
    https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-large-models#enable-large-datasets

Power BI datasets can store data in a 
    -highly compressed in-memory cache for optimized query performance, 
    -enabling fast user interactivity. 
With Premium capacities, 
large datasets beyond the default limit can be enabled with the Large dataset storage format setting. 
When enabled, dataset size is limited by the Premium capacity size or the maximum size set by the administrator.

Availability
    -all Premium P SKUs, Embedded A SKUs, and with Premium Per User (PPU)

    Steps here describe enabling large datasets for a new model published to the service. For existing datasets, only step 3 is necessary.

    1. Create a model in Power BI Desktop. 
    If your dataset will become larger and progressively consume more memory, 
        be sure to configure (Incremental refresh)

    2. Publish the model as a dataset to the service.

    3. In the service > dataset > Settings, expand Large dataset storage format, set the slider to On, and then select Apply.

###### View native query
It only allow in direct query, 
View native query locate in the steps of Power query

    it will translate to SQL query




    https://community.powerbi.com/t5/Power-Query/View-Native-Query-always-disabled/td-p/1305544

###### Incremental refresh 
Instead of refresh(update) the entire (Not just adding new data), incremental refresh only update centain period of data

    1. Set up parameter -> power query -> Manage Parameter
        Create 2 parameter
            a. RangeStart - datatype Date/Time  (Current Value YYYY/M/D  2021/1/1)
            b. RangeEnd - datatype Date/Time
        (Param name must be name as above)

    2. Go to the Fact date & filter the dataset to be updated
        Filter Row 
            -> "After or equal to"  "RangeStart"
            AND 
            -> "is before" "RangeEnd"

    (Once in Power Bi service, 
    it won't be able to download to Power Bi Desktop)

###### Incremental refresh and real-time data for datasets (Only Power BI Premium, Premium per user, Power BI Pro, and Power BI Embedded datasets)

With incremental refresh, the service dynamically partitions and separates data 
that needs to be refreshed frequently from data that can be refreshed less frequently. 
Table data is filtered by using Power Query date/time parameters with the reserved, case-sensitive names RangeStart and RangeEnd

https://learn.microsoft.com/en-us/power-bi/connect-data/incremental-refresh-overview

----------------------------------------------------
###### Supported data sources
----------------------------------------------------

    Incremental refresh and real-time data works best for structured, relational data sources like SQL Database and Azure Synapse, but can also work for other data sources. In any case, your data source must support the following:

Date filtering 

    filter table data based on the date column. For date columns of integer surrogate keys in the form of yyyymmdd, you can create a function that converts the date/time value in the RangeStart and RangeEnd parameters to match the integer surrogate keys of the date column. To learn more, see Configure incremental refresh - Convert DateTime to integer.

Query folding 



Configuring incremental refresh and real-time data
    We'll go over important concepts of configuring incremental refresh and real-time data here. When you're ready for more detailed step-by-step instructions, be sure to check out Configure incremental refresh and real-time data for datasets.

    Configuring incremental refresh is done in Power BI Desktop. For most models, only a few tasks are required. However, keep the following in mind:

    When published to the service, you can't publish the same model again from Power BI Desktop. Republishing would remove any existing partitions and data already in the dataset. If you're publishing to a Premium capacity, subsequent metadata schema changes can be made with tools such as the open-source ALM Toolkit or by using Tabular Model Scripting Language (TMSL). To learn more, see Advanced incremental refresh - Metadata-only deployment.
    When published to the service, you can't download the dataset back as a PBIX to Power BI Desktop. Because datasets in the service can grow so large, it's impractical to download back and open on a typical desktop computer.
    When getting real-time data with DirectQuery, you can't publish the dataset to a non-Premium workspace. Incremental refresh with real-time data is only supported with Power BI Premium.