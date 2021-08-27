<!-- default badges list -->
![](https://img.shields.io/endpoint?url=https://codecentral.devexpress.com/api/v1/VersionRange/128598826/16.1.4%2B)
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/T371460)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
<!-- default badges end -->
<!-- default file list -->
*Files to look at*:

* [Form1.cs](./CS/WeightedAverageSample/Form1.cs) (VB: [Form1.vb](./VB/WeightedAverageSample/Form1.vb))
<!-- default file list end -->
# How to calculate a weighted average function


This example illustrates how to calculate a weighted price average for the units in stock within each product category:<br><em>Sum (Unit Price * Units In Stock) / Sum (Units In Stock)</em><br><br>To solve this task, use any of the following approaches:<br><br>1. In the first report, the summaries are calculated at the level of a data source by using an <a href="https://documentation.devexpress.com/#CoreLibraries/clsDevExpressDataAccessSqlSqlDataSourcetopic">SqlDataSource</a> component to provide data to the report. The resulting query string is illustrated below:<br>


```sql
select sum([Products].[UnitsInStock]) as [Sum_UnitsInStock],
       [Products].[CategoryID], sum(([Products].[UnitPrice] *
       [Products].[UnitsInStock])) as [Sum_PriceInStock]
  from [Products] [Products]
group by [Products].[CategoryID]
order by [Products].[CategoryID] asc
```


To view the resulting query, right-click the the report data source in the <strong>Report Explorer</strong> (under the <strong>Components</strong> category) and invoke the <strong>Query Editor</strong> by clicking the ellipsis button for the <strong>Products</strong> query. To edit the query, click the <strong>Run Query Builder</strong> button that invokes the <a href="https://documentation.devexpress.com/#XtraReports/CustomDocument17308">Query Builder</a> dialog.<br><br>2. In the second report, the group summaries are obtained by creating a <a href="https://documentation.devexpress.com/#XtraReports/CustomDocument12441">calculated field</a> with the following <a href="https://documentation.devexpress.com/#CoreLibraries/CustomDocument4928">expression</a>:<br><em>[][[CategoryID] == [^.CategoryID]].Sum([UnitPrice] * [UnitsInStock])  / [][[CategoryID] == [^.CategoryID]].Sum([UnitsInStock])</em><br>In the above expression, the '<strong>^</strong>' character is used to refer to the currently processed group.<br><br><br>Starting with  v.17.2, you can calculate a weighted average at the report level by specifying a control's expression using several built-in report summary functions. See <a href="https://documentation.devexpress.com/XtraReports/117095/Creating-Reports-in-Visual-Studio/Detailed-Guide-to-DevExpress-Reporting/Shaping-Report-Data/Using-Calculated-Fields/Calculating-a-Weighted-Average-Function">Calculating a Weighted Average Function</a> to see step-by-step instructions for all the available approaches.

<br/>


