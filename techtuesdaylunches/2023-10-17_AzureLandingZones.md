# Azure Landing Zones

## Intro

- Trondheim Cloud Community
- Møteserien Trondheim Tech Tuesday
- Formål
- Målgruppe
- Potensielle tema (Kom med forslag!)
- Dagens tema

## Kort om Cloud Adoption Framework (CAF)

![lifecycle](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/_images/caf-overview-graphic.png)

Først:

1. Strategy (Utarbeid Strategi)
2. Plan (Planlegg)
3. **Ready (Klargjør)**
4. Adopt (Ta i bruk)

Deretter:

- Secure (Sikre)
- Manage (Administrere)
- Govern (Styre/Håndheve)

## Kort om Azure Landing Zones (ALZ) / Enterprise Scale Landing Zones (ESLZ)

![ALZ-Gif](https://github.com/Azure/Enterprise-Scale/blob/main/docs/wiki/media/ESLZ.gif?raw=true)

![ALZ](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/media/customer-landing-zone-journey.png)

### Designområder

1. **Azure-fakturering og Active Directory-tenant**
2. **IIdentitet og tilgangsstyring**
3. **Ressursorganisering**
4. **Nettverkstopologi og tilkobling**
5. **Sikkerhet**
6. **Administrasjon**
7. **Styring**
8. **Plattformautomatisering og DevOps**

### Start "i det små" - ❌

- ARM/Portal
- Blueprint-basert (ikke anbefalt)
- Mer restriktivt
- Vanskeligere å utvide
- Ikke anbefalt for produksjon

### Start med Enterprise Scale - ✅

- ARM/Bicep/Terraform/Portal
- Ikke Blueprint-basert
- Stor fleksibilitet
- Fire referansearkitekturer

## Kjøkkenmetaforen

Tenk på Azure-plattformen som et enormt, velutstyrt kjøkken med alle ingrediensene og verktøyene du trenger for å lage deilige måltider.

Her kommer Azure Landing Zones inn som din personlige kjøkkensjef og oppskriftbok.

Den gir deg en veiledning om hvordan du best kan bruke kjøkkenet

- hvilke ingredienser som passer sammen
- hvordan du organiserer kjøkkenet ditt for effektiv matlaging
- hvordan du sørger for at måltidet blir både smakfullt og trygt
- hvordan du holder kostnaden nede ved tilberedelse
- hvordan du reduserer matsvinn

Azure Landing Zones gir deg en strukturert tilnærming til å ta i bruk Azure-plattformen, som å følge en oppskrift for å lage et mesterverk av en rett. Det gir deg veiledning for å optimalisere, organisere og sikre din skyinfrastruktur, akkurat som en kjøkkensjef hjelper deg med å lage en gourmetmiddag.

## Fundamentmetaforen

Azure Landing Zone i forhold til Azure-plattformen kan sammenlignes med et solid fundament for en skyskrapers bygging. Akkurat som et sterkt og godt konstruert fundament gir stabilitet og struktur til hele bygningen, gir Azure Landing Zone en solid struktur for organisasjonens skyimplementering i Azure.

Det etablerer retningslinjer, beste praksis og retningslinjer som sikrer at skyinfrastrukturen er stabil, sikkert og optimalisert for organisasjonens behov. 

På samme måte som fundamentet gir en solid base for skyskraperen, gir Azure Landing Zone en solid base for å bygge og administrere komplekse skytjenester på Azure-plattformen.

## Inngangsporten

Azure Landing Zone kan sammenlignes med en velorganisert og sikker "inngangsport" til den store, mangfoldige verdenen av Azure-plattformen.

Akkurat som en inngangsport gir reisende en strukturert og sikker vei inn i en stor flyplass, gir Azure Landing Zone en rammeverk og veiledning for organisasjoner når de navigerer og tar i bruk Azure-plattformen.

Det sørger for at organisasjonene har de nødvendige retningslinjene, sikkerhetstiltakene og ressursene for å komme i gang trygt og effektivt i skyen.

## Trafikk

Azure Landing Zones kan sammenlignes med veiskiltene og trafikkreglene på en motorvei. Akkurat som veiskiltene veileder førere til riktig bane og hjelper dem med å forstå reglene på veien, veileder Azure Landing Zones organisasjoner gjennom oppsett og praksis for riktig bruk av Azure-plattformen.

De gir en klar retning, sikrer overholdelse av bestemte standarder og gir retningslinjer for å opprettholde sikkerhet og effektivitet mens man navigerer gjennom den store verden av Azure-tjenester.

Akkurat som veiskiltene sørger for at førere holder seg trygge og i riktig spor på motorveien, sørger Azure Landing Zones for en trygg og organisert vei for organisasjoner som ønsker å dra nytte av Azure-plattformen.

## Subscription vending

- Lage subscriptions
- Legge inn i management group
- Lage diverse start-ressurser (vnet, automation account, terraform state, ++)
- [MS Terraform LZ Vending](https://github.com/Azure/terraform-azurerm-lz-vending)
- [MS Bicep LZ vending](https://github.com/Azure/bicep-lz-vending)
- [2SGo2Cloud Vending](https://github.com/2SGo2Cloud/tia-lz-vending)


### Referansearkitekturer

### Wingtip

- Azure uten hybrid tilkobling

![wingtip](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/media/es-without-networking.PNG?raw=true)

### Trey Research

- On-premises tilkobling med Hub & Spoke for små bedrifter

![trey-research](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/treyresearch/media/es-lite.png?raw=true)

### Adventureworks

- On-premises tilkobling med Hub & Spoke

![adventureworks](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/media/es-hubspoke.png?raw=true)

### Contoso

- On-premises tilkobling med Azure Virtual WAN

![contoso](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/media/ns-vwan.png?raw=true)

## Etablering

### ALZ Accelerator (Portalen)

- pek og klikk
- Ingen IaC

### Bicep

- IaC
- Azure Native DSL
- Automatisering med GitHub eller Azure DevOps
- Microsoft-støttede moduler

### Terraform

- IaC
- Multi-Cloud HCL
- Automatisering med GitHub eller Azure DevOps
- Microsoft-støttet modul
- Community-støttet modul (med Rover)

## Sovereign Landing Zone (Preview)

- Policy baseline
- Data sovereignity
- Confidential Compute
- Kryptering in-transit & at rest

## Mer info

- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/
- https://github.com/Azure/Enterprise-Scale
- https://github.com/Azure/terraform-azurerm-caf-enterprise-scale
- https://github.com/Azure/ALZ-Bicep
- https://github.com/Azure/terraform-provider-alz
- https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/get-started/
