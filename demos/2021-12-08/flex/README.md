# Bicep Flex

!["Spongebob"](.media/spongebob.png "Spongebob")

Mer avanserte demonstrasjoner for å vise hvordan Bicep er i bruk.

## Agenda

- Bicep <-> Json
- Private registre
- Offentlige registre
- Delte variabler
- Bicep Visualizer
- Mer avansert Bicep
  - Hub-spoke deployment
- GitHub Workflow
  - Deploy av ressurser
  - Validering av deploy
  - What-If deployment
- Azure/ResourceModules
  - Hva er det?
  - Hvor finner vi det?
  - Hva kan det brukes til?

## Bicep <-> Json

Konvertering fram og tilbake:

```bash
bicep --version
bicep --help

bicep build --help
bicep build main.bicep

bicep decompile --help
bicep decompile main.json
```

## Private registre

Automatisk publisering
Vis allerede etablert enkelt [eksempel](../../.github/workflows/bicep-publish.yml).

Bare et enkelt eksempel. Dette er ikke en riktig måte å sette opp på i f.eks. produksjon, men en måte å gjøre det på for å få publisert alle moduler.
Alle modulene vil med denne løsningen måtte inkrementeres for å kunne endre en enkelt modul.
Microsoft jobber med en måte å gjøre dette enklere på i sitt eget offisielle repository.

## Offentlige registre

[Azure/ResourceModules](https://github.com/Azure/ResourceModules)

Muligheter for et slags "InnerSource" med anonyme ACR.

Dessverre ikke kommet ny funksjonalitet for dette enda, men det kommer snart!

!["future release updated nov"](.media/future-release1.png "future release updated nov")

!["future release updated dec"](.media/future-release2.png "future release updated dec")

## Delte variabler

Lagre følgende i en tilgjengelig json (repository root/shared/shared-prefixes.json):

```json
{
    "storageAccountPrefix": "stg",
    "appServicePrefix": "app"
}
```

Importer filen i en bicep deployment (repository root/deployment):

```bicep
var sharedNamePrefixes = json(loadTextContent('../../shared/shared-prefixes.json'))
```

Bruk de delte navnene i en deployment:

```bicep
var appServiceAppName = '${sharedNamePrefixes.appServicePrefix}-myapp-${uniqueString(resourceGroup().id)}'
var storageAccountName = '${sharedNamePrefixes.storageAccountPrefix}myapp${uniqueString(resourceGroup().id)}'
```

[Doc](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/patterns-shared-variable-file)

## Mer avansert Bicep

### Enkel hjemmesnekret hub-spoke

- Vis og forklar kode
  - Start med modulbibliotek
    - Forklar hvor det kommer fra, hvem som har laget
    - Vis enkel readme-fil i en av modulene for selvhjelp
  - Fortsett med solutions
    - Forklar hub
    - Forklar spoke
    - Forklar tieredapp
  - Fortsett med [main.bicep](hub-spoke/main.bicep)
    - Forklar oppbygging
  - Fortsett med konseptet "layering"
    - Atomiske moduler i bunn
    - Solutions er neste som kombinerer forskjellige moduler i større systemer

Deployment:

```pwsh
cd .\bicep\demos\flex\hub-spoke\
az deployment mg create --template-file main.bicep `
--parameters "hubSubscriptionId=cf824313-8235-4ab9-8c52-83518a61f62f" `
--parameters "spoke1SubscriptionId=cf824313-8235-4ab9-8c52-83518a61f62f" `
--parameters "spoke2SubscriptionId=cf824313-8235-4ab9-8c52-83518a61f62f" `
--management-group 0c178fd5-1459-41d5-8731-3908efd207ea `
--location norwayeast
```

### Azure Kubernetes Service

- Vis og forklar kode
  - Start med modulbibliotek
    - Forklar hvor det kommer fra, hvem som har laget
    - Vis enkel readme-fil i en av modulene for selvhjelp
  - Fortsett med solutions
    - AKS

```pwsh
cd .\bicep\demos\flex\hub-spoke\solutions\aks\
az deployment group what-if --resource-group tia-aks-rg `
--template-file deploy.bicep `
--parameters 'baseName=tia-aks' `
--parameters aadGroupIds="['fcf6fa6a-f05a-45dd-a5a2-f22bbc9db105']" `
--parameters 'vnetResourceId=/subscriptions/cf824313-8235-4ab9-8c52-83518a61f62f/resourceGroups/tia-network-rg/providers/Microsoft.Network/virtualNetworks/vnet01'

cd .\bicep\demos\flex\hub-spoke\
az deployment mg create --template-file main.bicep `
--parameters "hubSubscriptionId=cf824313-8235-4ab9-8c52-83518a61f62f" `
--parameters "spoke1SubscriptionId=cf824313-8235-4ab9-8c52-83518a61f62f" `
--parameters "spoke2SubscriptionId=cf824313-8235-4ab9-8c52-83518a61f62f" `
--management-group 0c178fd5-1459-41d5-8731-3908efd207ea `
--location norwayeast
```

```bash
az deployment group what-if --resource-group 'tia-aks-rg' \
--template-file '.\main.bicep' \
--parameters 'baseName=tia-aks' \
--parameters aadGroupIds='("fcf6fa6a-f05a-45dd-a5a2-f22bbc9db105")' \
--parameters 'vnetResourceId=/subscriptions/cf824313-8235-4ab9-8c52-83518a61f62f/resourceGroups/tia-network-rg/providers/Microsoft.Network/virtualNetworks/vnet01'
```

## Bicep Visualizer

Vis bicep fil for AVD og hub-spoke.

## GitHub Workflow

Formål: Etablere ressurser (TieredApp solution) fra bicep template

Viktige punkter:

- GitHub Workflows generelt
- GitHub Actions generelt

- Spesielle GitHub Actions
  - Kobler opp etter GitHub beste praksis
  - [Ikke anbefalt å ha strukturert data i secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#naming-your-secrets)
  - Dvs. [Microsoft anbefaler](https://github.com/marketplace/actions/azure-login#configure-a-service-principal-with-a-secret) å bruke json-data som secret for az login men GitHub anbefaler å ikke gjøre det.
  - Leste et eller annet sted at az login action håndterer secret creds på en sikker måte, så det skal ikke være et stort sikkerhetshull.
  - Utfordringen kommer hvis man kjører noe output til logg, for da klarer ikke GitHub å automatisk redacte secret.

```yaml
---
env:
  Subscription: ${{ secrets.SUBSCRIPTION_ID }}
  AppID: ${{ secrets.APP_ID }}
  AppSecret: ${{ secrets.APP_SECRET }}
---
- name: Connect to Azure
  uses: torivara/AzConnect@v1
```

- Triggers
  - Push
  - PR
  - Workflow Dispatch

```yaml
---
on:
  workflow_dispatch:
  pull_request:
    paths:
      - '.github/workflows/resourcegroup.yml'
      - 'demos/flex/hub-spoke/solutions/tieredapp'
  push:
    branches:
      - main
    paths:
      - '.github/workflows/resourcegroup.yml'
      - 'demos/flex/hub-spoke/solutions/tieredapp'
---
```

## Azure/ResourceModules

- Hva er det?
- Hva kan vi bruke det til?
- Hva er Microsoft sine planer framover?
- Hvem kan bidra?

## Takk for meg

God jul

```plaintext
    |,\/,| |[_' |[_]) |[_]) \\//
    ||\/|| |[_, ||'\, ||'\,  ||

            ___ __ __ ____  __  __  ____  _  _    __    __
           // ' |[_]| |[_]) || ((_' '||' |,\/,|  //\\  ((_'
           \\_, |[']| ||'\, || ,_))  ||  ||\/|| //``\\ ,_))
                                                               

                                         ,;7,
                                       _ ||:|,
                     _,---,_           )\'  '|
                   .'_.-.,_ '.         ',')  j
                  /,'   ___}  \        _/   /
      .,         ,1  .''  =\ _.''.   ,`';_ |
    .'  \        (.'T ~, (' ) ',.'  /     ';',
    \   .\(\O/)_. \ (    _Z-'`>--, .'',      ;
     \  |   I  _|._>;--'`,-j-'    ;    ',  .'
    __\_|   _.'.-7 ) `'-' "       (      ;'
  .'.'_.'|.' .'   \ ',_           .'\   /
  | |  |.'  /      \   \          l  \ /
  | _.-'   /        '. ('._   _ ,.'   \i
,--' ---' / k  _.-,.-|__L, '-' ' ()    ;
 '._     (   ';   (    _-}             |
  / '     \   ;    ',.__;         ()   /
 /         |   ;    ; ___._._____.: :-j
|           \,__',-' ____: :_____.: :-\
|               F :   .  ' '        ,  L
',             J  |   ;             j  |
  \            |  |    L            |  J
   ;         .-F  |    ;           J    L
    \___,---' J'--:    j,---,___   |_   |
              |   |'--' L       '--| '-'|
               '.,L     |----.__   j.__.'
                | '----'   |,   '-'  }
                j         / ('-----';
               { "---'--;'  }       |
               |        |   '.----,.'
               ',.__.__.'    |=, _/
                |     /      |    '.
                |'= -x       L___   '--,
                L   __\          '-----'
                 '.____)


                             _._______....__
                           .:"`       `''"""'':....__
                        ::"`        _             `'''::..  
                     ..::'  `-../''' '''--':::._         `:.
                  .:'                      '  `":._        `.
                  :                              `":        `.
                 :'                                :.        `:.
               .:'                                  ::.        `.
              :                                      `:.         `.
              :           .. __ _...._                `::.        `:.
             .::  _..:":::' `  `      `':''  .  :       :::.       `:
           .:.   `:'  :..-. :.\_        .-':'::' :       `::        :
          :.-    ::    :   `'           '    '  '::..     ::       .'
          `.-    :    /'                     .   `: `:.  .:'      .'
          .:      :  : :'  .---._        _.----.  :   :  `:      :
        .:`:      `::' _: .:  O :.'.  .'. : O  :  `-.`:   :.     :....._.
        `: '      .'' .---  `""'   :  :    `""'   .  `.`.  `'-._.-'   `:`:.
         :.    .-'   :             :  :           \  .'  `.    `:         ::.
        .::   :      :       ___:       `.._      ::    .  `     `.        .:
       .:'    `:     `.   .-"   ` '._.'  '  `-._ .'  .. :         :        `:
      `-.-        .   `:''                      `'  ' : `:.'    .:        `:'
      :' _.    .: `"""'  ..    ._.------._      .    .:  `"     ::        .:
   .:"'""'      /--...--'  `--'  `......' `----'"'"""":         `":.__..'''
   :          :'     .'         `._____.'              `.          ':
  ::    .'   .:     :                                   :           `:
 ,:`   :'  .:'      :                                    `:.         :
 :'        :        :                                      :          `.
,:         :        `:                                     :           :
:'         :         :                                     :           :
:          `.        `                                   .'           .'
:           :                                            :            `.
`:.          `                                           `             `.
 `:                                                                     :
  `.                                                                   .'
   `.                                                                  :
    `.                                                                .'
     :.                                                            ..'
     `:                                                            `.
      `:.                                                           :
        `:.                                                         :
           `.                                                       :
            `.                                                  _.-'
             `:...                                           .''
               `''`:.......                             ___.'
                         `:::.                   .-....'
                            ``-..._______....-'`\:
                                 `'''''''
```

## Mer info

- [Bicep Docs Overview](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/)
- [Bicep File Structure and Syntax](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/file)
- [Bicep Best Practices](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/best-practices)
- [Bicep Patterns](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/patterns-configuration-set)

<!--
### AVD ala Frank Beerson hvis tiden tillater

- Moduler
- Referanser
- Interpolering
- Conditional deploy
- Ternary operators

Kjør deploy i spoke 1 og se at det fungerer og at ressurser blir etablert
-->
