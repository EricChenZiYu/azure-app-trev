dotnet new webapp -o Azure-App-Trev
dotnet publish -o publish
cd .\publish\
Compress-Archive * publish.zip
az group create --location eastus2 --resource-group az-group-rg2
az appservice plan create --name az-trev-plan --resource-group az-group-rg2 --sku B1

az webapp create --resource-group az-group-rg2 --plan az-trev-plan --name az-trev-app 

az webapp deployment source config-zip --resource-group az-group-rg2 --name az-trev-app --src .\publish.zip

az webapp browse --resource-group az-group-rg2 --name az-trev-app