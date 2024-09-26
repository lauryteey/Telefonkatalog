# Intro

Denne guiden hjelper deg med å sette opp en Raspberry Pi, installere Ubuntu på Raspberry Pi 4 og installere nødvendige verktøy som MariaDB og Git. Du vil også konfigurere systemet med oppdateringer, brannmur og SSH. Deretter lærer du hvordan du styrer Raspberry Pi eksternt fra en annen maskin ved hjelp av SSH, og logger inn via CMD på Windows. Til slutt oppretter vi en ny databasebruker, kloner et prosjekt fra GitHub, og kobler databasen til Python-koden.

# Oppsett av Raspberry Pi

## Fysisk oppsett

1. Gå til [denne YouTube-videoen](https://youtu.be/S9CYlpbSz-c?si=zw-Jelt5Yc_EjZT9) og følg instruksjonene for det fysiske oppsettet av din Raspberry Pi.
   - Husk å velge **norsk tastatur** under oppsettet.

2. Koble til det trådløse nettverket `kuben.it` med følgende passord:
   - **Passord:** `IMKuben1337!`

3. Sørg for at du har koblet til tastatur, mus og skjerm for å kunne fortsette oppsettet.




# SSH-oppsett på Raspberry Pi

Dette forklarer hvordan du installerer og konfigurerer SSH på en Raspberry Pi ved hjelp av terminalen. Etter fullføring vil du kunne styre Raspberry Pi eksternt fra en annen datamaskin.

## 1. Åpne terminalen

For å starte installasjonen, åpne terminalen ved å bruke tastatursnarveien `CTRL + ALT + T`.

## 2. Installer SSH-serveren

Installer SSH-serveren på Raspberry Pi ved å kjøre følgende kommando i terminalen:

```bash
sudo apt update  #Oppdaterer pakkelisten
sudo apt install openssh-server #Installerer SSH-serveren
```
Dette letter og installerer etter opdateringer til alle programvare som er installert. 

# Sette opp brannmur med UFW på Raspberry Pi

UFW (Uncomplicated Firewall) er et enkelt verktøy for å administrere en brannmur. Dette forklarer hvordan du installerer og konfigurerer UFW på Raspberry Pi for å beskytte systemet og tillate SSH-tilkoblinger.

## 1. Installer UFW

Først må du installere UFW ved å kjøre følgende kommando:

```bash
sudo apt install ufw #Installerer UFW
```

## 2. Aktiver brannmuren

Når UFW er installert, må du aktivere den slik at den starter automatisk hver gang Raspberry Pi starter:

```bash 
sudo ufw enable #Aktiverer brannmuren ved oppstart
```

## 3. Tillat SSH-tilkoblinger
For å bruke ssh til å administrere Raspberry Pi eksternt, må du tillate SSH-tilkoblinger gjennom brannmuren:

````bash
sudo ufw allow ssh #Tillater SSH-tilkoblinger
````

## 4. Sjekk statusen på brannmuren
For å sjekke om brannmuren er aktiv og hvilke regler som er satt opp, kjør følgende kommando:

````bash
sudo ufw status #Viser statusen til brannmuren
````

Du skal se noe lignende til dette: 

````cmd
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
````

# Aktivere SSH på Raspberry Pi

SSH (Secure Shell) lar deg administrere Raspberry Pi eksternt fra en annen maskin. Her skal du få vite hvordan installere og aktivere SSH-serveren på din Raspberry Pi.

## 1. Installer SSH-serveren
Først må du installere SSH-serveren for å kunne bruke SSH til å koble til Raspberry Pi:

```bash
sudo apt install openssh-server #Installerer SSH-serveren
```

## 2. Aktiver SSH ved oppstart
For å sikre at SSH starter automatisk hver gang Raspberry Pi starter, kjør følgende kommando:

````bash
sudo systemctl enable ssh #Aktiverer SSH ved oppstart
````

## 3. Start SSH-serveren med en gang
Hvis du vil bruke SSH umiddelbart, kan du starte SSH-serveren med denne kommandoen:

````bash
Kopier kode
sudo systemctl start ssh #Starter SSH-serveren nå
````
# Finne IP-adressen på Raspberry Pi

For å kunne koble til Raspberry Pi via SSH, må du finne IP-adressen. Følg disse trinnene for å identifisere IP-en din.

## 1. Åpne terminalen

Først må du åpne terminalen på Raspberry Pi. Du kan gjøre dette ved å bruke tastatursnarveien `CTRL + ALT + T`.

## 2. Kjør kommandoen for å finne IP-adressen

Skriv inn følgende kommando for å vise nettverksgrensesnittene og deres tilknyttede IP-adresser:
```bash
ip a
```
## 3. Identifiser din IP-adresse

Se etter din IP-adresse i utdataene fra kommandoen.

Hvis du er koblet til et kablet nettverk, finner du IP-adressen under eth0: linjen.
Hvis du bruker et trådløst nettverk, vil IP-adressen vises under wlan0: linjen.

# Installere Git, Python og MariaDB på Raspberry Pi

Dette forklarer hvordan du installerer Git, Python og MariaDB på din Raspberry Pi. Følg trinnene nedenfor for å sette opp nødvendige verktøy.

## 1. Åpne terminalen

Først må du åpne terminalen på Raspberry Pi. Du kan gjøre dette ved å bruke tastatursnarveien `CTRL + ALT + T`.

## 2. Installer Python-pakkehåndtereren (pip)

Start med å installere `pip`, som er Python-pakkehåndtereren:
```bash
sudo apt install python3-pip #Installerer Python-pakkehåndtereren
```
## 3. Installer Git

Deretter installerer du Git, som er et versjonskontrollsystem:

```bash
sudo apt install git #Installerer Git
```

## 4. Installer MariaDB

Installer MariaDB, som er en database-server:

```bash
sudo apt install mariadb-server #Installerer MariaDB-serveren
```

## 5. Sikre MariaDB-installasjonen

Etter installasjonen av MariaDB, kjør følgende kommando for å sikre installasjonen og sette opp grunnleggende sikkerhet:

```bash
sudo mysql_secure_installation #Sikrer MariaDB-installasjonen
```

# Opprette en ny databasebruker i MariaDB

Her lager du en ny databasebruker i MariaDB og gir den riktige rettighetene. Følg trinnene nedenfor for å sette opp en ny bruker.

## 1. Åpne terminalen
Åpne terminalen på Raspberry Pi ved å bruke tastatursnarveien `CTRL + ALT + T`.

## 2. Logg inn i MariaDB
For å opprette en ny bruker, må du først logge inn i MariaDB som root-bruker:
```bash
sudo mariadb -u root  #Logger inn som root-bruker
```
## 3. Lag en ny bruker
Når du er inne i MariaDB-prompten, kan du opprette en ny bruker med følgende kommando:

``` sql
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```
Bytt ut username med ønsket brukernavn, og bytt ut password med et sikkert passord for denne brukeren.

## 4. Gi ny bruker rettigheter

Etter at brukeren er opprettet, kan du gi denne brukeren nødvendige rettigheter:

``` sql
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' IDENTIFIED BY 'password';
```
`ALL PRIVILEGES` gir brukeren alle rettigheter på alle databaser og tabeller. 

## 5. Oppdater rettigheter

For at endringene skal fungere, må du oppdatere rettighetene i MariaDB:
```sql
FLUSH PRIVILEGES;  # Oppdaterer rettighetene
```
# Installere ekstra programvare på Raspberry Pi

Du kan installere annen programvare etter behov, som for eksempel VS Code, nettlesere, Wireshark, Nmap, etc. Følg trinnene nedenfor for å installere ønsket programvare.

## 1. Åpne terminalen

Start med å åpne terminalen ved å bruke tastatursnarveien `CTRL + ALT + T`.

## 2. Installer ønsket programvare

For å installere annen programvare, som for eksempel Wireshark eller Nmap. 

Hvis du får trøbbel med VS Code, last ned .deb for arm64 fra https://code.visualstudio.com/docs/setup/linux Naviger til mappen du lastet ned filen

Skriv `sudo apt install ./code` og trykk tab, så enter

# Oppdatere systemet og styre Raspberry Pi med SSH

Oppdaterer systemet på Raspberry Pi og kobler til den fra en annen maskin ved hjelp av SSH.

## 1. Oppdater systemet

Etter at du har installert ny programvare, bør du kjøre følgende kommandoer for å sikre at alt er oppdatert:

```bash
sudo apt update #Oppdaterer pakkelisten
sudo apt upgrade #Oppgraderer installert programvare
```

## 2. Styr Raspberry Pi fra laptopen med SSH

I fremtiden kan du styre Raspberry Pi eksternt fra din laptop eller en annen datamaskin ved hjelp av SSH. Følg disse trinnene for å koble til:

### Åpne terminalen på laptopen

Hvis du bruker Windows, kan du åpne CMD eller PowerShell. På macOS eller Linux åpner du terminalen.

### Koble til Raspberry Pi med SSH

For å koble til Raspberry Pi via SSH, skriver du følgende kommando:

```` bash 
ssh brukernavn@ip_adresse
````
Bytt ut brukernavn og IP- adressen med ditt faktiske brukernavn og IP-adressen på Raspberry Pi. 

### Full tilgang til Raspberry Pi

Når du er koblet til, har du full tilgang til Raspberry Pi og kan administrere den eksternt.

# Logge inn på Raspberry Pi fra CMD i Windows

Logge seg inn på Raspberry Pi ved hjelp av SSH fra Command Prompt (CMD) i Windows.

## 1. Åpne Command Prompt

Først må du åpne **Command Prompt (CMD)** i Windows:
- Trykk `Windows-tasten + R`, skriv `cmd`, og trykk `Enter`.

## 2. Koble til Raspberry Pi via SSH

Når CMD er åpen, kan du bruke følgende kommando for å koble til Raspberry Pi og trykk `Enter`:

```bash
ssh brukernavn@ip-adresse
```

## 3. Skriv inn passordet ditt

Etter å ha trykket `Enter`, vil du bli bedt om å skrive inn passordet til brukeren på Raspberry Pi (som standard er det ofte raspberry hvis du ikke har endret det).

**Merk:
Første gang du kobler til Raspberry Pi fra en ny datamaskin, vil du bli spurt om du vil godta tilkoblingen. Skriv `Yes`og trykk `Enter`.** 

## 4. Bekreft tilkoblingen

Når du har logget inn, vil du se terminalen til Raspberry Pi. Det betyr at nå er du logget inn på din Raspberry Pi fra laptopen/PC-en din via SSH.

## 5. Avslutte tilkoblingen

Når du er ferdig, kan du avslutte SSH-tilkoblingen ved å skrive:

````bash
exit
````
Dette vil avslutte tilkoblingen til Raspberry Pi.

# Installere Ubuntu på Raspberry Pi 4

laste ned og installerer Ubuntu på din Raspberry Pi 4.

## 1. Last ned Raspberry Pi Imager

1. Gå til [Raspberry Pi Imager](https://www.raspberrypi.com/software/) nettsiden.
2. Last ned og installer Raspberry Pi Imager på din PC eller Mac.

## 2. Velg din Raspberry Pi device

1. Åpne Raspberry Pi Imager 
2. Klikk på **Raspberry Pi device**
3. Velg **Raspberry Pi 4**

## 3. Velg Ubuntu som operativsystem

1. Åpne Raspberry Pi Imager.
2. Klikk på **Choose OS**.
3. Rull ned og velg **Other general-purpose OS**.
4. Velg **Ubuntu** og deretter den versjonen du vil installere, i denne tilfellet den nyeste versjon.

## 3. Velg SD-kort
1. Skru ned din Raspberry Pi 4 ved bruk av følgende kommando: 
````bash
sudo shutdown
````
2. Sett SD-kortet du vil bruke innen på PC-en din.
3. Klikk på **Choose Storage** og velg SD-kortet du vil bruke.

## 4. Skriv til SD-kortet
1. Klikk på **Write** for å skrive Ubuntu til SD-kortet.
2. Vent til prosessen er ferdig.

## 5. Sett inn SD-kortet i Raspberry Pi
1. Ta SD-kortet ut av PC-en når skrivingen er fullført.
2. Sett SD-kortet inn i Raspberry Pi.

## 6. Start opp Raspberry Pi
1. Koble til strøm, tastatur, mus, skjerm og eventuelt Ethernet-kabel.
2. Slå på Raspberry Pi.
3. Følg veiledningen på skjermen for å fullføre installasjonen av Ubuntu.

---

Nå har du Ubuntu installert på din Raspberry Pi 4!

# Last ned prosjekt fra GitHub til Raspberry Pi

Dette viser hvordan du lager en katalog og kloner et prosjekt fra GitHub på Raspberry Pi.

## 1. Åpne terminalen

Start med å åpne terminalen på Raspberry Pi ved å bruke tastatursnarveien `CTRL + ALT + T`.

## 2. Sjekk hvor du er (arbeidskatalogen)

For å se hvilken katalog du befinner deg i, bruk følgende kommando:
```bash
pwd #Sjekker gjeldende arbeidskatalog
```
## 3. Lag en ny katalog
Opprett en ny katalog som heter kode ved å bruke følgende kommando:

```bash
mkdir kode #Lager en ny katalog som heter kode
```

## 4. Gå inn i den nye katalogen

Naviger til katalogen du nettopp opprettet:

````bash 
cd kode #Bytter til katalogen 'kode'
````

## 5. Klon prosjektet fra GitHub

Bruk Git til å klone prosjektet fra GitHub:

````bash
git clone https://github.com/LektorRichvoldsen/telefonkatalog_og_database
````
Dette vil laste ned prosjektet til katalogen `kode`.

## 6. Se hva som er i katalogen

Sjekk innholdet i katalogen ved å bruke kommandoen:

````bash 
ls #Viser innholdet i katalogen
````
Du vil se prosjektmappen `telefonkatalog_og_database.`

## 7. Gå inn i prosjektkatalogen

Naviger inn i prosjektmappen:

````bash
cd telefonkatalog_og_database #Gå til prosjektmappen
````

## 8. Se innholdet i prosjektet

Bruk følgende kommando for å liste filer og mapper:

````bash
ls 
````
Du vil se mapper som `python`, `README.md`, og `sql`.

## 9. Gå inn i SQL-katalogen

Naviger inn i SQL-katalogen som inneholder databasens skript:

````bash
cd sql  #Gå til SQL-mappen
````
Se innholdet i SQL-katalogen ved bruk av `ls`. I katalogen du vil se filer som `1_lag_database.sql`, `2_lag_tabell.sql`, osv.

# Lage en database og koble den til Python-koden

Dette viser hvordan du oppretter en database i MariaDB, tester den, og kobler den til Python-koden som finnes i GitHub-prosjektet.

## 1. Logg inn i MariaDB

Start med å logge inn i MariaDB fra terminalen:
```bash
sudo mariadb -u root
```
## 2. Opprett databasen

Kjør følgende SQL-kommandoer for å opprette databasen `telefonkatalog` og tabellen `person`:

````sql
CREATE DATABASE telefonkatalog;
USE telefonkatalog;

CREATE TABLE person (
 id int NOT NULL AUTO_INCREMENT,
 fornavn VARCHAR(255) NOT NULL,
 etternavn VARCHAR(255) NOT NULL,
 telefonnummer CHAR(8),
 PRIMARY KEY (id)
);
````

## 3. Sett inn testdata

Kopier og lim inn følgende SQL-kommandoer for å legge til noen testdata i tabellen `person`:

````sql
INSERT INTO person (fornavn, etternavn, telefonnummer)
VALUES ('Erik', 'Perik', '12345678');
INSERT INTO person (fornavn, etternavn, telefonnummer)
VALUES ('Lise', 'Pise', '22334455');
INSERT INTO person (fornavn, etternavn, telefonnummer)
VALUES ('Testus', 'Jensen', '11114444');
INSERT INTO person (fornavn, etternavn, telefonnummer)
VALUES ('Knut', 'Donald', '31415926');
````

## 4. Test databasen

Kjør følgende SQL-kommandoer for å teste at databasen fungerer som forventet:

1. Vis alle personene i tabellen:

````sql
SELECT * FROM person;
````

2. Vis fornavn og telefonnummer for alle personene:

````sql
SELECT fornavn, telefonnummer FROM person;
````

3. Finn informasjon om en person: 

````sql
SELECT * FROM person WHERE fornavn = "Erik";
````

4. Finn mobilnummeret til en person: 

````sql 
SELECT telefonnummer FROM person WHERE fornavn = "Lise" AND etternavn = "Pise";
````

## 5. Koble Python-koden til databasen

I GitHub-prosjektet du klonet tidligere, finnes en Python-fil som kobler til databasen.

1. Hent Python-filen: 

Naviger til GitHub-prosjektets Python-katalog og hent filen `telefonkatalog_oppdater_sql.py`. Lagre denne filen på din laptop (ikke på Pi-en).

2. Koble til databasen i Python-koden. Det ser slik ut:

````python
mydb = mysql.connector.connect(
	host="172.29.51.19",
	user="test",
	password="1234",
	database="telefonkatalog"
)
````
I Python-koden skal du legge informasjonen din.

## 6. Test prosjektet
Kjør Python-koden `telefonkatalog_oppdater_sql.py` fra laptopen din og sjekk om personene fra databasen vises korrekt.

Hvis alt er satt opp riktig, vil Python-programmet hente data fra databasen og vise det i terminalen.








































