# Bicep Basics

!["Biceplogo"](.media/biceplogo.png "Biceplogo")

Grunnleggende informasjon for å legge til rette for felles forståelse.

## Agenda

- Praktisk info
- Hvem er jeg?
- Viktige begreper
- Hva er Bicep?
- Utviklingsmiljø
- Bicep vs ARM Templates
- Bicep vs Terraform
- Bicep = Next big thing?
- CI/CD

## Hvem er jeg?

!["whoami"](.media/whoami.png)

- Azure Platform and Infrastructure
  - Experienced with platform services like App Services, Azure SQL DB, AKS, AppGW with WAF, ++
  - Experienced with IaaS solutions
  - Networking in Azure (NSG, Azure Firewall, AppGW with WAF, UDR)
- Azure Management and Governance (Azure Policy, Cost Management, Azure Structure)
- PowerShell (both scripting and management)
- Azure DevOps (YAML build/release pipelines, and repos) and GitHub (repos mostly, but some workflows/actions)
- IaC
  - Modular use of ARM and PowerShell deployments with what-if
  - Terraform
  - Bicep

## Viktige begreper

- Variabel
- Parameter
- Ressurs
- Eksisterende ressursreferanse
- Modul
- TemplateSpecs
- Funksjoner
- DeploymentScope
- Interpolasjon / Interpolation
- Avhengigheter (eksplisitt/implisitt)
- Continuous Integration / Continuous Deployment (CI/CD)
- _Ternary operators_

## Hva er Bicep?

>Bicep is a domain-specific language (DSL) that uses declarative syntax to deploy Azure resources.
>It provides concise syntax, reliable type safety, and support for code reuse.
>We believe Bicep offers the best authoring experience for your infrastructure-as-code solutions in Azure.
>[Microsoft](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview) 

- Domain Specific Language (DSL) for Azure
- Satsingsområde fremover for Microsoft
- Lokalt "program" (v0.4)
- Transpilerer til ARM
- Terraformkonkurrent?
- Open source

### Project Bicep

Skjermskudd fra demonstrasjon av Mark Russinovich på Ignite 2020

!["Bicep ARM diagram"](.media/bicep-arm-diagram.png "Bicep ARM diagram")

## Utviklingsmiljø

- Visual Studio Code
- Extensions
  - Bicep
  - ARM
  - Dracula
- Settings
  - .vscode
  - user|workspace|folder

## Enkle eksempler

- [StorageAccount](storageaccount/main.bicep)
- [WebApp](webapp/main.bicep)
- [ContainerRegistry (ACR)](webapp/main.bicep)

## Hvorfor Bicep over ARM?

- Microsoft sin mer eller mindre offisielle stand er: lær Bicep, ignorer ARM atm.
  - **Hvis du ikke allerede kan ARM, lær Bicep**
- Full paritet med ARM fra dag èn

### Støtte for både private og offentlige modulbiblioteker med ACR

> Note:
> The choice between template specs and private registries is mostly a matter of preference. If you're deploying templates or Bicep files without other project artifacts, template specs are an easier option. If you're deploying project artifacts > with the templates or Bicep files, you can integrate the private registry with your development work and then more easily deploy all of it from the registry.

Privat bibliotek:

```pwsh
$RANDOM='2514'
$ACRNAME="bicepmodulesdemo$RANDOM"
$RGNAME="tia-community-demo$RANDOM-rg"

az login
az account set -s cf824313-8235-4ab9-8c52-83518a61f62f
az group create --name $RGNAME --location norwayeast


az deployment group create `
  --name bicepAcrDeploy `
  --resource-group $RGNAME `
  --template-file .\bicep\deployments\acr\deploy.bicep `
  --parameters acrName=$ACRNAME

bicep publish .\bicep\modules\storage\main.bicep --target "br:$ACRNAME.azurecr.io/bicep/modules/storage:v1"
```

Bruk av modul fra privat bibliotek:

```bicep
module storage 'br:bicepmodulesdemo#####.azurecr.io/storage:v1' = {
  scope: resourceGroup
  name: 'stgDeploy'
  params: {
    storageAccountName: '${prefix}sa${uniqueString(resourceGroup.id)}'
    skuName: sku
  }
}
```

Offentlig bibliotek:

```pwsh
$RANDOM='6123'
$ACRNAME="bicepmodulesdemopublic$RANDOM"
$RGNAME="tia-community-demo$RANDOM-rg"

az login
az account set -s cf824313-8235-4ab9-8c52-83518a61f62f
az group create --name $RGNAME --location norwayeast


az deployment group create `
  --name bicepAcrDeploy `
  --resource-group $RGNAME `
  --template-file .\bicep\deployments\acr\deploy.bicep `
  --parameters acrName=$ACRNAME `
  --parameters anonymousPullEnabled=true `
  --parameters acrSku=Premium

bicep publish .\bicep\modules\storage\main.bicep --target 'br:$ACRNAME.azurecr.io/bicep/modules/storage:v1'
```

Bruk av modul fra offentlig bibliotek:

```bicep
module storage 'br:bicepmodulesdemopublic#####.azurecr.io/storage:v1' = {
  scope: resourceGroup()
  name: 'stgDeploy'
  params: {
    storageAccountName: '${prefix}sa${uniqueString(resourceGroup().id)}'
    skuName: sku
  }
}
```

Registry alias i bicepconfig.json:

```json
{
  "moduleAliases": {
    "br": {
      "privateRegistry": {
        "registry": "bicepmodulesdemo####.azurecr.io",
        "modulePath": "bicep/modules"
      },
      "publicRegistry": {
        "registry": "bicepmodulesdemopublic####.azurecr.io",
        "modulePath": "bicep/modules"
      }
    }
  }
}
```

Bruk av modul med alias:

```bicep
module storage1 'br:publicRegistry/storage:v1' = {
  scope: resourceGroup
  name: 'stgDeploy1'
  params: {
    storageAccountName: '${prefix}sa${uniqueString(resourceGroup.id)}1'
    skuName: sku
  }
}

module storage2 'br:privateRegistry/storage:v1' = {
  scope: resourceGroup
  name: 'stgDeploy2'
  params: {
    storageAccountName: '${prefix}sa${uniqueString(resourceGroup.id)}2'
    skuName: sku
  }
}
```

### Støtte for både private modulbiblioteker med TemplateSpecs

Private fordi man må være autentisert for å bruke en TemplateSpec.

Moduler i TemplateSpecs:

> Note:
> The choice between template specs and private registries is mostly a matter of preference. If you're deploying templates or Bicep files without other project artifacts, template specs are an easier option. If you're deploying project artifacts > with the templates or Bicep files, you can integrate the private registry with your development work and then more easily deploy all of it from the registry.

```pwsh
$RANDOM=Get-Random -Maximum 10000
$SPECNAME="bicepmodulesdemopublic$RANDOM"
$RGNAME="tia-community-demo$RANDOM-rg"

#az login
#az account set -s cf824313-8235-4ab9-8c52-83518a61f62f
az group create --name $RGNAME --location norwayeast

az ts create `
  --name $SPECNAME `
  --version "1.0" `
  --resource-group $RGNAME `
  --location "norwayeast" `
  --template-file ".\bicep\modules\storage\main.bicep"
```

```pwsh
$RANDOM='6123'
$SPECNAME="bicepmodulesdemopublic$RANDOM"
$RGNAME="tia-community-demo$RANDOM-rg"

az login
az account set -s cf824313-8235-4ab9-8c52-83518a61f62f
az group create --name $RGNAME --location norwayeast

az ts create \
  --name $SPECNAME \
  --version "1.0" \
  --resource-group $RGNAME \
  --location "norwayeast" \
  --template-file ".\bicep\modules\storage\main.bicep"
```

Registry alias i bicepconfig.json:

```json
{
  "moduleAliases": {
    "ts": {
      "templateSpecs": {
        "subscription": "cf824313-8235-4ab9-8c52-83518a61f62f",
        "resourceGroup": "tia-community-demo6123-rg"
      }
    }
  }
}
```

Bruk av modul med og uten alias:

```bicep
module storage 'ts:cf824313-8235-4ab9-8c52-83518a61f62f/tia-community-demo6123-rg/storageSpec:v1' = {
scope: resourceGroup
  name: 'stgDeploy1'
  params: {
    storageAccountName: '${prefix}sa${uniqueString(resourceGroup.id)}1'
    skuName: sku
  }
}
module storage 'ts:templateSpecs/storageSpec:v1' = {
scope: resourceGroup
  name: 'stgDeploy1'
  params: {
    storageAccountName: '${prefix}sa${uniqueString(resourceGroup.id)}1'
    skuName: sku
  }
}

```

### Moduler istedenfor nested templates

Eksempel:

- [json](nestedtemplate/main.json)
- [bicep parent](nestedtemplate/main.bicep)
- [bicep child](nestedtemplate/nested_nestedTemplate1.bicep)

### Syntaks er mer forståelig (intuitiv)

Output i json:

```json
"outputs": {
  "hostname": {
      "type": "string",
      "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses', variables('publicIPAddressName'))).dnsSettings.fqdn]"
    },
}
```

Samme output i Bicep:

```bicep
output hostname string = publicIP.properties.dnsSettings.fqdn
```

- StorageAccount
  - [json](storageaccount/main.json)
  - [bicep](storageaccount/main.bicep)
- WebApp
  - [json](webapp/main.json)
  - [bicep](webapp/main.bicep)

[Mer info](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/compare-template-syntax)

### Bedre håndtering av implisitte avhengigheter automatisk

- SqlDb
  - [json](sqldb/main.json)
  - [bicep](sqldb/main.bicep)
- WebAppRg
  - [json](webappRg/main.json)
  - [bicep](webbppRg/main.bicep)

### Ternary operators

Simple example:

```bicep
param input string = ''
var calculatedVariable = input != '' ? input : 'No input provided in parameter'
output calculatedVariable string = calculatedVariable
```

More complex example with a Virtual Network Gateway:

[VnetGateway](https://github.com/Azure/ResourceModules/blob/main/arm/Microsoft.Network/virtualNetworkGateways/deploy.bicep)

!["vnetgateway"](.media/vnetgateway.png "vnetgateway")

## Hvorfor Bicep over Terraform?

- Umiddelbar native støtte for ny funksjonalitet
  - Private previews
  - Public previews
- Umiddelbar støtte for alle ressurstyper og API-versjoner
- Ingen state-fil å håndtere
  - Azure er "state-filen" din, og den lagres ikke noe eksternt sted
- Viktig satsingsområde for Microsoft
- Sidestilles med ARM i "first class Azure citizen": Bicep, ARM, og Terraform
  - Streber etter å tilby samme opplevelse ved deployment, så langt det lar seg gjøre for Enterprise Scale Landing Zones
  - De jobber med "bicep-ifisering" av ESLZ
- Mye likheter med Terraform, men kompleksiteten i syntax er lavere
- Lite/ingen ekstra konfigurasjon (backend, providers, ++)
- Planlagt støtte for K8s og Microsoft Graph(!) på sikt
- Lav oppstartskost som ARM med noen av fordelene til Terraform syntax og funksjonalitet
- Open source og ingen ekstra kostnad for bruk

[Mer info](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview#benefits-of-bicep-versus-other-tools)

## Xbox og Bicep

Bilder fra Community Call Oct '21

!["Xbox what we're deploying"](.media/xbox1.png "Xbox what we're deploying")

!["Xbox why we're using"](.media/xbox2.png "Xbox why we're using")

!["Xbox common patterns"](.media/xbox3.png "Xbox common patterns")

!["Xbox common patterns"](.media/xbox4.png "Xbox common patterns")

!["Xbox interesting stuff"](.media/xbox5.png "Xbox interesting stuff")

!["Xbox interesting stuff"](.media/xbox6.png "Xbox interesting stuff")

## Bicep = Next big thing?

- Nei, "__current big thing__"
- Bicep er allerede aktivt i bruk flere steder
- "Alle" driver med det
- Forvent forbedringer og videreutvikling
- Lær det om IaC på Azure er interessant

## CI/CD

- GitHub Workflows
  - Kommer tilbake til det i neste sesjon
- Azure DevOps Pipelines
  - Hopper over denne, da AzDO uansett er på vei ut
- Gitlab
  - Kunne gjort noe her, men det blir i så fall ganske likt som GitHub uansett.
- DevSecOps
  - Checkov (Infrastructure Compliance check)
  - Linter vNext (Bicep) / ARM-TTK (ARM)
  - Snyk (Infrastructure Security analysis)
- AzOps
  - AzOps-Accelerator - for ferske Azure Site Reliability Engineers
  - Blir litt låst inn i AzOps, og det er kanskje ikke ønskelig
  - Bruker AzOps-modul i PowerShell
