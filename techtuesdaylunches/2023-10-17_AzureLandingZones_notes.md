# Prep ALZ sesjon

### Nøkkelord

1. **Cloud Computing:** Microsoft Azure Landing Zones er en tilnærming for å ta i bruk cloud computing-tjenester fra Microsoft.
2. **Skalerbarhet:** Azure Landing Zones gir mulighet for enkel og kostnadseffektiv skalerbarhet etter behov.
3. **Sikkerthet:** Sikkerhetsaspekter er innebygd, og Landing Zones hjelper med å beskytte data og systemer.
4. **Beste praksis:** Landing Zones følger bransjens beste praksiser for å bygge og administrere skyinfrastruktur.
5. **Lett å komme i gang:** Azure Landing Zones gjør det enkelt å komme i gang med skytjenester uten behov for dypt teknisk kjennskap.
6. **Administrasjon:** Tilbyr en konsistent måte å administrere ressurser og tjenester på Azure-plattformen.
7. **Kostnadsoptimalisering:** Hjelper med å kontrollere kostnadene ved å tilby forhåndsdefinerte retningslinjer og konfigurasjoner.
8. **Automatisering:** Muliggjør automatisering av oppsett og administrasjon av skyinfrastruktur.
9. **Overvåkning:** Gir verktøy for å overvåke ytelse og helse av skytjenestene dine.
10. **Compliance:** Landing Zones hjelper med å oppfylle bransje- og reguleringskrav.
11. **Fleksibilitet:** Azure Landing Zones kan tilpasses etter behov, og gir valgmuligheter for ulike scenarioer.
12. **Opplæring:** Microsoft tilbyr ressurser og opplæring for å hjelpe organisasjoner med å komme i gang med Azure Landing Zones.

### Designområder

De åtte designområdene som nevnes i Azure Landing Zones fra Microsofts Cloud Adoption Framework er:

1. **Azure billing and Active Directory Tenant (Azure-fakturering og Active Directory-tenant):** Dette området handler om administrasjon av fakturering for Azure-tjenester og oppsett av Azure Active Directory Tenant, som er en sentral komponent for Azure-miljøet.

2. **Identity and access management (Identitet og tilgangsstyring):** Dette området fokuserer på administrasjon av brukeridentiteter og tilgangsstyring til Azure-ressurser. Det inkluderer opprettelse og administrasjon av brukerkontoer, rollebasert tilgangskontroll (RBAC) og flerfaktorautentisering for økt sikkerhet.

3. **Resource organization (Ressursorganisering):** Her handler det om å strukturere og organisere Azure-ressurser på en måte som er logisk og administrerbar for organisasjonen. Dette kan inkludere bruk av ressursgrupper, ressursgruppesett og navngivningskonvensjoner.

4. **Network topology and connectivity (Nettverkstopologi og tilkobling):** Dette området omhandler design og konfigurasjon av nettverksarkitektur i Azure, inkludert oppsett av virtuelle nettverk, subnett og tilkobling til lokale nettverk. Herunder Hub-Spoke-topologi eller Virtual WAN

5. **Security (Sikkerhet):** Sikkerhetsaspektet handler om å implementere sikkerhetskontroller og prinsipper for å beskytte Azure-ressurser. Dette kan inkludere brannmurer, sikkerhetsgrupper, trusselovervåking og konformitetskontroller.

6. **Management (Administrasjon):** Administrasjon omfatter effektiv styring av Azure-ressurser. Dette inkluderer overvåkning, feilsøking, oppdateringer og konfigurasjon av ressurser.

7. **Governance (Styring):** Dette området dreier seg om å etablere retningslinjer og retningslinjer for administrasjon av Azure-ressurser. Det inkluderer administrasjon av kostnader, sikkerhet og overholdelse/samsvar. Azure Policy er sentralt her, og spesielt DeployIfNotExists og Deny.

8. **Platform automation and DevOps (Plattformautomatisering og DevOps):** Dette området handler om å automatisere prosesser for ressursimplementering og administrasjon. DevOps-prinsipper brukes for å effektivisere utviklings- og driftsoperasjoner.

Disse åtte designområdene gir en helhetlig tilnærming til å forberede organisasjonen på en vellykket implementering og administrasjon av Azure-tjenester gjennom Azure Landing Zones. De gir et rammeverk for å ta hensyn til alle viktige aspekter, fra økonomi og identitet til nettverk og sikkerhet.

### Velg landingssone

[Mer info](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/choose-landing-zone-option)

### Referanse-arkitekturer

## Deploying Enterprise-Scale Architecture in your own environment

The Enterprise-Scale architecture is modular by design and allows customers to start with foundational Landing Zones that support their application portfolios, regardless of whether the applications are being migrated or are newly developed and deployed to Azure. The architecture can scale alongside the customer's business requirements regardless of scale point. In this repository we are providing the following five templates representing different scenarios composed using ARM templates.

| Reference implementation | Description | ARM Template | Link |
|:-------------------------|:-------------|:-------------|------|
| Contoso | On-premises connectivity using Azure vWAN |[![Deploy To Azure](https://learn.microsoft.com/en-us/azure/templates/media/deploy-to-azure.svg)](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2FeslzArm%2FeslzArm.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2FeslzArm%2Feslz-portal.json) | [Detailed description](./docs/reference/contoso/Readme.md) |
| AdventureWorks | On-premises connectivity with Hub & Spoke  |[![Deploy To Azure](https://learn.microsoft.com/en-us/azure/templates/media/deploy-to-azure.svg)](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2FeslzArm%2FeslzArm.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2FeslzArm%2Feslz-portal.json) | [Detailed description](./docs/reference/adventureworks/README.md) |
| WingTip | Azure without hybrid connectivity |[![Deploy To Azure](https://learn.microsoft.com/en-us/azure/templates/media/deploy-to-azure.svg)](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2FeslzArm%2FeslzArm.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2FeslzArm%2Feslz-portal.json) | [Detailed description](./docs/reference/wingtip/README.md) |
| Trey Research | On-premises connectivity with Hub and Spoke for small Enterprises | [![Deploy To Azure](https://learn.microsoft.com/en-us/azure/templates/media/deploy-to-azure.svg)](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Ftreyresearch%2FarmTemplates%2Fes-lite.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Ftreyresearch%2FarmTemplates%2Fportal-es-lite.json) | [Detailed description](./docs/reference/treyresearch/README.md) |
| Azure Gov | Reference implementation that can be deployed to Azure gov and includes all options in a converged experience | [![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.svg?sanitize=true)](https://portal.azure.us/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2FeslzArm%2FeslzArm.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2FeslzArm%2Ffairfaxeslz-portal.json) | N/A

> The Bicep version is now available in Public Preview here: [https://github.com/Azure/ALZ-Bicep](https://github.com/Azure/ALZ-Bicep)

### ALZ Accelerator

En akselerator for etablering av infrastrukturplattformer hos kunder. Under arbeid, og krever tilbakemeldinger fra aktive konsulenter for å bli så bra som mulig.

### Etablering av ALZ

#### Terraform

[Azure Landing Zones Terraform-modulen]((https://registry.terraform.io/modules/Azure/caf-enterprise-scale/azurerm/latest)) gir en rask implementering av plattformressurser som du trenger for å administrere [Azure Landing Zones]((https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/#azure-landing-zone-architecture)) i stor skala ved hjelp av Terraform. Modulen er utformet for å forenkle implementeringen av management group-hierarkiet, Azure Policies og ressurser i nettverk og management subscriptions. Du kan finne mer informasjon om modulen  og om Azure Landing Zones [her].

Velbrukt og velprøvd modul fra Microsoft:
https://github.com/Azure/terraform-azurerm-caf-enterprise-scale

Modul fra tredjepart:
https://github.com/aztfmod/rover

#### Bicep

Azure Landing Zones Bicep-repositoriet gir en tilnærming for implementering og administrasjon av kjerneplattformkapabiliteter for konseptuell arkitektur i Cloud Adoption Framework Azure Landing Zones ved hjelp av Bicep.

I sin nåværende utgave kan hver modul implementeres separat via kommandolinjen. I fremtidige utgivelser vil det bli publisert en mer automatisert tilnærming gjennom orkestreringsmoduler. På grunn av begrensninger i Bicep og ARM i dag er dette imidlertid ikke mulig.

Det er gjort en orchestrering

Informasjon her:
https://github.com/Azure/ALZ-Bicep

#### Manuelt

Kan etableres manuelt, men det er krevende og vil gi mye merarbeid.

[ALZ Accelerator (Portal)](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options#azure-landing-zone-accelerator-approach)

## Sovereign Landing Zone (Preview)

Sovereign Landing Zone (SLZ) Preview gir en tydelig definert IaC-automatisering for implementering av workloads som bidrar til å oppfylle visse regulatoriske samsvarskrav for offentlig sektor og offentlige etater over hele verden.

### SLZ vs ALZ

SLZ Preview leveres med Sovereignty Policy Baseline innebygd og muliggjør at andre policy-samlinger, som for eksempel ALZ-Policies, kan implementeres innenfor SLZ Preview. I tillegg kan policy-samlinger som støtter kontrollrammeverk som NIST 800-171 rev2 og Microsoft Cloud Security Benchmark legges oppå SLZ Preview.

Med Sovereignty Policy Baseline kan en kunde håndheve bruk av konfidensiell databehandling (Confidential Compute) og ressurser for nøkkelbehandling for riktig implementerte arbeidsbelastninger som skal implementeres i konfidensielle management groups. Dette gjør det mulig å beskytte arbeidsbelastningsdata i ro, under overføring og mens de er i bruk, og støtter dermed en organisasjon i å oppnå sine mål for datasuverenitet.

SLZ Preview tilbyr dette gjennom tilpasset orkestrering som tillater konfigurering av hele landingssonen fra en enkelt parameterfil og kan implementeres med en enkelt kommando, noe som gjør at organisasjoner raskt kan teste SLZ Preview.

### Mer info

https://github.com/Azure/sovereign-landing-zone
https://github.com/Azure/sovereign-landing-zone/blob/main/docs/01-Overview.md
https://learn.microsoft.com/industry/sovereignty/

## Azure Monitor Baseline ALerts for ALZ

The solution is located in GitHub https://aka.ms/alz/monitor/repo and contains a list of recommended Azure Monitor metric and activity log alert rules for the Azure Infrastructure platform. We've worked to collate these alert rules into a single location with recommended values such as threshold. A full list of the alert details can be found here.
 
Each of the alert rules documented have been compiled into Azure Policy definitions and these have then been packaged into logical Policy Initiatives based on the ALZ management group structure Management groups - Cloud Adoption Framework | Microsoft Learn as demonstrated below.

- [Azure Monitor Baseline Alerts](https://techcommunity.microsoft.com/t5/azure-governance-and-management/azure-monitor-baseline-alerts-preview/ba-p/3810463)
- [Generally available](https://techcommunity.microsoft.com/t5/azure-governance-and-management/azure-monitor-baseline-alerts-amba-for-azure-landing-zone-alz-is/ba-p/3936951)


## Linker

- [GitHub](https://github.com/Azure/Enterprise-Scale/tree/main)
