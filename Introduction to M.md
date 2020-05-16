## Introduction to M language





### Declarative and Imperative Language

The common query languages such as, SQL or, MDX  can be considered as *declative language* where is **M** is considered as a *imperative language*.

***Declarative language :***

SQL is the most common declarative language where we used to write some codes to get the desired results.

*For example :*
```SQL
SELECT Name, Color
FROM
Products
WHERE Color IN {'Black','Red'};
```

***Imperative language :***

SQL is the most common declarative language where we used to write some codes to get the desired results.

*For example :*
```M
Let
  Source = Sql.Database("localhost","AdventureWorks2017"),
  Production_Product = Source{[Schema = "Production",Item= "Product"]}[Data],
  #"Removed Other Columns" = Table.SelectColumns(Production_Product,{"Name","Color"}),
  #"Filtered Rows" = (#"Removed Other Columns",
      each ([Color]="Black" or [Color]="Red"))

In
  #"Filtered Rows"
```

### Where is M used ?

- **M** started as an add-in to Excel Power Query to help users do the complex data manipulation in an easier way.
- Now, **M** is used in the following platforms -:
  1. Power BI
  2. SSAS 2017 and above
  3. Microsoft Flow AKA Power Automate
  4. SSIS
  5. Azure Data Factory
- **M** seems to become more popular in future.

### M is Smart

There are two main reason that makes **M** smart and they are -:
1. Lazy evaluation
2. Query folding

#### Lazy Evaluation

**M** avoids unnecessary work. It performs "*lazy evaluation*",i.e., not performing any extra work until its absolutely necessary.

So, if there is something wrong in step-2 then, it will not perform any operation in the steps following.

In another way, suppose if we do a lot of transformation in a single column and at the end we deleted it then, **M** is smart enough to understand the end result of our earlier steps and will not perform any of them.

#### Query folding

Sometimes the source of our data can perform the steps much quickly than power query and by virtue of *query folding* ability, the **M** code can be transformed into the equivalent source code that can be pushed back into the data source.

So, let's say we load a dataset from *SQL Server* and then removed some rows and filtered some columns in **M**.

Now, rather than loading the entire dataset into the power query and then performing the steps in **M**, power query actually utilizes the *query folding* ability to retrieve the filtered data.

### M is relaxed language

Based on their approach, querying and data processing languages can either be very strict/uptight or, a bit relaxed.

*SQL Server Integration Services (SSIS)* comes under the strict languages category, whereas, **M** is considered to be a relaxed one.

***Benefits of a strict language :***

- Better performance
- Better accuracy
- Pre-compilation check

***Benefits of a relaxed language :***

- Easier to use
- Easier to integrate
- Handles poor schema


> "The Power query M formula language is a useful and expressive data mashup language but, it does have some limitations. For example : <u>there is no strong enforcement of the type system</u>"</br> - **Microsoft Documentation**
