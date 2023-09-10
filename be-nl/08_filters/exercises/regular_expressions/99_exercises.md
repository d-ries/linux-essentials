# Oefeningen op Reguliere Expressies

?> <i class="fa-solid fa-circle-info"></i> http://www.regular-expressions.info/

## Oefening 1
Maak het bestand regtest.txt met de volgende inhoud: 
```
apple
banana
apricot
pear
peach
strawberry
mango
grape
orange
5isanumber
123
123abc
abc123
35abcd35
5five5
55fivefive55
555fivefivefive555
77sevenseven77
@d
@tsign@@
atsiiiiiiiiiiiign
```

## Oefening 2
Gebruik reguliere expressies om de regels te filteren die: 

1. De letter a bevatten
2. De letter a of s bevatten
3. De letter a en s bevatten
4. Een @ bevatten
5. Beginnen met de letter p 
6. Eindigen met de letter t  
7. Beginnen met een getal  
8. Beginnen met een cijfer en eindigen met een letter  
9. 2 of meer opeenvolgende letters i bevatten
10. Alleen nummers bevatten
11. Alleen letters bevatten
12. Een of meer cijfers bevatten, gevolgd door een of meer letters 
13. Een of meer cijfers bevatten, gevolgd door een of meer letters en eindigend op een cijfer. 


## Oefening 3
Gebruik sed om:  

1. Maak een bestand regtest_5.txt van het bestand regtest.txt waarbij alle cijfers 5 worden vervangen door "vijf" 
2. Maak een bestand regtest_7.txt van het bestand regtest.txt waarbij de tekst 'seven' wordt vervangen door het getal 7 
3. Maak een bestand regtest_at.txt van het bestand regtest.txt waarbij alle @-symbolen worden vervangen door _at_ 


## Oefening 4
Tel het aantal keer dat 5 kan worden gevonden in regtest.txt 
Zoek in de manpage van grep naar een oplossing 


## Oefening 5
Zoek in de bash manpage naar de header met de naam "REDIRECTION" (De tekst begint bij de linker regel). Is deze zoekfunctie hoofdlettergevoelig? 


## Oefening 6
Probeer met dezelfde reguliere expressie alleen verborgen bestanden uit uw thuismap weer te geven. 

  
## Oefening 7
Gebruik het commando `ls -la ~` en verander in de uitvoer:  

?> <i class="fa-solid fa-circle-info"></i> De referentie "." Naar ". (deze map)" en ".." tot ".. (bovenliggende map)". Verwijder ook de regel die het aantal bestanden en mappen in de map weergeeft  

?> <i class="fa-solid fa-circle-info"></i> Hint: als je het $-teken aan het einde van een tekenreeks gebruikt om te zoeken, betekent dit dat de regel met die tekenreeks moet eindigen.  
Om deze taak te voltooien, moet je het commando `sed` meerdere keren gebruiken 
