Del 1 – Fysisk nettverk

Kravspesifikasjon

1.SERVER01 og CLIENT01 skal kunne kommunisere i det fysiske labnettet.
2. SERVER01 skal ha fast IP-adresse.
3.CLIENT01 skal kunne få nettverksinnstillinger fra ruteren med DHCP.
4.CLIENT01 skal kunne bruke minst én tjeneste på SERVER01.
5. Bedriftsnettverket i Packet Tracer skal ha flere LAN og routing mellom dem.
6. Klientene i Packet Tracer skal få riktige nettverksinnstillinger og kunne bruke DNS og HTTP.
7. Nettverkene skal testes og resultatene dokumenteres.
                                     Mitt eget krav
8. CLIENT01 skal kunne opprette en testfil i den delte mappen på SERVER01.
<img width="753" height="534" alt="image" src="https://github.com/user-attachments/assets/5185b288-19f0-4816-b7dd-e6e590d8fa94" />




 
Steg 1 – tegn og koble nettverket
<img width="945" height="554" alt="image" src="https://github.com/user-attachments/assets/013a7485-6a98-43f1-b7ff-01d4017fd894" />
<img width="945" height="553" alt="image" src="https://github.com/user-attachments/assets/233d2f91-3204-4a66-85e5-f6115358838d" />
<img width="1057" height="626" alt="image" src="https://github.com/user-attachments/assets/3bb50b06-63cb-4ed1-8f25-4484ba521378" />

Jeg har laget et enkelt nettverk i Cisco Packet Tracer. Nettverket består av en ruter (R1), en switch (SW1), en server (SERVER01) og en bærbar PC (CLIENT01).
Jeg koblet SERVER01 og CLIENT01 til switchen SW1. Deretter koblet jeg ruteren R1 til switchen. Jeg kontrollerte at forbindelsene fungerte. Linkene var grønne.
Jeg konfigurerte IP-adressen på ruteren R1 til 192.168.50.1. Jeg testet også nettverksforbindelsen med ping fra CLIENT01 til serveren og ruteren. Testene var vellykkede.
Jeg tok skjermbilder av nettverksdiagrammet, CLI på ruteren og CMD på klienten som dokumentasjon.
Switchporter som ble brukt
 SERVER01: Fa0 → SW1: Fa0/1
 CLIENT01: Fa0 → SW1: Fa0/2
 R1: GigabitEthernet0/0 → SW1: Fa0/3


Steg 2 – Adresseplan og gateway
Nettverk: 192.168.50.0/24
<img width="1920" height="1128" alt="image" src="https://github.com/user-attachments/assets/5f7d1061-50dd-496f-aa55-24c435e7f4c7" />
<img width="1098" height="560" alt="image" src="https://github.com/user-attachments/assets/349d4668-cc95-4d3c-9d4b-dadf1526d900" />

Forklaring
Nettverket bruker adresseområdet 192.168.50.0/24. R1 er konfigurert med IP-adressen 192.168.50.1 på grensesnittet GigabitEthernet0/0. SERVER01 har den statiske IP-adressen 192.168.50.10, og CLIENT01 har den statiske IP-adressen 192.168.50.20. Begge maskinene bruker 255.255.255.0 som subnettmaske og 192.168.50.1 som standard gateway.
Jeg konfigurerte LAN-grensesnittet på R1 med riktig IP-adresse og aktiverte det med kommandoen no shutdown. Jeg kontrollerte konfigurasjonen med show ip interface brief. Resultatet viser at GigabitEthernet0/0 har riktig IP-adresse, og at både status og protokoll er up.
Skjermbildet dokumenterer konfigurasjonen av LAN-grensesnittet på R1.



Steg 3 – Grunnleggende testing
<img width="945" height="553" alt="image" src="https://github.com/user-attachments/assets/9cb4fa1c-4d16-4192-b348-db053c7fef37" />
<img width="945" height="520" alt="image" src="https://github.com/user-attachments/assets/bfa4430c-9479-45c8-899c-09b5ebcf9788" />

Jeg brukte Cisco Packet Tracer til å sette opp nettverket med SERVER01, CLIENT01, R1 og en 2960-switch. Jeg koblet enhetene sammen med nettverkskabler og konfigurerte nettverket slik at SERVER01 og CLIENT01 kunne kommunisere med hverandre og med ruteren R1.
Jeg startet med å kontrollere IP-konfigurasjonen på SERVER01 og CLIENT01 ved hjelp av kommandoen ipconfig.
SERVER01 hadde IP-adressen 192.168.50.10, og CLIENT01 hadde IP-adressen 192.168.50.20. Begge maskinene hadde subnettmaske 255.255.255.0 og standard gateway 192.168.50.1.
Deretter testet jeg nettverkstilkoblingen med ping. Fra CLIENT01 pinget jeg SERVER01 (192.168.50.10) og ruteren R1 (192.168.50.1). Jeg testet også tilkoblingen fra SERVER01 til R1.
Alle ping-testene var vellykkede, med 0 % pakketap. Dette viser at maskinene kan kommunisere med hverandre, og at forbindelsen til ruteren fungerer.
Jeg har tatt skjermbilder av nettverkstopologien og testresultatene som dokumentasjon på arbeidet mitt.
Steg 4 – DHCP til klienten
<img width="945" height="564" alt="image" src="https://github.com/user-attachments/assets/670f6991-1069-4fd0-ac3c-ee29e3703440" />
<img width="945" height="564" alt="image" src="https://github.com/user-attachments/assets/980f9297-d752-4233-9800-6463f4411362" />
<img width="945" height="553" alt="image" src="https://github.com/user-attachments/assets/18ad67ad-155f-48c8-bff8-cffc08f36c17" />

Jeg konfigurerte R1 som DHCP-server for klienten CLIENT01. Jeg opprettet en DHCP-pool med navnet LAB og konfigurerte nettverket med IP-adresseområdet 192.168.50.0/24. Standard gateway ble satt til 192.168.50.1
Jeg reserverte IP-adressene fra 192.168.50.1 til 192.168.50.20, slik at DHCP-serveren ikke deler ut disse adressene automatisk.
Deretter satte jeg CLIENT01 til å motta IP-adresse automatisk via DHCP. Klienten fikk IP-adressen 192.168.50.21, subnettmasken 255.255.255.0 og standard gateway 192.168.50.1. Packet Tracer viste meldingen «DHCP request successful».
SERVER01 beholder den statiske IP-adressen 192.168.50.10. Serveren bruker fast IP-adresse fordi andre enheter og tjenester skal kunne finne serveren på samme adresse hele tiden, uten at adressen endres ved DHCP-fornyelse.
Jeg tok skjermbilde av DHCP-konfigurasjonen og IP-adressen klienten mottok som dokumentasjon.

Steg 5 – bruk SERVER01 som server
 Test av nettverkstilkobling
 <img width="945" height="559" alt="image" src="https://github.com/user-attachments/assets/dac63637-cf88-4edf-9032-56844c6aaaa5" />
 <img width="945" height="536" alt="image" src="https://github.com/user-attachments/assets/bb5e038b-290e-40c4-a39f-a4f255dfcea9" />

Jeg brukte Cisco Packet Tracer til å teste nettverkstilkoblingen mellom CLIENT01, SERVER01 og ruteren R1.
Først testet jeg forbindelsen fra CLIENT01 til SERVER01 ved hjelp av kommandoen ping 192.168.50.10. Testen var vellykket. Fire pakker ble sendt, fire pakker ble mottatt, og pakketapet var 0 %.
Deretter testet jeg forbindelsen fra SERVER01 til ruteren R1 med kommandoen ping 192.168.50.1. Også denne testen var vellykket, med 0 % pakketap.
Jeg opprettet også mappen C:\Felles på en Windows 11-maskin i VirtualBox og aktiverte fildeling. Jeg kontrollerte at mappen var delt, og opprettet en testfil.
Målet var å åpne den delte mappen fra CLIENT01 ved å bruke adressen \\192.168.50.10\Felles, opprette en testfil fra klienten og kontrollere at filen ble synlig på serveren. Denne testen ble imidlertid ikke fullført i Cisco Packet Tracer, fordi Packet Tracer ikke støtter ekte Windows-fildeling (SMB). Windows 11-maskinen i VirtualBox bruker dessuten et annet nettverk enn klienten i Packet Tracer.

Steg 6 – porter og Nmap
<img width="945" height="536" alt="image" src="https://github.com/user-attachments/assets/9343ef39-ba3f-4b2a-a479-f1c3df10cea9" />
<img width="945" height="541" alt="image" src="https://github.com/user-attachments/assets/d16a9f4e-20f8-43be-9b7d-42a52636ef27" />
<img width="945" height="144" alt="image" src="https://github.com/user-attachments/assets/acdb4480-62b3-492a-9329-6cfa47473dcf" />

Jeg undersøkte tjenestene på SERVER01 i Cisco Packet Tracer. Jeg fant at HTTP og FTP var slått på. HTTP bruker vanligvis port 80, mens FTP vanligvis bruker port 21.
Jeg prøvde å kjøre kommandoen nmap 192.168.50.10 fra CLIENT01, men fikk meldingen «Invalid Command». Derfor fikk jeg ikke utført en faktisk Nmap-skanning i Packet Tracer.
Jeg testet i stedet nettverkstilkoblingen med ping 192.168.50.10. Testen var vellykket, med fire pakker sendt, fire mottatt og 0 % pakketap.
En åpen port betyr at en nettverkstjeneste lytter etter tilkoblinger på den aktuelle porten. HTTP bruker vanligvis port 80, og FTP bruker vanligvis port 21. Jeg har ikke bekreftet at disse portene er åpne med Nmap, og jeg har derfor ikke registrert noen faktiske Nmap-resultater for PORT, STATE og SERVICE.

Steg 7 – Wireshark og Nmap
<img width="945" height="587" alt="image" src="https://github.com/user-attachments/assets/e440bf37-396a-464c-898a-422bf1987c0f" />
<img width="945" height="567" alt="image" src="https://github.com/user-attachments/assets/9190692c-b837-4f95-be00-fedb92ae8ebb" />
<img width="945" height="599" alt="image" src="https://github.com/user-attachments/assets/1bebbe5e-2f27-4190-b326-7de14471f5c4" />
<img width="945" height="606" alt="image" src="https://github.com/user-attachments/assets/2f1351ff-43dc-46fa-9d4c-47e73a725b4f" />

Installasjon av Wireshark og Nmap på CLIENT01
Før jeg startet oppgaven, lastet jeg ned og installerte Wireshark og Nmap på CLIENT01.
Etter installasjonen åpnet jeg Zenmap, som er det grafiske brukergrensesnittet til Nmap, og kontrollerte at programmet fungerte.
Jeg startet også Wireshark for å kunne fange og analysere nettverkstrafikk mellom CLIENT01 og SERVER01.
Begge programmene ble brukt til å undersøke nettverkskommunikasjonen i labmiljøet.

Nmap – Portskanning av SERVER01

Jeg brukte Zenmap (Nmap) på CLIENT01 for å undersøke hvilke porter og tjenester som var tilgjengelige på SERVER01.
Jeg skrev inn IP-adressen 192.168.50.10 som Target og valgte profilen Regular scan.
Etter at skanningen var ferdig, fikk jeg følgende resultater:
IP-adresse: 192.168.50.10
Host is up: SERVER01 var aktiv.
1000 TCP-porter: Alle var filtrert.
Åpne porter: Ingen bekreftede åpne porter.
Skannetid: 6,91 sekunder.
Resultatet viste at SERVER01 var tilgjengelig, men Nmap kunne ikke identifisere åpne porter eller tjenester. Dette kan skyldes brannmurregler som filtrerer trafikken.
Skjermbilde 1: Resultatet fra Nmap-skanningen av SERVER01.

Jeg startet Wireshark på CLIENT01 og valgte nettverksgrensesnittet som brukes i laben.
Deretter startet jeg en pakkefangst og pinget SERVER01.
Etter ping-testen stoppet jeg fangsten og brukte filteret icmp.
Jeg undersøkte ICMP Echo Request og Echo Reply.
Sendes fra CLIENT01 til SERVER01.
 Sendes fra SERVER01 til CLIENT01.
Kilde-IP og mål-IP:
Request: CLIENT01 (IP: 10.0.3.15) → SERVER01 (192.168.50.10)
Reply: SERVER01 (192.168.50.10) → CLIENT01 (IP: 10.0.3.15)
Dette viser hvordan ICMP brukes til å teste kommunikasjonen mellom to maskiner.

Skjermbilde 2: ICMP-trafikk i Wireshark.

Wireshark – TCP og delt mappe

Jeg startet en ny pakkefangst i Wireshark på CLIENT01.
Deretter åpnet jeg den delte mappen på SERVER01 fra CLIENT01.
Jeg stoppet pakkefangsten og undersøkte TCP-trafikken ved å bruke filteret tcp.
TCP brukes til kommunikasjon mellom maskinene. SMB bruker vanligvis TCP-port 445 til fildeling i Windows.
Skjermbilde 3: TCP-trafikk mellom CLIENT01 og SERVER01.
Forskjellen mellom Nmap og Wireshark

Nmap:

Nmap brukes til å undersøke hvilke porter og tjenester som er tilgjengelige på en maskin.
I denne oppgaven viste Nmap at SERVER01 var aktiv, men at alle de 1000 undersøkte TCP-portene var filtrert.

Wireshark:

Wireshark brukes til å fange og analysere nettverkstrafikk.
Med Wireshark kan vi se hvilke pakker som sendes mellom CLIENT01 og SERVER01, for eksempel ICMP ved ping og TCP ved fildeling.

Forskjellen:

Nmap viser hvilke porter og tjenester som kan nås på en maskin, mens Wireshark viser den faktiske nettverkstrafikken mellom maskinene.
Konklusjon
I denne oppgaven installerte og brukte jeg Nmap og Wireshark på CLIENT01 for å undersøke nettverkskommunikasjonen mellom CLIENT01 og SERVER01.
Jeg gjennomførte en portskanning med Nmap og undersøkte ICMP- og TCP-trafikk med Wireshark.
Jeg lærte at Nmap viser hvilke porter og tjenester som er tilgjengelige, mens Wireshark viser den faktiske trafikken mellom maskinene.
Begge verktøyene er nyttige for nettverksanalyse og feilsøking.
NB. Jeg tok skjermbildene med mobilen fordi jeg ikke tatt skjermbilder direkt på datamaskinen.

Steg 8 – tracert og nettverksvei

<img width="945" height="614" alt="image" src="https://github.com/user-attachments/assets/1d8a3d6a-b65e-4231-94d4-f8995d3c929a" />
Jeg testet nettverksforbindelsen mellom CLIENT01 og SERVER01.
Først brukte jeg kommandoen tracert -d 10.0.2.4. Jeg brukte denne IP-adressen fordi SERVER01 hadde adressen 10.0.2.4 i mitt virtuelle nettverk.
Resultatet viste at SERVER01 ble nådd på ett hopp, og sporingen ble fullført.
Deretter brukte jeg kommandoen ping 10.0.2.4. Alle fire pakkene fikk svar, og pakketapet var 0 %.


<img width="945" height="617" alt="image" src="https://github.com/user-attachments/assets/68fab32f-339a-4827-a36e-68fb4c81b91b" />

 
Fysisk feilsøking
Symptom CLIENT01 mistet forbindelsen til SERVER01.
Hypotese Nettverksforbindelsen fungerte ikke fordi Ethernet-adapteren på CLIENT01 var deaktivert.
Test: Jeg brukte kommandoen ping 10.0.2.4 fra CLIENT01. Testen viste fire tapte pakker og 100 % pakketap.
Fun  Ethernet-adapteren på CLIENT01 var deaktivert, og CLIENT01 kunne derfor ikke kommunisere med SERVER01 under testen.
Løsning Jeg aktiverte Ethernet-adapteren igjen og kjørte ping 10.0.2.4 på nytt. Alle fire pakkene fikk svar, og pakketapet var 0 %.
Konklusjon Feilen ble rettet, og nettverksforbindelsen mellom CLIENT01 og SERVER01 fungerte igjen.
Packet Tracer
 
Packet Tracer


<img width="945" height="566" alt="image" src="https://github.com/user-attachments/assets/bfa3c19a-2532-4855-b094-7a10d7ed1ed5" />

<img width="945" height="588" alt="image" src="https://github.com/user-attachments/assets/9a16f1db-5d39-4fd6-ae18-6704901f4fed" />

<img width="945" height="552" alt="image" src="https://github.com/user-attachments/assets/e68b6563-9640-4342-b7db-d9d542a67732" />

<img width="945" height="553" alt="image" src="https://github.com/user-attachments/assets/9247c634-39f0-43c7-bdb3-cb1fdaf84dc2" />

<img width="945" height="482" alt="image" src="https://github.com/user-attachments/assets/394208f3-190d-4d92-8396-770511fdeaec" />

Jeg opprettet et nettverk i Cisco Packet Tracer med to rutere (R1 og R2), to svitsjer, en server og to klientenheter.
Jeg brukte følgende IP-adresser:
Nettverk 1: 192.168.60.0/24
Nettverk 2: 192.168.50.0/24
Forbindelse mellom ruterne: 10.0.0.0/30
Ruterne ble konfigurert med IP-adresser på grensesnittene. Jeg aktiverte grensesnittene med kommandoen no shutdown.
Statisk ruting
Jeg konfigurerte statiske ruter slik at de to nettverkene kunne kommunisere med hverandre.
Jeg brukte kommandoen show ip route for å kontrollere rutingtabellene og bekrefte at de statiske rutene var registrert.
Testing med ping og tracert
Jeg testet forbindelsen fra PC2 til adressen 192.168.50.10 ved hjelp av ping.
Den første testen viste 25 % pakketap. Da jeg gjentok testen, fikk jeg fire svar av fire pakker, altså 0 % pakketap.
Jeg brukte også tracert for å undersøke hvilken vei pakkene tok gjennom nettverket.
Resultatet viste følgende rute:
192.168.60.1
10.0.0.1
192.168.50.10
Konklusjon
Testene viste at kommunikasjonen mellom de to nettverkene fungerte. Både ping og tracert bekreftet at pakkene kunne sendes gjennom ruterne til riktig destinasjon.


Del 2-Bedriftsnettverk i Cisco Packet Tracer-fjordTek AS

<img width="945" height="563" alt="image" src="https://github.com/user-attachments/assets/6d1442ef-fe7b-478a-bb96-789d8c525e93" />

Ferdig nettverkstopologi for FjordTek AS
Jeg har bygget bedriftsnettverket til FjordTek AS i Cisco Packet Tracer.
Jeg har koblet sammen to rutere, fire switcher, seks PC-er og én server. Nettverket består av Administrasjon, Support, Servere og Salg.
Alle enhetene er koblet sammen med nettverkskabler, og alle kabelforbindelsene viser grønt lys. Dette betyr at de fysiske forbindelsene er aktive.
Jeg har også konfigurert IP-adresser, VLAN og DHCP. DHCP fungerer i salgsavdelingen. DNS og HTTP er konfigurert på serveren, men må fortsatt testes for å bekrefte at de fungerer.


<img width="945" height="538" alt="image" src="https://github.com/user-attachments/assets/94e1d3fa-3d6a-49c2-9ebd-6b2a0fc28793" />

Figur 1: DHCP-konfigurasjon for PC4 i salgsavdelingen.
PC4 har fått IP-adressen 192.168.40.2 automatisk via DHCP. Subnettmasken er 255.255.255.0, standard gateway er 192.168.40.1, og DNS-serveren er 192.168.30.10. Dette viser at DHCP fungerer i salgsnettverket.


<img width="945" height="547" alt="image" src="https://github.com/user-attachments/assets/2d0ce2c3-0ce4-49ac-a159-e949f9cb8ea8" />

Figur 2: VLAN-konfigurasjon på administrasjonsswitchen.
Bildet viser at VLAN 10 (Administrasjon), VLAN 20 (Support) og VLAN 30 (Servere) er opprettet på switchen.

Steg 1 – bygg og test LAN-ene
Test av LAN – Administrasjon
Jeg testet forbindelsen mellom PC0 og standard gateway 192.168.10.1 ved hjelp av ping-kommandoen.
Testen var vellykket. Alle fire pakkene ble mottatt, med 0 % pakketap.
Dette viser at PC0 kan kommunisere med ruteren i administrasjonsnettverket.
Se bilde.
<img width="945" height="539" alt="image" src="https://github.com/user-attachments/assets/a66f5698-e52f-4f99-ace0-b2e6b724de9f" />

Figur: Ping-test av supportnettverket.
Jeg testet forbindelsen mellom PC2 og standard gateway 192.168.20.1. Alle fire pakkene ble mottatt, med 0 % pakketap. Dette viser at supportnettverket fungerer mot egen gateway.
Se bilde
<img width="945" height="552" alt="image" src="https://github.com/user-attachments/assets/d31cb357-5d4f-4c00-8c8b-7ab56a6c57c5" />

 
Figur: Ping-test av supportnettverket.
Jeg testet forbindelsen mellom PC2 og standard gateway 192.168.20.1. Alle fire pakkene ble mottatt, med 0 % pakketap. Dette viser at supportnettverket fungerer mot egen gateway.
Se bilde
<img width="945" height="536" alt="image" src="https://github.com/user-attachments/assets/75ac72aa-037d-4fc2-a206-caecd08c4fe6" />

 
Figur: Ping-test av salgsnettverket.
Jeg testet forbindelsen mellom PC4 og standard gateway 192.168.40.1. Alle fire pakkene ble mottatt, med 0 % pakketap. Dette viser at salgsnettverket fungerer mot egen gateway.

<img width="945" height="545" alt="image" src="https://github.com/user-attachments/assets/e0d7d127-913b-43cb-a4d6-7d2e5114e790" />

 
 
Figur: Test av forbindelsen mellom R1 og R2.
Jeg testet forbindelsen mellom de to ruterne ved å sende ping fra R1 til R2 (10.0.0.2). Testen var vellykket med 100 % suksessrate (5 av 5 pakker).
<img width="945" height="552" alt="image" src="https://github.com/user-attachments/assets/9fe88a11-7584-41c3-ac0f-438386d28513" />

Jeg har bygget og testet fire lokale nettverk: Administrasjon, Support, Servere og Salg. Alle nettverkene kan kommunisere med sin egen gateway. Forbindelsen mellom R1 og R2 fungerer også.

Steg 2 – Routing mellom nettene

<img width="945" height="572" alt="image" src="https://github.com/user-attachments/assets/fee6bd8d-f209-48b7-8bb9-5fb2f45715c3" />
Jeg konfigurerte statiske ruter på R1 og R2 slik at hovedkontoret og salgsavdelingen kan kommunisere.
Jeg kontrollerte rutingtabellene med show ip route og testet forbindelsen med ping.
Ping-testen mellom PC4 i Salg og PC0 i Administrasjon var vellykket med 0 % pakketap.
Jeg brukte også tracert fra PC4 til PC0. Resultatet viste at trafikken gikk via R2 (192.168.40.1) og R1 (10.0.0.1) før den nådde PC0 (192.168.10.11).
Dette viser at rutingen mellom nettverkene fungerer.

Steg 3 – DHCP, DNS og HTTP

<img width="945" height="555" alt="image" src="https://github.com/user-attachments/assets/c7c2d58f-dff3-40a2-b4be-4d496eb5b46d" />

<img width="945" height="566" alt="image" src="https://github.com/user-attachments/assets/8f3bfa8c-67c1-4aa7-8241-03a4eb320be4" />

DHCP ble konfigurert for klientnettverkene Administrasjon, Support og Salg. Klientene mottok IP-adresse, subnettmaske, standard gateway og DNS-server automatisk.
Serveren har den faste IP-adressen 192.168.30.10. HTTP og DNS ble aktivert, og DNS-navnet intranett.fjordtek.local ble koblet til serverens IP-adresse.
Testene viste at PC5 kunne åpne nettsiden både med IP-adressen http://192.168.30.10 og med DNS-navnet http://intranett.fjordtek.local.
Resultat: DHCP, DNS og HTTP fungerer som forventet.

Steg 4 – Simulation Mode

<img width="945" height="541" alt="image" src="https://github.com/user-attachments/assets/8e841e4c-4c41-4f96-b804-f3f3cc2dc983" />

<img width="945" height="563" alt="image" src="https://github.com/user-attachments/assets/f2cdd880-affc-41ae-9466-695231d7a274" />

<img width="945" height="544" alt="image" src="https://github.com/user-attachments/assets/051be549-a8d8-4341-9e12-6f06c4d489b1" />

Jeg brukte Simulation Mode i Cisco Packet Tracer for å undersøke hvordan datapakker beveger seg gjennom nettverket.
Test 1 – Kommunikasjon i samme LAN
Jeg testet kommunikasjonen mellom PC2 og PC3 i Support-nettverket. I Simulation Mode kunne jeg se både ARP og ICMP. ARP brukes til å finne MAC-adressen til mottakeren, mens ICMP brukes til å teste kommunikasjonen med ping.
Skjermbilde 1: ARP og ICMP mellom PC2 og PC3.
Test 2 – Kommunikasjon mellom Administrasjon og Salg
Jeg testet kommunikasjonen fra PC0 i Administrasjon til PC4 i Salg. I Simulation Mode fulgte jeg ICMP-pakken gjennom R1 Hovedkontor og R2 Salgsavdeling. Dette viste hvordan ruterne videresender pakker mellom ulike nettverk.
Skjermbilde 2: ICMP-pakken gjennom begge ruterne.
Test 3 – DNS og HTTP
Jeg åpnet intranettsiden fra PC5 ved å bruke DNS-navnet. I Simulation Mode kunne jeg se DNS, TCP og HTTP. DNS oversatte navnet til serverens IP-adresse, TCP opprettet forbindelsen, og HTTP ble brukt til å hente nettsiden.
Skjermbilde 3: DNS, TCP og HTTP i Simulation Mode.
Konklusjon
Simulation Mode gjorde det lettere å forstå hvordan ARP, ICMP, DNS, TCP og HTTP fungerer i nettverket. Testene viste også hvordan klienter kommuniserer både innenfor samme LAN og mellom forskjellige nettverk,

Steg 5 – Telnet som avgrenset labøvelse

<img width="679" height="1014" alt="image" src="https://github.com/user-attachments/assets/c2a21c9c-3360-4c81-a977-12ef87153702" />
I denne labøvelsen konfigurerte jeg Telnet på en Cisco-ruter for å undersøke fjernadministrasjon. Telnet er en ukryptert protokoll, og passord og data kan derfor bli lest av andre på nettverket. I moderne nettverk anbefales SSH fordi kommunikasjonen er kryptert.

10. Akseptansetest – QA
Formålet med akseptansetesten er å kontrollere at nettverket oppfyller kravene i kravspesifikasjonen.


<img width="679" height="1014" alt="image" src="https://github.com/user-attachments/assets/95477bc9-1019-47dc-a5b8-81a822d6c655" />

Krav	Test som gjennomføres	Forventet resultat	Faktisk resultat
DHCP	Sett en PC til DHCP og kontroller adressen med ipconfig.	PC-en får automatisk riktig IP-adresse, nettverksmaske og gateway.	Må testes
Routing	Kjør ping 192.168.40.7 fra administrasjonsnettet.	PC-en i salgsnettet svarer på ping.	Bestått – 3 av 4 svar i tidligere test
DNS	Kjør nslookup intranett.fjordtek.local.	Domenenavnet blir oversatt til 192.168.30.10.	Bestått
HTTP	Åpne http://192.168.30.10 i nettleseren på en PC.	Nettsiden på serveren vises.	Må bekreftes
Konklusjon
Testene viser at DNS fungerer, og at det er oppnådd kommunikasjon mellom administrasjonsnettet og salgsnettet. DHCP og HTTP må kontrolleres før alle kravene kan markeres som bestått.

Oppsummering
I dette prosjektet har jeg bygget og konfigurert et bedriftsnettverk for FjordTek AS i Cisco Packet Tracer.
Nettverket består av to rutere, fire svitsjer, seks PC-er og en server. Jeg har arbeidet med IP-adressering, VLAN, routing, DHCP, DNS og HTTP.
Jeg har testet kommunikasjonen mellom ulike nettverk ved hjelp av ping og nslookup. Jeg har også brukt Simulation Mode for å undersøke hvordan ARP, ICMP, DNS, TCP og HTTP fungerer.
Underveis har jeg lært å feilsøke nettverksproblemer og dokumentere konfigurasjoner og testresultater.
Prosjektet har gitt meg bedre forståelse av hvordan rutere, svitsjer, IP-adresser og nettverkstjenester samarbeider i et bedriftsnettverk.



































##GitHub Kanban.
https://github.com/users/qaranbabmakah-source/projects/1/views/1 
