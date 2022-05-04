# Files and Directories
In het vorige hoofdstuk had Linus een server bestand gedownload voor de minecraft server. Maar waar staat dit bestand nu? In dit hoofdstuk zoeken we uit hoe we kunnen navigeren in mappen & hoe we enkele basisbewerkingen met bestanden kunnen uitvoeren.

## Directories

### verkennen
Als start wil Linus zoeken naar het `server.jar` bestand dat hij in het vorige hoofdstuk gedwonload heeft. Via het `man -k directory` commando ziet hij al snel dat er verschillende commando's zijn om met directories te werken.

Het eerste commando dat we bekijken is het `pwd` commando. Uit de manpage van het commando zelf:
```
pwd - print name of current/working directory
```

Hiermee drukken we dus de directory af waarin we ons bevinden. na het uitvoeren van het commando krijgen we als output:

```
/home/student
```

In windows start een _absoluut_ pad met `c:\....`. In Linux kennen we geen schijf letters. De hoogst liggende map (in windows vaak `c:\`) noemen we de _root directory_. Deze wordt weergegeven als `/`.

De map `student` waar we ons in bevinden is dus een submap van de map `home`. De map `home` bevindt zich op zijn beurt in de _root directory_ `/`.

![homefolder](../images/04/homefolder-struct.png)

?> <i class="fa-solid fa-circle-info"></i> Herrinner je nog de prompt waarin het actieve pad stond? het `~` teken was een afkorting voor `/home/student`. Dit wordt ook wel de homefolder genoemd. Elke gebruiker heeft zijn eigen homefolder in de map `/home`. Net zoals in Windows elke gebruiker dit heeft onder `c:\Gebruikers\`. Hierin heeft een standaardgebruiker ook alle rechten (lezen, schrijven, uitvoeren). Daarbuiten heeft de gebruiker maar beperkte rechten!

Linus heeft het `wget` commando uitgevoerd in zijn homefolder (`~`), dus hij denkt dat het server bestand ook in die map staat. Via de manpages komt hij bij het `ls`commando dat de inhoud van een map weergeeft. Hij heeft 2 opties:
- `ls` zonder argument geeft de listing van de huidige map
- `ls /home/student` of `ls ~` afgekort geeft de listing van het pad dat erachter staat, in dit geval `/home/student`

Beide geven in dit geval dezelfde output:
```bash
student@linux-essentials:~$ ls
server.jar
student@linux-essentials:~$ ls /home/student
server.jar
```
In deze output ziet Linus enkel de bestandsnaam, hij is ook geïntereseerd in order andere de grootte van de file. Hierbij voert hij volgend commando uit:
```bash
$ ls -alh .
total 45M
drwxr-xr-x 5 student student 4.0K Mar 27 16:36 .
drwxr-xr-x 3 root    root    4.0K Oct  5 13:40 ..
-rw------- 1 student student 1.7K Mar 17 12:14 .bash_history
-rw-r--r-- 1 student student  220 Oct  5 13:40 .bash_logout
-rw-r--r-- 1 student student 3.7K Oct  5 13:40 .bashrc
-rw-r--r-- 1 student student  807 Oct  5 13:40 .profile
-rw-r--r-- 1 student student    0 Oct  6 08:20 .sudo_as_admin_successful
-rw-r--r-- 1 student student  45M Feb 28 11:48 server.jar
```
?> <i class="fa-solid fa-circle-info"></i> verschillende opties kan je combineren. In bovenstaande voorbeeld is `ls -a -l -h` hetzelfde als `ls -alh`! 
De gebruikte opties kan je uiteraard opzoeken in de manpages, maar wel helpen je alvast even verder:
* de optie `-a` toont ook verborgen bestanden en mappen. Deze starten in linux met een `.`.
* de optie `-l` toont een _longlisting_. Dit zorg ervoor dat we al de extra informatie in bovenstaande output krijgen.
* de optie `-h` staat voor _human readable sizes_ en zorgt ervoor dat bestandsgroottes mooier weergegeven worden.

Nu weet Linus dat het `server.jar`bestand 45MB groot is en dat het het laatst aangepast is op 28 februari om 11:48.

De reeks `-rw-r--r-- 1` heeft te maken met rechten en permissies, hier komen we later op terug. de `student student` kolommen hebben te maken met wie eigenaar is van het bestand / de map & zijn ook gelinkt aan deze permissies.

### navigeren & maken
Linus wil een duidelijke mappenstructuur aanmaken voor _LinusCraft_. In zijn homefolder wil hij graag een map met de naam `linuscraft` aanmaken. Hiervoor heeft hij via de manpages het commando `mkdir` gevonden.
```bash
mkdir linuscraft
```
Het argument van het commando is een pad. Je zou dus ook bijvoorbeeld `mkdir /home/student/minuscraft` kunnen uitvoeren. Zowel relatieve als absolute paden (zie verder) kunnen gebruikt worden in het `mkdir` commando.

?> <i class="fa-solid fa-circle-info"></i> Zoals eerder aangegeven is alles in Linux hoofdlettergevoelig. Ook hier is dit belangrijk in functie van de mapnamen. Voor een keer het commando `mkdir abc ABC` uit. Je zal zien dat er 2 mappen op je systeem aangemaakt zijn: één met de naam `abc` en één met de naam `ABC`.

vervolgens wil hij in de map alvast een map met de naam `serverfiles` maken. Hiervoor gaat hij eerst navigeren naar de map `linuscraft` die we net aangemaakt hebben. Dit kan je doen met het `cd` (change directory) commando:
```bash
cd linuscraft
```
Daarna kan hij opnieuw het `mkdir serverfiles` commando uitvoeren om een map `serverfiles` aan te maken in de map `linuscraft`. Controleer dit door volgende commando's uit te voeren:
```bash
student@linux-essentials:~/linuscraft$ cd serverfiles
student@linux-essentials:~/linuscraft/serverfiles$ pwd
/home/student/linuscraft/serverfiles
```
## Relatieve & absolute paden
Paden worden gebruikt om aan te duiden waar zowel directories als bestanden zich bevinden op het filesysteem. Hierin maken we onderscheid tussen _absolute_ en _relatieve_ paden. De werken van deze 2 is hetzelfde binnen zowel Linux als Windows systemen.

#### Absoluut pad
Absolute paden starten *altijd* met een `/`. Een absoluut pad start dus vanaf de _root_ directory en werkt zijn weg naar beneden. Bijvoorbeeld:
```bash
student@linux-essentials:/opt/$ ls /home/student/linuscraft
```
?> <i class="fa-solid fa-circle-info"></i> Binnen Windows start een absoluut pad niet met `/` maar met `C:\`!

#### Relatief pad
Een relatief pad start vanuit *de huidige directory* en werkt vanuit daar naar een andere map. Bijvoorbeeld:
```bash
$ pwd
/home/student
$ cd Downloads/testfolder
$ pwd
/home/student/Downloads/testfolder
```
Binnen relatieve paden werken we ook vaak met volgende _shortcuts_:
```
.(één punt) - Hiermee refereren we naar de huidige directory
..(2 punten) - Hiermee refereren we naar de parent(=bovenliggende) directory. 
```
Wat dit wil zeggen is dat als we in de directory `/home/student/abc` zitten, we `..` kunnen gebruiken om naar de parent directory `/home/student` te gaan:
```bash
$ pwd
/home/student/abc
$ cd ..
$ pwd
/home/student
```
De punt & dubbelpunt syntax kunnen we ook in paden zelf gebruiken:
```bash
$ ls /home # absoluut pad
student bob arthur
$ pwd
/home/student/abc
$ cd ../../bob # relatief pad
$ pwd
/home/bob
```
?> <i class="fa-solid fa-circle-info"></i> Een hekje `#` geef aan dat alles wat erna komt commentaar is en dus niet uitgevoerd zal worden als een commando

## Files

### Files aanmaken

touch, echo, nano

### Files verplaatsen

mv, cp, rename

## Wissen 

Extra lesmateriaal:


<i class="fa-solid fa-film"></i> [[Pluralsight] Linux command syntax patterns](https://app.pluralsight.com/course-player?clipId=5c3b8432-e324-4b4b-adfd-2615298a7aba)

<i class="fa-solid fa-film"></i> [[Pluralsight] Working with files & directories](https://app.pluralsight.com/course-player?clipId=f98f5110-6ee4-43c4-af00-4de294c17bc9)