#  M300-Services

## Dokumentation

Einleitung

Hier handelt es sich um eine Dokumentation für die LB02 im Modul 300. Da werde ich meine Arbeitsschritte festhalten und einige Sachen, die ich gelernt habe.

## Einrichtung

Inhaltsverzeichnis

* 01 - GitHub Account
* 02 - Git Client
* 03 - VirtualBox
* 04 - Vagrant
* 05 - Visual Studio Code
* 06 - Fazit / Reflexion
* 07 - Quellenverzeichnis

## 01 - Github Account

Man erstellt als erstes ein Github Account, dieser dient als Cloud-Speicher, von dieser Dokumentation.

Folgende Schritte müssen gemacht werden:

### Account erstellen

1. Auf www.github.com muss ein Account erstellt werden.
2. Nun muss die Email bestätigt werden und meldet sich wieder an.

### Repository erstellen

In der Repository erstellt man ein Readme File um dann hier dokuemntieren zu können.

1. Anmelden unter www.github.com
2. Innerhalb der Willkommens-Seite auf Start a project klicken
3. Unter Repository name einen Name definieren (z.B. M300)
4. Optional: kurze Beschreibung eingeben
5. Radio-Button bei Public belassen
6. Hacken bei Initialize this repository with a README setzen
7. Auf Create repository klicken

### SSH-Key erstellen

1. Terminal Bash öffnen
2. Den Befehl eingeben mit der Emailadresse des Github Accounts:

| $ ssh-keygen -t rsa -b 4096 -C 'DEINE EMAILADRESSE'        |    Regeniert den SSH Key     |
| ------------- |:-------------:|

3. Danach wird ein Key erstellt und man muss mit Enter bestätigen.

4. Nun erstellt man ein Passwort.

### SSH-Key hinzufügen

1. Anmelden unter www.github.com
2. Auf Benutzerkonto klicken (oben rechts) und den Punkt Settings aufrufen
3. Unter den Menübereichen auf der linken Seite zum Abschnitt SSH und GPG keys wechseln
4. Auf New SSH key klicken
5. Im Formular unter Title eine Bezeichnung vergeben (z.B. MB SSH-Key)
6. Den zuvor kopierten Key mit CTRL + V einfügen und auf Add SSH key klicken
7. Der Schlüssel (SSH-Key) sollte nun in der übergeordneten Liste auftauchen

## 02 - Git Client

Jetzt muss der Git Client installiert werden. Dieser ermöglicht uns, Cloud-Repositories zu klonen, zu pullen (herunteraden) oder ein lokales Repository zu pushen (hochladen).

Hierzu müssen folgende Schritte durchgeführt werden:

1. Git Client installieren
2. Konfigurieren des Git Clients

| Befehle      |    Bedeutung    |
| ------------- |:-------------:|
| $ git config --global user.name <username>       |      Konfiguration Username  |
| $ $ git config --global user.email <e-mail>   | Konfiguration Email

3. Konfiguration abgeschlossen

### Repository klonen

1. Terminal öffnen

| Befehle      |    Bedeutung    |
| ------------- |:-------------:|
| $ git clone https://github.com/YangGorgoni/M300/     |      Repository klonen  |
| $ git pull    |      zeigt ob es up to date ist   |
|   $ git status   |     Geänderte Datei(en) werden rot aufgelistet |

### Repository herunteraden

1. Terminal Bash öffnen
2. Ordner im gewünschtenn Verzeichnis erstellen
3. Repository mit SSH klonen:

| Befehle      |    Bedeutung    |
| ------------- |:-------------:|
|  $ git clone git@github.com:YangGorgoni/M300.git    |      Klonen des Respository mit SSH  |

### Repository pushen (hochladen)

1. Terminal Bash öffnen
2. Zum Verzeichnis gehen des repository
3. Dateien dem Upload hinzufügen:

| Befehle      |    Bedeutung    |
| ------------- |:-------------:|
|  $ git add -a.  |      Upload wird "commited" > Kommentar zu Dokumentationszwecken ist dafür notwendig  |

4. Upload commiten:

| Befehle      |    Bedeutung    |
| ------------- |:-------------:|
|   $ git commit -m "Mein Kommentar" |      commiten |

5. Zum Schluss noch pushen:

| Befehle      |    Bedeutung    |
| ------------- |:-------------:|
|    $ git push |      pushen (hochladen) |


## 03 - VirtualBox

 Wie man es schon kennt, muss man eine VM erstellen mit Ubuntu in Virtual Box. Das werde ich nicht dokumentieren, da das nichts neues ist und ich schon weiss wie das funktioniert.

## 04 - Vagrant

Wenn man schon einmal selber die VM's erstellt hat, dann weiss man für mehrere braucht man lange. Für eine schnellere Variante gibt es Vagrant. Mit dem können VM's automatisch erstellt werden mit nur einem kurzen Code.

Im gewünschten Verzeichnis kann man mit einer Zeile, die VM erzeugen:

| Befehle      |    Bedeutung    |
| ------------- |:-------------:|
|  $ vagrant init ubuntu/xenial64 |   Vagrantfile erzeugen |
|  $ vagrant up --provider virtualbox | Virtuelle Maschine erstellen & starten |

## 05 - Visual Studio

Ich habe mich nicht für Visual Studio entschieden, sondern für Atom. Diese wurde mir von einem Kollegen empfohlen. Das ist ein Editor. Dieser wird benutzt, um dort zu dokumentieren, für eine gute Übersicht. Natürich muss es zuerst mit Github verbunden werden.


## Eigene Lernumgebung




## Sicherheitsaspekte sind implementiert
