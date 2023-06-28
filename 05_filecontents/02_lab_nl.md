# Lab <!-- {docsify-ignore} --> 
In het vorige lab heeft Linus een aantal mappen en bestanden gemaakt. Het probleem is dat deze bestanden nog steeds leeg zijn. In dit lab zullen we inhoud toevoegen aan enkele van de bestaande bestanden en ook enkele nieuwe bestanden toevoegen.  

We beginnen met de eenvoudigste manier om tekst in een bestand in te voeren. We kunnen dit doen met behulp van een teksteditor zoals `nano`. Linus gebruikt het commando `nano linuscraft/todo` om het todo-bestand de volgende inhoud te geven: 
```
TODO LINUSCRAFT
===============
start server - unfinished
automate backups - unfinished
create a website - unfinished
create an account for Mark - unfinished
install security updates - unfinished
create directory sturcture - done
install server - done
design logo - done
```
?> <i class="fa-solid fa-circle-info"></i> Let op de spaties, hoofdletters en streepjes. Deze zijn belangrijk in een van de volgende hoofdstukken! 

We kunnen het bestand opslaan met behulp van de toetsenbordcombinatie `ctrl + o`. Het zal vragen om het pad naar het bestand (naam) te bevestigen. Als je op enter drukt, wordt de inhoud van het bestand opgeslagen.  

Zorg ervoor dat je controleert of de inhoud correct is opgeslagen met behulp van het commando `cat linuscraft/todo`. Als we alleen de laatste paar regels willen controleren, kunnen we ook het commando `tail linuscraft/todo` gebruiken. 

<i class="fa-solid fa-pencil"></i> Wil je een uitdaging? Probeer de editor `vi` of `vim` te gebruiken om de tekst in te voegen. Dit is een speciale en populaire teksteditor met een opdracht- en invoegmodus. Meer informatie over deze editor die je eerst moet lezen, vind je [hier](https://linuxfoundation.org/blog/classic-sysadmin-vim-101-a-beginners-guide-to-vim/). 

Het bovenstaande commando gebruikt een relatief pad naar het bestaande `todo`-bestand.  

We kunnen nano ook gebruiken om nieuwe bestanden te maken door een bestandsnaam op te geven die nog niet bestaat:  
```bash
student@linux-ess:~/linuscraft$ nano playerinfo/dries.txt
```

We geven dit bestand de volgende inhoud: 
```
player aliases: dries, 3s, d r 1 3 s
age: 32
Notes:
- Has way to much free time, is always online
- Likes to grief other people's bases
```

Het `contact`-bestand bestaat alleen uit Linus zijn e-mailadres. We kunnen dit eenvoudig invoegen met behulp van het `echo`-commando: 
```bash
student@linux-ess:~/linuscraft$ echo linus@pxl.be > ./contact
student@linux-ess:~/linuscraft$ cat contact
linus@pxl.be
```

<i class="fa-solid fa-pencil"></i> Wat gebeurt er als we het commando `echo mark@pxl.be > ./contact` uitvoeren na het uitvoeren van het bovenstaande commando? Probeer twee `echo`-commando's te gebruiken om zowel Linus als Mark's contactgegevens toe te voegen! 

Vervolgens wil Linus snel de eerste 2 items op zijn todo-lijst bekijken. We kunnen dit doen door het commando `head` te gebruiken: 
```bash
student@linux-ess:~/linuscraft$ head -2 todo
TODO LINUSCRAFT
===============
```
We merken dat dit niet de uitvoer is die we willen, omdat het alleen de titel van het tekstbestand toont. We passen het commando als volgt aan: 
```bash
student@linux-ess:~/linuscraft$ head -4 todo
TODO LINUSCRAFT
===============
start server - unfinished
automate backups - unfinished
```
<i class="fa-solid fa-pencil"></i> Wat als we een hele lange todo-lijst hadden die niet in ons CLI-venster past. Probeer nog een paar todo-items toe te voegen om dit uit te proberen. Welk commando kan je gebruiken om door deze lijst te bladeren? 

Ten slotte wil Linus een `playerlist`-bestand maken dat afkomstig is van de inhoud van de map `playerinfo`. We kunnen een lijst maken van alle tekstbestanden van alle spelers en deze opslaan in het `playerinfo`-bestand in plaats van alle namen handmatig te typen. We kunnen dit als volgt doen: 
```bash
student@linux-ess:~/linuscraft$ ls -l playerinfo/ > playerlist
student@linux-ess:~/linuscraft$ cat playerlist
total 4
-rw-r--r-- 1 dries dries 113 Sep  6 12:50 dries.txt
-rw-r--r-- 1 dries dries   0 Aug 25 09:04 linus.txt
```
Zoals je in de uitvoer kunt zien, bevat de bestandsinhoud van de spelerslijst veel extra informatie die we een eigenlijk willen verwijderen, maar we zullen leren hoe we dit moeten doen in een van de volgende hoofdstukken. Voor nu volstaat dit. 
