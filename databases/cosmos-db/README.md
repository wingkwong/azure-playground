Set Variables
```
$rg="cosmosdb"
$location="westus"
$accountName="abcdcosmosdb"
$databaseName="thisismydb"
```

Create resource group
```
az group create -n $rg -l $location
```

Create Cosmos DB Account
```
az cosmosdb create -g $rg --name $accountName --kind GlobalDocumentDB --locations "West US=0" "North Central US=1" -- default-consistency-level Strong --enable-multiple-write-locations true --enable-automatic-failover true
```

Create Database
```
az cosmosdb database create -g $rg --name $accountName --db-name $databaseName
```

Retrieve Account Keys
```
az cosmosdb list-keys --name $accountName -g $rg
```

Retrieve Connection Strings
```
az cosmosdb list-connectin-strings --name $accountName -g $rg
```

Retrieve Primary Endpoint
```
az cosmosdb show --name $accountName -g $rg --query "documentEndpoint"
```