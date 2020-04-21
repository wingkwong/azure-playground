# Table Query

```csharp
 public static async Task<List<YOUR_TABLE_OBJECT>> FindByFieldAsync(
            CloudTable table, string field) 
{
    var filterCondition = TableQuery.GenerateFilterCondition("<FIELD>", QueryComparisons.Equal, field);
    var query = new TableQuery<YOUR_TABLE_OBJECT>().Where(filterCondition);
    var results = await table.ExecuteQuerySegmentedAsync(query, null); 
    return results.ToList();
}
```