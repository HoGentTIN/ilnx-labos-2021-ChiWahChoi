# Labo 2: Linux leren kennen

## Hulp zoeken

1. Hoe vraag je op de command-line documentatie op voor het *commando* `passwd`?

    ```
    [chichoi@localhost ~]$ man passwd
    PASSWD(1)                       User utilities                       PASSWD(1)

    NAME
       passwd - update user's authentication tokens

    SYNOPSIS
       passwd  [-k]  [-l]  [-u  [-f]]  [-d] [-e] [-n mindays] [-x maxdays] [-w

       warndays] [-i inactivedays] [-S] [--stdin] [-?] [--usage] [username]

    DESCRIPTION
       The passwd utility is used to update user's authentication token(s).
       [...]
    ```

2. Hoe vraag je documentatie op voor het *configuratiebestand* `/etc/passwd`?

    ```
    [chichoi@localhost ~]$ man 5 passwd
    PASSWD(5)                  Linux Programmer's Manual                 PASSWD(5)
    
    NAME
       passwd - password file

    DESCRIPTION
       The  /etc/passwd file is a text file that describes user login accounts
       for the system.  It should have read permission allowed for  all  users
       (many  utilities,  like ls(1) use it to map user IDs to usernames), but
       write access only for the superuser.
       [...]
    ```

3. Hoe vraag je een lijst op van alle documentatie die de string `passwd` bevat?

    ```
    [chichoi@localhost ~]$ apropos passwd OF man -k passwd
    chgpasswd (8)        - update group passwords in batch mode
    chpasswd (8)         - update passwords in batch mode
    fgetpwent_r (3)      - get passwd file entry reentrantly
    getpwent_r (3)       - get passwd file entry reentrantly
    gpasswd (1)          - administer /etc/group and /etc/gshado
    grub2-mkpasswd-pbkdf2 (1) - Generate a PBKDF2 password hash.
    htpasswd (1)         - Manage user files for basic authentication
    lpasswd (1)          - Change group or user password
    mkpasswd (1)         - Overfeatured front end to crypt(3)
    openssl-passwd (1ssl) - compute password hashes
    pam_localuser (8)    - require users to be listed in /etc/passwd
    pam_passwdqc (8)     - Password quality-control PAM module
    passwd (1)           - update user's authentication tokens
    passwd (5)           - password file
    passwd2des (3)       - RFS password encryption
    passwdqc.conf (5)    - libpasswdqc configuration file
    pwhistory_helper (8) - Helper binary that transfers password hashes from pass...
    saslpasswd2 (8)      - set a user's sasl password
    smbpasswd (5)        - The Samba encrypted password file
    sslpasswd (1ssl)     - compute password hashes
    vncpasswd (1)        - change the VNC password
    ```

## Werken op de command-line

1. Wat is de huidige datum en uur?

    ```
    [chichoi@localhost ~]$ date +"%D %T"
    11/05/20 17:55:28
    ```

2. Wat is de huidige directory?

    ```
    [chichoi@localhost ~]$ pwd
    /home/chichoi
    ```

3. Toon de inhoud van de huidige directory. De uitvoer zou er ongeveer zo moeten uit zien:

    ```
    [chichoi@localhost ~]$ ls
    Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
    ```

4. Toon de inhoud van de huidige directory, maar toon voor elk bestand meer informatie en ook "verborgen" bestanden.

    ```
    [chichoi@localhost ~]$ ls -al
    total 96
    drwx------. 14 student student 4096 Sep 24 09:14 .
    drwxr-xr-x.  3 root    root    4096 Sep 20 13:46 ..
    -rw-------.  1 student student  146 Sep 20 14:06 .bash_history
    -rw-r--r--.  1 student student   18 Mar 11  2013 .bash_logout
    -rw-r--r--.  1 student student  193 Mar 11  2013 .bash_profile
    -rw-r--r--.  1 student student  124 Mar 11  2013 .bashrc
    drwx------.  8 student student 4096 Sep 20 13:54 .cache
    drwxr-xr-x. 16 student student 4096 Sep 20 13:55 .config
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Desktop
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Documents
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Downloads
    [...]
    ```

5. Toon de inhoud van de hoofddirectory van het Linux-systeem, ook vaak de root-directory genoemd. Geef een uitgebreide listing zoals in de vorige vraag, maar *zonder* verborgen bestanden.

    ```
    [chichoi@localhost ~]$ ls -l /
    total 64
    lrwxrwxrwx.   1 root root     7 Jan 28  2020 bin -> usr/bin
    dr-xr-xr-x.   7 root root  4096 Sep 30 12:06 boot
    drwxr-xr-x.  21 root root  3980 Nov  5 13:57 dev
    drwxr-xr-x. 147 root root 12288 Nov  5 15:22 etc
    drwxr-xr-x.   4 root root  4096 Sep 23 11:49 home
    lrwxrwxrwx.   1 root root     7 Jan 28  2020 lib -> usr/lib
    lrwxrwxrwx.   1 root root     9 Jan 28  2020 lib64 -> usr/lib64
    drwx------.   2 root root 16384 Apr 23  2020 lost+found
    drwxr-xr-x.   2 root root  4096 Jan 28  2020 media
    drwxr-xr-x.   2 root root  4096 Jan 28  2020 mnt
    drwxr-xr-x.   2 root root  4096 Jan 28  2020 opt
    dr-xr-xr-x. 300 root root     0 Nov  5 13:57 proc
    dr-xr-x---.   4 root root  4096 Nov  5 15:21 root
    drwxr-xr-x.  48 root root  1320 Nov  5 15:24 run
    lrwxrwxrwx.   1 root root     8 Jan 28  2020 sbin -> usr/sbin
    drwxr-xr-x.   2 root root  4096 Sep 30 12:04 srv
    dr-xr-xr-x.  13 root root     0 Nov  5 13:57 sys
    drwxrwxrwt.  19 root root   460 Nov  5 17:22 tmp
    drwxr-xr-x.  12 root root  4096 Apr 23  2020 usr
    drwxr-xr-x.  22 root root  4096 Apr 23  2020 var
    -rw-------.   1 root root     0 Sep 30 10:38 VBox.log
    ```

6. Wat betekenen volgende elementen van de uitvoer hierboven?
    - 1e kolom (bv. `drwxr-xr-x.`): bestandpermissies
    - 2e kolom (getal): aantal hard links
    - 3e kolom (bv. `root`, `student`): bestandseigenaar
    - 4e kolom (bv. `root`): gebruikersgroep
    - 5e kolom (getal): bestandsgrootte in bytes
    - 6e - 8e kolom (datum): datum van de laatste wijziging
    - de aanduiding `->` (bv. `bin -> usr/bin`): symbolische link
7. Hoe kan je commando's die je voordien uitgevoerd hebt terug ophalen (de "commandogeschiedenis")?

    ```
    [chichoi@localhost ~]$ history
    1  man hier
    2  man builtins
    3  man 7 glo
    4  man passwd
    5  man -k passwd
    6  q
    7  pwd
    ```

## De plaats van bestanden op een Linux-systeem

Vul de tabel hieronder aan. In de linkerkolom vind je de namen van een directory, in de rechter het soort bestanden dat er in thuis hoort.

| Directory                         | Inhoud                                                  |
| :---                              | :---                                                    |
| `/bin`, `/usr/bin`                | Uitvoerbare bestanden                                   |
| `/sbin`, `/usr/sbin`              | Uitvoerbare bestanden voor systeembeheertaken           |
| `/var`                            | Variabele data                                          |
| `/tmp`                            | Tijdelijke bestanden                                    |
| `/opt`, `/usr/local`              | Software die geïnstalleerd werd buiten de packetmanager |
| `/root`                           | Home-directory van de `root` gebruiker                  |
| `/home/student`                   | Home-directory van de gebruiker `student`               |
| `/usr/share/man`                  | De inhoud van de man-pages                              |
| `/usr/share/dat`                  | Andere documentatie                                     |
| `/lib`, `/usr/lib`, `lib64`, enz. | Gedeelde bibliotheken                                   |
| `/run/media/student               | De inhoud van de installatie-cd voor Guest Additions(*) |
| `/dev`                            | Apparaatbestande                                        |
| `/proc`                           | Kernel-informatie                                       |
| `/etc`                            | Systeemconfiguratiebestanden                            |

(*) Je kan het insteken van de cd simuleren in het VirtualBox-venster van je VM in het menu "Devices" > "Insert Guest Additions CD image..." (of het Nederlandstalige equivalent).


## Werken met bestanden en directories

Om het verschil tussen een bestand en directory te verduidelijken, wordt in wat volgt de naam van een directory telkens afgesloten met “/”.

### Directories

Open eerst een terminalvenster, start de oefening vanuit je eigen home-directory. Ga enkel naar een andere directory als dat expliciet gevraagd wordt. Geef telkens de gevraagde commando's niet alleen om de taak uit te voeren, maar ook om te testen of dit correct gebeurd is.

In deze oefening leer je onderscheid maken tussen *relatieve* en *absolute paden*. Een *absoluut* pad begint altijd met een `/`, wat overeenkomt met de root-directory. Een *relatief* pad geldt vanaf de huidige directory.

1. Blijf in je home-directory en maak van hieruit een directory `tijdelijk/` aan onder `/tmp/`

    ```
    [chichoi@localhost ~]$ mkdir /tmp/tijdelijk
    UITVOER: /
    ```

2. Verwijder deze directory meteen

    ```
    [chichoi@localhost ~]$ rmdir /tmp/tijdelijk
    UITVOER: /
    ```

3. Maak onder je home-directory een submap aan met de naam `linux/`

    ```
    [chichoi@localhost ~]$ mkdir linux
    UITVOER: /
    ```

4. Ga naar deze directory

    ```
    [chichoi@localhost ~]$ cd linux/
    UITVOER: /
    ```

5. Maak met één commando de subdirectory `a/b/` aan onder `linux/`. Als je nadien het commando `tree` geeft, moet je de gegeven uitvoer zien.

    ```
    [chichoi@localhost linux]$ mkdir -p a/b
    UITVOER: /
    
    [chichoi@localhost linux]$ tree
    .
    └── a
        └── b
    2 directories, 0 files
    ```

6. Verwijder directory `b/` en daarna `a/` (in twee commando's)

    ```
    [chichoi@localhost linux]$ rmdir a/b
    UITVOER: /
    [chichoi@localhost linux]$ rmdir a
    UITVOER: /
    ```

7. Maak met één commando deze directorystructuur aan.

    ```
    [chichoi@localhost linux]$ mkdir -p c/{d,e}
    UITVOER: /
    
    [chichoi@localhost linux]$ tree
    .
    └── c
        ├── d
        └── e
    3 directories, 0 files
    ```

8. Verwijder in één commando de directory `c/` en alle onderliggende

    ```
    [chichoi@localhost linux]$ rm -r c
    UITVOER: /
    ```

9. Maak met één commando deze directorystructuur aan. Het is de bedoeling de opdrachtregel zo kort mogelijk te maken, dus niet alle directories apart opgeven!

    ```
    [chichoi@localhost linux] $ mkdir -p f/{g,h}/i
    UITVOER: /
    
    [chichoi@localhost linux] $ tree
    .
    └── f
        ├── g
        │   └── i
        └── h
            └── i

    5 directories, 0 files
    ```

Behoud deze directorystructuur voor de volgende oefeningen over bestanden.

### Bestanden

1. Maak een leeg bestand aan met de naam `file1`

    ```
    [chichoi@localhost linux]$ touch file1
    UITVOER: /
    ```

2. Maak een *verborgen* bestand aan met de naam `hidden`. Verborgen betekent dat je het niet kan zien met een "gewone" `ls`, maar wel met de gepaste optie.

    ```
    [chichoi@localhost linux]$ touch .hidden
    UITVOER: /
    ```

3. Tik volgend commando in, leg uit wat er hier precies gebeurt, wat het effect is.

    ```
    [chichoi@localhost linux]$ echo hello world > file2
    ```

    **Antwoord: De output van echo werd weggeschreven naar file2.** 

4. Toon de inhoud van `file2`

    ```
    [chichoi@localhost linux]$ cat file2
    Hello world
    ```

5. Kopieer `file1` naar een nieuw bestand `file3` in de huidige directory

    ```
    [chichoi@localhost linux]$ cp file1 file3
    UITVOER: /
    ```

6. Kopieer `file1` naar de directory `f/` (die zou je nog moeten hebben van vorige oefening)

    ```
    [chichoi@localhost linux]$ cp file1 f/
    UITVOER: /
    ```

7. Kopieer `file1` en file2 in één keer naar `f/g/`. Je zou de gegeven situatie moeten krijgen.

    ```
    [chichoi@localhost linux]$ cp {file1,file2} f/g/
    UITVOER: /
    
    [chichoi@localhost linux]$ tree
    .
    ├── f
    │   ├── file1
    │   ├── g
    │   │   ├── file1
    │   │   ├── file2
    │   │   └── i
    │   └── h
    │       └── i
    ├── file1
    ├── file2
    └── file3
    ```

8. *Hernoem* `file3` naar `file4`

    ```
    [chichoi@localhost linux]$ mv file3 file4
    UITVOER: /
    ```

9. Verplaats `file2` naar directory `f/`

    ```
    [chichoi@localhost linux]$ mv file2 f/
    UITVOER: /
    ```

10. Verplaats `file1` en `file4` in één keer naar `f/h/`. Je zou de gegeven situatie moeten krijgen.

    ```
    [chichoi@localhost linux]$ mv {file1,file4} f/h/
    UITVOER: /
    
    [chichoi@localhost linux]$ tree
    .
    └── f
        ├── file1
        ├── file2
        ├── g
        │   ├── file1
        │   ├── file2
        │   └── i
        └── h
            ├── file1
            ├── file4
            └── i

    5 directories, 6 files
    ```

11. Kopieer `f/h/`, inclusief de inhoud, naar een nieuwe directory `f/j/`

    ```
    [chichoi@localhost linux]$ cp -r f/h/ f/j/
    UITVOER: /
    ```

### Pathname expansion (of *file globbing*)

Creëer in de directory `linux/` een aantal lege bestanden met de naam `filea` t/m `filed`, `file1` t/m `file9` en `file10` t/m `file19`. Hier is een trucje om dat snel te doen:

```
[student@localhost ~/linux] $ touch filea fileb filec filed
[student@localhost ~/linux] $ for i in {1..19}; do touch "file${i}"; done 
[student@localhost ~/linux] $ ls 
f       file11  file14  file17  file2  file5  file8  fileb 
file1   file12  file15  file18  file3  file6  file9  filec 
file10  file13  file16  file19  file4  file7  filea  filed 
```

Toon met `ls` telkens de gevraagde bestanden, niet meer en niet minder.

1. Alle bestanden die beginnen met `file`

    ```
    [chichoi@localhost linux]$ ls file*
    file1   file11  file13  file15  file17  file19  file3  file5  file7  file9  fileb  filed
    file10  file12  file14  file16  file18  file2   file4  file6  file8  filea  filec
    ```

2. Alle bestanden die beginnen met `file`, gevolgd door één letterteken (cijfer of letter)

    ```
    [chichoi@localhost linux]$ ls file[a-z0-9]
    file1  file2  file3  file4  file5  file6  file7  file8  file9  filea  fileb  filec  filed
    ```

3. Alle bestanden die beginnen met `file`, gevolgd door één letter, maar geen cijfer

    ```
    [chichoi@localhost linux]$ ls file[a-z]
    filea  fileb  filec  filed
    ```

4. Alle bestanden die beginnen met `file`, gevolgd door één cijfer, maar geen letter

    ```
    [chichoi@localhost linux]$ ls file[0-9]
    file1  file2  file3  file4  file5  file6  file7  file8  file9
    ```

5. De bestanden `file12` t/m `file16`

    ```
    [chichoi@localhost linux]$ ls file1[2-6]
    file12  file13  file14  file15  file16
    ```

6. Bestandern die beginnen met `file`, *niet* gevolgd door een `1`

    ```
    [chichoi@localhost linux]$ ls file[!1]
    file2  file3  file4  file5  file6  file7  file8  file9  filea  fileb  filec  filed
    ```

### Links

Maak in de directory `linux/` twee tekstbestanden aan, met naam `tekst1a` en `tekst2a`. Beide hebben als inhoud “Dit is bestand tekst1” en “Dit is bestand tekst2”, respectievelijk.

1. Voor het volgende commando uit en geef de uitvoer:

    ```
    [chichoi@localhost linux]$ ls -l tekst*
    -rw-rw-r--. 1 chichoi chichoi 22 Nov  5 19:02 tekst1a
    -rw-rw-r--. 1 chichoi chichoi 22 Nov  5 19:03 tekst2a
    ```

2. Maak een *harde link* aan met naam `tekst1b` die verwijst naar bestand `tekst1a`

    ```
    [chichoi@localhost linux]$ ln tekst1a tekst1b
    UITVOER: /
    ```

3. Maak een *symbolische link* aan met naam `tekst2b` die verwijst naar bestand `tekst2a`

    ```
    [chichoi@localhost linux]$ ln -s tekst2a tekst2b
    UITVOER: /
    ```
4. Voor het volgende commando uit en geef de uitvoer:

    ```
    [chichoi@localhost linux]$ ls -l tekst*
    -rw-rw-r--. 2 chichoi chichoi 22 Nov  5 19:02 tekst1a
    -rw-rw-r--. 2 chichoi chichoi 22 Nov  5 19:02 tekst1
    -rw-rw-r--. 1 chichoi chichoi 22 Nov  5 19:03 tekst2a
    lrwxrwxrwx. 1 chichoi chichoi  7 Nov  5 19:09 tekst2b -> tekst2a
    ```

5. Hoe zie je aan de uitvoer van `ls` dat `tekst1b` een harde link is en `tekst2b` een symbolische? Tip: Vergelijk met de uitvoer uit vraag 1!

    **Antwoord**: De aanduiding "->" bij de laatste kolom (tekst2b -> tekst2a) duidt een symbolische link aan.

6. Verwijder de oorspronkelijke bestanden, `tekst1a` en `tekst2a`. Maak het commando zo kort mogelijk!

    ```
    [chichoi@localhost linux]$ rm tekst[1-2]a
    UITVOER: /
    ```

7. Toon opnieuw de uitvoer van `ls -l tekst*`, en bekijk de inhoud van `tekst1b` en `tekst2b`. Wat valt je op?

    ```
    [chichoi@localhost linux]$ ls -l tekst*
    -rw-rw-r--. 1 chichoi chichoi 22 Nov  5 19:02 tekst1b
    lrwxrwxrwx. 1 chichoi chichoi  7 Nov  5 19:09 tekst2b -> tekst2a
    ```

    **Antwoord**: Tekst2b staat in het rood en tekst2a staat rood gemarkeerd. Waarschijnlijk omdat de symbolische link het bestand niet kan vinden waaraan het gelinkt is.

### Bestanden archiveren

1. Creëer in je home-directory een archief `linux.tar.bz2` van de directory `linux/` en alle inhoud.

    ```
    [chichoi@localhost ~]$ tar cjf linux.tar.bz2 linux/
    UITVOER: /
    ```

2. Verwijder nu volledig de directory `linux/`

    ```
    [chichoi@localhost ~]$ rm -r linux
    UITVOER
    ```

3. Toon de inhoud van het archief zonder opnieuw uit te pakken

    ```
    [chichoi@localhost ~]$ tar tjf linux.tar.bz2 
    linux/
    linux/file4
    linux/filec
    linux/file3
    linux/file16
    linux/f/
    linux/f/g/
    linux/f/g/i/
    linux/f/g/file2
    linux/f/g/file1
    linux/f/j/
    linux/f/j/file4
    linux/f/j/i/
    [...]
    ```

4. Pak het archief opnieuw uit in je home-directory.

    ```
    [chichoi@localhost ~]$ tar xjf linux.tar.bz2 
    UITVOER: /
    ```

