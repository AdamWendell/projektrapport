# Projekt Arbete - Adam Wendell

## Rapport

### Syfte

Under utbildningen så har jag kännt att jag saknat mycket av leverans. 
För att kunna kalla mig fullstack utbildad så vill jag kunna leverera en produkt
från första raden kod till att leverera framtida uppdateringar.
Efter lite reasearch innan kursen så ser docker väldigt lovande ut. Det används flitigt av företag. Samt gör det enklare att leverera snabbt.

### Metod

##### Start

Jag ska starta med att hitta resurser för att lära mig grunderna i docker. 
Både för att få förståelse för produktions deployments samt hur docker förenklar 
mitt liv som utvecklare.
Sen ska jag implementera en app som använder minst två containrar som pratar med varandra. 

##### Förändring

Onsdagen vecka 4 insåg jag att docker inte var så simpelt. Som de exempel appar jag sett. Där Dockerfile bara är ett par lätt förståeliga rader.

Det krävs en hel del förståelse från normala deploys av ens tech stack. Och resurserna blev lätt förvirrande när de förväntade sig att läsaren hade denna kunskap.

Så efter att ha läst [Dockerbook](https://www.dockerbook.com/) samt läst en hel del i dockers dokumentation. Så insåg jag att det är för stort och det finns saker som jag vill lära mig men hinner inte.

Istället för att leta efter än mer nybörjarvänliga resurser. Så gick jag över till att köra JIT(Just In Time) Learning. 

Jag planerade genom att måla upp hur det minsta möjliga av en 2 container app skulle kunna vara. Där jag ändå kan få in ett red-green-deploy flöde så att om alla tester går igenom så ska appen uppdateras på min server.

Planen blev en NGINX container som proxy. Med en väldigt simpel node app som levererar en Elm frontend. Både backend och frontend har tester som körs. Om testerna går igenom så ska en uppdatering av live appen ske.

### Resultat

##### Vecka 1

Leta resurser, kolla på en del gratis resurser men de saknades för mycket information för att det skulle klicka.

##### Vecka 2

Fick tips om att The Dockerbook är en bra resurs. Köpte den för ca 100kr. 
Läser första 1/3 av boken. 

##### Vecka 3

Läser och jobbar igenom uppgifterna i boken. Hinner klart lite mer än 2/3 totalt av boken. Boken har hittils givit en bra grund till docker och Dockerfile. Det jag känner vid detta laget är att det saknas en del i själva produktion av backend system. 
Bestämmer mig för att göra klart boken.

##### Vecka 4

Gör klart tills docker swarm kapitlet tills Onsdagen. Känner att det inte är aktuellt att lära sig server orkestrion just nu. Inser att jag måste gå vidare från att bara fokusera på docker då jag vill ha med CI/CD. Börjar då att skissa på hur skalet till appen ska vara. Jag ville få in CI/CD där tester körs och om de går igenom så ska appen uppdateras på servern. Även att det ska minst vara 2 containrar som pratar med varandra.

Bestämmer mig för att starta med NGINX då jag aldrig använt en proxy innan. Samt en väldigt simpel node backend som servar en frontend. Både backend och frontend ska köra sina egna tester.


##### Vecka 5 

Byggde en simpel node app. Som levererar filerna i frontendens dist mapp. Samt en frontend som kompilerar en produktions build till dist. Både frontend och backend har tester som kan köras med npm test. Använder Circle CI för att köra tester. 

##### Vecka 6

Får build att funka. Men det går långsamt då servern som man får tillgång till som gratis användare på Circle ci är väldigt liten och klen. Samtidigt som webbpack är resurs tungt. En build tar oftast runt 20minuter. Testade Drone CI som är ett CI verktyg som man hostar själv. Lyckades få ihop en fungerande konfiguration. Som var betydligt snabbare. Men det kräver att jag ska ha en till server endast för CI. Vilket inte är värt pengarna för detta projekt. 

##### Vecka 7 

Koppla ihop min NGINX och node app. Samt få det live på en digital ocean server.
Circle ci kör testerna. Om de går igenom så pushar det min nya container till docker hub. När docker hub fått en uppdatering så skickar den en notic till docker cloud som uppdaterar containern på min server.


### Diskussion

Jag trodde docker var simpelt. Men det kräver fortfarande samma kunskap som en vanlig server deploy. Dock ger det en garanti att man kan scala sin miljö genom att starta flera containrar på olika servar. Det hjälper framförallt att bygga små appar (microservices). Det gör så att man scala delar av sin applikation beroende på belastning.
Om jag skulle göra om mitt projekt så skulle jag tidigare gå över till att bygga min app och bara göra det som krävdes i docker. Istället för att försöka lära mig hela docker direkt.


### Slutsats

Målet när jag startade kursen var att få en större förståelse för deployments. Då utbildningen saknade det. Docker var det verktyg som jag hörde mest om innan för att hjälpa med det.

Min metod var att börja med att försöka lära mig så mycket om docker det bara gick. Detta ändrades lite då docker är väldigt stort och det går att göra enormt mycket.

Reslutatet blev mindre app bygge än planerat. Men jag fick byggt de saker som var viktigast för mig. Ett system där man kan bygga sin app och kontinuerligt göra deploments till live servern.


### Källförteckning

 1. [Dockers dokumentation](https://docs.docker.com/)
 2. [Dockerbook](https://www.dockerbook.com/)


### Kod

 1. [Nginx](https://github.com/AdamWendell/projektnginx)
 2. [Web server](https://github.com/AdamWendell/projektweb)
