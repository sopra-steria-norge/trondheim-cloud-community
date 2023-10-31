# Azure Policy Notes

## Hva er Azure Policy?

Azure Policy er en tjeneste fra Microsoft Azure som hjelper organisasjoner med å håndheve og overvåke overholdelse av retningslinjer og standarder i Azure-miljøet. Den gir en mekanisme for å implementere retningslinjer, også kjent som "policies," for ressurser i Azure.

- Trafikklys i Azure.
- Kjegler og rekkverk.
- Fartskamera og fartsmåler.

## Begreper

- Policy definition
- Policy set / Initiative definition
- Policy assignment
- Policy effect
- Assignment Scope
- Exemption
  - MG / Sub / RG / Ressurs
- Remediation
  - Add tag to resources
- Assignment identity & location (modify/remediate)

## Portal

Demo

- Overview
  - Enkel oversikt over all compliance i ditt miljø.
  - Vis compliance
- Getting started
  - Sjelden brukt, men det er noen verktøy og oppstartsgreier her
- Compliance
  - Viser samsvar i plattformen
  - Demo med compliance på Azure Subscription 2
- Remediation
  - Her kan man lage og se på remediation tasks.
  - Remediate tags policy for å vise
- Events
  - Aldri brukt, ikke helt sikker på hva det gjør.
- Definitions
  - Alle policy definitions i miljøet.
- Assignments
  - Alle policy assignments i miljøet.
  - Assign policy for å vise
- Exemptions
  - Alle policy exemptions i miljøet
  - Lag en exemption for å vise

## Struktur

### Policy definition

- display name
- description
- mode
  - all
  - indexed
- metadata
  - version
  - category
  - preview
  - deprecated
- parameters
- policy rule
  - logical evaluation
  - effect

### Policy set definition

- display name
- description
- metadata
- parameters
- policy definitions & parameters
- policy groups (this property is part of the Regulatory Compliance (Preview) feature)

### Azure EPAC

Enterprise Policy as Code

### Terraform ALZ

Innebygd policies og noen assignments

## AzAdvertizer

Bra oversikt og søking i policies, både innebygde, ALZ, og community.

[Her](https://www.azadvertizer.net/index.html)

## Enterprise Scale policies

- [Policy Definitions](https://github.com/Azure/Enterprise-Scale/tree/main/src/resources/Microsoft.Authorization/policyDefinitions)
- [Policy Set Definitions](https://github.com/Azure/Enterprise-Scale/tree/main/src/resources/Microsoft.Authorization/policySetDefinitions)
- [Role Definitions](https://github.com/Azure/Enterprise-Scale/tree/main/src/resources/Microsoft.Authorization/roleDefinitions)

## ChatGPT sier om nøkkelkonseptene i Azure Policy:

Her er en enkel forklaring på nøkkelkonseptene i Azure Policy:

1. **Policy (Retningslinje)**: Dette er reglene eller retningslinjene som du vil håndheve i Azure-miljøet ditt. En policy er et sett med betingelser som definerer kravene som må oppfylles av Azure-ressurser, for eksempel virtuelle maskiner, lagringskontoer eller nettverk.

2. **Initiativer**: En samling av policydefinisjoner kalles et initiativ. Initiativer er nyttige når du har flere policyer som hører sammen og bør brukes sammen for å sikre at en bestemt sikkerhetsstandard eller retningslinje oppfylles.

3. **Policydefinisjon**: Dette er den faktiske konfigurasjonen av en policy. En policydefinisjon inneholder detaljene om hva som skal håndheves, hvilke ressurser den gjelder for, og hvilke handlinger som skal utføres hvis retningslinjen ikke overholdes. For eksempel kan en policydefinisjon kreve at alle virtuelle maskiner i en bestemt ressursgruppe skal ha brannmuren aktivert.

4. **Håndhevelse**: Når policyer er definert, kan Azure Policy automatisk sjekke og håndheve disse retningslinjene på ressursene i ditt Azure-miljø. Dette bidrar til å sikre at ressursene overholder organisasjonens krav og standarder.

5. **Overholdelsesstatus**: Azure Policy gir oversikt over overholdelsesstatusen for ressursene. Du kan se hvilke ressurser som overholder retningslinjene og hvilke som ikke gjør det.

6. **Tvangsmidler (Remediation)**: I tilfeller der en ressurs ikke overholder en policy, kan Azure Policy automatisk prøve å rette opp dette ved å bruke forhåndsdefinerte handlinger. For eksempel kan det forsøke å aktivere brannmuren på en virtuell maskin som ikke har den aktivert.

Azure Policy er spesielt nyttig for å opprettholde sikkerhet og etterlevelse av retningslinjer i Azure-miljøer, spesielt når det er mange ressurser og flere team som administrerer dem. Det hjelper organisasjoner med å opprettholde kontroll, sikkerhet og standarder i skyinfrastrukturen.
