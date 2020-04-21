```csharp
public static class OrderProcessor {
    [FunctionName("ProcessORders")]
    public static void ProcessORders(
        [QueueTrigger("incoming-orders", Connection="AzureWebJobsStorage")] // process storage queue messages
        CloudQueueMessage queueItem,
        [Table("Orders", Connection="AzureWebJobsStorage"] // output a storage table
        ILogger log
    )
    {
        tableBindings.Add(
            JsonConvert.DeserializeObject<Order>(queueItem.AsString);
        )
    }
}

```