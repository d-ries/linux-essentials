# Oefeningen op installatie
## Oefening 1 - Download Ubuntu Desktop
Linux heeft ook een desktopversie. Download [Ubuntu Desktop](https://ubuntu.com/download/desktop). 

![DownloadUbuntuDesktop](../images/02/GetUbuntuDesktop_Download_Ubuntu.png)

## Oefening 2 - Installeer Ubuntu Desktop 

Installeer [Ubuntu Desktop](https://ubuntu.com/download/desktop) in een nieuwe virtuele machine en verken de interface. 

### De nieuwe VM maken 
Om een nieuwe virtuele machine (VM) aan te maken in VMWare ga je naar het menu `file`>`New virtual machine`. De wizard voor het maken van een nieuwe VM wordt weergegeven. 

![VMware-bestand nieuwe VM](../images/02/VMware_File_New_VM.png) 

In het eerste scherm selecteren we de optie `Typical`: 

![VMware Installatie Standaard](../images/02/VMware_Typical.png) 

Vervolgens kiezen we voor `install the operating system later`:

![VMware installeert besturingssysteem later](../images/02/VMware_Operating_System_Later.png) 

Vervolgens kiezen we voor het besturingssysteem `Linux`. In de versie dropdown selecteren we `Ubuntu 64 bit`. Dit is de Linux-distributie die we tijdens deze cursus zullen gebruiken. 

![VMware Ubuntu 64bit](../images/02/VMware_Ubuntu_64bit.png) 

In het volgende scherm geven we de virtuele machine een naam. Je kunt ook een andere map opgeven om de virtuele machine op je computer op te slaan. 

![VMware noemt de VM](../images/02/LAB_VMware_Name_The_VM.png) 

In het volgende scherm configureren we de grootte van de virtuele harde schijf voor de VM. We zullen een schijf maken met 30 GB opslagruimte. Houd er rekening mee dat de schijfruimte wordt toegewezen tijdens het opslaan van bestanden (max. 30 GB): 

![VMware-schijfgrootte](../images/02/LAB_VMware_Disk_Size.png) 

We moeten op `Customize Hardware` klikken om de virtuele machine iets meer te configureren: 

![VMware past hardware aan](../images/02/LAB_VMware_Customize_Hardware.png) 

We moeten het ISO-bestand van de Ubuntu-desktop nog koppelen aan het virtuele cd-rom-station. Dit doen we door `New CD/DVD` te selecteren en naar het gedownloade `iso` bestand te bladeren: 

![VMware Selecteer ISO](../images/02/LAB_VMware_Select_ISO.png) 

Klik op `Finish` en de virtuele machine wordt gemaakt. 

![VMware-afwerking](../images/02/LAB_VMware_Finish.png) 

Je kan de VM nu opstarten door op het groene pijltje te klikken. Hiermee wordt de virtuele machine opgestart en wordt het installatieproces uitgevoerd. 

![VMware-afwerking](../images/02/LAB_VMware_Start_VM.png) 

### Installatie Ubuntu Desktop 

?> <i class="fa-solid fa-circle-info"></i> Resulteert het opstarten van de VM in de fout `This host supports Intel VT-x, but Intel VT-x is diabled`? Dan moet je de VT-X-optie activeren in de BIOS van je laptop. Meer informatie is te vinden in [dit artikel](https://www.qtithow.com/2020/12/fix-error-this-host-supports-Intel-VT-x.html). 

Wanneer we de VM voor de eerste keer opstarten, moeten we op `enter` drukken of 30 seconden wachten: 

![Ubuntu_Desktop_First_Grub](../images/02/LAB_Ubuntu_Desktop_First_Grub.png) 

We moeten een paar seconden wachten tot de boot klaar is: 

![Ubuntu_Desktop_First_Boot_Screen](../images/02/LAB_Ubuntu_Desktop_First_Boot_Screen.png) 

In de volgende paar stappen zal er een installatieproces zijn dat we moeten doorlopen.  
Wij maken de keuze om het volgende te installeren: 

![Ubuntu_Desktop_Try_Or_Install](../images/02/LAB_Ubuntu_Desktop_Try_Or_Install.png) 

We kiezen de juiste toetsenbordindeling. Voor `azerty` selecteren we `Belgian`: 

![Ubuntu_Desktop_Keyboard_AZERTY](../images/02/LAB_Ubuntu_Desktop_Keyboard_Belgian.png) 

?> <i class="fa-solid fa-circle-info"></i> Als je een QWERTY-toetsenbord hebt, moet je het bij `English (US)` houden 

We gaan voor de normale installatie met wat extra closed source drivers en software: 

![Ubuntu_Desktop_Normal_Install](../images/02/LAB_Ubuntu_Desktop_Normal_Install.png) 

We kiezen ervoor om de schijf te wissen en Ubuntu Desktop erop te installeren: 

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Erase_Disk.png) 

We kiezen ervoor om de wijzigingen toe te passen door de wijzigingen naar de schijf te schrijven: 

![Ubuntu_Desktop_Write_Changes_To_Disk](../images/02/LAB_Ubuntu_Desktop_Write_Changes_To_Disk.png) 

?> <i class="fa-solid fa-circle-info"></i> Houd er rekening mee dat je de virtuele schijf van je VM wist. `De harde schijf van je computer/laptop wordt niet gewist!` 

Voor de tijdzone wijzen we Brussel aan op de kaart of schrijven we het in het tekstvak: 

![Ubuntu_Desktop_TimeZone_Brussels](../images/02/LAB_Ubuntu_Desktop_TimeZone_Brussels.png) 

We specificeren de gebruikersnaam en computernaam: 

![Ubuntu_Desktop_Username_and_Computername](../images/02/LAB_Ubuntu_Desktop_Username_and_Computername.png) 

Nu moeten we wachten tot de installatie klaar is: 

![Ubuntu_Desktop_Installaton_Runs](../images/02/LAB_Ubuntu_Desktop_Installaton_Runs.png) 

Zodra de installatie is voltooid, moeten we op `Restart Now` klikken om de VM opnieuw op te starten: 

![Ubuntu_Desktop_Reboot_After_Install](../images/02/LAB_Ubuntu_Desktop_Reboot_After_Install.png) 

Op het laatste scherm druk je gewoon op `enter`. De computer wordt opnieuw opgestart en de installatie is voltooid: 

![Ubuntu_Desktop_Enter_to_Restart](../images/02/LAB_Ubuntu_Desktop_Enter_to_Restart.png) 

## Oefening 3 - Log voor de eerste keer in 

De allereerste keer dat we inloggen, moeten we enkele configuratieschermen doorlopen: 

?> <i class="fa-solid fa-circle-info"></i> Als er een venster met de naam `Software Updater` verschijnt, kunnen we op `Install Now` klikken! 
[Ubuntu_Desktop_First_Login_Click_Updates](../images/02/LAB_Ubuntu_Desktop_First_Boot_Updates.png)

![Ubuntu_Desktop_First_Login_Click_Student](../images/02/LAB_Ubuntu_Desktop_First_Login_Click_Student.png)

![Ubuntu_Desktop_First_Login_Enter_Password](../images/02/LAB_Ubuntu_Desktop_First_Login_Enter_Password.png)

![Ubuntu_Desktop_First_Login_Online_Accounts](../images/02/LAB_Ubuntu_Desktop_First_Login_Online_Accounts.png)

![Ubuntu_Desktop_First_Login_LivePatch](../images/02/LAB_Ubuntu_Desktop_First_Boot_Livepatch.png)

![Ubuntu_Desktop_First_Login_Help_Improve](../images/02/LAB_Ubuntu_Desktop_First_Login_Help_Improve.png)

![Ubuntu_Desktop_First_Login_Privacy](../images/02/LAB_Ubuntu_Desktop_First_Login_Privacy.png)

![Ubuntu_Desktop_First_Login_Ready_To_Go](../images/02/LAB_Ubuntu_Desktop_First_Login_Ready_To_Go.png)

Nu zijn we klaar om Ubuntu Desktop te verkennen: 

![Ubuntu_Desktop_First_Login_Ready_To_Explore](../images/02/LAB_Ubuntu_Desktop_First_Login_Ready_To_Explore.png)

## Oefening 4 - Maak een momentopname van de VM 

Voordat je iets anders doet, is het een goede gewoonte om een momentopname, oftewel snapshot, te maken. Als op een later tijdstip onze Ubuntu Desktop breekt, kunnen we altijd terugkeren naar deze momentopname. 
Het is een tijdsbesparing om terug te kunnen keren naar dit punt, omdat we anders het Linux-systeem opnieuw moeten installeren. 

`Maak een momentopname van de Ubuntu Desktop VM, genaamd "Clean Install"` als volgt: 

_Sluit eerst de VM af..._

![Ubuntu_Desktop_Snapshot_Poweroff](../images/02/LAB_Ubuntu_Desktop_Snapshot_Poweroff.png)

![Ubuntu_Desktop_Snapshot_Poweroff_Confirm](../images/02/LAB_Ubuntu_Desktop_Snapshot_Poweroff_Confirm.png)


_VM/Snapshot/Take Snapshot..._
 
![Ubuntu_Desktop_Snapshot_Take_Snapshot](../images/02/LAB_Ubuntu_Desktop_Snapshot_Take_Snapshot.png)

![Ubuntu_Desktop_Snapshot_Take_Snapshot_Name](../images/02/LAB_Ubuntu_Desktop_Snapshot_Take_Snapshot_Name.png)


?> <i class="fa-solid fa-circle-info"></i> Op een later tijdstip kun je altijd teruggaan naar deze momentopname in de tijd met: 

_VM/Snapshot/Revert to Snapshot..._

![Ubuntu_Desktop_Snapshot_Revert_To_Snapshot](../images/02/LAB_Ubuntu_Desktop_Snapshot_Revert_To_Snapshot.png)

## Oefening 5 - Verken de desktopomgeving 
Probeer op de Ubuntu-desktopmachine de volgende suboefeningen uit te voeren:  
- Verander de desktopachtergrond
- Maak een nieuw tekstbestand met de tool "Text Editor" (= gedit) en probeer het op te slaan in je documentenmap  
- Controleer met de bestandsverkenner (Files) of het bestand bestaat  
- Verwijder het bestand en leeg de prullenbak  
- Pin (=Favorite) de Terminal-applicatie aan het Dock (=launcher)  
- Surf met Firefox naar de website van de school 
- Installeer de Chromium-webbrowser, start de app, maak deze vast aan het Dock en plaats deze boven het Firefox-pictogram  
- Surf met Chromium naar de school webmail portal 
- Installeer wps-office en test de apps  
- Installeer Spotify en test de app  
- Installeer Visual Studio Code en test de app  
- Installeer Gimp en bekijk de app 