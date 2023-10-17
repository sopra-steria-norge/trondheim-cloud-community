# Prep ALZ sesjon

The Azure landing zone conceptual architecture represents scale and maturity decisions. It's based on lessons learned and feedback from customers who have adopted Azure as part of their digital estate. This conceptual architecture can help your organization set a direction for designing and implementing a landing zone.

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

The Azure service presents a range of active subscription offers, and customers can use these offers at the same time to gain flexible billing options. Example subscriptions include Enterprise Agreement (Enterprise Agreement), Microsoft customer agreement, cloud service provider, and others.

The Azure landing zone architecture supports subscriptions from any Azure offer. Subscriptions can only exist within one Microsoft Entra tenant to then relocate into the management group hierarchy within that tenant. They can then be managed by the various controls with enterprise-scale platforms like Azure Policy and role-based access control (RBAC).

2. **Identity and access management (Identitet og tilgangsstyring):** Dette området fokuserer på administrasjon av brukeridentiteter og tilgangsstyring til Azure-ressurser. Det inkluderer opprettelse og administrasjon av brukerkontoer, rollebasert tilgangskontroll (RBAC) og flerfaktorautentisering for økt sikkerhet.

Identity provides the basis for a wide variety of security assurance. It grants access based on identity authentication and authorization controls in cloud services. Access control protects data and resources and helps decide which requests should be permitted.

The technological landscape in the enterprise is becoming complex and heterogenous. To manage compliance and security for this environment, identity and access management lets the right individuals access the right resources at the right time for the right reasons.

Identity and access management is boundary security in the public cloud. It must be treated as the foundation of any secure and fully compliant public cloud architecture. Azure offers a comprehensive set of services, tools, and reference architectures to help organizations make highly secure, operationally efficient environments.

3. **Resource organization (Ressursorganisering):** Her handler det om å strukturere og organisere Azure-ressurser på en måte som er logisk og administrerbar for organisasjonen. Dette kan inkludere bruk av ressursgrupper, ressursgruppesett og navngivningskonvensjoner.

Cloud adoption journeys have varying starting points and scale requirements. Some enterprises start with a few applications in the cloud and grow over time. Other enterprises must scale quickly to address business demands like a datacenter migration. In either scenario, resource organization planning should include environment growth to accommodate further applications and services.

A key consideration for resource organization design is to simplify management across the environment for increased workload numbers and scale. Azure landing zone design and implementation should consider foundational management group and subscription structure, to avoid creating scaling constraints later.

The resource organization design area explores techniques and technologies that help maintain good resource topologies in cloud environments. The following diagram shows the four scope levels for organizing Azure resources: management groups, subscriptions, resource groups, and resources.

4. **Network topology and connectivity (Nettverkstopologi og tilkobling):** Dette området omhandler design og konfigurasjon av nettverksarkitektur i Azure, inkludert oppsett av virtuelle nettverk, subnett og tilkobling til lokale nettverk. Herunder Hub-Spoke-topologi eller Virtual WAN

Network topology and connectivity are fundamental for organizations that are planning their landing zone design. Networking is central to almost everything inside a landing zone. It enables connectivity to other Azure services, external users, and on-premises infrastructure. Network topology and connectivity are in the environmental group of Azure landing zone design areas. This grouping is based on their importance in core design and implementation decisions.

In the conceptual Azure landing zone architecture, there are two main management groups hosting workloads: Corp and Online. These management groups serve distinct purposes in organizing and governing Azure subscriptions. The networking relationship between the various Azure landing zones management groups depends on the organization's specific requirements and network architecture. The next few sections discuss the networking relationship between Corp, Online, and the Connectivity management groups in relation to what the Azure landing zone accelerator provides.

5. **Security (Sikkerhet):** Sikkerhetsaspektet handler om å implementere sikkerhetskontroller og prinsipper for å beskytte Azure-ressurser. Dette kan inkludere brannmurer, sikkerhetsgrupper, trusselovervåking og konformitetskontroller.

Security is a core consideration for all customers, in every environment. When designing and implementing an Azure landing zone, security should be a consideration throughout the process.

The security design area focuses on considerations and recommendations for landing zone decisions. The Secure methodology of the Cloud Adoption Framework also provides further in-depth guidance for holistic security processes and tools.

New (greenfield) cloud environment: To start your cloud journey with a small set of subscriptions, see Create your initial Azure subscriptions. Also, consider using Bicep deployment templates in building out your Azure landing zones. For more information, see Azure Landing Zones Bicep - Deployment Flow.

Existing (brownfield) cloud environment: Consider using the following Microsoft Entra identity and access services if you are interested in applying the principles from security design area to existing Azure environments:

6. **Management (Administrasjon):** Administrasjon omfatter effektiv styring av Azure-ressurser. Dette inkluderer overvåkning, feilsøking, oppdateringer og konfigurasjon av ressurser.

For stable, ongoing operations in the cloud, a management baseline is required to provide visibility, operations compliance, and protect and recover capabilities.

The management design area focuses on the considerations and recommendations for landing zone design decisions. Also, the Manage methodology of the Cloud Adoption Framework provides further in-depth guidance for holistic management processes and tools.

7. **Governance (Styring):** Dette området dreier seg om å etablere retningslinjer og retningslinjer for administrasjon av Azure-ressurser. Det inkluderer administrasjon av kostnader, sikkerhet og overholdelse/samsvar. Azure Policy er sentralt her, og spesielt DeployIfNotExists og Deny.

An organizations cloud adoption journey starts with strong controls to government environments.

Governance provides mechanisms and processes for maintaining control over platforms, applications, and resources in Azure.

The design area review explores the considerations and recommendations that help you make informed decisions as you plan your landing zone.

The governance design area focuses on the design decisions in the landing zone. Also, the Govern methodology of the Cloud Adoption Framework gives guidance for governance processes and tools.

8. **Platform automation and DevOps (Plattformautomatisering og DevOps):** Dette området handler om å automatisere prosesser for ressursimplementering og administrasjon. DevOps-prinsipper brukes for å effektivisere utviklings- og driftsoperasjoner.

The scale, agility, and flexibility part of cloud technologies leads to opportunities for new ways of working and modern approaches to service delivery.

Many traditional IT operating models aren't compatible with the cloud and must undergo operational transformation to deliver against enterprise migration targets. You can evaluate using DevOps processes and tools for application and central teams.

Disse åtte designområdene gir en helhetlig tilnærming til å forberede organisasjonen på en vellykket implementering og administrasjon av Azure-tjenester gjennom Azure Landing Zones. De gir et rammeverk for å ta hensyn til alle viktige aspekter, fra økonomi og identitet til nettverk og sikkerhet.

### Velg landingssone

[Mer info](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/choose-landing-zone-option)

Platform landing zone: A platform landing zone is a subscription that provides shared services (identity, connectivity, management) to applications in application landing zones. Consolidating these shared services often improves operational efficiency. One or more central teams manage the platform landing zones. In the conceptual architecture (see figure 1), the "Identity subscription", "Management subscription", and "Connectivity subscription" represent three different platform landing zones. The conceptual architecture shows these three platform landing zones in detail. It depicts representative resources and policies applied to each platform landing zone.

Application landing zone: An application landing zone is a subscription for hosting an application. You pre-provision application landing zones through code and use management groups to assign policy controls to them. In the conceptual architecture (see figure 1), the "Landing zone A1 subscription" and "Landing zone A2 subscription" represent two different application landing zones. The conceptual architecture shows only the "Landing zone A2 subscription" in detail. It depicts representative resources and policies applied to the application landing zone.

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
