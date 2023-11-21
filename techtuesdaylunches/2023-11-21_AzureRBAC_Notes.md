# Notater til Azure Tilgangsstyring

## Forhåndskunnskap

- [Struktur](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-setup-guide/media/organize-resources/scope-levels.png) (Management Grroup -> (Child management group) -> Subscription -> Resource Group -> Resource -> Sub-Resources)
- Azure-tilgang er forskjellig fra Entra ID-tilgang
  - En Entra ID Global Administrator har ikke automatisk Owner på Azure-ressurser.
- Entra ID brukere, grupper, service principals, og managed identities kan tildeles tilgang i Azure

## Azure Role-Based Access Control

- Rollebasert tilgangsstyring
- [Forhåndsdefinerte roller / Built-in Roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)
- [Skreddersydde roller / Custom Roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/custom-roles)
- Hvem? (Assignee)
- Hva? (Role)
- Hvor? (Scope)

## Azure Attribute-Based Access Control (kun for storage accounts)

- Rollebasert tilgangsstyring med betingelser
- Mer finkornet tilgangskontroll
- Kan redusere antall tildelinger
- Bruk atributter som har betydning i bedriften

Eksempler på bruk:

- Lesetilgang til blobs med taggen Prosjekt=Skred
- Nye blobs må inkludere taggen Prosjekt=Skred
- Eksisterende blobs må merkes med minst én prosjektnøkkel eller programnøkkel
- Eksisterende blobs må merkes med en prosjektnøkkel og verdier som Skred, Baker eller Skagit
- Les, skriv eller slett blobs i containere med navnet blobs-eksempel-beholder
- Lesetilgang til blobs i containere med navnet blobs-eksempel-beholder med en sti som er skrivebeskyttet
- Skrivetilgang til blobs i containere med navnet Contosocorp med en sti som er opplastinger/contoso
- Lesetilgang til blobs med taggen Program=Alpine og en sti som er logger
- Lesetilgang til blobs med taggen Prosjekt=Baker og brukeren har en tilsvarende attributt Prosjekt=Baker
- Lesetilgang til blobs i en spesifikk dato-/tidsserie.
- Skrivetilgang til blobs kun via en privat kobling eller fra et spesifikt subnett.

Tilgjengelige med følgende roller:

- Storage Blob Data Contributor
- Storage Blob Data Owner
- Storage Blob Data Reader
- Storage Queue Data Contributor
- Storage Queue Data Message Processor
- Storage Queue Data Message Sender
- Storage Queue Data Reader

## Hvordan "gi seg selv tilgang" som global administrator i Entra ID?

- ["Access management for Azure resources"](https://learn.microsoft.com/en-us/azure/role-based-access-control/elevate-access-global-admin)
- Gir "User Access Administrator" på Tenant Root Management Group (TRG)
- Man kan så gi seg selv alle rettigheter på alle nivåer
- Deretter kan man slå av denne funksjonen og fortsatt ha all tilgang

## Arving av rettigheter

- Alle tilganger arves nedover i hierarkiet
- Arv kan ikke slås av i noen ledd
- Deny assignments ikke mulig uten deployment stacks eller blueprints (som ikke bør brukes)

## Hva er en assignment?

- En entitet får tilgang til å gjøre noe i et eller annet scope.

## Tildeling av rettigheter

- Hvem trenger tilgang?
  - Bruker/Gruppe/Service principal/Managed identity
- Hva trenger de tilgang til å gjøre?
  - Owner/Reader/Contributor/++
- Hvor trenger de tilgang?
  - Management group/Subscription/Ressursgruppe/Ressurs/Under-ressurs
- Alltid tenk least privilege!!
  - Ikke tildel owner eller user access administrator til hvem som helst.
- Bare brukere med "Owner"-, eller "User Access Administrator"-rollen kan tildele rettigheter til andre.

### Tildeling i portalen

DEMO

### Tildeling i Azure CLI

```bash
az role assignment create --assignee "<objectId>" \
--role "<roleName>" \
--scope "/subscriptions/<subscriptionId>"

# Example
az role assignment create --assignee "55555555-5555-5555-5555-555555555555" \
--role "Storage Blob Data Contributor" \
--scope "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Example-Storage-rg/providers/Microsoft.Storage/storageAccounts/storage12345"
```

### Tildeling i Azure PowerShell

```powershell
New-AzRoleAssignment -ObjectId <objectId> `
-RoleDefinitionName <roleName> `
-Scope /subscriptions/<subscriptionId>

# Example
New-AzRoleAssignment -ObjectId 66666666-6666-6666-6666-666666666666 `
-RoleDefinitionName "Storage Blob Data Contributor" `
-Scope "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Example-Storage-rg/providers/Microsoft.Storage/storageAccounts/storage12345"
```

### Granulær tilgangsstyring

- Tildel tilgang på kun en spesifikk container i en storage account
- Tildel tilgang på kun en spesifikk secret i key vault
- Tildel tilgang på kun et spesifikt namespace i eventhub

##  Innebygde Rolledefinisjoner (Built-in Role Definitions)

Alltid bruk en av de innebygde hvis de tilfredsstiller kravene til least privilege. Vedlikehold av custom roles kan kreve en del oppfølging.

- Owner = Kan gjøre alt (nylig fått innebygd Storage Account Data Access)
- Contributor = Kan gjøre alt unntatt tildeling av rettigheter (nylig fått innebygd Storage Account Data Access)
- Reader = Kan lese det meste men ofte ikke data (Key Vault Secrets, Storage Account Blobs/Shares)
- Storage Blob Data Contributor = Kan lese og skrive data i storage blobs

Utilsiktet konsekvens av Owner/Contributor-tildeling? Man får lese/skrivetilgang til all data i storage accounts hvor shared access keys er aktivert.

## Skreddersydde rolledefinisjoner (Custom Role Definitions)

Hjemmelagde rolledefinisjoner for å enten samle flere roller i ett, eller lage en mer restriktiv versjon av en rolle. Lagres i et scope, som oftest i en management group langt oppe. Rolle kan brukes som angitt i "assignableScopes". Må lages i json-format.

### Owner

```json
{
  "assignableScopes": [
    "/"
  ],
  "description": "Grants full access to manage all resources, including the ability to assign roles in Azure RBAC.",
  "id": "/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
  "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": [],
      "dataActions": [],
      "notDataActions": []
    }
  ],
  "roleName": "Owner",
  "roleType": "BuiltInRole",
  "type": "Microsoft.Authorization/roleDefinitions"
}
```

### Reader

```json
{
  "assignableScopes": [
    "/"
  ],
  "description": "View all resources, but does not allow you to make any changes.",
  "id": "/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
  "name": "acdd72a7-3385-48ef-bd42-f606fba81ae7",
  "permissions": [
    {
      "actions": [
        "*/read"
      ],
      "notActions": [],
      "dataActions": [],
      "notDataActions": []
    }
  ],
  "roleName": "Reader",
  "roleType": "BuiltInRole",
  "type": "Microsoft.Authorization/roleDefinitions"
}
```

F.eks. en owner-rolle, men man vil ikke at rolleinnehaver skal kunne endre på nettverk. Legg inn microsoft.network/* under NotActions.

Gjort ganske enkelt i Azure CAF terraform-modul.

## Liste ut roller

### PowerShell

```powershell
# All roles
Get-AzRoleDefinition -Scope "/providers/Microsoft.Management/managementGroups/<groupid>"

# Only custom roles
Get-AzRoleDefinition -Scope "/providers/Microsoft.Management/managementGroups/<groupid>" `
| Where-Object {$_.IsCustom}
```

### Azure CLI

```bash
# All roles
az role definition list --scope "/providers/Microsoft.Management/managementGroups/<groupid>"

# Only custom roles
az role definition list --scope "/providers/Microsoft.Management/managementGroups/<groupid>" \
--custom-role-only
```

## Liste ut assignments

PowerShell lister kun de assignments i scopet du angir, ikke assignments som ligger lenger nede i "arverekken".

```powershell
Get-AzRoleAssignment -Scope "/providers/Microsoft.Management/managementGroups/<groupid>"
```

```bash
az role assignment list --all --include-inherited --include-groups
```

Azure Resource Graph!

```groovy
authorizationresources
| where type =~ "microsoft.authorization/roleassignments"
| where id startswith "/subscriptions"
| extend RoleDefinitionId = tolower(tostring(properties.roleDefinitionId))
| extend PrincipalId = tolower(properties.principalId)
| extend RoleDefinitionId_PrincipalId = strcat(RoleDefinitionId, "_", PrincipalId)
| join kind = leftouter (
  authorizationresources
  | where type =~ "microsoft.authorization/roledefinitions"
  | extend RoleDefinitionName = tostring(properties.roleName)
  | extend rdId = tolower(id)
  | project RoleDefinitionName, rdId
) on $left.RoleDefinitionId == $right.rdId
| summarize count_ = count(), Scopes = make_set(tolower(properties.scope)) by RoleDefinitionId_PrincipalId,RoleDefinitionName
| project RoleDefinitionId = split(RoleDefinitionId_PrincipalId, "_", 0)[0], RoleDefinitionName, PrincipalId = split(RoleDefinitionId_PrincipalId, "_", 1)[0], count_, Scopes
| where count_ > 0
| order by count_ desc
| order by ['RoleDefinitionName'] asc
```

## Privileged Identity Management

- Elevering av tilgang "Just-In-Time"
- Automatisk eller manuell godkjenning
- Logging av eleveringer (også mulig med e-postvarsling)

## Delegering av RBAC-tildeling

- Delegere kun visse RBAC-rolletildelinger
- [Delegate Role Assignments](https://learn.microsoft.com/en-us/azure/role-based-access-control/delegate-role-assignments-portal?tabs=template)

## Azure RBAC beste praksiser

Oppsummert:

- Kun gi tilgangen brukerne trenger
- Begrens antall subscription owners
- Begrens priviligerte rolletildelinger
- Bruk PIM
- Tildel roller til grupper istedenfor brukere
- Bruk roleId for tildeling istedenfor roleName
- Unngå wildcard actions når man lager skreddersydde rolledefinisjoner

[Mer utfyllende](https://learn.microsoft.com/en-us/azure/role-based-access-control/best-practices)
