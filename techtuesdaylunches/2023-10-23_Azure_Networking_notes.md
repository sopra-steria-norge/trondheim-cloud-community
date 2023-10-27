# Prep til networking sesjon

## Hva er et vnet?

- Må ha for å lage en VM
- Software Defined Networking
- Som å koble VM inn i en switch med internett-tilgang

## Ett vnet for seg selv

- Ingen default kontakt med andre vnet
- [Default outbound access](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/default-outbound-access)
- Akkurat nå: default internett
- Senere: default blokkert
  - Public IP direkte på VM
  - Public IP med load balancer
  - Nat Gateway med Public IPs (optimalt ifølge MS)

## To vnet hver for seg

- Ingen kontakt som standard
- VM i ett kan ikke snakke med VM i annet

## Enter Peering

- Peering mellom nettverkene kobler dem sammen i backend
- VM i ett vnet kan snakke med VM i annet vnet

## Network Security Groups

- Nettverks ACL
- Assosieres med enten NIC eller subnet
- Anbefalt på subnet for mikrosegmentering
- Bare innkommende trafikk sperres som regel (sperring av utgående kan bli unødvendig komplekst)
- Uten NSG er alt pip åpent mellom subnets (bortsett fra evt. Windows Firewall)

## Enter Hub & Spoke

- Sentral nettverkshub med fortrinnsvis Azure Firewall eller annen NVA
- User Defined Routing på hvert subnet
- Default ikke noen tvunget routing
- Hver landingssone er en spoke og har minst ett vnet for kontakt med hub
- Må fortsatt lage peering mellom hub og spoke
- East-West-trafikk (mellom spokes)
- North-Sount-trafikk (mot internett)

## Enter Virtual WAN

- Sentral nettverkshub med fortrinnsvis Azure Firewall eller annen NVA
- Ingen User Defined Routing på hvert subnet nødvendig
- Default vnet routing når du kobler deg på hub

## Ingress

- Azure Application Gateway (for containers) with WAF
- Traffic Manager
- Azure Load Balancer
- PaaS offentlige endepunkter (public endpoints)

## Egress

- Azure Firewall
- Public IP
- Load Balanced Public IP
- Nat Gateway

## VPN

- Kryptert kobling over offentlig internett
- VPN Gateway ++
- Ikke veldig kostbart
- Begrenset hastighet

## ExpressRoute

- Ikke kryptert kobling over privat kobling
- ExpressRoute Gateway ++
- Kan bli ganske kostbart (ubegrenset vs begrenset trafikk)
- Kan få høy hastighet hvis ønskelig
