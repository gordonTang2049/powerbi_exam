###### Parameter
    Query Parameter

        Click Edit Query -> Manage parameters / new parameters 

        List of Value -> need to have current value
        
    Use Query Parameter in a table -> go to column -> Drop down -> filter -> dropdown (ABC icon) -> select parameter

Only Modified by PowerBi Desktop

    Param only use by Power BI Model Authors, not users


###### DirectQuery vs m Code vs Power Query vs Dax vs Advance Editor
    
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





###### Steps

    Sources -> Dataset -> reports -> dashboard

###### Synonyms (Q&A)
    
    define Synonyms (Words) in Q&A  for the data table
    
    Insert -> Q & A -> Gear(Setting) -> Field Synonyms -> With the data fields

    Insert -> Q & A -> Gear(Setting) -> teach Q&A
    
    I can Synonyms in Data modelling -> click the fields -> Properties -> General -> Synonyms

###### Data Classification Vs. Sensitivity Labels
Data Classification
-------------------------------------
    -Precaution about data
    -Awareness
    -Apply to only dashbaord

    The solution needs to minimize the configuration efforts and effect on the dashboard design.

    What data to share to who, data Sensitivity 

    Admin Portal -> Tenant Settings -> dashboard settings -> Data Classification

    -> Go to the dashboard itself -> setting

Sensitivity Labels
---------------------------------------
    -Protection of data
    -Prevent Unauthorized Access Data
    -Apply to Dashboard, Reports, DataSets & DataFlow 



###### Display in Published report -> Tab order and Layer Order 
 logical way. =>    View -> Selection -> Layer or Tab order



###### Power Query Editor-> Column quality vs profile vs distribution

    -Column Quality
    -Column distribution
    -Column profile 
        are data profiling functionalities under the View tab in Data Preview Section. 
        These functionalities help in understanding the data anomalies and statistics. 
        Out of these three functionalities, Column quality is the one that can be used to show the percentages of data that is in error, empty and valid.

    Column profile ->
        provides a deeper look into the statistics within the column. 
        This column can be used to provide many different values like the count of rows 
        but it does not help in identifying the percentage of empty cells in the column.

    Column Quality ->
        Column quality is the data preview option that is used to show the percentages of data that is in error, empty and valid.        

    Column distribution ->
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
    One Table has not been related

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
        TreatAs(Summarize(DimDate, DimDate[Year], DimDate[Month]), 
        MonthlyExpense[Year], MonthlyExpense[Month]),
        DimDate[month] = "December"
        )
-----------------------------------------------------------------------
Switch
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
###### SelectedValue

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

        

**Tips**
    Use Column Tools -> Sort by Column -> To Sort with right order


USERELATIONSHIP 

RELATEDTETABLE 

RELATED 




###### Look up table & data table
    - Look up table -> Dimension Table
    - Data Table -> Fact Table


###### Slicers
    O------O
    --> Slicer is the Horitzontal Bar
        Hortzontal -> Categories Bottom

    - provide an interactive way for users
        - sort and filter a report 

         with 2 Big Dot

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

