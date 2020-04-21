# To build our image                                          

```bash
docker build -t helloworld-web:v1 . 
```
# To create the registry

```bash
az acr create --resource-group containersrg --name wingkwong --sku Basic
```
# To prepare docker image

```bash
docker tag helloworld-web:v1 wingkwong.azurecr.io/helloworld-web:v1
```

# To log into registry

```bash
docker login wingkwong.azurecr.io
```

# To upload docker image

```bash
docker push wingkwong.azurecr.io/helloworld-web:v1
```

# Create and Run ASP.NET Core App
```bash
mkdir helloworld
cd helloworld
dotnet new mvc
dotnet build
dotnet run
```
