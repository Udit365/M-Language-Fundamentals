## Data Extraction



### Extraction from flat files

#### CSV file

The **M** syntax for extracting data from a *CSV* file is :
```m
Source = File.Contents("file location/fileName.csv"),
CSV = Csv.Document(Source, [Delimiter=",", Columns = 3, Encoding = 1252, QuoteStyle = QuoteStyle.None]),
#"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars = true]),
......
.....
```

In Power Query, we actually don't have to write all these long codes rather, we can play with the GUI to do so.

Here is the example of *M-Script* that extracts and loads data from a *CSV* file named *ChessGame* -:

```M
let
    Source = Csv.Document(File.Contents("C:\Users\udit.chatterjee\Desktop\M-Language\Datasets\ChessGame.csv"),[Delimiter=",", Columns=3, Encoding=65001, QuoteStyle=QuoteStyle.None]),
    #"Promoted Headers" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Changed Type" = Table.TransformColumnTypes(#"Promoted Headers",{{"Year", Int64.Type}, {"Rounds", Int64.Type}, {"Winner", type text}})
in
    #"Changed Type"
```

#### XML File

The common hierarchical data formats are :
1. XML files
2. JSON files

M-code syntax for parsing a *XML* document :

```M
let
  Source = Xml.Tables(File.Contents("file location\fileName.xml")),
  TableName = Source{0}[Table name],
  .....
  ....
in
  #"Changed Type"
```
#### JSON File

M-code syntax for parsing a *JSON* document :

```M
let
  Source = Json.Document(File.Contents("file location\fileName.json")),
  TableName = Source{0}[Table name],
  .....
  ....
in
  #"Changed Type"
```
