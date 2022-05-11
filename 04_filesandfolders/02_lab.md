# Lab <!-- {docsify-ignore} -->
In het vorige hoofdstuk had Linus een server bestand gedownload voor de minecraft server. Maar waar staat dit bestand nu? In deze lab zoeken we uit hoe we kunnen navigeren in mappen & hoe we enkele basisbewerkingen met bestanden kunnen uitvoeren.

## het server.jar bestand vinden <!-- {docsify-ignore} -->

Als start wil Linus zoeken naar het `server.jar` bestand dat hij in het vorige hoofdstuk gedwonload heeft. Via het `man -k directory` commando ziet hij al snel dat er verschillende commando's zijn om met directories te werken.

Het eerste commando dat Linus bekijkt, is het `pwd` commando. Uit de manpage van het commando zelf:
```
pwd - print name of current/working directory
```
Bij het uitvoeren krijgen we volgende output:
```bash
student@linux-ess:~$ pwd
/home/student
```

Linus heeft het `wget` commando uitgevoerd in zijn homefolder (`~`), dus hij denkt dat het server bestand ook in die map staat. Via de manpages komt hij bij het `ls` commando dat de inhoud van een map weergeeft:
```bash
student@linux-ess:~$ ls
server.jar
```

Zijn vermoedens worden bevestigd. Om zeker te zijn dat de download gelukt is, wil hij ook even de bestandsgrootte controleren

```bash
student@linux-ess:~$ ls -lh
-rw-r--r-- 1 student student  45M Feb 28 11:48 server.jar
```

Nu weet Linus dat het `server.jar`bestand 45MB groot is en dat het het laatst aangepast is op 28 februari om 11:48.

## Aanmaken mappenstructuur <!-- {docsify-ignore} -->
Linus wil een duidelijke mappenstructuur aanmaken voor _LinusCraft_. In zijn homefolder wil hij graag een map met de naam `linuscraft` aanmaken. Hiervoor heeft hij via de manpages het commando `mkdir` gevonden.
```bash
mkdir linuscraft
```
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
Daarnaast wil hij onder de folder `linuscraft` ook nog een folder `administratie` maken. Hij doet dit a.d.h.v. een relatief pad:
```bash
mkdir ../administratie
```

Tenslotte maakt hij nog een map met de naam `backups` aan de hand van een absoluut pad:
```bash
mkdir /home/student/linuscraft/backups
```

Linus gaat terug naar zijn homefolder door het `cd` commando uit te voeren. Daarna checkt hij de inhoud van zijn aangemaakte folder `linuscraft`:
```bash
student@linux-ess:~$ ls -lh linuscraft
total 12K
drwxr-xr-x 2 student student 4.0K May  4 21:45 administratie
drwxr-xr-x 2 student student 4.0K May  4 21:48 backups
drwxr-xr-x 2 student student 4.0K May  4 21:44 serverfiles
```

## Aanmaken files <!-- {docsify-ignore} -->
Linus wil op zijn server graag een bestandje om openstaande werkzaamheden op te lijsten. Hij maakt deze file aan in de folder `linuscraft`:
```bash
touch linuscraft/todo.txt
```

vervolgens gebruikt hij `nano linuscraft/todo.txt` om het bestand te openen. Geef dit bestand volgende inhoud:
```
TODO LINUSCRAFT
===============
opstarten server - unfinished
automatisatie backups - unfinished
opzetten website - unfinished
aanmaken account mark - unfinished
installatie updates - unfinished
aanmaken mappenstructuur - done
installatie server - done
ontwerpen logo - done
```

Hij wil voor het gemak ook de belangrijke informatie in een verborgen bestand zetten. Hij maakt alvast het bestand aan met het `touch` commando:
```bash
touch /home/dries/linuscraft/.important
```

## Verplaatsen bestanden en mappen <!-- {docsify-ignore} -->