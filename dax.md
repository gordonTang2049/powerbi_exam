###### Priority

    revision, not so understand
---------------------------
    summarize + rollup + rollup group

    count vs countrows

    Allselected -> How to create a filter table by slicer

---------------------------
    DATESBETWEEN
    
<!-- ====================== -->
    Data base concept
    How to create distribution 
<!-- ====================== -->

##### Usage
Treatas
------------------------------------------

\\ To show FactTb Figures
TreatASMeasure = CALCULATE(
        SUM(factTb2[fact Price]),
        TREATAS(
            SUMMARIZE('calendar', 
            'calendar'[YearNumber],   // Column Year A Match 
            'calendar'[MonthNumber]), 
            factTb2[Year], // Column Year B Match 
            factTb2[Month])
            )

Calculate
------------------------------------------
Use Calculate , if I want to calculcate with filters
Calculate(, Filter)

Calculate(
    [Sales Amount],     \\Column
    'Date'[Year Number]  IN {2007, 2008} \\Filter expression
)

CALCULATETABLE
------------------------------------------
Return a table after filtered 

CALCULATETABLE(
    'InternetSales_USD',  \\ Table name 
    'DateTime'[CalendarYear] = 2006 \\ Filter Condition
)

SUMX MAXX ---X
------------------------------------------
SUMX(
    TableName,
    Expression e.g. [Sales amount Column] * [Quantity]
) 

SUMX(
 CALCULATETABLE(
        'InternetSales_USD',
        'DateTime'[CalendarYear] = 2006
    ),
    [SalesAmount_USD]
)  

SUMMARIZE
------------------------------------------
SummarizePurchaseTb = SUMMARIZE(
    Purchase,  \\ table name
    'Purchase'[ProductId],  \\ group by 
    'Calendar'[YearNumber], \\ group by 
    "Purchase Amount", \\ Column name 
    sumx(Purchase, Purchase[Price] * Purchase[Quantity]) \\ how to group  Sum count Max etc
    ) 

Rand()
------------------------------------------
Random number between 1 and 0 

count / countrows / counta
------------------------------------------------------------------------------------
Performance
    Do the same job 
    (Less efficient) Sales Orders = COUNT(Sales[OrderDate])
    (More efficient) Sales Orders = COUNTROWS(Sales)

        - It's more efficient, and so it will perform better.
        - It doesn't consider BLANKs contained in any column of the table.
        - The intention of formula is clearer, to the point of being self-describing.


Counta is count if cell is ***True***
    it means it doesnt count empty / False cell

Countx
    Example If I want to Count how many transaction in the Filter table - ProductCat
        CountX(
            RELATEDTABLE(ProductCat), \\ Filter or Lookup Table
            Sales[TransactionID] \\ item you want to count
        )
    Example of Count On Filtered Table
    COUNTX(
        FILTER(Product, RELATED(ProductSubcategory[EnglishProductSubcategoryName])="Caps"), \\ Filtered by ProductSubcategory
            Product[ListPrice] 
        )


    e.g. SUMX(RELATEDTABLE(InternetSales_USD), InternetSales_USD[SalesAmount_USD]) 


TOPN 
------------------------------------------
Fill Rate Bottom 5 = TOPN (
    5, 
    ‘FillRate’, \\ Table 
    ‘FillRate’[Fill Rate], \\By what column
    ASC 
    )

For Bottom 5  

    Fill Rate Bottom 5 = TOPN (5, ‘FillRate’, ‘FillRate’[Fill Rate], ASC)

For TOP 5  

    Fill Rate Top 5 = TOPN (5, ‘FillRate’, ‘FillRate’[Fill Rate], DESC)

SelectedValue
-----------------------------------------------------------------------
Returns the value when the context for columnName has been filtered down to one distinct value only. Otherwise returns alternateResult.

\\ Using Slicer, Check a Value to do some operation, e.g. Filter by checked value or Divided by 
\\ Set up require below

\\ place measure to ***Card*** to check whether selectedvalue has been selected
1. Create a Scale Table  
    Column
    ------
    val1
    val2, etc

2. Create a Measure (Not new Column) in the target table, place this Measure in Matrix/table

\\ example divided by Scale
Divided by SelectedVal = 
    VAR SelectedVal = SELECTEDVALUE(Scale[ScaleVal]) 
RETURN
DIVIDE(
    SUM([Price]),
    SelectedVal)

\\ Filter by one Category
Select 1 cat =
    VAR SelectedVal = SELECTEDVALUE(
        Scale[ScaleVal] \\ Column Name
        ) 
RETURN
    Calculate(
        [Total amount]), \\ Column
        Filter(Order, Orders[Category] = SelectedVal)


SelectedValue(
    'Product'[Class],
    "more than one value" \\ (Optional, if more than one value show "more than one value")
    )
     is same as
    IF(
        HasOneValue('Product'[Class]),
        Values('Product'[Class])
    )

AllSelected
-----------------------------------------------------------------------
\\ In 
\\ 

Using Slicer, Check a Value to do some operation, e.g. Filter by checked value or Divided by 

\\ Set up require below

SELECTCOLUMNS  
-----------------------------------------------------------------------
(reorder Table columns, table created by DAX) / move column

SELECTCOLUMNS(
    SummarizePurchaseTb, // Table name
        "Year", // new Column name
        [YearNumber], // Selected Table column name
        "ProductId" , // new Column name
        [ProductId], // Selected Table column name
        "Purchase Amount", // new Column name
        [Purchase Amount] // Selected Table column name
)


ADDCOLUMNS
--------------------------------------------------------------------
It returns a table
Adds calculated columns to the given table or table expression.

ADDCOLUMNS(
    <table>, 
    <name>, 
    <expression>[, <name>, <expression>]…)

ADDCOLUMNS(
        ProductCategory, \\ Add in what table
        , "Internet Sales", \\ Column Name 
        SUMX(RELATEDTABLE(InternetSales_USD), InternetSales_USD[SalesAmount_USD])  \\ How 
        , "Reseller Sales", 
        SUMX(RELATEDTABLE(ResellerSales_USD), 
        ResellerSales_USD[SalesAmount_USD])
        )


Summarize Table-2 = ADDCOLUMNS(
--------------------------------------
    SUMMARIZE('Table',  \\ use Summarize created Table
    'Table'[Product]),
--------------------------------------
    "Profit", \\ Column Name to be added
--------------------------------------
    \\ Adding what column (Column Expression)
    CALCULATE(  \\ return a column
        SUMX(
            'Table', 
            'Table'[Sales] * 'Table'[Unit Price])
        )
--------------------------------------
    )
    
USERELATIONSHIP
-----------------------------------------------------------------------
Sales on DueDate = CALCULATE(
    SUM(Sales[Sales Amount]), \\ Expression -> Sum / Max / Average
    USERELATIONSHIP(
        'Sales'[DueDateKey],  \\ Inactive Date Relateionship Column
        'Date'[Date]) \\ Date Dim table
        )

Date Dax Functions
==================================================================
##### EDate 
--------------------------------------------------
EVALUATE 
AddColumns(
    values('Date'[Date]),
    "EDate +1", EDate('Date'[Date], +1),
    "EDate 0", EDate('Date'[Date], 0),
    "EDate -1", EDate('Date'[Date], -1),
    "EDate -12", EDate('Date'[Date], -12),
    "EDate +12", EDate('Date'[Date], +12)
)

Date        EDate +1    EDate 0     EDate -1    EDate -12   EDate +12
---------------------------------------------------------------------
1/07/2017 	1/08/2017 	1/07/2017 	1/06/2017 	1/07/2016 	1/07/2018 
2/07/2017 	2/08/2017 	2/07/2017 	2/06/2017 	2/07/2016 	2/07/2018 
3/07/2017 	3/08/2017 	3/07/2017 	3/06/2017 	3/07/2016 	3/07/2018 


EMonth
--------------------------------------------------------
EVALUATE 
AddColumns(
    values('Date'[Date]),
    "Emonth +1", Eomonth('Date'[Date], +1),
    "Emonth 0", Eomonth('Date'[Date], 0),
    "Emonth -1", Eomonth('Date'[Date], -1),
    "Emonth +12", Eomonth('Date'[Date], +12),
    "Emonth -12", Eomonth('Date'[Date], -12)
)

Date        Emonth +1   Emonth 0    Emonth -1   Emonth +12   Emonth -12
---------------------------------------------------------------------
1/07/2017	31/08/2017	31/07/2017	30/06/2017	31/07/2018	31/07/2016
2/07/2017	31/08/2017	31/07/2017	30/06/2017	31/07/2018	31/07/2016
3/07/2017	31/08/2017	31/07/2017	30/06/2017	31/07/2018	31/07/2016


DateAdd
----------------------------------------------------------------

EVALUATE 
AddColumns(
    values('Date'[Date]),
    "DateAdd +1", DATEADD('Date'[Date], +1, DAY),
    "DateAdd 0", DATEADD('Date'[Date], 0, DAY),
    "DateAdd -1", DATEADD('Date'[Date], -1, DAY),
    "DateAdd +12", DATEADD('Date'[Date], +12, DAY),
    "DateAdd -12", DATEADD('Date'[Date], -12, DAY)
)



SAMEPERIODLASTYEAR 
----------------------------------------------------------------
-> Same period Last year (It does not return ***Date not exist in 'Date'[Date]***)
    SAMEPERIODLASTYEAR('Date'[Date]) same as DATEADD('Date'[Date], -1, YEAR),



    "Same period Last year",SAMEPERIODLASTYEAR('Date'[Date])


RLS - related DAX
-----------------------------------------------------------------------
    - CUSTOMDATA() -> it is Custom String for connection
        \\ Set up as  ConnectionString="Conenct String"
    - Username() -> Username ON This machine (If use ***Analysis Services instance***, it will be the login username)
    - UserObjectID() -> User Machine Identifier (If use ***Analysis Services instance***, Azure Domain System)
    - USERPRINCIPALNAME() -> user Principal Name , usually Email ***Analysis Services instance***, login user email
    - USERculture() -> Choice Locate 

    https://www.youtube.com/watch?v=7O-QbzImmsA&ab_channel=SQLBI


===========================================================================================================
#### fully qualified 

Q: When is it required to use fully qualified table[column] references in DAX?

    A: 
        It is best practice to use fully qualified table[column] reference in ***measures*** 
            but not for ***calculated columns***
    
    Explan:
        One can safely omit fully qualified table[column] 
            (as opposed to just specifying the [column]) 
        when you're creating a calculated column 
        since it will only ever be used within the context of that table - row context.

        However, it is best practice to use fully qualified references everywhere else.
        Measures have report-global relevance and can be used in any table,
        in other measures and calculated columns and should therefore always use fully qualified references. 

        The measure's home table has no effect on its functioning and is simply a visual organisation technique in Power BI Desktop so you don't have to reference a measure's home table in this way. 


    https://learn.microsoft.com/en-us/dax/best-practices/dax-column-measure-references


##### Implicit Measures
------------------------------------------------------------------------------------------------------------
Q: 
    False regarding implicit measures?

    A:
        Implicit measures use DAX formulas in Power BI

    Explan:
    - Explicit measures 
        ->> DAX formulas in Power BI
    - implicit measures 
        ->> direct column references. 

    Implicit measures (AKA automatic measures)  
         https://docs.microsoft.com/en-us/power-bi/desktop-tutorial-create-measures#automatic-measures

    Explicit measures 
        https://docs.microsoft.com/en-us/power-bi/desktop-measures



A measure is a model-level object. 
For this reason, measure names must be unique within the model. 

However, in the Fields pane, report authors will see each measure associated with a single model table. 

This association is set for cosmetic reasons, 
    and you can configure it by setting the Home Table property for the measure.
        For more information, see Measures in Power BI Desktop (Organizing your measures).

It's possible to use a fully qualified measure in your expressions. 
DAX intellisense will even offer the suggestion. 

Reason not to use ***fully qualified measure***
----------------------------
However, it isn't necessary, and it's not a recommended practice. 
If you change the home table for a measure, 
any expression that uses a fully qualified measure reference to it will break.
You'll then need to edit each broken formula to remove (or update) the measure reference.
----------------------------

It's recommended you never qualify your measure references. The reasons are provided in the Recommendations section.

##### Order of operations for a DAX measure
------------------------------------------------------------------------------------------------------------

Q : 
    Which of the following accurately describes the order of operations for a DAX measure?

    A:
    c. Apply filter context from visual
    d. Apply filter context from upstream tables
    b. Apply filter context from DAX formula
    a. Calculate result

    Explain:
        https://docs.microsoft.com/en-us/power-bi/desktop-quickstart-learn-dax-basics
        

===========================================================================================================

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
##### EOMONTH

Q: a DAX calculated column formula that returns the 1st day of the month for each of the dates in the Date column in the Sales table.

    A:
    1st of Month =
        EOMONTH(Sales[Dates], -1) +1


    Explan
    The correct formula is:

    1st of Month = 
    EOMONTH ( Sales[Date], -1 ) + 1   
    The syntax of the function is as follows: EOMONTH(<start_date>, <months>)

    First we set the start_date to the reference date in the row.

    Then we set the months argument to -1 to return the last date of the previous month.   

    Then we add one day to the result in order to arrive at the 1st day of the month for the referenced date.

    https://docs.microsoft.com/en-us/dax/eomonth-function-dax

##### Convert 
Convert data type

Summarize(
    Order_detail,
    'Calendar'[Year],
    "Total sales",
    Convert([Sales], integer)
)

##### Switch
-----------------------------------------------------------------------
Switch function example
    - use True(), if test a range
    - Simplely lookup value, if match one to one, e.g. Customer[Card] "Blue", "Standard"



Value Cat = Switch(true(),
'Product'[ProductionCost] < 5, "Low value",  \\ if less than 5 use "low Value"
'Product'[ProductionCost] < 10, "Mid value", \\ ...
'Product'[ProductionCost] >= 10, "high value" \\ ...
)

Q:
    Switch Func
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

Q: 
    Use the DAX SWITCH function to add a calculated column named Price Point to the Products table:
        If Price > 500 then "High"
        If Price > 300 then "Mid"
        If Price <= 300 then "Low"

    A: 
        PRICE POINT =
            SWITCH (
                TRUE (),  // if the expression is true return the string value
                Product[Price] > 500, "High", 
                Product[Price] > 300, "Mid",
                Product[Price] > 500 , "Low"
            )

Creates a calculated column of month names.

    = SWITCH([Month], 1, "January", 2, "February", 3, "March", 4, "April"  
               , 5, "May", 6, "June", 7, "July", 8, "August"  
               , 9, "September", 10, "October", 11, "November", 12, "December"  
               , "Unknown month number" )  


Q:
    Use the most efficient DAX function to add a column called Type to the Customer table:
        If Card = "Blue" then "Standard"
        If Card = "Silver" then "Midrange"
        If Card = "Gold" then "Premium"
        If Card is anything else then "Unknown"

    A:
        Type =
            SWITCH(
                Customer[Card],
                "Blue", "Standard",
                "Silver", "Midrange"
                "Gold", "Premium",
                "Unknown"
            )

    Explain:
        If the lookup value is simply a text string or a single number, 
        you can simply use the SWITCH() function.  

        If you want to test a range in the lookup value, 
        use SWITCH() in combination with TRUE().

        SWITCH function https://docs.microsoft.com/en-us/dax/switch-function-dax
        Also see this: https://powerpivotpro.com/2015/03/the-diabolical-genius-of-switch-true/        


COUNTA(<column>)  
Coloumn contains value count


##### Dax function X and no X
E.g. 
- Sumx Sum by each condiition / ID group

- No X sum() sums the entire column


##### Value
Convert text number to numeric value
---------------------------------

=VALUE("3")



##### ADDCOLUMNS
--------------------------------------------------------------------
It returns a table
Adds calculated columns to the given table or table expression.

ADDCOLUMNS(<table>, <name>, <expression>[, <name>, <expression>]…)

ADDCOLUMNS(
        ProductCategory, \\ Add in what table
        , "Internet Sales", \\ Column Name 
        SUMX(RELATEDTABLE(InternetSales_USD), InternetSales_USD[SalesAmount_USD])  \\ How 
        , "Reseller Sales", 
        SUMX(RELATEDTABLE(ResellerSales_USD), 
        ResellerSales_USD[SalesAmount_USD])
        )

***Don't*** Use example, Nexted group in Summarize with Addcolumns
-----------------------------------------------
AddColumns(
        Summarize(
            AddColumns(
                Summarize(
                    'Product',
                    'Product Category'[Category],
                    'Product SubCategory'[Category]
                ),
                "Average Price", Calculate(AVERAGE(Product[Unit Price]))
            ),
            'Product Category'[Category]
        ),
        "Max SubCat Avg Price", Calculate(Max[Average Price])
)

How Summarize work
-----------------------------------------------
SummarizePurchaseTb = SUMMARIZE(
    Purchase,  \\ table name
    'Purchase'[ProductId],  \\ group by 
    'Calendar'[YearNumber], \\ group by 
    "Purchase Amount", \\ Column name 
    sumx(Purchase, Purchase[Price] * Purchase[Quantity]) \\ how to group  Sum count Max etc
    ) 

AddColumns in Summarize
-----------------------------------------------
Summarize (
    AddColumns(
        Sales, // Split with 2 Rows
        "SalesType", 
        IF(Sales[Quantity] > 1, "Large", "Small")
    ), \\ The addColumns become [Tablename]
    [SalesType], \\ Group by Column
    "Amt", 
    Sum([Sales Amount]) \\ Expression
)

How TopN work
-----------------------------------------------
For Bottom 5  

    Fill Rate Bottom 5 = TOPN (5, ‘FillRate’, ‘FillRate’[Fill Rate], ASC)

For TOP 5  

    Fill Rate Top 5 = TOPN (5, ‘FillRate’, ‘FillRate’[Fill Rate], DESC)

AddColumns in TopN
-----------------------------------------------

    TOPN(
        3,
        ADDCOLUMNS(
            VALUES('Product'[Product Name]), \\ Get unqiue value of Product name
            "@Sales Amount", \\ As column name 
            MROUND([Sales Amount], 500000)
            ),
            [@Sales Amount], Desc,
            [Product Name], ASC
    )
    order by [@Sales Amount] DESC

What actually happen in AddColumns
----------------------------------------
\\ If use [NEW Table], it will return the entire table of 'Purcahse',
\\ and new column "Product Profits" as Purchase[Total profit per transaction]
AddColTable = ADDCOLUMNS('Purchase',  "Product Profits", Purchase[Total profit per transaction])


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

KPI Value =
    VAR _thisyear = 
        if (isBlank([Total Sales]), False, True )
    VAR _lastyear =
        if (isBlank(Total Sales SPLY), False, True )
    Return
        IF (
            _thisyear && _lastyear
        )


    ##### TOPN - CALCULATE + Add column While in DAX function
        -----------------------------------------------------------------------
    TOPN input is table, return topn row of the table -> It must be using new Table


    TOPN function does not guarantee the order of the results. When you create your new table, 
    you need to sort the Fill Rate column ascending or descending.

    Input -> Table 
    Output -> Table

    = TOPN (
        <nvalue>, // Top How many rows
        <Table>, // Return what Table
        [OrderbyExpression], // Express by what table (e.g. base on Top Sales Table, Return Calendar table rows In Above) 
        [Order],
    )

    TOPN(
        3,
        ADDCOLUMNS(
            VALUES('Product'[Product Name]), \\ Get unqiue value of Product name
            "@Sales Amount", \\ As column name 
            MROUND([Sales Amount], 500000)
            ),
            [@Sales Amount], Desc,
            [Product Name], ASC
    )
    order by [@Sales Amount] DESC

    Asc / Desc Order
    Calendar
    Date

    New Table =

        TOPN(
            1,
            'Calendar', // Show Calendar table
            '[Total Sales]'
        )

        TOPN(
            1,
            Values(), // Show Calendar table
            '[Total Sales]'
        )

    For Bottom 5  

        Fill Rate Bottom 5 = TOPN (5, ‘FillRate’, ‘FillRate’[Fill Rate], ASC)

    For TOP 5  

        Fill Rate Top 5 = TOPN (5, ‘FillRate’, ‘FillRate’[Fill Rate], DESC)


    ##### cardinality - type of relationship

        --Relationship type 1

        -One to Many or Many to One (Same)
            -(1:* & *:1)

        e.g. 
        Customer                                Order
        |ID-Customer|FirstName|SecondName|      |ID-Order|OrderDate  |ID-Customer|
        |1          |Maxim    |Schwa     |      |A       |01 Jan 2017|1          |
        |2          |John     |Meyer     |      |B       |08 Jan 2017|2          |

        Each Customer is unique                 Each Customer can have multiple orders

        --Relationship type 2

        -One to one (1:1) - Cross filter

        That Table can be "seperate" and  be 1:1 relationship

        |ID-Passport|Valid    |Issued|FirstName|SecondName|Country |
        |1          |2025     |2005  |Maxim    |Schwa     |Germany |
        |2          |2019     |1999  |John     |Meyer     |USA     |

        ->Seperate to 2 Tables From one & can be one to one relationship.

        Passport                            Person
        |ID-Passport|Valid    |Issued|      |ID-Passport|FirstName|SecondName|Country |
        |1          |2025     |2005  |      |1          |Maxim    |Schwa     |Germany |
        |2          |2019     |1999  |      |2          |John     |Meyer     |USA     |



        >>> Active vs Inactive relationship and relationship
        >>> type of cardinality describes the ideal type of table relationship

##### Rewrite DAX for better structure / debug

    -----------------------------------------------------------------------
    1. Use variables to improve performance and troubleshooting

    https://docs.microsoft.com/en-za/training/modules/optimize-model-power-bi/3-variables

    Example
    -------Without Variable

    Sales YoY Growth =
    DIVIDE (
        ( [Sales] - CALCULATE ( [Sales], PARALLELPERIOD ( 'Date'[Date], -12, MONTH ) ) ),
        CALCULATE ( [Sales], PARALLELPERIOD ( 'Date'[Date], -12, MONTH ) )
    )

    -------With Variable
// Return 
//---------------------------------------------
    Sales YoY Growth =
// Var AAA = Calculate 
    VAR SalesPriorYear =
        CALCULATE ( [Sales], PARALLELPERIOD ( 'Date'[Date], -12, MONTH ) )
//
    VAR SalesVariance =
        DIVIDE ( ( [Sales] - SalesPriorYear ), SalesPriorYear )
    RETURN
        SalesVariance

    2. Use variables to troubleshoot multiple steps
    ---> "debug you temporarily rewrite the RETURN expression to write to the variable."

    Sales YoY Growth % =
    VAR SalesPriorYear =  CALCULATE([Sales], PARALLELPERIOD('Date'[Date], -12, MONTH))
    VAR SalesPriorYear% = DIVIDE(([Sales] - SalesPriorYear), SalesPriorYear)  
    RETURN  SalesPriorYear%

    Explain : The RETURN expression will display the SalesPriorYear value only. 

    Sales YoY Growth =
    DIVIDE (
    ( [Sales] - CALCULATE ( [Sales], PARALLELPERIOD ( 'Date'[Date], -12, MONTH ) ) ),
    CALCULATE ( [Sales], PARALLELPERIOD ( 'Date'[Date], -12, MONTH ) )
    )
    Sales YoY Growth =
    AAA SalesPriorYear =
    CALCULATE ( [Sales], PARALLELPERIOD ( 'Date'[Date], -12, MONTH ) )
    BBB SalesVariance =
    DIVIDE ( ( [Sales] - SalesPriorYear ), SalesPriorYear )
    CCC
    SalesVariance



##### Calculate & in
    -----------------------------------------------------------------------
Use Calculate , if I want to calculcate with filters
Calculate(, Filter)

Calculate(
    [Sales Amount],
    'Date'[Year Number]  IN {2007, 2008}
)



##### Calendar
------------------------------
    CALENDAR(<start_date>, <end_date>)  
    = CALENDAR (DATE (2015, 1, 1), DATE (2021, 12, 31))
    = CALENDAR (MINX (Sales, [Date]), MAXX (Forecast, [Date]))


    It creates table of Date 

    Calendar 
        -returns a table Specified Start date and End date
    
    Usage
        Calendar(Date(2010,11,1),Date(2025,12,31))

    Not:
        dont use CALCULATE
        Don't use strings within the CALENDAR function. 
        - Dates require the DATE function.

    

##### CalendarAuto
CALENDARAUTO([fiscal_year_end_month])  
e.g. 
    CALENDARAUTO(3)  
    ***It starts 1/4/2015***
    It starts from Apr of the earliest date in model,
        Not 
            in calculated column / calculated table
    End at MaxDate of data Model

    The earliest date in the model which is not in a calculated column or calculated table is taken as the MinDate.
    The latest date in the model which is not in a calculated column or calculated table is taken as the MaxDate.
    The date range returned is dates between the beginning of the fiscal year associated with MinDate and the end of the fiscal year associated with MaxDate.

Error 
    model does not contain any datetime values which are not in calculated columns or calculated tables.

Not support
    DirectQuery mode when used in calculated columns or row-level security (RLS) rules.



CalendarAuto() -> 
    The range of dates is calculated automatically based on data in the model. 
    Set up Fiscal year by Month 
    Since the fiscal year ends March 31, the parameter is 3.

    


###### REMOVEFilters() -> it cant be used in Directquery same as All()
    -----------------------------------------------------------------------
    alias or replacement for your all func a particular column




###### TOTALYTD / TOTALMTD / TOTALQTD
-----------------------------------------------------------------------
    Calculate Running balance of 
        Within a 
        - Year 
        - Month
        - Quarter

// It accumulates the balance for one year, 
    and next year start balance from 1/1 

        TotalYTD Measure = TOTALYTD(sum(Sales[Sales amount]), Sales[Date].[Date])

// It accumulates the balance from 1/4 

        TotalYTD Measure = TOTALYTD(
            sum(Sales[Sales amount]), 
            Sales[Date].[Date], 
            "3/31" \\ it ends at "31/3"
        )

as of TOTALQTD / TOTALMTD


// With One Filter

    TotalYTD = TotalYTD(
        Sum(Sales[Quantity], 
        DimDate[Date].[Date],
        Sales[Ordertype name] = "On Shop", \\ It works for only one filter
        "3/31"
        )
    )

// Manual Way to Calculate TOTALYTD 

    Calculate(
        [Sales Total],
    Filter(
        ALL('Date'),
        Date[Year] = Max(Date[Year]) &&
        Date[Date] <= Max(Date[Date])
    ))

//with DAX func 
    TotalYTD([Sales Total], Date[Date])


###### DATEADD
-----------------------------------------------------------------------
It must use Calculate with 
    datedd  

    DateDD Year Measure = 
        CALCULATE(
            Sum(Sales[Sales amount]), 
            DATEADD(Sales[Date].[Date],
            -1, \\ can be --->>> Positive / Negative 
            year)
            )


// DateADD is a more generic functions.
// It shift a period back and forth over time using
// DAY, MONTH, QUARTER, YEAR

//DateADD has a quite complex logic to move months and quarters
//the right way, handling months with different dates.
//You can find the detailed rules on dax.guide.


// It returns the entire month
EVALUATE
VAR StartDate = DATE(2008, 02, 01)
VAR EndDate = DATE(2008, 02, 29)
RETURN 
	CALCULATETABLE(
		DATEADD(
			'Date'[Date],
			+1,
			MONTH
		),
		'DATE'[Date] >= StartDate && 'DATE'[Date] <= EndDate
		
	)
ORDER BY [Date]

###### DATEADD vs SAMEPERIODLASTYEAR
-----------------------------------------------------------------------
     DATEADD - it return the entire period, Year 366 days / Feb +1  Month will give entire March, not til 29/3 
    SAMEPERIODLASTYEAR - it returns the exact period 


// SAMEPERIODLASTYEAR returns the selected period shifted back one year

EVALUATE
VAR StartDate = DATE(2008, 01, 01)
VAR EndDate = DATE(2008, 01, 31)
RETURN
{
//	First Calculate is to Filter By  StartDate & EndDate 
	CALCULATE(
		CALCULATE(
		[Sales Amount],
		SAMEPERIODLASTYEAR('Date'[Date])  // Return 2007-01-01 to 2007-01-31
		
		),
	'DATE'[Date] >= StartDate && 
	'DATE'[Date] <= EndDate
	)
}


==============================
CALCULATE(
	[Sales Amount],
	SAMEPERIODLASTYEAR('Date'[Date])
)
==============================
Same as

CALCULATE(
	[Sales Amount],
	SAMEPERIODLASTYEAR(
		CALCULATETABLE(
			DISTINCT('Date'[Date])
		)
	)
)






###### CorssFilter
-----------------------------------------------------------------------
https://www.youtube.com/watch?app=desktop&v=bdUdJVd2mdw&ab_channel=AnalyticswithNags

CorssFilter(col1, col2, direction)
        
- Col1 -> Many Side of the relationship (Many / fact table)
- Col2 -> One side or lookup side of the relationship (Lookup table)

- Direction -> 
    None , Both, Oneway, 
    OneWay_LeftFiltersRight(use when 2 tables are Many-to-Many), 
    OneWay_RightFiltersLeft(use when 2 tables are Many-to-Many)

Many student <-> Many 

    Business Question:
        - Each country

Business Q: How many colors the product are selling?

                                                                         {Target Table}
        DimProduct              1->*        Fact_Sales    *<-1           DimSalesCountry
        -----------------                   -----------------           -----------------
        Arabic Desc                         CarrierTrackingNumber       SalesTerritoryAlternateKey
        Chinese Desc                        CurrencyKey                 **-> SalesTerritoryCountry <- Target to Filter the  
        English Desc                        CustomerKey                 SalesTerritoryGroup
        Class                               CustomerPONumber            SalesTerritoryKey
        Color                               DiscountAmount              SalesTerritoryRegion
        DaysToManufacture                   DueDate
        DealerPrice                         DueDateKey
        EndDate                             ExtendedAmount
        EnglishProductName                  Freight
        ***ProductKey                          ***ProductKey

    Explain:
    End result Table

    color Distn Count = 
        Distinctcount(DimProduct[Color])  -> All 10 (Will give the ""total number of Color count"" )


                            {With only DistinctCount}
    (DimSalesCountry Table) (DimProduct)                (DimProduct)
    |SalesTerritoryCountry |Color Distin Count       |Cross filter color Count |
    -----------------------------------------------------------------------------
    |Australia             | 10                      | 2
    |Canada                | 10                      | 3
    |France                | 10                      | 2
    |United Kingdom        | 10                      | 3
    |United State          | 10                      | 4
    
    Because the data modelling is 
        DimSalesCountry filter **Fact_Sales table** only and ,
        DimProduct filter **Fact_Sales table** only 
    
MEASURE Cross filter color Count = 
Calculate(
    Distinctcount(DimProduct[Color]), 
        CrossFilter(
            FactInternetSales[ProductKey]),  \\ FactTable  Many-To-One Table with Identify Key (Fact to Dimension Table)
            DimProduct[ProductKey], \\ Dimension Table Many-to-One
            Both) 

    It means DimProduct -> Link to Fact Sales (Which they originally linked) -> and then linked DimSalesCountry

        Filter 

- DimSalesCountry is filtering Fact_Sales Table

DimSalesCountry -> filtering FactSales  but FactSales does not filter DimProduct attribute
therefore -> cross filter


Should Write code

        Country -> Fact -> Product
        To Link the filter From Fact to Product

================================================================================================================
can used in Calculate()
    - bidirectional
    - unidirectional
    - disable relationship

Define
measure Sales[Customers] = 
    CountRows(Customer)
measure Sales[CustomersFiltered] = 
    Calculate(
        [Customers],
        CrossFilter(Sales[CustomerKey], Customer[CustomerKey], BOTH)
    )
measure Sales[ProductDoesNotFilter] = 
    Calculate(
        [Customers],
        CrossFilter(Sales[CustomerKey], Customer[CustomerKey], BOTH),
        CrossFilter(Sales[ProductKey], 'Product'[ProductKey], NONE)
    )
EVALUATE

Problem is Customer and Product does not have relationship

            One to many relationship            One to many relationship
    Customer          1->*          Sales        *<-1               Product
    -----------                 ------------                        --------------
    Addr Line 1                 CurrencyKey                         Brand
    Addr Line 2                 ***CustomerKey***                         Category
    Brith Date                  Delivery Date                       Color
    Cars Owned                  Net Price                           List Price
    Children At Home            Order Date                          Manufacturer
    City                        Order Line Number                   Product code
    Company Name                Order Number                        Product Name
    Continent                   Order Time                          ProductKey
    Country                     OrderDateKey                        SubCategory


Output Table
| Brand                 | Customer | Customer Buying | Products does not filter Sales |
| Contoso               | 18,869   | 4346            | 18,869
| Wide World Importers  | 18,869   | 517             | 18,869
|Northwind Traders      | 18,869   | 1002            | 18,869
|Adventure Works        | 18,869   | 2587            | 18,869

================================================================================================================

###### SELECTCOLUMNS (reorder Table columns, table created by DAX) / move column 
-----------------------------------------------------------------------
SELECTCOLUMNS(
    SummarizePurchaseTb, // Table name
        "Year", // new Column name
        [YearNumber], // Selected Table column name
        "ProductId" , // new Column name
        [ProductId], // Selected Table column name
        "Purchase Amount", // new Column name
        [Purchase Amount] // Selected Table column name
)


-----------------------------------------------------------------------
##### bi-Directional vs related vs relatedTable
-----------------------------------------------------------------------
related() -> Vlookup in Excel -> access many to one relattionship(Lookup Table)
To Calculate sum price of each Categories
---------------------------------

--- Each Cat Sales
Total Sales = 
    Sumx(
        Sales,
        Related(Lookuptable_Products[Price]) * Sales[Units]
    )


RelatedTable
--------------------------------
 Work for one to one, many to many , many to one, need some relationship with the table
    
    Returns a table, Not a scalar value(single value)
        Related Table not works for new Column, it returns a table
-----------------------------------------------------------------------
    // it will works, because it is Counting rows for each Categories
    Col = COUNTROWS(RelatedTable(Sales)) 

    Table A (many) to (many) Table

    Count times on each other table

    Col = COUNTROWS(RelatedTable(Sales))

SUMX(   
    RELATEDTABLE('InternetSales_USD'), // Target table
        [SalesAmount_USD] // The amount to extract
        )  

--- Tips - use CountRows to check whether the data modelling correct
Col = countrows(relatedtable(Sales))


Items Profit = SUMX(RELATEDTABLE(Purchase), [Total profit per transaction]) 


To use Relate(), the table must be linked data Modeling
    It will related the row with lookup table id

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



##### HasOneValue
------------------------------------------------------------
// HasOneValue check that a column has only one value 

Define
    Measure Sales[Audio only] = 
        Calculate(
            HASONEVALUE('Product'[Category]),
            'Product'[Category] = 'Audio'
        )
    Measure Sales[Audio only] = 
        Calculate(
            HASONEVALUE('Product'[Category]),
            'Product'[Category] IN {"Audio", "Computers"}
        )
        
|Val 1              | Val 2|
Audio               true        - One Value so is true
Audio & Computers   false       - Has two Value is False


##### SelectedValue (In Matrix) & SelectedValue vs AllSelected
-----------------------------------------------------------------------
Product Category = 
    IF(
        NOT ISEMPTY(Sales),
        SelectedValue('Product Category'[Category])
    )


SelectedValue goes to select 1 Category only

SelectedValue allows to select multiple Value


Sales 2 or more cat =
    VAR selectedCategory = ALLselected(Category[Categories])
Return
    Calculate([Total amount],
    // it won't work because it selected 2 Cats
    Filter(Order, Orders[Category]= selectedCategory))

[Use]
Sales 2 or more cat =
    VAR selectedCategory = ALLselected(Category[Categories])
Return
    Calculate([Total amount],
    // it won't work because it selected 2 Cats
    Filter(Order, Orders[Category] IN selectedCategory))

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

##### Value
-----------------------------------------------------------------------
Value() 
    -> VALUE converts a string to a number.

###### ALL Vs ALLSELECTED Vs ALLEXCEPT
-----------------------------------------------------------------------

###### ALLSELECTED
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

--ALLEXCEPT - Copy a table and except columns
---------------------------------------------------
// Use All Filter Except (Product Category) Sales Except Product Category  
Sales Cat AllExcept = Calculate([Total Sales], Allexcept(Sales, Sales[Product Category]))

--AllSelected
https://www.youtube.com/watch?v=gD8yLTtyW1k
Slicer -> by Selection



MROUND
-----------------------------------------------------------------------
Round to Mutiply of 

Mround(
    1.3, \\ the input number
    0.2 \\ round to Mutiply of .2 means 1.4
)

MROUND(-10,-3)  \\ round to -9


##### RANKX - CALCULATE
    -----------------------------------------------------------------------
Ranking position of an item 

>>> DESC / ASC
It makes the column sort in order first, 
and then rank. 

If no DESC / ASC, it will rank with shuffling order.

>>> (Ties) Optional (It means the ranking values where more than 1 value are same)

if use Dense
e.g. 

Value Rank
10      1
20      2
30      3
30      3
40      4

if use Skip
Value Rank
10      1
20      2
30      3
30      3
40      5


***RANK.EQ*** and RANKX is similiar, RANKX has more argument to adjust the function

Usage Can be similiar to TOPN 
RANKX function to rank your fill rates 
    -> CALCULATE 
    -> FILTER to limit the output to the *bottom* or *top values*.

Product Profit Rank = rankx(
    all('Product'), \\ Table to rank with 
    [Items Profit] \\ Item for rank 
    ,,ASC,Dense) \\ option how (desc asc)

TABLE SampleData = {"A", "B", "B", "B", "C", "D", "F"}

RANKX(
    TableName, 
    TableColumn_Expression, \\ the Column condition to rank
    70 \\ item to rank 
    )


RANK.EQ("A", SampleData[Value], ASC)

###### Treat as / USERELATIONSHIP  / active & inactive relationship 
----------------------------------------

###### TREATAS -> treatAs
-----------------------------------------------------------------------
Treatas is virtual mapping

Treat as -> A real example will make it easier to understand.  TREAT 1 AS a filter for 2.
    Example : https://exceleratorbi.com.au/virtual-filters-using-treatas/

e.g.
    Sales 2007-2008 = 
        Calculate(
            Sum([Sales Amount]),
            Treatas({2007, 2008},   \\ Filter Condition
            'Date'[Year Number]) \\ Filter from what
        )

    Same as

    Calculate(
        Sum([Sales Amount]),
        'Date'[Year Number]  \\ Filter from what
            IN
        {2007, 2008} \\ Filter Condition
    )        

Can be

    Sales 2007-2008 = 
        Calculate(
            Sum([Sales Amount]),
            Treatas({ (2007, 12), (2008, 1)},   \\ Filter Condition Sou
            'Date'[Year Number]), \\ Filter from Table 1
            'Date'[Month Number]) \\ Filter from Table 2
        )


Multiple Treat as 
    Total Budget =
        Calculate(
            Sum(Budget[Budget]),
            TREATAS(VALUES(Budget[Category]), Budget[Category]),
            TREATAS(VALUES(Budget[MonthName]), Budget[MonthName]),
            TREATAS(VALUES(Budget[Year]), Budget[Year])
        )

Without create relationship
= 
    TreatAS (Values(SourceTable[Column]),  
            TargetTable[Column] 
            )
=============================================================================            
=============================================================================
\\ If I do a similiar filter as 
-----------------------------
    Sales 2007-2008 = 
        Calculate(
            Sum([Sales Amount]),
            Treatas({2007, 2008},   \\ Filter Condition
            'Date'[Year Number]) \\ Filter from what
        )
\\ using treatAs
-----------------------------
\\ I must filter the Summarize Table as only contain 2007 & 2008, 
\\ and then match the unlinked table CalTb

CALCULATE(
    SUM(Purchase[Profit per item]), 
    TREATAS(
        SUMMARIZE(          
            'Purchase',
            'Calendar'[YearNumber]), 
        CalTb[YearNumber] )
    )


=============================================================================
=============================================================================
EVALUATE
CALCULATETABLE (
    SUMMARIZE (
        Sales,
        ROLLUP ( 'Date'[Calendar Year] ),
        "Year total", ISSUBTOTAL ( 'Date'[Calendar Year] ),
        "Amount", [Sales Amount]
    ),
    TREATAS ( { "CY 2008", "CY 2009" }, 'Date'[Calendar Year] ),
    TREATAS ( { "Bachelors", "Partial College" }, Customer[Education] )
)
ORDER BY
    [Year total],
    [Calendar Year]

Create tables without linking relationship to tables 

-Applies the result of a table expression as filters to columns from an unrelated table.
-One Table has not been related

Usage remark
    1. The ***number of columns*** specified must match the ***number of columns in the table expression*** and be in the same order.
    2. If a value returned in the table expression does not exist in the column, it is ignored. 
         DimProduct[Color]) sets a filter on - TREATAS({"Red", "Green", "Yellow"}, 
         If "Yellow" does not exist in DimProduct[Color], only are "Red" and "Green".
    3.  a relationship does not exist between the tables,  have multiple relationships ***USERELATIONSHIP****
    4.  not supported for use in DirectQuery

<!-- CALCULATE(SUM(Purchase[Price]),TREATAS('Purchase'[ProductId],TopNTable[ProductId])) -->
    e.g. 
    CALCULATE(
        SUM(Sales[Amount]), //Expression to return result
        TREATAS(
    VALUES(DimProduct1[ProductCategory]), 
    DimProduct2[ProductCategory])  
    )

    CALCULATE(
            SUM(MonthlyExpense[Expense]),
            TREATAS(
                Summarize(
                    DimDate,
                    DimDate[Year],
                    DimDate[Month],
                    MonthlyExpense[Year],
                    MonthlyExpense[Month]
                ))
                

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

    MEASURE Expense Total = 
    Calculate(
        Sum(
            MonthlyExpense[Expense]), 
                TreatAs(
                    Summarize(
                        DimDate, 
                        DimDate[Year], 
                        DimDate[Month]), 
                        MonthlyExpense[Year], 
                        MonthlyExpense[Month]
                        ),
                DimDate[month] = "December"
        )

USERELATIONSHIP
--------------------------------------------------------------------------------
Dealing with Active & InActive relationship - means having 2 date columns
Fact Table has more than 1 date

Active & Inactive relationship
    
    Active relationship, when the Main relationship connect with 
        e.g. 
            Purchase date
    InAcive relationship, when the second relationship 
        e.g. 
            Delivery Date (It will be kept disable, inactive relationship)

    FACT TABLE has 2 columns of date 
    
    Fact TB                                 DimDate
    Active(linked)  Inactive(linked)          
    |Purchase Date | Delivery Date |        |Date | Quarter | Year |

Delivery amount =
    Calculate(
        [Sales Amount],
        Userelationship(
                'Sales'[Delivery Date], //Fact Table inactive date column
                'Date'[Date] //Connecting to DateDim table Date column
        )
    )

Another example :

Total Sales by Req Date = Calculate(
        [TOTAL SALES],
        userRelationship(
            Order[RequiredDate], // Fact Table
            DimDate[Date]) // DateDim table
    )

###### Summarize and GroupBy
-Summarize can Filter first and group
-Summarize perform implicit calculation

***Important*** 
    To use value in summarize, it must be included in summarize function.

    The function layer is
Summarize(
    'Table name'
    [Group by Value],
    "Group by Value"
    Sum([Value]) \\ group function and the value to sum


Groupby                         Summarize
do Nested aggregation           DON'T Nested aggregation
DON'T do Implicit function      do Implicit function

-->  One way to see when we are using groupby and Summarize 
Whenever we use Nested aggregation, we need to use ***GROUPBY***

// Dont use, it donest work

AddColumns(
        Summarize(
            AddColumns(
                Summarize(
                    'Product',
                    'Product Category'[Category],
                    'Product SubCategory'[Category]
                ),
                "Average Price", Calculate(AVERAGE(Product[Unit Price]))
            ),
            'Product Category'[Category]
        ),
        "Max SubCat Avg Price", Calculate(Max[Average Price])
)

// Use, Current Group function allow  nested group (allow nested aggregation) 

Groupby(
    AddColumns(
        Groupby(
            'Product',
            'Product Category'[Category],
            'Product Subcategory'[Subcategory]
        ),
        "Average", Calculate(AVERAGE(Product[Unit Price]))
    ),
    'Product Category'[Category],
    "Max SubCat Avg Price", MAXX(CURRENTGROUP(), [Average Price])
)



##### GroupBy
------------------------------------------
Return with Table, Group by can not filter the table before Grouping, 
-- GROUPBY does not do an implicit CALCULATE for any extension columns that it adds.
-- GROUPBY permits a new function, CURRENTGROUP, to be used inside aggregation functions in the extension columns that it adds

-- Groupby will not do implicit function, it needs CurrentGroup()
-- No implicit function means can't use Calculate / Sum, directly apply inside Groupby
-- it must use CURRENTGROUP() + Sumx etc.

    GruopByTable = GROUPBY(
        'Purchase', 
            Purchase[CentreId], // Group 1 - How to Group 
            Purchase[ProductId], // Group 2 - How to Group 
        "Price", // Must have Grouped value name First
            SUMX(
                    CURRENTGROUP(), 'Purchase'[Price] * 'Purchase'[Quantity]), // Must use iterate group function
        "MAX Quatity",
        MAXX(CURRENTGROUP(), 'Purchase'[Quantity]),
        "Avg Price",
        AVERAGEX(CURRENTGROUP(), 'Purchase'[Price])
    )

    Max Product Sales By State = 
        VAR ProductState =
            Groupby(
                Sales, 
                Product[Product Name],
                "Sales",
                SUMX(CURRENTGROUP(), Sales[Revenue])
                )
            Return 
                MAXX(Productstates, [Sales])


##### Summarize + ROLLUP + ROLLUPGroup + IsSubtotal
    -----------------------------------------------------------------------
Summarize is to group the data 
ROLLUP provide subtotal

Use Rollup to group in Summarize and use IsSubtotal to create a group total 


    CalculateTable(
        Summarize(
            Sales,
            ROLLUP('Date'[Calendar Year]),
            "Year Total", ISSUBTOTAL('Date'[Calendar Year]), // To check is this a subtotal
            "Amount", [Sales Amount]
        ),
        TREATAS({"CY 2008", "CY2009"}, 'DATE'[Calendar Year])  \\ FILTER OF   ,  FILTER WITH Target table
        TREATAS({"Bachelors", "Partial College"}, )
    )

Example Summarize group by other table
----------------------------------
SUMMARIZE(
    Purchase,
    'Product'[ProductName],
    'Calendar'[YearNumber],
    "Price per year",
    CONVERT(SUM(Purchase[Profit per item]), INTEGER)
     )


//https://www.youtube.com/watch?v=IeaPNw_YuQc
Use Summarize, Group by / Scan
Calculate Subtotal

 
    SummarizePurchaseTb = SUMMARIZE(
        Purchase,  // table name
        'Purchase'[ProductId],  // group by 
        'Calendar'[YearNumber], // group by 
        "Purchase Amount", // Column name 
        sumx(Purchase, Purchase[Price] * Purchase[Quantity]) // how to group  Sum count Max etc
        ) 


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

SummarizeColumns
-----------------------------------------------------------------------
SUMMARIZECOLUMNS( <groupBy_columnName> [, < groupBy_columnName >]…, [<filterTable>]…[, <name>, <expression>]…)

SUMMARIZECOLUMNS is to solve when SUMMARIZE has expression inside, e.g. SUMX() filter()

if you want to summarize [Product] and [Sales]*[Unit Price] as [Profit] column, 
    maybe you will use this, but not correct

    Summarize Table = SUMMARIZE('Table','Table'[Product],"Profit",SUMX('Table','Table'[Sales]*'Table'[Unit Price]))

instead should use,

    Summarize Table-2 = ADDCOLUMNS(
        SUMMARIZE(
            'Table',            \\ Target Table to summarize(group)
            'Table'[Product]
            ),  \\ Target Column to summarize(group)
            "Profit", \\ Name of the 
            CALCULATE(  
                    \\ It will first SUMX the "" Sales *  Unit Price""
                    \\ and then display of group by 'Table'[Product]
                SUMX(
                    'Table',
                    'Table'[Sales]*'Table'[Unit Price]
                )
            )
        )

In new version of Power bi - SummarizeColumns 
    SummarizeColumns Table = 
        SUMMARIZECOLUMNS(
            'Table'[Product],
            "Profit",
            SUMX('Table','Table'[Sales]*'Table'[Unit Price]
            )
        )

SummarizeColumns(
    'Product'[Brand],
    'Date'[Calendar Year],
    Treatas({"CY 2008","CY 2009"}, 'Date'[Calendar Year]),
    Treatas({"Red","Blue"}, 'Product'[Color]),
    "Amount", [Sales Amount],
    "Qty", SUM(Sales[Quantity])
)

SUMMARIZECOLUMNS
(
    DimDate[CalendarYear],
    TREATAS({2007, 2008}, DimDate[CalendarYear]),
    "Sales", [Sales],
    "Visual Total Sales", CALCULATE([Sales], ALLSELECTED(DimDate[CalendarYear]))
)

SummarizeColumns(
    RollupAddIsSubtotal('Product'[brand], "Brand total"),
    RollupAddIsSubtotal('Date'[Calendar Year], "Year total"),
    Treatas({"CY 2008"}, 'Date'[Calendar Year]),
    Treatas({"Contoso", "Litware"}, 'Product'[Brand]),
    "Amount", [Sales amount],
    "Qty", SUM(Sales[Quantity])
)

Why have SummarizeColumns
https://community.powerbi.com/t5/Desktop/Summarize-VS-Summarizecolumn-function-in-DAX/m-p/928113

https://community.powerbi.com/t5/Desktop/Difference-Summarize-and-Summarizecolumns/m-p/920375


##### Meaning of .Date -> DimDate[DATE].DATE Date Hierachy
----------------------------------------------------------------------------------------------------------------------------------------------
***Notice*** : 
    DimDate[DATE] -> will give Last date of the Table
    If Last date in DimDate[DATE] is 21/07/2021, it will give exact this date

    e.g. 
        MAX(DimDate[DATE]) -> 21/07/2021
        lastDate(DimDate[DATE]) -> 21/07/2021
While
    DimDate[DATE].[Date] give last date of the year 
        e.g. 
            MAX(DimDate[DATE]) -> 31/12/2021
            lastDate(DimDate[DATE]) -> 31/12/2021


***Notice 2***

    Distinctcount() in DimDate[DATE].[Date] will be more than DimDate[DATE]
    because it is DimDate[DATE].[Date] 31/12/2021


--------------------------------------------------------------

In dataload > Time intelligence > already have check Auto date/time

Date Hierachy is a hidden table, Dax function can not calculate the whole table

e.g. 
    The Correct way to use  TotalMTD
    Sales Quantity MTD = TotalMTD(
        Sum(Sales[Quantity]),  
        DimDate[Date].[Date]
        )
    Does not work as 
    Sales Quantity MTD = TotalMTD(
        Sum(Sales[Quantity]),  
        DimDate[Date]
        )

##### TOTALYTD
----------------------------------------------------------------------------------------------------------------------------------------------
It culmulates only for the year

 - TOTALQTD -> It culmulates only for the Quarter
 - TOTALMTD -> It culmulates only for the Month

    Sales Quantity MTD = TotalMTD(
        Sum(Sales[Quantity]),  
        DimDate[Date].[Date]
        )

Also can specifiy the End date 
        year_end_date can be specified as "6/30", "Jun 30", "30 June"

        Sales Quantity MTD = TotalMTD(
        Sum(Sales[Quantity]),  
        DimDate[Date].[Date],
        "6/30")


##### DATESYTD vs TOTALYTD
----------------------------------------------------------------------------------------------------------------------------------------------
 - TOTALQTD
 - TOTALMTD


DATESYTD can have ***Multiple filters***, while TotalYTD can only have ***one filter***

 // Multiple filters

Calculate(
    Sum(Sales[Quantity]),
    DATESYTD(DimDate[Date].[Date]),
    Sales[Ordertype name] = "On Shop", \\ Filter number 1
    Sales[Product name] = "Formal"
)

// TOTALYTD, It gives error when 

TotalYTD = TotalYTD(
    Sum(Sales[Quantity], 
    DimDate[Date].[Date],
    Sales[Ordertype name] = "On Shop" && Sales[Product name]="Formal", \\ It will be error since it has 2 filters
    "3/31"
    )
)


TotalYTD = TotalYTD(
    Sum(Sales[Quantity], 
    DimDate[Date].[Date],
    Sales[Ordertype name] = "On Shop", \\ It works for only one filter
    "3/31"
    )
)


##### DATESINPERIOD & Calculate 3 months moving average
##### Count Month become Different When .[Date] Apply and not apply
-----------------------------------------------------------------------
DATESINPERIOD add up the figure in the period defined 


3 Month Cum Total =
    Calculate(
        [Total Sales],
        DatesInPeriod(
            DimDate[Date].[Date],
            LastDate(DimDate[Date].[Date],  \\ Starting point    From End to Start 
            -3,
            Month
            )
        )
    )

Result of Above 

    |Month|Total Sales|3 Month Cum Total|    
    |Jan |165200      | 165200|
    |Feb |146350      | 311550|    
    |Mar |171900      | 483450| -> Sum of Jan Feb Mar
    |Apr |161750      | 480000| -> Sum of Feb Mar Apr

3 months moving average
------------------------------------

    3 month Cum Avg = 
        VAR sumtotal =
            Calculate(
                [Total Sales], 
                DatesInPeriod(
                    DimDate[Date].[Date],
                    LastDate(DimDate[Date].[Date]),
                    -3,
                    MONTH
                )
            )

        VAR countmonth = 
            Calculate(
                DISTINCTCOUNT(DimDate[Date].[Month]),
                DATEINPERIOD(
                    DimDate[Date].[Date],
                    LastDate(DimDate[Date].[DATE]),
                    -3,
                    MONTH
                )
            )
    RETURN
        DIVIDE(sumtotal, countmonth, 0)

Apply .[Date] in all parameter

    countMonth = CALCULATE(
        DISTINCTCOUNT(Sales[Date].[Month]),
        DATESINPERIOD(Sales[Date].[Date],
        LASTDATE(Sales[Date].[Date]),
    -3,
    MONTH))

Apply .[Date] only in DATESINPERIOD StartDate  -> Ans 12

    countMonth = CALCULATE(
        DISTINCTCOUNT(Sales[Date].[Month]),
        DATESINPERIOD(Sales[Date],
        LASTDATE(Sales[Date].[Date]), *********
    -3,
    MONTH))

Apply .[Date] only in DATESINPERIOD First Argument  -> Ans 4

    countMonth = CALCULATE(
        DISTINCTCOUNT(Sales[Date].[Month]),
        DATESINPERIOD(Sales[Date].[Date], *********
        LASTDATE(Sales[Date]), 
        -3,  *********
        MONTH))


##### PreviousYear / PreviousMonth
-----------------------------------------------------------------------
Return previous entire period of the date 


##### PreviousYear vs SAMEPERIODLASTYEAR
-----------------------------------------------------------------------
https://community.powerbi.com/t5/Desktop/Previous-Year-vs-SAMEPERIODLASTYEAR/m-p/591924



-----------------------------------------------------------------------
##### SUMX vs Sum
    dO Calculation row by row, iterator SUMX / AVERAGEX
-----------------------------------------------------------------------
    Measure = SUMX(<table>, expression )

    e.g. 
        Sales Amount = Sumx(Sales, Sales[Unit Price] * Sales[QTY])
-----------------------------------------------------------------------
    Sum / Count (Aggregate Func)
    e.g. Total Sales = Sum(Sales[Quantity])


##### Eariler
How to Cumulative total of a column / Adding Running Balance
-----------------------------------------------------------------------

    Earlier = Current row

How to Cumulative total of a column / Adding Running Balance
Top down Running add up balance

Acc Sales by date = 
    Calculate(
        [total Sales],
        Filter(
            TableName,
            eariler(TableName[Date]) >= TableName[Date]
        )
    )

Reverse Bottom up add up balance 

Reversed Sales by date = 
    Calculate(
        [total Sales],
        Filter(
            TableName,
            TableName[Date] >= eariler(TableName[Date])
        )
    )

    Explain :
    https://www.youtube.com/watch?v=lyhS2txtZ44&ab_channel=Curbal

    |Item|Total Sales|Date| Acc Sales|
    |P1 |90000|01-01-16| 90000|
    |P2 |90000|02-01-16| 180000|
    |P3 |16000|03-01-16| 340000|
    |P4 |20000|04-01-16| 360000|
    |P5 |10000|05-01-16| 370000|

    Filter(
            TableName,
            TableName[Date] >= eariler(TableName[Date])
        )

    It compares with the row from above to bottom sequentially the operator >=, > , < , <=
     - >= is current row larger or equal to row from above to bottom

        1. 
        - The filter compare is 01-01-16 Larger than or equal to rows 
                01-01-16, 02-01-16, 03-01-16, 04-01-16, 05-01-16
        
        Result -> it will return the row of |P1 |90000|01-01-16| 90000|
                since 01-01-16 is equal to 01-01-16

        2. 
        - The filter compare is 02-01-16 Larger than or equal to rows 
                01-01-16, 02-01-16, 03-01-16, 04-01-16, 05-01-16

        Result -> it will return the row of 
            |P1 |90000|01-01-16| 90000|
            |P2 |90000|02-01-16| 180000|
                adding 90000 , 90000
        since 02-01-16 is equal to 02-01-16 and larger than 01-01-16

        , and so on

##### Create Dynamic title in Power bi report 
----------------------------------------------------------------------------------------------------------------------------------------------

Title by SPORT = IF(
    ISCROSSFILTERED('Athlete Medals'[Sport]),
    \\ "Total Medal count for" & FirstNonBlank('Athlete Medals'[Sport], True) \\ It will only pick the first selected
    or use, which concat all selected items\\ "Total Medal count for" & CONCATENATEX('Athlete Medals', 'Athlete Medals'[Sport], ", "),
    "Medal count by Sport"
)




Title by SPORT = IF(
    ISFILTERED('Athlete Medals'[Sport]) || ISFILTERED('GEO DATA'[Continent]),
    "Total Medal count for " & VALUES('Athlete Medals'[Medal] &" and "& VALUES('GEO DATA'[Continent])),
    "Medal count by Sport"
)
    
    
##### Values / Distinct / AllNoBlankRow (For calculate Total sales Denomiation, need to be careful)
Returns Scalar , One column table with unique value
- Returns the distinct values in a column
- Only return Values visible in current context
- Includes additional no-match row

---------------------------------
- Values equal to remove duplicate, pick unique value
- can not place in the table

DimItem             SalesInfo
- ITEM ID             - ITEM ID
- ITEM NAME           - Sales Amount

DimItem                     SalesInfo
ITEM ID | ITEM NAME         item id  | Sales Amount
1        clothes            1          100
2        car                1          100
3        door               2          200
                            3          300 
                            4          400

Values() -> because SalesInfo has id 4 but not in DimItem
    the function reutrn


        clothes  1
        car      1
        door     1
        (blank)  1

    Countrow is 4 

Distinct() -> Only return 3 item that listed in Dimension table

    Countrow is 3

                values  Distinct    allnoblankRow
        clothes  1      1           1
        car      1      1           1
        door     1      1           1
        (blank)  1
                4       3           3

All and allnoblankRow(Except Blank Row)
- it removes all filters  
- return all row 
- Result can be iterate by X function 
- Need table / table column 

##### Values
----------------------------------------------------------------------------------------------------------------------------------------------
return a colunm -> Removes  duplicate values 
\\ Use Dax studio to check what values has returned
    
    e.g.
    EVALUATE
	    values(Sales[Sales amount])

Title by SPORT = IF(
    ISCROSSFILTERED('Athlete Medals'[Sport]),
    "Total Medal count for" & CONCATENATEX(
        Values('Athlete Medals'), 
        'Athlete Medals'[Sport], ", "),
    "Medal count by Sport"
)


##### ParallelPeriod
----------------------------------------------------------------------------------------------------------------------------------------------

    Calculate(
        ParallelPeriod('Date', -1, Year),
        Date[Date] = Date(2008, 08, 15)
    )

##### PATH / PathContains / PathItem / PathItemReverse / PathLength
----------------------------------------------------------------------------------------------------------------------------------------------

PATH() -> give hierarchy of the row
    e.g. 
          Parent | child | child of the child (Current position)    
          1|24|2

DEFINE
    Column Account[AccountPath] = PATH(Account[AccountKey], Account[ParentAccountKey])
    Column Account[PathLength] = PATHLength(Account[AccountPath])
    Column Account[PathContains] = PATHContains(Account[AccountPath], 2)
Evaluate
    ACCOUNT
ORDER BY 
    [AccountPath]
    
|AccountKey|ParentAccountKey |AccountName              |AccountPath|PathLength|PathContains2|
|1         |                 |Profit and Loss after tax|    1      |1         |False        |
|19        |1                |Taxation                 |    1|19   |2         |False        |
|2         |24               |Income                   |    1|24|2 |3         |True         |
|4         |2                |Sale Revenue             |  1|24|2|4 |4         |True         |


DEFINE
    Column Account[AccountPath] = PATH(Account[AccountKey], Account[ParentAccountKey])
    Column Account[level1] = PathItem(Account[AccountPath], 1, Integer)
    Column Account[level2] = PathItem(Account[AccountPath], 2, Integer)
    Column Account[level3] = PathItem(Account[AccountPath], 3, Integer)
    Column Account[level4] = PathItem(Account[AccountPath], 4, Integer)
    Column Account[level1R] = PathItemReverse(Account[AccountPath], 1, Integer)
    Column Account[level2R] = PathItemReverse(Account[AccountPath], 2, Integer)
    Column Account[level3R] = PathItemReverse(Account[AccountPath], 3, Integer)
    Column Account[level4R] = PathItemReverse(Account[AccountPath], 4, Integer)
Evaluate
    ACCOUNT
ORDER BY 
    [AccountPath]



Parent and Child Function
PATH / PATHITEM / PATHITEMREVERSE / PATHLENGTH / PATHCONTAINS
-----------------------------------------------------------------------
Path -> Parent Child Function is base on Data Hierarchy

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

<!-- CALCULATETABLE(SUMMARIZECOLUMNS(
    'Purchase'[StaffId],
    'Calendar'[YearNumber],
    'Purchase'[Price]),
    TREATAS({2015}, CalTb[YearNumber])
    ) -->

