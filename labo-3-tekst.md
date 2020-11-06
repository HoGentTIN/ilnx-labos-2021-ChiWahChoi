# Werken met tekst

Als je gebruik maakt van andere bronnen (bv. blog-artikel of HOWTO die je op het Internet vond), voeg die dan toe aan het einde van dit document. Zo kan je het later terug vinden.

Maak ter voorbereiding zeker de oefeningen in Linux Fundamentals van Paul Cobbaut over dit onderwerp (pp. 114-134).

Bekijk ook eens de [presentatie over Vim en tmux](https://www.openminds.be/nl/blog/detail/verslag-techtak-vim-en-tmux) gegeven in 2015 bij Openminds (een Gents webhostingbedrijf).

## De Vim editor

Gebruik de Vi-editor om een bestand aan te maken met de naam `landen`. De inhoud is de volgende (incl. de cijfers):

```
1 België
2 Frankrijk
3 Zwitserland
4 Duitsland
5 Nederland
```

Maak ook een bestand aan met de naam `autokentekens` met deze inhoud:

```
1 B
2 F
3 CH
4 D
5 NL
```

1. Hoe start je Vi op om deze bestanden aan te maken?

    ```
    [chichoi@localhost ~]$ vim [FILENAME]
    UITVOER: VIM EDITOR
    ```

2. Hoe ga je van *normal mode* naar *insert mode*? Geef verschillende manieren:

    | Invoegen vanaf                  | Commando |
    | :---                            | :---     |
    | op de huidige cursorpositie     | `i`      |
    | rechts van de cursor            | `a`      |
    | begin van huidige regel         | `I`      |
    | einde van huidige regel         | `A`      |
    | regel toevoegen onder deze      | `o`      |
    | regel toevoegen op huidige lijn | `O`      |

3. Hoe kopieer je vanuit *normal mode*?

    | Te kopiëren                              | Commando |
    | :---                                     | :---     |
    | Huidige regel                            | `yy`      |
    | Huidige regel en die eronder             | `2yy`      |
    | Het huidige woord                        | `yw`      |
    | Het huidige en de twee volgende woorden  | `3yw`      |
    | Van de cursor tot het einde van de regel | `y$`      |
    | Tot het einde van de *zin*               | `yis`      |
    | Tot het einde van de *paragraaf*         | `yip`      |
    | Alle tekst tussen haakjes `(...)`        | `y%`      |

4. Hoe knip je tekst vanuit *normal* mode?

    | Te knippen                                  | Commando |
    | :---                                        | :---     |
    | Huidige regel                               | `dd`      |
    | Huidige regel en die eronder                | `2dd`      |
    | Het huidige woord                           | `dw`      |
    | Het huidige en de twee volgende woorden     | `3dw`      |
    | Het letterteken op de positie van de cursor | `x`      |
    | Van de cursor tot het einde van de regel    | `d$`      |
    | Tot het einde van de *zin*                  | `dis`      |
    | Tot het einde van de *paragraaf*            | `dip`      |
    | Alle tekst tussen haakjes `(...)`           | `d%`      |

6. Hoe kan je gekopieerde/geknipte tekst plakken?


    | Tekst plakken          | Commando |
    | :---                   | :---     |
    | Rechts/onder de cursur | `p`      |
    | Op de cursur           | `P`      |

De bedoeling van voorgaande oefening is om een idee te geven van hoe veelzijdig Vi is. Er zijn *veel* commando's, maar er zit een duidelijke logica in. Een voorbeeld is `ci{`: dit staat voor *Change inside braces*. Vim zal links en rechts van de cursor zoeken naar accolades, alle tekst ertussen verwijderen en naar insert mode gaan. Je kan in het commando de `{` vervangen door een ander teken zoals bv. `(`, `"`, `'`, `[`, `<`.

Eens je meer commando's leert kennen kan je zo heel productief zijn in Vim. En dan hebben we het nog niet eens gehad over de vele mogelijke instellingen en plugins. Het uitlijnen van de vertikale lijnen in de tabellen hierboven werd bijvoorbeeld gedaan met een Vim plugin, [vimwiki](https://github.com/vimwiki/vimwiki).

## Streams, pipes, redirects

In onderstaande vragen is het telkens de bedoeling één commando te geven om de taak uit te voeren. Probeer altijd eerst om de uitvoer op de console te tonen voordat je wegschrijft naar het gevraagde bestand. Zo zie je sneller eventuele fouten.

1. Voeg het bestand `landen` en `autokentekens` samen met het commando `join` (zoek de werking ervan op met het man-commando). Het resultaat wordt opgeslagen in het bestand `landenkentekens`.

    ```
    [chichoi@localhost ~]$ join landen autokentekens > landenkentekens
    UITVOER: /
    ```

2. Bekijk de inhoud van `landenkentekens` en controleer of het overeenkomt met de uitvoer hieronder.

    ```
    [chichoi@localhost ~]$ cat landenkentekens 
    1 België B
    2 Frankrijk F
    3 Zwitserland CH
    4 Duitsland D
    5 Nederland NL
    ```

3. Haal uit `landenkentekens` alleen kolom 2 en kolom 3 eruit en sla dit resultaat op als `landenkentekens2`.

    ```
    [chichoi@localhost ~]$ cut -d' ' -f2,3 landenkentekens > landenkentekens2
    UITVOER: /
    ```

4. Controleer of de inhoud van `landenkentekens2` overeenkomt met de uitvoer hieronder.

    ```
    [chichoi@localhost ~]$ cat landenkentekens2
    België B
    Frankrijk F
    Zwitserland CH
    Duitsland D
    Nederland NL
    ```

5. Voeg vanop de command-line Italië en Spanje toe aan het einde van `landenkentekens2` met hun respectievelijke kentekens. Je mag hier voor elk land een apart commando gebruiken.

    ```
    [chichoi@localhost ~]$ echo Spanje E >> landenkentekens2
    UITVOER: /
    
    [chichoi@localhost ~]$ echo Italië I >> landenkentekens2
    UITVOER: /
    ```

6. Sorteer `landenkentekens2` alfabetisch op de autokentekens. Sla het bekomen resultaat op in `gesorteerdeautokentekens`. Controleer het resultaat.

    ```
    [chichoi@localhost ~]$ sort -k2 landenkentekens2 > gesorteerdeautokentekens
    UITVOER: /
    
    [chichoi@localhost ~]$ cat gesorteerdeautokentekens
    België B
    Zwitserland CH
    Duitsland D
    Spanje E
    Frankrijk F
    Italië I
    Nederland NL
    ```

## Filters

Sommige van onderstaande oefeningen maken gebruik van specifieke tekstbestanden die je in de subdirectory `labo3` kan vinden. Het antwoord is telkens één enkele opdrachtregel, maar meestal moet je wel een aantal commando's combineren. In principe kan je alle oefeningen oplossen met de commando's die je in de [studiewijzer](../studiewijzer/tekst.md) opgesomd werden.

### Uitvoer van commando's bewerken

1. Bekijk de uitvoer van het commando `ip a` (opvragen van de IP-adressen van deze host). Filter de IPv4 (niet IPv6) adressen er uit:

    ```
    [chichoi@localhost ~]$ ip a | grep inet[^6] | cut -d' ' -f6
    127.0.0.1/8
    10.0.2.15/24
    192.168.56.101/24
    ```

### Werken met doorlopende tekst

Deze oefeningen gebeuren met `lorem.txt`

1. Tel het aantal regels, wooren en tekens in `lorem.txt`

    ```
    [chichoi@localhost labo3]$ wc lorem.txt 
    45  404 2738 lorem.txt
    ```

2. Herformatteer `lorem.txt` zodat elke tekstregel max. 50 lettertekens bevat en nummer daarna elke (niet-lege) regel. Het resultaat wordt weggeschreven in een nieuw bestand, `nlorem.txt`.

    ```
    [chichoi@localhost labo3]$ fmt -w 50 lorem.txt | nl lorem.txt > nlorem.txt
    UITVOER: /
    ```

3. Druk een lijst af van alle individuele woorden in `lorem.txt` (negeer hoofdletters), samen met het aantal keer dat elk woord voorkomt. De lijst is omgekeerd gesorteerd op aantal voorkomens, en dan alfabetisch geordend. Werk stap voor stap:

    - Maak eerst een lijst van woorden, m.a.w. druk `lorem.txt` af met elk woord op een aparte regel
        ```
        [chichoi@localhost labo3]$ cat lorem.txt | sed 's/\s/\n/g'
        ```
    - Verwijder overblijvende leestekens (`,` en `.`) en lege regels
        ```
        [chichoi@localhost labo3]$ cat lorem.txt | sed 's/[,. ]//g'
        ```
    - Sorteer de woorden (niet hoofdlettergevoelig)
        ```
        [chichoi@localhost labo3]$ cat lorem.txt | sort -f
        ```
    - Maak een lijst met voor elk woord het aantal keer dat het voorkomt
        ```
        [chichoi@localhost labo3]$ cat lorem.txt | uniq -ci
        ```
    - Sorteer op het aantal voorkomens en behoud de alfabetische sortering van de woorden
        ```
        [chichoi@localhost labo3]$ cat lorem.txt | sort -nr
        ```
        
    ```
    [chichoi@localhost labo3]$ cat lorem.txt | sed 's/\s/\n/g' | sed 's/[,. ]//g' | sort -f | uniq -ci | sort -nr
     11 sed 
     10 et 
      8 quis 
      7 eget 
      7 mi 
      6 in 
      6 nec 
      6 nunc 
      6 tortor 
      5 ac 
      5 accumsan 
    [...]
    ```

### Gestructureerde tekst

Vele tekstbestanden zijn gestructureerd als tabellen, bv. CSV (comma-separated values). Op een Linux-systeem zijn verschillende configuratiebestanden ook op zo'n manier opgedeeld, maar dan vaak met een `:` als scheidingsteken. In de volgende oefeningen werken we met het bestand `passwd`, dat zich ook in de `labo3`-directory bevindt.


1. Schrijf in `users.txt` een gesorteerde lijst weg van gebruikers met een UID strikt groter dan 1000 (tip: gebruik hiervoor `awk`).

    ```
    [chichoi@localhost labo3]$ awk -F ':' '$3 > 1000 {print $1}'  passwd | sort > user.txt
    [chichoi@localhost labo3]$ cat users.txt
    roberts
    ryu
    sparrow
    student
    teach
    yoshiro
    ```

2. Tel het aantal gebruikers in `users.txt`

    ```
    [chichoi@localhost labo3]$ cat user.txt | wc -l
    6
    ```

3. Genereer voor elke gebruiker in `users.txt` een nieuw wachtwoord m.h.v. het commando `apg -n AANTAL` en schrijf deze weg in `newpass.txt`. Het aantal gebruikers in `users.txt` wordt berekend in de opdrachtregel.  Tip: gebruik "command substitution," notatie `$(commando)`. Dit zal het gegeven commando uitvoeren en de uitdrukking `$(...)` vervangen door de uitvoer (stdout) ervan.

    ```
    [chichoi@localhost labo3]$ apg -n $(wc -l user.txt) > newpass.txt
    ```

4. Maak een tekstbestand `newusers.txt` met daarin de lijst van gebruikers uit `users.txt` en hun overeenkomstige wachtwoord uit `newpass.txt`, gescheiden door een TAB, vb:

    ```
    [chichoi@localhost labo3]$ paste user.txt newpass.txt > newusers.txt
    
    [chichoi@localhost labo3]$ cat newusers.txt
    roberts hewpopIrb6
    ryu     vicNimEp
    sparrow whowlash4
    student Evcorfoi
    teach   cymgardye
    yoshiro sirgElkont
    ```

5. Converteer `newusers.txt` naar een CSV-bestand `newusers.csv` waar de inhoud van elke kolom omgeven is door dubbele aanhalingstekens en gescheiden door een kommapunt.

    ```
    [chichoi@localhost labo3]$ awk '  {printf("\"%s\";\"%s\"\n", $1, $2)} ' newusers.txt > newusers.csv
    $ cat newusers.csv
    "roberts";"hewpopIrb6"
    "ryu";"vicNimEp"
    "sparrow";"whowlash4"
    "student";"Evcorfoi"
    "teach";"cymgardye"
    "yoshiro";"sirgElkont"
    ```

6. Druk een lijst af van de gebruikers in `passwd` die Bash als shell hebben, samen met hun UID en home-directory. Sorteer op UID.

    ```
    [chichoi@localhost labo3]$ grep :/bin/bash$ passwd | cut -f1,3,6 -d:
    root:0:/root
    vagrant:1000:/home/vagrant
    student:1001:/home/student
    ryu:1002:/home/ryu
    yoshiro:1003:/home/yoshiro
    sparrow:1004:/home/sparrow
    teach:1005:/home/teach
    roberts:1006:/home/roberts
    ```

## Gebruikte bronnen

Vul hier aan welke interessante informatiebronnen je tegengekomen bent.
https://www.gnu.org/software/sed/manual/sed.html
https://www.geeksforgeeks.org/awk-command-unixlinux-examples/
https://vim.fandom.com/wiki/Copy,_cut_and_paste#:~:text=There%20are%20two%20approaches%20to,register%20identified%20by%20the%20character.
