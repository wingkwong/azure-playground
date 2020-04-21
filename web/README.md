```
$rg = "guccigang"
$planname = "thisismyplan"
$appname = "helloworld"
$container = "microsoft/dotnet-samples:aspnetapp"
```

create resource group 
```
az group create -n $rg -l westus
```

create app service plan
```
az app service plan create -n $planname -g $rg --sku B1 --is-linux
```

create web app
```
az webapp create -n $appname -g $rg --plan $planname -deployment-container-image-name $container
```

configure github deployment
```
az webapp cnfig appsettings set -g $rg -n $appanme --settings WEBSITES PORT=80
```
