# Sopra Steria Trondheim Cloud Community

Offentlig repository med innhold relatert til Trondheim Cloud Community i Sopra Steria

Alle filer i dette repositoriet er offentlig tilgjengelig på internett. Det skal ikke ligge noen proprietær informasjon her.

Sopra Steria Trondheim Cloud Community er et internt kompetasemiljø for utvikling av skykompetanse hovedsakelig i Trondheim. Det kan bli aktuelt med community-møter for utenforstående, men for øyeblikket er dette kun for interne. Slide decks er dog for øyeblikket offentlig tilgjengelig.

## Konsept: Tech Tuesday

Det er forsøkt startet en tradisjon for intern Tech Tuesday/Teknolunsj, og formatet er korte teknolunsjer hvor vi presenterer et eller annet teknisk tema. Noen teknolunsjer erstattes med større demonstrasjoner i MS Cloud Community, eller andre events som tar tid fra teknolunsjene.

### Avholdte møter

- [Tech Tuesday: Tilgangsstyring i Azure](./techtuesdaylunches/2023-11-21_AzureRBAC_Notes.md)
- [Tech Tuesday: Docker, Kubernetes and AKS](./SlideDecks/2023-11-07/TechTuesday_Containers-kubernetes-aks.pdf)
- [Tech Tuesday: Azure Policy](./techtuesdaylunches/2023-10-31_Azure_Policy_notes.md)
- [Tech Tuesday: Azure Networking](./techtuesdaylunches/2023-10-24_Azure_Networking_notes.md)
- [Tech Tuesday: Azure Landing Zones](./techtuesdaylunches/2023-10-17_AzureLandingZones.md)
- [Tech Tuesday: Terraform intro](./SlideDecks/2021-10-12/Tech%20Tuesday%20-%20Terraform%20intro.pptx)
- [Tech Tuesday: CAF ESLZ](./SlideDecks/2021-11-23/Tech%20Tuesday%20-%20CAF%20ESLZ.pptx)
- [MS Cloud Community: Bicep demo](SlideDecks/2021-12-08/Presentasjon%20-%20Bicep.pptx)
- [Tech Tuesday: Network Security Groups](SlideDecks/2022-02-14/Presentasjon%20-%20Network%20Security%20Groups.pptx)

### Planlagte møter

#### 28. november - Tech Tuesday: Sertifikater avmystifisert!

Hvordan kan du lese helseinformasjon på helsenorge.no i visshet om at ingen ser hemmelighetene dine?

- Hva er et sertifikat?
- Offentlig og privat nøkkel, hva er forskjellen?
- PKI - Hvorfor trenger du å vite om det?
- Enkel og sikker autentisering? Hvordan fungerer det?!

Dette og mere til går vi gjennom kommende tirsdag.

🤓 Be there or be non-authenticated, like a server rejecting a self-signed cert! 🤓

- *Be there or be unverified, like a certificate without a private key!*
- *Be there or be non-authenticated, like a server rejecting a self-signed cert!*
- *Be there or be as obsolete as SHA-1 in a modern PKI world!*
- *Be there or be unencrypted, like plaintext waiting to be intercepted!*
- *Be there or be untrusted, like a self-signed certificate on first access!*
- *Be there or be as expired as a certificate left unchecked!*
- *Be there or be insecure, like an open door in a robust security system!*
- *Be there or be revoked, like a compromised certificate in need of immediate action!*
- *Be there or be unauthenticated, like a user without valid credentials!*
- *Be there or be as vulnerable as plaintext in transit without SSL/TLS!*

### Brainstorming

- Tech Tuesday: Introduction to Azure
- Tech Tuesday: Azure Networking - Virtual Neworks, Subnets
- Tech Tuesday: Azure Networking - Vnet Peering
- Tech Tuesday: Azure Networking - Network Security Groups, UDRs
- Tech Tuesday: Azure Networking - Hub/Spoke topology
- Tech Tuesday: Azure Networking - Routing
- Tech Tuesday: Azure Networking - Azure Firewall
- Tech Tuesday: Azure Networking - Azure Web Application Gateway
- Tech Tuesday: Azure Networking - Azure Load Balancer
- Tech Tuesday: Azure Networking - Virtual WAN
- Tech Tuesday: Azure Storage - Azure Storage Accounts
- Tech Tuesday: Azure Storage - Azure Blob Storage (Https)
- Tech Tuesday: Azure Storage - Azure Files (SMB/SFTP)
- Tech Tuesday: Azure Storage - Azure Tables/Queues
- Tech Tuesday: Azure Storage - Azure Managed Disks
- Tech Tuesday: Azure Virtual Machines
- Tech Tuesday: Azure App Services
- Tech Tuesday: Azure IAM (Identity and Access Management) - Basics
- Tech Tuesday: Azure IAM - Azure Active Directory
- Tech Tuesday: Azure IAM - PIM (Privileged Identity Management)
- Tech Tuesday: Azure Monitoring and Management
- Tech Tuesday: Azure DevOps and CI/CD
- Tech Tuesday: GitHub and CI/CD
- Tech Tuesday: Azure Cost Management and Optimization
- Tech Tuesday: Azure Security and Compliance
- Tech Tuesday: Azure Governance
- Tech Tuesday: Azure Kubernetes Service
- Tech Tuesday: Azure Databricks
- Tech Tuesday: Azure Data Factory
- Tech Tuesday: Azure Databases
- Tech Tuesday: Azure Functions
- Tech Tuesday: Azure Virtual Desktop
- Tech Tuesday: DevOps with GitHub
- Tech Tuesday: DevOps with Gitlab
- Tech Tuesday: GitHub Actions/Workflows

## Bidra

Jeg har stort sett brukt [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow) som branching strategi, så jeg følger samme modell her.

Dette betyr:

- Alle bidrag må gjøres i egen branch
- Pull Request må godkjennes av en "moderator"
- Ny branch blir merget inn i main
- Ny branch slettes

Vi prøver å ha så kortlevde brancher som mulig.

### Editor

Jeg anbefaler å bruke Visual Studio Code for redigering av dokumenter. Den er gratis, og veldig bra med mange utvidelser for ekstra funksjonalitet.

### Lag egen branch

Lag din egen branch med et beskrivende navn, og helst ditt brukernavn på github som prefix. Eksempler: `torivara-updated-readme`, `torivara-added-scripts`, `gybrushthreepwood-added-some-pirate-stuff`, etc.

Sørg for at du sjekker ut denne branchen lokalt før du gjør endringene dine. Hvis du er usikker:

```bash
git checkout -b <ditt branch navn>
git branch -l
```

### Gjør endringer

Gjør de endringene du tenkte å gjøre. Legg til mapper, endre filer, slett filer, og "go nuts". Du kan ikke skade main branch, og alle endringer må godkjennes før de merges med main uansett.

### Lag Pull Request

Lag en Pull Request i GitHub. Dette er enkelt, og gir deg mulighet til å se over de endringene du har gjort. Deretter må du be om godkjenning fra noen. Dette er stort sett moderator av repository, som for øyeblikket er [torivara](https://github.com/torivara).

### Merge

Når PR er godkjent, kan endringer merges inn i main branch. Kun squash merge er tillatt her, slik at alle commits gjort i din branch reduseres til en commit message. Skriv en beskrivelse over hva som er gjort, og hvorfor, så er det enklere for moderator å godkjenne.

### Slett branch lokalt og remote

Når alt er ferdig merget inn i main, må du slette unna branch. Dette gjøres på følgende måte:

```bash
git branch -D <ditt branch navn>
```

Du må bruke parametret `-D` fordi når man gjør squash merge vil ikke commit history på main være identisk med dine commits gjort i din branch. Git tror derfor at det mangler informasjon. Det gjør mest sannsynligvis ikke det. Hvis du er usikker kan du dobbeltsjekke innhold for å se at alt er likt.
Kjør en `git push` etter branch er slettet for å publisere endringene til remote repository.

## Kontakt

Tor Ivar Asbølmo i Sopra Steria kan kontaktes ved eventuelle spørsmål.

E-post: `tor[dot]asbolmo[alfakrøll]soprasteria[dot]com`
