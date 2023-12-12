# Sopra Steria Trondheim Cloud Community

Offentlig repository med innhold relatert til Trondheim Cloud Community i Sopra Steria

Alle filer i dette repositoriet er offentlig tilgjengelig på internett. Det skal ikke ligge noen proprietær informasjon her.

Sopra Steria Trondheim Cloud Community er et internt kompetasemiljø for utvikling av skykompetanse hovedsakelig i Trondheim. Det kan bli aktuelt med community-møter for utenforstående, men for øyeblikket er dette kun for interne. Slide decks er dog for øyeblikket offentlig tilgjengelig.

## Konsept: Tech Tuesday

Det er forsøkt startet en tradisjon for intern Tech Tuesday/Teknolunsj, og formatet er korte teknolunsjer hvor vi presenterer et eller annet teknisk tema. Noen teknolunsjer erstattes med større demonstrasjoner i MS Cloud Community, eller andre events som tar tid fra teknolunsjene.

### Avholdte møter

- [Tech Tuesday: Terraform vs Azure Bicep fritt etter hukommelsen](./SlideDecks/2023-12-12/Terraform_vs_Azure_Bicep.pdf)
- [Tech Tuesday: Sertifikater avmystifisert!](./SlideDecks/2023-11-28/Sertifikater_avmystifisert.pdf)
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

🎄🎅 Juleferie frem til januar 2024. Se forrige avholdte sesjon for generelle planer til neste år. God jul! 🎅🎄

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
