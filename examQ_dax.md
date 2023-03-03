
Q:
    The Sales table contains distinct order entries.
    You have this DAX measure:
        ```Average Price All Orders =  CALCULATE ( AVERAGE ( Sales[TotalPrice] ), ALL ( Sales ) )```
        - DAX formula -> Above Average Orders measure.
        ***COUNT the orders*** where
            TotalPrice > the Average Price All Orders measure
        
    A:
        Above Average Orders =
            Calcalate(
                CountRows(Sales),
                Filter(Sales, Sales[TotalPrice] > [Average Price All Orders])
            )

    Using multiple nested functions that might include previously 
    calculated measures is an important skill for any Power BI analyst, 
    especially for ones that might be asked around 50 questions at a time about the topic for whatever reason. 

    Please refer to the DAX reference for the syntax. 
    The only way to really get to know these is to use them repeatedly in exercises.  Good luck.
    https://docs.microsoft.com/en-us/dax/calculate-function-dax


Q:
    What are the conditions for the DAX ***RELATED()*** function to work?

    A:
        - There must be a relationship between the tables
        - It can be used as a calculated column
        - It can only be used in a measure if used in conjunction with an iterator function
        - Require row-context

    Explain:
    - RELATED ( ) returns a related value from another table. 
    - It requires a relationship to exist between the tables 
    and 
    must be given row-context either by using it in a calculated column or by using an iterator function like SUMX.
    Measures are global and its table home has no effect.  Filter-context is not a requirement.

    https://docs.microsoft.com/en-us/dax/related-function-dax


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

Switch
    - use True(), if test a range
    - Simplely lookup value, if match one to one, e.g. Customer[Card] "Blue", "Standard"





#### DAX Search 
Q:
    You have a table with the following schema:
    Table name = Pets
    Column name = Enclosure
    Row content = Doghouse
    Data type = Text
        What does the following DAX formula return?
    Return = SEARCH ( "house", Pets[Enclosure], 1, BLANK ( ) )

    A: 
        4 , 
            Search function search the word "House", Start from 4th character, If not found Blank()
    
    Explain:
        SEARCH(<find_text>, <within_text>[, [<start_num>][, <NotFoundValue>]])

    https://docs.microsoft.com/en-us/dax/search-function-dax


Q:
    Give the DAX formula for 
        calculating the average price (ProductPrice column) for products (Products table) 
        ***regardless of the filter applied to products*** on the visual.

    A:
        APAP =
            Calculate(
                Average(Products[ProductPrice]), all(Products)
            )


    Explain:
    Be aware of the 
        basic syntax of all commonly used DAX expressions like 
        CALCULATE, SUMX, SUM, FILTER etc. for the exam.

Use Calculate remove all filter