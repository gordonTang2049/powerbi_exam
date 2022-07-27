###### R Viusal
-R visuals for plotting are limited to 150,000 rows
-R visuals are all displayed at a 72 DPI resolution.
- version of the plotly will not affect the number of rows

###### Parameter
    Query Parameter

        Click Edit Query -> Manage parameters / new parameters 

        List of Value -> need to have current value
        
    Use Query Parameter in a table -> go to column -> Drop down -> filter -> dropdown (ABC icon) -> select parameter

Only Modified by PowerBi Desktop

    Param only use by Power BI Model Authors, not users

###### DirectQuery vs m Code vs Power Query vs Dax vs Advance Editor / refresh import excel

    F5 -> refresh the local Excel file

    import Table
        -Cached
        -static or low volume
        -small Size (less than 1m)
    
    -> Import smaller size dataset, less than million 
    DirectQuery 
        -Large size (More tahn 1m)
        -shown immediately in report

    Dual 
        -either cached o not cached, depend on context of the query

    
DirectQuery
------------------------------------------------------------------------------------
    The database is updated on a frequent basis.
     Some data sources have the option of connecting directly to the data source using DirectQuery. 
     With the DirectQuery option, 
     no data is imported or copied to Power BI Desktop. For relational sources,
    the chosen columns and tables appear in the Fields list. 
    In multi-dimensional sources such as SAP Business Warehouse, 
    the dimensions and measures for the chosen cube appear in the Fields list. As you interact with the visualization,
    you always view the current data.



    -Import Data -> cache Data -> fast & less space use
    -DirectQuery -> Pull Schema not data itself
    
        DirectQuery limitation
            from power query and DAX

    -Live Connection
        Analysis Services -> powerBI -> powerBI Dataset
            No change with model

    -Composite Model
        Mix and Match


     Azure SQL database -> connect with  -> By setting the data connectivity mode to DirectQuery
            While connecting to a data source in Power BI Desktop, it is always possible to import a copy of the data in Power BI Desktop.
             Some data sources have the option of connecting directly to the data source using DirectQuery. 
             With the DirectQuery option, no data is imported or copied to Power BI Desktop. 
             For relational sources, the chosen columns and tables appear in the Fields list.
              In multi-dimensional sources such as SAP Business Warehouse, 
              the dimensions and measures for the chosen cube appear in the Fields list. 
              As you interact with the visualization, Power BI queries the underlying data source and you always view the current data.



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


###### Steps

    Sources -> Dataset -> reports -> dashboard

###### Synonyms (Q&A)
    
    define Synonyms (Words) in Q&A  for the data table
    
    Insert -> Q & A -> Gear(Setting) -> Field Synonyms -> With the data fields

    Insert -> Q & A -> Gear(Setting) -> teach Q&A
    
    I can Synonyms in Data modelling -> click the fields -> Properties -> General -> Synonyms

###### Data Classification Vs. Sensitivity Labels vs RLS vs PDF option
PDF option
-------------------------------------
no PDF options in the tenant settings.

RLS 
-------------------------------------
-Do not use Row-level Security (RLS) for PDF exports. 
-restrict data access for given users by filtering the rows they see. 
-does nothing to encrypt reports that are printed to PDF.

Data Classification
-------------------------------------
    -ON -> tenant settings, all dashboards are given a default classification type. 

    -OFF -> none of the tags are remembered if you decided to switch on data classifications later.
    
    -optionally add a URL with more information about your organization’s classification guidelines and usage requirements.

    -Precaution about data
    -Awareness
    -Apply to only dashbaord

    The solution needs to minimize the configuration efforts and effect on the dashboard design.

    What data to share to who, data Sensitivity 

    Admin Portal -> Tenant Settings -> dashboard settings -> Data Classification

    -> Go to the dashboard itself -> setting

Sensitivity Labels (all exported reports need to be encrypted, data can remain protected, even when it leaves Power BI.)
---------------------------------------
    -> the exported file and protects it according to the label's file encryption settings.

    -Protection of data
    -Prevent Unauthorized Access Data
    -Apply to Dashboard, Reports, DataSets & DataFlow 



###### Display in Published report -> Tab order and Layer Order  / Bookmark
 logical way. =>    View -> Selection -> Layer or Tab order
 Bookmark => save the current filters and slicers, cross-highlighted visuals, sort order.
 layer order => The layer order is used to control the order in which visuals are shown and is used if you have visuals that overlap. 

###### Power Query Editor-> Column quality vs profile vs distribution

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
        -Check unique and distinct values for each
        displays the data distribution within the column and the counts of unique and distinct values. It is not the right choice for the target goal.

###### the dataset settings
    it has user Q&A comment session enable

    no -> Check the cardinality for the columns in the dataset

###### RLS 

    RLS roles that use the DAX functions USERNAME and USERPRINCIPALNAME are examples of dynamic RLS roles

    B. 1-2-3-5-4-6
    1. Create a report in Microsoft Power BI Desktop that involves import the data, confirm the data model between both tables, and create the report visuals.
    2. Create RLS roles in Power BI Desktop by using DAX.
    3. Test the roles in Power BI Desktop.
    4. Add members to the role in the Power BI service.
    5. Deploy the report to Microsoft Power BI service.
    6. Test the roles in the Power BI service.


###### decomposition tree & Key influencer
    understand and explore the potential causes 

    Option -> preview feature -> enable decomposition tree

        -> Visualiation has 3 icons in the bottom

                Select Explained by -> 
        
        can rename the attribute names


###### Admin Feature only
    Creating a report in another workspace depending upon the dataset of this workspace


###### query editor -> where the query at the beignning of importing the ds

    There are steps of queries, if I want to split your query into two parts,
    I right click "Extract previous"

    resharpe transform and then load data into data model

###### Active vs Inactive relationship and relationship

type of cardinality describes the ideal type of table relationship


###### M code vs Dax Function 
    M code is for Data processing Manuplation 
    Dax Function is for Viusalize data


##### Dax Function  
-----------------------------------------------------------------------
| MATH & STATS              | LOGICAL           | TEXT            | FILTER              | DATE & TIME           |
Basic **Aggregation** func    Conditional Ex     text strings       Lookup Func             date & time 
**iterators** eval row lvl                       controls format    Filtering Func          time intelligenece

-SUM                          -IF                -CONCATENATE       -CALCULATE              -DATEDIFF
-AVERAGE                      -IFERROR           -FORMAT            -FILTER                 -YEARFRAC
-MAX/MIN                      -AND               -LEFT/MID/RIGHT    -ALL                    -YEAR/MONTH/DAY
-COUNT/COUNTA                 -OR                -UPPER/LOWER       -ALLEXCEPT              -HOUR/MINUTE/SECOND
-COUNTROWS                    -NOT               -PROPER            -RELATED                -TODAY/NOW
-DISTINCTCOUNT                -SWITCH            -LEN               -RELATEDTABLE           -WEEKDAY/WEEKNUM
                              -TRUE              -SEARCH/FIND       -DISTINCT
**ITERATOR**                  -FALSE             -REPLACE           -VALUES                 time intelligence
-SUMX                                            -REPT              -EARLIER/EARLIEST       -DATESYTD
-AVERAGEX                                        -SUBSTITUTE        -HASONEVALUE            -DATESQTD
-MAXX/MINX                                       -TRIM              -HASONEFILTER           -DATESMTD
-RANKX                                           -UNICHAR           -ISFILTERED             -DATESMDD
-COUNTX                                                             -USERELATIONSHIP        -DATESINPERIOD
                                                                    -TOPN
##### Calculate vs Summarise
 Summarise -> since we want to create a virtual table. 

##### if /or /and
OR -> Users see both Texas OR Shipping, with no restriction both condition

· If the value is greater than 80 and Units are F, then ‘Hot’. Otherwise ‘Not Hot’
Value > 80 & F -> Hot  
· If the value is greater than 26 and Units are C, then ‘Hot’. Otherwise ‘Not Hot’
Value > 26 & C -> Hot
Category =

if ( OR
 ( AND
    (Temperature[Value] > 80,Temperature[Units]="F"), 
    AND (Temperature[Value] > 26,Temperature[Units]="C") ),"Hot","Not Hot")


##### Calculate
    -----------------------------------------------------------------------
Use Calculate , if I want to calculcate with filters
Calcualt(, Filter)

##### Summarize
    -----------------------------------------------------------------------
//https://www.youtube.com/watch?v=IeaPNw_YuQc
Use Summarize, Group by / Scan
Calculate Subtotal

    Evaluate
        Summarize(
            Sales,
            Product[Brand],
            Date[Calendar Year]
        )

    To Create new Column
        Evaluate
        Summarize(
            Sales,
            Product[Brand],
            Date[Calendar Year],
            // Qty -> Column Name , Sum(Sales[Quantity]) actual data
            "Qty", Sum(Sales[Quantity]),
            "Brand & Year", Product[Brand] & " - " & Date[Calendar Year]
        )
    To Calculate Subtotal
        Evaluate
        CalculateTable(
            Summarize(
                Sales,
                    ROLLUP('Product'[Brand], 'Date'[Calendar Year]),
                    "Amt", [Sales Amount]
            ),
            'Product'[Brand] IN {"Contoso", "Litware"},
            'Date'[Calendar Year] IN {"CY 2008", "CY 2007"}
        )
    //Summarize - Group by sales Icon
    Evaluate
        Summarize (
            AddColumns(
                Sales,
                // Split with 2 Rows
                "SalesType"
                    IF(Sales[Quantity] > 1, "Large", "Small")
            ),
            [SalesType],
            "Amt", [Sales Amount]
        )



// CALCULATE VS SUMMARIZE

##### Calendar
    Calendar -> returns a table Specified Start date and End date 
##### CalendarAuto
CalendarAuto() -> The range of dates is calculated automatically based on data in the model. 
    Set up Fiscal year by Month 
    Since the fiscal year ends March 31, the parameter is 3.
###### REMOVEFilters() -> it cant be used in Directquery same as All()
    -----------------------------------------------------------------------
    alias or replacement for your all func a particular column

###### TOTALYTD 
-----------------------------------------------------------------------
// Manual Way to Calculate TOTALYTD 
    Calculate([Sales Total],
    Filter(
        ALL('Date'),
        Date[Year] = Max(Date[Year]) &&
        Date[Date] <= Max(Date[Date])
    ))
//with DAX func 
    TotalYTD([Sales Total], Date[Date])
###### Corss Filter
    -----------------------------------------------------------------------
        CorssFilter(col1, col2, direction)
        
        - Col1 Many Side of the relationship
        - Col2 One side or lookup side of the relationship
        - Direction -> None , Both, Oneway, OneWay_LeftFiltersRight, OneWay_RightFiltersLeft

    Data Model

        DimProduct attribute                    Fact_Sales              DimSalesCountry
            - Arabic Description                -ProductKey             -SalesCountry
            - Chinese Desc                      -Product Number         -SalesGroup
            - Color
            - etc.....

        DimSalesCountry -> filtering FactSales  but FactSales does not filter DimProduct attribute
        therefore -> cross filter


        Business Question:
            ***Each country -> how many colors the product are selling
            
color Distn Count = Distinctcount(DimProduct[Color])  ==>it will all same numebr, because fact table does not filter color 
    
    |country    | Color||
    Australia    10
    Canada       10
    
Should Write code


        Country -> Fact -> Product

        To Link the filter From Fact to Product

    MEASURE Cross filter color Count = Calculate(Distinctcount(DimProduct[Color]), 
        CrossFilter(FactInternetSales[ProductKey]), DimProduct[ProductKey], Both) 

###### TREATAS -> treatAs
    -----------------------------------------------------------------------
-Applies the result of a table expression as filters to columns from an unrelated table.
-One Table has not been related

    Business question : want to see Expense Vs Sales?

    issues 
        Expense is at month Level 
        Sales is at day level

    Data Model
                                                            This is daily 
        Product_Master          Sales                      DimDate
            -Category Name      -Cost Amount                -Date
            -Cost Price         -Cost Per Unit              -DayName
                                -Customer Name              -Etc...

                                                                No Relationship with the Fact sales table
                                                            MonthlyExpense
                                                                -Expense
                                                                - Month
                                                                -Year
**I can also apply filter**

    MEASURE Expense Total = Calculate(Sum(MonthlyExpense[Expense]), 

        TreatAs(
            Summarize(DimDate, DimDate[Year], DimDate[Month]), 
        MonthlyExpense[Year], MonthlyExpense[Month]),

        DimDate[month] = "December"
        )
-----------------------------------------------------------------------
##### SUMX vs Sum
    dO Calculation row by row, iterator SUMX / AVERAGEX
-----------------------------------------------------------------------
    e.g. 
        Sales Amount = Sumx(Sales, Sales[Unit Price] * Sales[QTY])
-----------------------------------------------------------------------
    Sum / Count (Aggregate Func)
    e.g. Total Sales = Sum(Sales[Quantity])

##### Switch
-----------------------------------------------------------------------
    Column -> Competitor Price

    if Competitor Price is Zero/Empty  -> Show me Cost Price


    Some Product is not sold by Competitors
    
    |Name       |Brand |Cost Price |Competitor Price|
    |Jeans Levis|Levis |650        |0               |

If competitor Price is Larger than 0, use competitor Price otherwise use Cost Price

    New Price = Switch(true(), 
        Sum('Product Master'[competitor Price]) > 0,
        Sum('Product Master'[competitor Price]),
        Sum('Product Master'[Cost Price])
    )

-----------------------------------------------------------------------
##### bi-Directional vs related vs relatedTable
-----------------------------------------------------------------------
related() -> Vlookup in Excel 
    When there is an active relationship between 2 tables and One-to-Many Relationship


    e.g.    1 -> many      (Only work in this sales table)
        [Product]          [Sales] 
        -Product Code       -Channel
        -Price              -Date
        -etc                -Product_ID
---------
    Scence - has a sales table only quantity & sales amount
        Cal profit -> get price from cost 

        SumX-> sum for each rows

        PROFIT = Sumx(Sales,
                Sales[Sales Amount] - (
                    Sales[Quantity] * Related('Product Master'[Cost Price])
                    )
                )
e.g. -> like vlookup

    Lookup for the Price

    Price Lookup = Related(Product[Price])

    //Measure 
    // Calcualte every single row of the sales table
        Total Sales =
            SUMX(
                Sales,
                RELATED(Products[Price]) * Sales[Units]
            )
-----------------------------------------------------------------------
relatedTable()
    Work for one to one, many to many , many to one, need some relationship with the table
    
    Returns a table, Not a scalar value(single value)
        Related Table not works for new Column, it returns a table
-----------------------------------------------------------------------
    // it will works, because it is Counting rows for each Categories
    Col = COUNTROWS(RelatedTable(Sales)) 

    Table A (many) to (many) Table

    Count times on each other table

    Col = COUNTROWS(RelatedTable(Sales)) 
#### UserRelationship
-----------------------------------------------------------------------
-handling inactive relationship

Fact Table has more than 1 date

By Default, The table will use active date

if we have 
    -Required Date
    -Order Date

We use UserRelationship for inactive date

// Default using Order Date
// Require Date is inactive relationship
    Measure 
        Total Sales by Req Date = Calculat(
            [TOTAL SALES],
            userRelationship(Order[RequiredDate], DimDate[Date])
        )




##### SelectedValue vs AllSelected
-----------------------------------------------------------------------
SelectedValue goes to select 1 Category only


SelectedValue allows to select multiple Value


Sales 2 or more cat =
    VAR selectedCategory = ALLselected(Category[Categories])
Return
    Calculate([Total amount],
    // it won't work because it selected 2 Cats
    Filter(Order, Orders[Category]= selectedCategory))

[Use ]
Sales 2 or more cat =
    VAR selectedCategory = ALLselected(Category[Categories])
Return
    Calculate([Total amount],
    // it won't work because it selected 2 Cats
    Filter(Order, Orders[Category] IN selectedCategory))


##### SelectedValue (In Matrix)
-----------------------------------------------------------------------
//They are one to one relationship
//They can use bi-Directional relationship
//We want to active bi-Directional only in Calculation
Data Model
                    // It is not Product to SubCat
Sales<---Product Table   <---Product SubCategory <---Product Category       
Key        Brand               ProductCategoryKey      Category   
Date       Class               ProductSubCat           Category Code
            Color               SubCate                 ProductCatKey
            ETC 

e.g. A table
| Product Name | Sales Amount | Class |
| WW1 WIRELESS | 2499         | Deluxe|       
| WW1 LAMP     | 203.98       | Economy|

Transform to Matrix (Put Category stand alone column)

    Put Product Class as Row -> lose the value of product class

new measure [don't use this]
    -> Product Class = Value('Product'[Class]) -> it does not let you put the measure into the matrix table 

[use this]
    -> One more protection if Sales 

    Product Class =
    if( NOT isEMPTY(Sales),
        if(HASoneValue('Product'[Class]),
        Value('Product'[Class]))
    )

SelectedValue work same as -> if(HASoneValue(), Value('Product'[Class]))
Product Class =
     if( 
        NOT isEMPTY(Sales),
        SelectedValue('Product'[Class], "******")
    )   
if no Product class use "******"

USE this for Category with Cat and SubCat

    Product Category = 
        IF(
            NOT isEmpty(Sales),
            Calcalute(
            // This is One value visible
                SelectedValue('Product Category'[Category]),
            // Those are relate them in Calculation
                CrossFilter(
                    'Product'[ProductSubcategoryKey],
                    'Product SubCategory'[ProductSubcategoryKey],
                    Both
                ),
                CrossFilter(
                    'Product Subcategory'[ProductCategoryKey],
                    'Product Category'[ProductcategoryKey],
                    Both
                )

            )
        )

USE SelectedValue for picking Scale 1, 1000 , 100 000

Sales by Scale =
    Divide(
        [Sales Amount],
        // Pop up error if user select more than one Scale value
        SelectedValue(['Scale'[Scale], Error("Select only One Scale Val"))
    )


    Data table 
        Location       Year     Month

    When user select One Month, It is only shows that one month 

    e.g. When User Select June User wants to show from January to June 
    
    Default From Jan to Dec

    // Create Table for all Months name\
    // Filter the measures
1. Table Tools -> New Table 

    MonthList = Summarize(DimDate, DimDate[Month], DimDate[MonthNum])


    // Param1 -> From what ds
    // Param2 -> Default Value select till
// This will return what Month Value you Selected  
    Sales Till Selmonth = Var sm = SELECTEDVALUE(MonthList[MonthNum],12)
    return sm

// Actual Calculation
    Sales Till Selmonth = Var sm = SELECTEDVALUE(MonthList[MonthNum],12)
    return Calculate(Sum(Sales[Sales Amount]), FILTER(DimDate, DimDate[MonthNum] <= sm) )

ALL Vs ALLSELECTED Vs ALLEXCEPT
-----------------------------------------------------------------------

-ALLSELECTED
----------------
A table 
|Product Category|Sales Amount|% Cat Sales
|Accessories|513000|6.95%
|Casual Wear|4691600|63.59%
|etc        |etc    |etc

If it filters by location, it doesn't goes with the 100%

All Sel Sales =
    Calculate([Total sales], AllSelected(Sales))

% Cat AllSel Sales = Divide([TOTAL sales], [All Sel Sales])


ignoring any filters that might have been applied inside the query, 
but keeping filters that come from outside.

want to calculate percentage with **selected** categories

categoryTotal = Calculate([Sales Total], ALLSelected('product'[Category]))
categoryPercetage = DIVIDE([Sales Total], categoryTotal)
Return categoryPercetage


--ALL
Data Model
-------------
Product Master      Sales               DimDate
____                ________            _______
Category Name       Cost Amount         Date
                                        Day Name

// All is to remove all filter, Copy a table
                    (Table name)
Product Ref = All('Product Master')

(Calculate Percentage of the total Sales)

All Sales = Calculate([Total Sales], All(Sales))  -> This will calculate all (Category) sales Number

// Percentage of sales
                                    (Total Category sales column)
New Measure ->  % Category Sales = Divide([Total Sales], [All Sales])

--ALLEXCEPT
// Use All Filter Except (Product Category) Sales Except Product Category  
Sales Cat AllExcept = Calculate([Total Sales], Allexcept(Sales, Sales[Product Category]))

--AllSelected
https://www.youtube.com/watch?v=gD8yLTtyW1k
Slicer -> by Selection


Parent and Child Function
PATH / PATHITEM / PATHITEMREVERSE / PATHLENGTH / PATHCONTAINS
-----------------------------------------------------------------------
Path -> Parent Child Function is base on Data Hier

Hierachy is Manager and suboridnate

Parent(Brian) -> Child (Julio)

Brian is Julio's Manager


|Employee ID| Employee Name | Manager ID | Manager Name | Gender | Job Title | Location | Path Func
| 112       | Brian         |            |              | M      | Manager   | Canada   | 112
| 14        | Julio         | 112        | Brain        | M      |Manager    | Canada   | 112 | 14


                    (ID Column)             (Parent Column)
New Column = PATH(employee[Employee ID], employee[Manager ID])
-----------------------------------------------------------------------

Bus question -> Employee who are the manager


PATHCONTAINS -> Where Path Func Contains Employee ID

//if Path contains 3
NEW COLUMN -> PATHCONTAINS COL = PATHCONTAINS(Employee[Path Func] "3")

// What is the 4th Position of the employee id   ->  manager > manager > manager > employee
// From left to right
new column = PATHITEM(Employee[Path Func], 4)

//What is the position 3rd from right to left 
// From right to left
PATHITEMReverse(Employee[Path Func], 3) 

// How many of the hierachy
Pathlength(Employee[Path func])


USERELATIONSHIP 

RELATEDTETABLE 

RELATED 


##### RANKX - CALCULATE
    -----------------------------------------------------------------------

##### TOPN - CALCULATE
    -----------------------------------------------------------------------

##### FILTER - SUMMARIZE 
    -----------------------------------------------------------------------

##### TOPN - SUMMARIZE 
    -----------------------------------------------------------------------

**Tips**
    Use Column Tools -> Sort by Column -> To Sort with right order



###### Look up table & data table
    - Look up table -> Dimension Table
    - Data Table -> Fact Table


###### Slicers
    Also the check box select 
          Category
        [] A
        [] B
        [] C

    O------O
    --> Slicer is the Horitzontal Bar
        Hortzontal -> Categories Bottom

    - provide an interactive way for users
        - sort and filter a report 

         with 2 Big Dot


    -Filter charts using the date slicer, then bookmarks

    You can get back to an exact state when you select your saved bookmark. 
    This makes bookmarks ideal for creating a presentation in Power BI.


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

###### Workspace admin Security
    only for admin ->  Adding or removing the other users from the workspace    

    Private 
    Public
    Organization

###### Performance
     improve the performance while getting the data in Power BI?
            Calculation in Powerquery -> C. Performing some calculations in the original data source 


###### Workspace security - User level -  Admin, Member, Contributor, Viewer

    Admin, Member, or Contributor 
        -lineage view only available

    Contributor (The lowest lvl can)
        - publish reports and delete dashboards within a workspace

    Member
        - assign viewer, contributor, and member roles?

###### Analytics Pane

    sales data by day in a time series chart
    >produce-> a **25 day forecast** with a **90% confidence interval** as per the below exhibit. 
    >ignore-> data anomalies in the last 5 days of data that you want to ignore for the forecast.

    analytics pane and under forecast select ‘+ Add’

        -Go to analytics pane & under Select '+Add'
        -Set forcast length to 25 points & ignore last 5 points
        -Set the confidence interval to 90% and click on apply

###### Drill through
     
    Perform Drill through

    report page &  a detailed chart in a separate page using the drill through feature
    
    a detailed chart in a separate page using the drill through feature.

    The Sales page shows a visual of total sales by month.
    When you click on drill through on the sales by month chart, 

    redirect to a detail page -> Sales Detail -> selected month by category

    What FOUR actions should you perform?

        -On the Sales Detail page, under drill through option add month as the drill through field
        -Create a new page called Sales Detail
        -On the Sales Details page under Drill through, toggle Keep all filter on
        -Create a table visual to show total sales by month and Category

###### chart Choice

    1. Show progress of conversion rates against a target -> KPI
    2. Identify outliers in sentiment scores -> Scatter
    3. Show the factors that influence sentiment scores -> Key influencers

    Key influencers -> show the factors that drive a metric you're interested in.
    scatter chart -> visually identify outliers 
    Treemap chart ->  displays hierarchical data as a set of nested rectangles.
    Funnel chart -> helps you visualize a linear process that has sequential connected stages.
    Card -> visual shows a single number such as a total.
    waterfall chart -> is used to understand how an initial value is affected by a series of positive and negative changes.
     ribbon charts -> discover which data category has the highest rank /rank change

###### mobile visualize

    -Set slicers to be reposive
    -Add the most important visuals to the mobile canvas
    -Resize the visuals to fit the mobile canvas


###### Paginated reports / ‘pixel perfect
    are designed to be printed or shared. 
    They are called paginated because they are formatted to fit well on a page 
    and are sometimes called ‘pixel perfect.’

###### Quick Insights
    Quick Insights doesn't work with DirectQuery, streaming, and PUSH datasets.

###### Azure Security group
    -Manage member & computer access
    -Create specific secuirty policies -> for different group
    -Allows you to set permission for all members of a group
    -Managing user join & leave

###### diagnostic logging
    diagnostic logging like Sql profiler to check process of data coming from and steps
        trace info, analytics

        Log Analytics

###### Performance tricks / performance analyzer 

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



###### Alert
    Send an email
    MS power Automate 
    
###### Azure Active Directory / Azure Active Directory security group
    situation -> RLS has been created

    with Azure Active Directory security group, 
        add the user to Azure Active Directory for France

    Azure -> identity and access management service.



###### Merge & Append
    Append query -> the same structure and headings

