In deze tutorial leer je de basisprincipes van het versiecontrolesysteem git kennen.

- [Referentiemateriaal](#referentiemateriaal)
- [Introductie](#introductie)
- [Repository aanmaken](#repository-aanmaken)
  - [GitHub](#github)
- [Repository clonen](#repository-clonen)
- [Bestand wijzigen](#bestand-wijzigen)
- [Bestand toevoegen](#bestand-toevoegen)
- [Wijzigingen van anderen ophalen](#wijzigingen-van-anderen-ophalen)
- [Oude versie van bestand bekijken](#oude-versie-van-bestand-bekijken)
- [Bestand herstellen](#bestand-herstellen)
- [Git branch](#git-branch)
- [Merge conflict](#merge-conflict)

- [Basiskennis van Linux](https://github.com/informaticawerktuigen/oefenzitting-linux)
- [Werkende Linux-omgeving](https://github.com/informaticawerktuigen/klaarzetten-werkomgeving)

# Referentiemateriaal

Een uitgebreidere versie van deze tutorial kan je terugvinden in het [Git Book](https://git-scm.com/book/nl/v2).

# Introductie

Git is een _Version Control System_. Een _Git-repository_ is een bestandensysteem waarin verschillende versies van éénzelfde bestand bewaard kan worden.

Bijna alle programmeerprojecten ter wereld maken gebruik van Git. Met Git kan je:

- eenvoudig bestanden delen;
- op meerdere machines aan hetzelfde project werken;
- met meerdere mensen aan hetzelfde project werken;
- oude versies van bestanden terug ophalen;
- grote wijzigingen maken in aparte vertakkingen van het project zonder daarbij het hoofdproject te moeten wijzigien;
- bijhouden hoeveel regels code elk lid van een team bijgedragen heeft;
- nog veel meer.

Git is een technologie die je best vroeg in je opleiding onder de knie krijgt. Het is dus een sterke aanrader deze tutorial te volgen.

# Repository aanmaken

## GitHub

[GitHub](https://github.com/) is een website van Microsoft waar Git-repositories gratis gehost kunnen worden. Je kan een repository laten aanmaken op de server van GitHub en deze eenvoudig delen met anderen.

Het is ook mogelijk je eigen GitHub-repository te hosten op een eigen server. Dat zal niet behandeld worden in deze tutorial.

Als eerste stap van deze tutorial maken we een repository aan op GitHub:

- Maak een account op GitHub.
- Druk rechtsboven op het +-icoon en klik op _New repository_.
- Geef de repository de naam _oefenrepo_
- Kies zelf of je de repository publiek of privaat maakt.
- Vink de optie _Add a README file_ aan
- Maak de repository aan

Vervolgens kom je op de pagina van de repository terecht. Op deze pagina zie je een overzicht van het bestandensysteem en wordt de _README_ file weergegeven.

Onze repository heeft een URL waarmee we deze kunnen importeren op onze eigen machine.

- Druk op de groene knop met Code rechtsboven op de pagina van de repository
- Selecteer _HTTPS_ en kopieer de link in het vakje. Deze heeft typisch het formaat `https://github.com/<gebruikersnaam>/<repository-naam>.git`.

# Repository clonen

Met behulp van `git clone` kunnen we een lokale kopie maken van onze repository. Vervolgens kunnen we bestanden toevoegen, wijzigen of verwijderen.

- Open een terminal
- Maak een lokale kopie van je repository met `git clone`. **Gebruik hiervoor je eigen URL**.

  ```shell
  git clone https://github.com/<gebruikersnaam>/oefenrepo.git
  ```

Het uitvoeren van dit commando maakt een nieuwe folder aan met de naam van de repository, in dit geval _oefenrepo_.

- Navigeer naar de repository-folder met `cd`.

  ```shell
  cd oefenrepo
  ```

**Alle volgende stappen in de tutorial nemen aan dat de working directory van je terminal de folder van je repository is.** Dit kan je verifiëren met met het commando `pwd`

# Bestand wijzigen

- Open het bestand `README.md` in een editor naar keuze.

  ```shell
  nano README.md
  ```

- Bewerk de README met een boodschap naar keuze.

We hebben een bestand in onze repository gewijzigd. Deze wijzigingen zijn enkel doorgevoerd op onze eigen machine. Wanneer we tevreden zijn met onze aanpassingen moeten we Git de nieuwe versie van het bestand laten bewaren.

- Voer het commando `git add <filename>` uit om aan Git te laten weten voor welk bestand we wijzigingen willen bewaren.

  ```shell
  git add README.md
  ```

- Voer het commando `git commit -m "<boodschap>"` uit om de wijzigingen te bewaren. In de boodschap beschrijf je welke wijzigingen er zijn doorgevoerd.

  ```shell
  git commit -m "Bericht aan README toegevoegd."
  ```

Op dit moment zijn de wijzigingen correct bewaard in je lokale repository. Wanneer je naar je repository-pagina surft zal je echter merken dat daar nog steeds de oude versie van het README-bestand staat.

- Gebruik `git push` om de lokale wijzigingen naar de remote repository _pushen_.

  ```shell
  git push origin master
  ```

Ververs nu de webpagina van je repository op GitHub. De nieuwe inhoud van je README-bestand zou daar nu ook zichtbaar moeten zijn.

# Bestand toevoegen

Nieuwe bestanden toevoegen aan een repository gebeurt op dezelfde wijze als het bewerken van bestaande bestanden.

- Maak twee nieuwe lege bestanden aan

  ```shell
  touch file1
  touch file2
  ```

- Voer het commando `git status` uit. Git toont je dat `file1` en `file2` nog niet getracked worden.

  ```shell
  git status
  ```

- Track deze files in je repository met `git add`

  ```shell
  git add file1 file2
  ```

- Bewaar de nieuwe bestanden in de repository met `git commit`.

  ```shell
  git commit -m "Twee lege bestanden toegevoegd"
  ```

- Gebruik `git push` om de remote repository te synchroniseren met je lokale repository

  ```shell
  git push origin master
  ```

# Wijzigingen van anderen ophalen

In een repository met meerdere gebruikers kan je de wijzigingen die anderen _gepushet_ hebben opvragen met behulp van het commando `git pull`.

In deze tutorial werk je alleen, dus zal het onderstaande commando geen effect hebben.

```shell
git pull origin master
```

# Oude versie van bestand bekijken

Elke commit in de repository bewaart wijzigingen in één of meerdere bestanden. Elke wijziging kan ook ongedaan gemaakt worden. Een commit wordt geïdentificeerd door een unieke code van 40 karakters.

- Bekijk met behulp van het commando `git log` de geschiedenis van je commits.

  ```shell
  git log
  ```

- Kopieer de commit hash van de eerste commit in je repository uit de log.
- Herstel de eerste versie van `README.md` met `git checkout`.

  ```shell
  git checkout <commit-hash> -- README.md
  ```

- Verifieer dat de oude versie van `README.md` hersteld is door de inhoud van het bestand te bekijken

  ```shell
  cat README.md
  ```

# Bestand herstellen

- Gebruik `git log` en `git checkout` om de nieuwste versie van het bestand terug te herstellen. Gebruik hiervoor de hash van de nieuwste commit.

  ```shell
  git log
  git checkout <commit-hash> -- README.md
  ```

- Verifieer dat de nieuwste versie van `README.md` hersteld is door de inhoud van het bestand te bekijken
  ```shell
  cat README.md
  ```

# Git branch

Een git-repository is intern gestructureerd door middel van branches. Elke repository heeft een _master_-branch die kan beschouwd worden als de stam van je repository. Hierop vind je vaak de meest recente werkende versies van software-projecten.

Wanneer een developer een functionaliteit gaat toevoegen aan een project, maakt deze hiervoor een nieuwe tak (branch) aan. Wijzigingen op deze tak gebeuren afzonderlijk van de wijzigingen op de master.

Door gebruik te maken van een branch kan een developer code aanpassen, committen en pushen zonder bang te moeten zijn dat hij hierdoor werk van anderen stuk kan maken.

Typisch worden branches aangemaakt voor nieuwe functionaliteiten. Wanneer deze functionaliteit klaar is wordt de branch samengevoegd met de master-branch. Dit proces heet mergen.

- Maak een branch genaamd `readme-wijzigen` aan met behulp van het `git branch` commando

  ```shell
  git branch -b readme-wijzigen
  ```

- Wijzig het bestand `README.md` naar keuze

  ```shell
  nano README.md
  ```

- Commit de wijzigingen naar de huidige branch

  ```shell
  git add README.md
  git commit -m "README aangepast"
  ```

- Switch terug naar de master-branch met `git checkout`

  ```shell
  git checkout master
  ```

- Verifieer dat `README.md` op de master branch **niet** is aangepast

  ```shell
  cat README.md
  ```

- Voeg `readme-wijzigingen` toe aan de master branch met `git merge`

  ```shell
  git merge readme-wijzigingen
  ```

- Verifieer dat `README.md` op de master branch nu **wel** is aangepast

  ```shell
  cat README.md
  ```

# Merge conflict

Soms gebeurt het dat meerdere ontwikkelaars op hetzelfde moment in een bestand aan het werken zijn. Neem het volgende scenario

1. Ontwikkelaar A en B clonen een repository met bestand X
2. Ontwikkelaar A wijzigt bestand X: X<sub>1</sub>
3. Ontwikkelaar B wijzigt bestand X: X<sub>2</sub>
4. Ontwikkelaar A pusht X<sub>1</sub> naar de remote repository
5. Ontwikkelaar B probeert X<sub>2</sub> te pushen naar de remote repository

In stap 5 zal Git een melding geven aan ontwikkelaar B dat er een nieuwere commit van een andere ontwikkelaar aanwezig is in de remote repository. Hij kan zijn bestand niet pushen.

6. Ontwikkelaar B voert `git pull origin master` uit

Git detecteert nu twee versies van bestand X: X<sub>1</sub> en X<sub>2</sub>. In eerste instantie probeert Git deze bestanden automatisch samen te voegen. Wanneer dit niet, heb je een _merge conflict_.

Op dit moment maakt Git een bestand X<sub>3</sub> aan. De plaatsen in het bestand waar Git geen automatische merge kon uitvoeren staan in X<sub>3</sub> gemarkeerd door markers die er als volgt uitzien:

```shell
$ cat README.md
<<<<<< HEAD:README.md
Readme van ontwikkelaar B
=======
Readme van ontwikkelaar A
>>>>>> master:README.md
```

De bedoeling is dat ontwikkelaar B nu voor elk conflict in het bestand kiest welke versie bewaard moet worden. Dit kiest hij door de markers te verwijderen en telkens de correcte versie te kiezen. Hij zou het bestand bijvoorbeeld kunnen wijzigen naar:

```shell
$ cat README.md
Readme van ontwikkelaar A en B
```

Wanneer de conflicts opgelost zijn kan developer B zijn wijzigingen committen en pushen:

```shell
git commit -m "Resolved merge conflict on README"
git push origin master
```
