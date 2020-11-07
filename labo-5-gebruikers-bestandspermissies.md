# Labo 5: Bestandspermissies

Als je gebruik maakt van andere bronnen (bv. blog-artikel of HOWTO die je op het Internet vond), voeg die dan toe aan het einde van dit document. Zo kan je het later terug vinden.

Maak ter voorbereiding zeker de oefeningen in Linux Fundamentals (Paul Cobbaut) over dit onderwerp (pp. 222 en 228).


## Gebruikers en groepen aanmaken

Het doel van deze opgave is om de opdrachten en de begrippen met betrekking tot  gebruikers en groepen te bestuderen, binnen de context van Linux als een multi-user-systeem.

Tussen de vragen is ruimte voorzien om je antwoorden in te vullen. Het gaat telkens om zgn. codeblokken in Markdown, die starten en eindigen met drie backquotes. Binnen elk codeblok geef je telkens het commando dat je hebt ingetikt en de uitvoer die je krijgt.

1. Je hebt al een gebruiker aangemaakt voor jezelf. Log in als deze gebruiker. Geef hieronder telkens het commando en de uitvoer
    - Wat is het commando om de huidige directory op te vragen? Welke uitvoer toont het commando?

        ```
        [chichoi@localhost ~]$ pwd
        /home/chichoi
        ```

    - Wat is het UID van deze gebruiker?

        ```
        [chichoi@localhost ~]$ id -u chichoi OF [chichoi@localhost ~]$ echo $UID  
        1000
        ```

    - Wat is het GID van deze gebruiker?

        ```
        [chichoi@localhost ~]$ id -g chichoi
        1000
        ```

2. Log in als de `root`-gebruiker met het commando `su -` (let op de spatie!) (Werkte niet voor mij, ik gebruikte `sudo -i`)
    - Wat is de home-directory van `root`?

        ```
        [root@localhost ~]# pwd
        /root
        ```

    - Wat is het UID van deze gebruiker?

        ```
        [root@localhost ~]# id -u root
        0
        ```

    - Wat is het GID van deze gebruiker?

        ```
        [root@localhost ~]# id -g root
        0
        ```

3. Maak een nieuwe gebruiker aan met de naam `alice`, zonder specifieke opties
    - Geef het gebruikte commando:

        ```
        [root@localhost ~]# useradd alice
        UITVOER: /
        ```

    - Voorzie een geschikt wachtwoord voor deze gebruiker (en vergeet het niet! Noteer het eventueel hier in je verslag of in de beschrijving van je VM) [lolio1234]

        ```
        [root@localhost ~]# passwd alice
        New password: [INVOER]
        Retype new password: [INVOER]
        passwd: all authentication tokens updated successfully.
        ```

4. Configuratiebestanden voor gebruikersbeheer:
    - In welk bestand kan je de UID, gebruikersnaam, homedirectory, enz. van alle gebruikers terugvinden?

        ```
        [root@localhost ~]# cat /etc/passwd
        ```

    - In welk configuratiebestand kan je al de bestaande gebruikersgroepen nakijken, en ook de gebruikers die lid zijn van elke groep?

        ```
        [root@localhost ~]# cat /etc/group
        ```

    - In welk configuratiebestand vind je de *wachtwoorden* van alle gebruikers?

        ```
        [root@localhost ~]# cat /etc/shadow
        ```

5. Gebruikersgroepen aanmaken
    - Maak een groep aan met de naam `sporten`

        ```
        [root@localhost ~]# groupadd sporten
        UITVOER: /
        ```

    - In welk configuratiebestand vind je het GID van deze groep terug?

        ```
        [root@localhost ~]# cat /etc/group
        UITVOER: /
        ```

    - Wat zal het GID zijn van de groepen `zwemmen` en `judo` als je deze nu onmiddellijk zou aanmaken? Maak ze aan en controleer!

        ```
        [root@localhost ~]# groupadd zwemmen
        UITVOER: /
        
        [root@localhost ~]# groupadd judo
        UITVOER: /
        ```
        **Antwoord: zwemmen(1003), judo(1004)**

    - Voeg de gebruiker `alice` toe aan de groepen `sporten` en `zwemmen`

        ```
        [root@localhost ~]# usermod -aG sporten,zwemmen alice
        UITVOER: /
        ```

    - Log in als `alice` door in een terminal het commando `su - alice` (let op de spaties!) uit te voeren

        ```
        [root@localhost ~]# su - alice
        UITVOER: /
        ```

    - Zorg er nu voor dat de groep `sporten` de primaire groep wordt van `alice`.

        ```
        [alice@localhost ~]$ sudo usermod -g sporten alice
        [sudo] password for alice: 
        alice is not in the sudoers file.  This incident will be reported.
        ```
        **Alleen de root-gebruiker kan de primaire groep veranderen? Of je moet alice eerst in de sudoer file steken zodat je sudo kunt oproepen (Door haar in groep 10(wheel) te steken.**
    - Zorg er voor dat `alice` uitgelogd is, ga terug naar `root`

        ```
        [alice@localhost ~]$ exit
        logout
        ```

6. Maak nu de gebruikers in onderstaande tabel aan. Zorg er voor dat ze al meteen bij aanmaken tot de aangegeven groepen behoren. Kies zelf geschikte wachtwoorden voor deze gebruikers en vergeet ze niet (vul eventueel een kolom toe aan de tabel).

    | Gebruikersnaam | Primaire groep | Secundaire groep | Wachtwoord   |
    | :---           | :---           | :---             | :---         |
    | `bob`          | `sporten`      | `judo`           | ikbenbob     |
    | `carol`        | `sporten`      | `zwemmen`        | ikbencarol   |
    | `daniel`       | `sporten`      | `judo`           | ikbendaniel  |
    | `eva`          | `sporten`      | `zwemmen`        | ikbeneva     |

    - Geef de gebruikte commando's om de gebruikers aan te maken en ook om te verifiëren of dit correct gebeurd is:

        ```
        [root@localhost ~]# useradd -g sporten -G judo bob
        UITVOER: /
        
        [root@localhost ~]# passwd  bob             #ikbenbob
        BAD PASSWORD: The password fails the dictionary check - it is based on a dictionary word
        Retype new password: 
        passwd: all authentication tokens updated successfully.
        
        [root@localhost ~]# id bob
        uid=1002(bob) gid=1002(sporten) groups=1002(sporten),1004(judo)
        ...
        ```

    - Verwijder nu de *groep* `alice` en controleer.

        ```
        [root@localhost ~]# groupdel alice
        UITVOER: /
        ```

    - Gebruiker `daniel` gaat een tijdje niet meer sporten. Zorg er voor dat deze gebruiker tot nader order geen toegang meer kan hebben tot het systeem (zonder het wachtwoord of de gebruiker te verwijderen!).

        ```
        [root@localhost ~]# usermod -L daniel
        UITVOER: /
        ```

    - Hoe kan je controleren dat `daniel` inderdaad geen toegang meer heeft tot het systeem? In welk bestand kan dat en hoe zie je daar dan dat het account afgesloten is?

        ```
        [root@localhost ~]# cat /etc/shadow | grep daniel
        daniel:!$6$BJ59/NxX6xaarwJy$of/xckjGhztCSYFsw1l9rTPoOldXR42KbdMVLGmtlOTb24NpBnwq.FRryrAzwZQzmLxzU1erOSZIaq8SN921S1:18573:0:99999:7:::
        ```
        
        **Antwoord: net na [USER]: staat een uitroepteken (!) dit geeft aan dat dit account gelocked is.**

    - Gebruiker `daniel` komt terug naar de sportclub. Geef hem opnieuw toegang tot het systeem.

        ```
        [root@localhost ~]# usermod -U daniel
        UITVOER: /
        ```

    - Gebruiker `eva` stopt helemaal met sporten. Verwijder deze gebruiker, maar doe dit zorgvuldig: zorg er in het bijzonder voor dat ook haar homedirectory verwijderd wordt.

        ```
        [root@localhost ~]# userdel -r eva
        UITVOER: /
        ```

7. Log aan als de gebruiker `carol`

    ```
    [root@localhost ~]# su - carol
    UITVOER: /
    ```

    - Controleer of je in de “thuismap” bent van deze gebruiker. Maak onder deze map een bestand `test` aan door middel van het commando `touch`.

        ```
        [carol@localhost ~]$ pwd
        /home/carol
        
        [carol@localhost ~]$ touch test
        UITVOER: /
        ```

    - Probeer nu als gebruiker `carol` je te verplaatsen naar de “thuismap” van `alice`.

        ```
        [carol@localhost ~]$ cd /home/alice
        -bash: cd: /home/alice: Permission denied


        ```

    - Kan je de inhoud van de mappen binnen de thuismap van `alice` bekijken?

        ```
        [carol@localhost ~]$ ls /home/alice
        ls: cannot open directory '/home/alice': Permission denied
        ```

    - Probeer nu als `carol` onder de “thuismap” van `alice` ook een bestand `test` te maken. Lukt dit? Kan je dit verklaren?

        ```
        [carol@localhost ~]$ touch /home/alice/test
        touch: cannot touch '/home/alice/test': Permission denied
        ```
        **De gebruiker 'carol' heeft geen rechten van die directory (van alice)"
## Algemene permissies

Geef in de volgende oefeningen telkens het commando dat nodig is om de taak uit te voeren en ook het resultaat.

1. Log in als gewone gebruiker. Wat is de waarde van umask?

    ```
    umask
    0002
    ```

2. Maak een directory `oefenenMetPermissies` aan. Welke octale permissies verwacht je voor deze nieuwe directory?

    ```
    [chichoi@localhost ~]$ mkdir oefenenMetPermissies/
    UITVOER: /
    ```
    **Antwoord: Permissies : 777 (standaard directory permissies) - 002 (umask) = 775**

3. Controleer dit door de *symbolische* permissies op te vragen.

    ```
    [chichoi@localhost ~]$ ls -l | grep oefenenMetPermissies
    drwxrwxr-x. 2 chichoi chichoi 4096 Nov  7 20:36 oefenenMetPermissies
    ```

4. Controleer of de symbolische waarden en octale waarden overeen komen!
    ```
    drwxrwxr-x.
    d = directory
    rwx = 7
    rwx = 7
    r-x = 5
    = 775
    ```
    **Antwoord: De symbolische waarden en octale waarden komen overeen.**
5. Stel nu de umask waarde zo in dat niemand permissies heeft op de bestanden en directories die je aanmaakt, behalve jijzelf.

    ```
    [chichoi@localhost ~]$ chmod 700 oefenenMetPermissies/
    [chichoi@localhost ~]$ ls -l | grep oefenenMetPermissies
    drwx------. 2 chichoi chichoi 4096 Nov  7 20:36 oefenenMetPermissies
    ```

6. Maak nu een bestand aan met de naam `vanmij`, in de directory `oefenenMetPermissies` met als inhoud de tekst: `echo "Waarschuwing: eigendom van ${USER}!"` Schrijf neer hoe je dit bestand gemaakt hebt. Controleer de permissies; schrijf ze neer en was dit wat je verwachtte? Verklaar!

    ```
    [chichoi@localhost ~]$ echo "Waarschuwing: eigendom van ${USER}!" > oefenenMetPermissies/vanmij
    UITVOER:/
    
    [chichoi@localhost ~]$ ls -l oefenenMetPermissies/
    -rw-rw-r--. 1 chichoi chichoi 36 Nov  7 20:55 vanmij
    ```
    
    ```
    -   = file
    rw- = 6
    rw  = 6
    r-- = 4
    ```
    **Antwoord: Permissies : 666 (standaard file permissies) - 002 (umask) = 664**

7. Verander nu de permissies van het bestand `vanmij` zodat je zelf het bestand kan uitvoeren. Geef het gebruikte commando (op de octale manier) en test het resultaat.

    ```
    [chichoi@localhost ~]$ chmod 744 oefenenMetPermissies/vanmij
    UITVOER: /
    ```

8. Log in als de gebruiker `alice` (als je deze niet meer hebt, maak je die aan en voorzie de gebruiker van een eenvoudig paswoord), maar zorg dat je niet verandert van directory. Kan `alice` het bestand `vanmij` uitvoeren? Verklaar!

    ```
    [chichoi@localhost ~]$ su alice
    Password: 
    
    [alice@localhost chichoi]$ ./vanmij
    bash: ./vanmij: Permission denied
    ```
    **Alleen de u(USER) heeft de x permissie gekregen, de groepen of andere gebruiker hebben deze rechten niet.**

9. Verander nu de permissies van het bestand vanmij zodat iedereen het bestand kan uitvoeren. Geef het gebruikte commando (op de symbolische manier) en test het resultaat.

    ```
    [chichoi@localhost ~]$ chmod g+x,o+x oefenenMetPermissies/vanmij    #Symbolische notatie
    [chichoi@localhost ~]$ chmod 755 oefenenMetPermissies/vanmij        #Octale notatie
    [chichoi@localhost ~]$ su alice
    Password: 
    [alice@localhost chichoi]$ ./vanmij
    bash: ./vanmij: Permission denied
    ```
    **Antwoord: Dit lukt nog steeds niet omdat de directory geen permission geeft aan groepen en andere gebruikers.**

## Geavanceerde permissies

1. Zoek alle bestanden in het systeem waar de SUID-permissie op ingesteld staat. Schrijf het resultaat in een bestand met de naam `suidBestanden. Schrijf de fouten weg naar een `foutenBestand`. Doe dit in één commandolijn. (Tip: gebruik het commando `find` en zoek in de manpages naar de geschikte opties).

    ```
    [chichoi@localhost ~]$ find / -perm -4000 > suidbestanden 2> foutenBestan
    UITVOER: /
    ```

2. Controleer het resultaat door een bestand te nemen uit `suidBestanden` en de permissies op te vragen van dat bestand.

    ```
    [chichoi@localhost ~]$ ls -l /usr/bin/mount
    -rwsr-xr-x. 1 root root 58560 May 20 17:16 /usr/bin/mount
    ```

3. Check of het programmabestand `/usr/bin/passwd` in het bestand `suidBestanden` aanwezig is. Schrijf het gebruikte commando op. Is het aanwezig?

    ```
    [chichoi@localhost ~]$ grep bin/passwd suidbestanden 
    /usr/bin/passwd
    ```

## Geavanceerde permissies: setGID en de *sticky bit*

1. Ga naar de directory `oefenenMetPermissies`, als gewone gebruiker (dus niet als `root`) en kopieer het bestand `/etc/hosts` daar naartoe.

    ```
    $ COMMANDO
    UITVOER
    ```

2. Verander nu de permissies van het bestand `hosts` in directory `oefenenMetPermissies` als volgt: SGID aan, `rx` voor *others*, `rw` voor *group* en geen permissies voor de eigenaar (merk op dat deze combinatie van permissies geen praktisch nut heeft!). Geef het gebruikte commando en ook het commando om te controleren of de permissies juist ingesteld zijn.

    ```
    $ COMMANDO
    UITVOER
    ```

3. Kan de eigenaar nu het bestand bekijken? Waarom wel of niet? Noteer hoe je dit controleert:

    ```
    $ COMMANDO
    UITVOER
    ```

4. Kan de eigenaar de permissies wijzigen? Controleer.

    ```
    $ COMMANDO
    UITVOER
    ```

5. Kan de eigenaar het bestand verwijderen? Controleer.

    ```
    $ COMMANDO
    UITVOER
    ```

Kopieer als je eigen gebruiker (niet als root!) nu opnieuw het bestand `/etc/hosts` in het directory `oefenenMetPermissies` en pas de permissies opnieuw aan zoals eerder voorgeschreven. Zorg dat gebruiker `alice` lid is van de groep die groepseigenaar is van het bestand `hosts` in directory `oefenenMetPermissies`. Switch nu naar gebruiker alice.

1. Kan alice nu het bestand bekijken? Controleer.

    ```
    $ COMMANDO
    UITVOER
    ```

2. Kan alice de permissies wijzigen? Controleer.

    ```
    $ COMMANDO
    UITVOER
    ```

3. Kan alice het bestand verwijderen? Is dit de bedoeling? Controleer.

    ```
    $ COMMANDO
    UITVOER
    ```

4. Stel nu de sticky-bit in op het directory oefenenMetPermissies. Geef het geschikte commando en controleer het resultaat.

    ```
    $ COMMANDO
    UITVOER
    ```

## Eigenaars en groepseigenaars veranderen

1. Maak als `root` onder `/srv/` twee directories aan met de naam `groep/verkoop` en `groep/inkoop`. Maak ook 2 groepen aan met de namen `verkoop` en `inkoop`. Maak twee gebruikers aan, `margriet` met primaire groep `verkoop` en `roza`, die als primaire groep `inkoop` heeft. Zorg dat de groepen eigenaar zijn van de overeenkomstige directories en dat `margriet` eigenaar is van directory `verkoop` en `roza` van het directory `inkoop`. Geef de gebruikte commando’s en controleer:

    ```
    # COMMANDO
    UITVOER
    ...
    # ls -l groep/
    total 0
    drwxr-xr-x. 2 roza     inkoop  6 Sep 22 22:23 inkoop
    drwxr-xr-x. 2 margriet verkoop 6 Sep 22 22:23 verkoop
    ```

2. Zorg ervoor dat gebruikers en groepen uit de vorige stap alle permissies hebben. Geef het geschikte commando en controleer.

    ```
    $ COMMANDO
    UITVOER
    ```

3. Voeg een gebruiker, vb `alice`, toe aan de groep `inkoop` en `verkoop` en controleer. Geen van beide groepen zijn primair.

    ```
    $ COMMANDO
    UITVOER
    ```

4. Log in als `alice` en ga naar de directory verkoop. Laat de gebruiker hier een leeg bestand, `bestand1`, aanmaken in de directory verkoop. (Indien je hier problemen ondervindt, log dan in via een andere terminalvenster).

    ```
    $ COMMANDO
    UITVOER
    ```

5. Wie is nu eigenaar van `bestand1` en wie de groepseigenaar?

    ```
    $ COMMANDO
    UITVOER
    ```

6. Zorg er nu voor dat de groepseigenaar van de directory `verkoop` automatisch de groepseigenaar wordt van alle bestanden en directories die onder `verkoop` gemaakt worden. Geef de gebruikte commando’s.

    ```
    $ COMMANDO
    UITVOER
    ```

7. Doe hetzelfde voor de directory `inkoop`. Geef de gebruikte commando’s:

    ```
    $ COMMANDO
    UITVOER
    ```

8. Verander opnieuw naar gebruiker `alice` en laat deze gebruiker een leeg `bestand2` aanmaken in de directory `verkoop`. Geef de gebruikte commando’s:

    ```
    $ COMMANDO
    UITVOER
    ```

9. Wie is nu eigenaar van `bestand2` en wie groepseigenaar?

    ```
    $ COMMANDO
    UITVOER
    ```

10. Laat nu gebruiker `margriet` een leeg bestand `bestand3` aanmaken. Controleer de eigenaar van `bestand3` en de groepseigenaar.

    ```
    $ COMMANDO
    UITVOER
    ```

11. Laat nu gebruiker `alice` `bestand3` verwijderen. Lukt dit?

    ```
    $ COMMANDO
    UITVOER
    ```

12. Zorg er nu voor dat de gebruikers elkaars bestanden niet kunnen verwijderen. Als de gebruiker echter eigenaar is van het betreffende directory mag dit wel. Leg uit hoe je dit doet en controleer. Schrijf je gevolgde procedure op.

    ```
    $ COMMANDO
    UITVOER
    ```

## Gebruikte bronnen
