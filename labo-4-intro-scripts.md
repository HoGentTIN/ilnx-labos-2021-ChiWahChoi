# Labo 4: Intro scripting

Als je gebruik maakt van andere bronnen (bv. blog-artikel of HOWTO die je op het Internet vond), voeg die dan toe aan het einde van dit document. Zo kan je het later makkelijk terug vinden.

Maak ter voorbereiding zeker de oefeningen in Linux Fundamentals (Paul Cobbaut) over dit onderwerp (pp. 97, 174 en 181).

## Variabelen

Geef zoals gewoonlijk het commando om de opgegeven taak uit te voeren en controleer ook het resultaat.

1. Druk met behulp van de juiste systeemvariabele de gebruikte bash-versie af op het scherm. Geef het gebruikte commando weer.
    ```
    [chichoi@localhost ~]$ echo $PATH
    /home/chichoi/.local/bin:/home/chichoi/bin:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin
    ```
2. Je bent ingelogd als gewone gebruiker.
    1. Maak een variabele `pinguin` aan en geef deze de waarde Tux.
    ```
    [chichoi@localhost ~]$ pinguin=Tux
    UITVOER: /
    ````
    2. Hoe kan je de inhoud opvragen van deze variabele en afdrukken op het scherm?
    ```
    [chichoi@localhost ~]$ echo $pinguin 
    Tux
    ```
    3. Open nu een sub(bash)shell in je huidige bashomgeving.
    ```
    [chichoi@localhost ~]$ bash
    UITVOER: /
    ```
    4. Hoe kan je controleren dat er nu twee bashshells actief zijn en dat de ene een subshell is van de andere?
    ```
    [chichoi@localhost ~]$ pstree -s $$
    systemd───systemd───gnome-terminal-───bash───bash───pstree
    ```
    5. Probeer nu in deze nieuwe subshell de inhoud van de variabele PINGUIN af te drukken op het scherm. Lukt dit?

    ```
    [chichoi@localhost ~]$ echo $pinguin
    UITVOER: [LEEG]
    ```
    ***Dit lukt niet***
    
    6. De verklaring hiervoor ligt in het type variabele. Welke soort variabele is PINGUIN en hoe kan je dit controleren? Keer hiervoor terug naar je oorspronkelijke bashshell
    ```
    [chichoi@localhost ~]$ exit
    exit
    
    [chichoi@localhost ~]$ ??? #Hoe kan ik contreleren welk type mijn variabele "pinguin" is?
    UITVOER:
    ```
    ***pinguin is momenteel een lokale variabele (local variable)***
    
    7. Zorg er nu voor dat de inhoud van PINGUIN ook in elke nieuwe subshell kan gelezen worden? Hoe doe je dit? Schrijf het gebruikte commando neer.
    ```
    [chichoi@localhost ~]$ export pinguin
    ```

    8. Open opnieuw een sub(bash)shell in je huidige bashomgeving en controleer of je nu de inhoud van PINGUIN kan lezen. Welk soort variabele is PINGUIN nu? Doe dan ook de controle.
    ```
    [chichoi@localhost ~]$ bash
    UITVOER: /
    
    [chichoi@localhost ~]$ echo $pinguin
    Tux
    ```
    ***Variabele "pinguin" is nu een omgevingsvariabele (environmental variable) ***
    
3. Zoek de inhoud op van volgende shellvariabelen en vul volgende tabel aan:

    | Variabele  | Waarde |
    | :---       | :---   |
    | `PATH`     |        |
    | `HISTSIZE` |        |
    | `UID`      |        |
    | `HOME`     |        |
    | `HOSTNAME` |        |
    | `LANG`     |        |
    | `USER`     |        |
    | `OSTYPE`   |        |
    | `PWD`      |        |
    | `MANPATH`  |        |
