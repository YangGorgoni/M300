#  M300-Services

## Dokumentation

Einleitung

Hier handelt es sich um eine Dokumentation für die LB02 im Modul 300. Da werde ich meine Arbeitsschritte festhalten und einige Sachen, die ich gelernt habe.

# LB01

## Einrichtung

Inhaltsverzeichnis

* 01 - GitHub Account
* 02 - Git Client
* 03 - VirtualBox
* 04 - Vagrant
* 05 - Visual Studio Code
* 06 - Sicherheitsaspekte sind implementiert
* 07 - Fazit / Reflexion
* 08 - Glossar

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

| Befehl      |    Bedeutung    |
| ------------- |:-------------:|
| $ ssh-keygen -t rsa -b 4096 -C 'DEINE EMAILADRESSE'        |    Regeniert den SSH Key   |


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

 Auf dem Bild sieht man dann auch den Ubuntu Desktop:


![Ubuntu Desktop](https://github.com/YangGorgoni/M300/blob/main/pictures/ubuntudesktp.PNG)


## 04 - Vagrant

Wenn man schon einmal selber die VM's erstellt hat, dann weiss man für mehrere braucht man lange. Für eine schnellere Variante gibt es Vagrant. Mit dem können VM's automatisch erstellt werden mit nur einem kurzen Code.

Im gewünschten Verzeichnis kann man mit einer Zeile, die VM erzeugen:

| Befehle      |    Bedeutung    |
| ------------- |:-------------:|
|  $ vagrant init ubuntu/xenial64 |   Vagrantfile erzeugen |
|  $ vagrant up --provider virtualbox | Virtuelle Maschine erstellen & starten |

Das Vagrantfile kann auch angepasst werden wie folgendermassen:

````
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
  config.vm.synced_folder ".", "/var/www/html"  
  config.vm.provider "virtualbox" do |vb|
  vb.memory = "512"  
    end

  config.vm.provision "shell", inline: <<-SHELL
  sudo apt-get update
  sudo apt-get -y install apache2
  SHELL
end

````
### Netzwerkplan

![Netzplan](https://github.com/YangGorgoni/M300/blob/main/pictures/Netzplan.PNG)

### Befehle Vagrant

````
Vagrant box add [box add]: downloaded Vagrant image local store

Vagrant box remove [box add]: entfernt Vagrant image local store

Vagrant box list: Zeigt downloaded boxes an

vagrant init [box]: initialisiert Vagrantfile

Vagrant up: startet VM's aus Vagrantfile

Vagrant status: Zeigt Status der Vagrant box

Vagrant halt: stopt VM's

Vagrant destroy: zerstört VM's

Vagrant ssh [vmname]: Verbindet per ssh auf VM

vagrant version: zeig Version von Vagrant

vagrant port: Zeigt portmapping zwischen host und gast

````
### GIT Befehle

````
git add -A : Änderungen im aktuellen Verzeichnis zum Zwischenspeicher hinzufügen

git commit : Änderungen auf dem lokalen Git speichern

git push : Lokales Git auf Github synchronisieren

git clone : Github Repo herunterladen

git init : Repo initialisieren

````

### Testing

Apache2

Als erstes wird getestet auf dem Ubuntu Desktop, ob der Apache2 überhaupt aufrufbar ist.

![apache](https://github.com/YangGorgoni/M300/blob/main/pictures/apache.PNG)

#### Testergebnis: Mit Erfolg

Mit Vagrant eine Maschine erzeugt worden:

![vagrant](https://github.com/YangGorgoni/M300/blob/main/pictures/Vagrant.PNG)

#### Testergebnis: Mit Erfolg

## 05 - Visual Studio

Ich habe mich nicht für Visual Studio entschieden, sondern für Atom. Diese wurde mir von einem Kollegen empfohlen. Das ist ein Editor. Dieser wird benutzt, um dort zu dokumentieren, für eine gute Übersicht. Natürich muss es zuerst mit Github verbunden werden.


## 06 -  Sicherheitsaspekte sind implementiert

### Firewall

Eine Firewall ist ein Sicherungssystem, das ein Rechnernetz oder einen einzelnen Computer vor unerwünschten Netzwerkzugriffen schützt und ist weiter gefasst auch ein Teilaspekt eines Sicherheitskonzepts.

Mit einem vagrantfile wurde eine virtuelle Maschine erstellt, die Firewall-Regeln hat.

````
Vagrant.configure("2") do |config|
config.vm.box = "debian/buster64"
config.vm.provider "virtualbox" do |vb|
end
config.vm.provision "shell", inline: <<-SHELL
sudo apt-get install ufw
sudo ufw --force enable
sudo ufw allow 80/tcp
sudo ufw allow from any to any port 22
sudo ufw allow from any to any port 3306
SHELL
end

````

![firewall](https://github.com/YangGorgoni/M300/blob/main/pictures/Firewall.PNG)

### Reverse Proxy

Ein Reverse Proxy ("umgekehrter Proxy") ist eine zusätzliche Schutzmaßnahme, die vor einen oder mehreren Webservern geschaltet werden kann.
Im Gegensatz zu einem Proxy wird die Adressumsetzung in der entgegengesetzten Richtung durchgeführt.
Die Aufgabe des Reverse Proxys ist es Anfragen von Servern stellvertretend anzunehmen und an den entsprechenden Client weiterzuleiten.
Dabei gewährt der Reverse Proxy einem oder mehreren Clients eines externen Netzes den Zugriff auf ein internes Netz.

````
Vagrant.configure("2") do |config|
config.vm.box = "debian/buster64"
config.vm.provider "virtualbox" do |vb|
end
config.vm.provision "shell", inline: <<-SHELL
sudo apt-get install apache2 -y
sudo apt-get install libapache2-mod-proxy-html -y
sudo apt-get install libxml2-dev -y
sudo a2enmod proxy
sudo a2enmod proxy_html
sudo a2enmod proxy_http
sudo systemctl restart apache2
sudo echo "ServerName localhost" >> /etc/apache2/apache2.conf
sudo systemctl restart apache2
sudo touch /etc/apache2/sites-enabled/001-reverseproxy.conf
sudo echo "ProxyRequests Off
    <Proxy *>
        Order deny,allow
        Allow from all
    </Proxy>
    ProxyPass /master http://master
    ProxyPassReverse /master http://master" >> /etc/apache2/sites-enabled/001-reverseproxy.conf
SHELL
end

````

### Benutzer und Rechte

Mit einem Script wurde ein Benutzer, eine Gruppe und bestimmte Berechtigungen auf ein Textfile gesetzt.

````
Vagrant.configure("2") do |config|
config.vm.box = "debian/buster64"
config.vm.provider "virtualbox" do |vb|
end
config.vm.provision "shell", inline: <<-SHELL
sudo useradd yang
sudo groupadd informatik
sudo usermod -aG informatik yang
sudo touch test.txt
sudo chmod 774 test.txt
sudo chown yang test.txt
sudo chgrp informatik test.txt
SHELL
end

````
![Benutzer](https://github.com/YangGorgoni/M300/blob/main/pictures/Benutzer.PNG)

### SSH
Diese drei wichtigen Eigenschaften führten zum Erfolg von ssh:

* Authentifizierung der Gegenstelle, kein Ansprechen falscher Ziele
* Verschlüsselung der Datenübertragung, kein Mithören durch Unbefugte
* Datenintegrität, keine Manipulation der übertragenen Daten

Wem die Authentifizierung über Passwörter trotz der Verschlüsselung zu unsicher ist, der benutzt das Public-Key-Verfahren. Hierbei wird asymmetrische Verschlüsselung genutzt, um den Benutzer zu authentifizieren.


## Vergleich Vorwissen - Wissenszuwachs

Vorher wusste ich so ziemlich gar nichts über diese Themen ausser Virtualbox. Ich wusste wie man ein Ubuntu Server aufsetzt. Ich wusste am Anfang nicht was ein Atom ist. Jetzt weiss ich, dass ist ein Editor, nur besser und übersichtlicher. Wie man ein Vagrantfile gestaltet wusste ich auch nicht. Jetzt weiss ich auch wie man diese erweitern kann.

## Reflexion

Ich hatte Spass diese Aufgaben zu erledigen, da ich offen für neue Sachen bin. Ich habe einiges lernen können, über diese Themen. Vor allem wusste ich nicht was Vagrant ist und jetzt weiss ich was es macht und wie ich ein solches File erzeugen kann. Es ist beeindruckend was das für ein Programm ist. Was ich auch noch gelernt habe ist, was Github überhaupt ist und was ein Markdown ist. Mit dem kann man in Atom eine Dokumentation schreiben und gleichzeitig auf Github hochladen mit dem pushen. Anfangs wusste ich nicht genau wie das geht, nach einer Erklärung wusste ich das dann. Bilder konnte ich mit der Zeit dann auch schon hochladen. Die bestimmten Befehle wie man Tabellen oder Schriften gestalten möchte, habe ich kennengelernt.

## Glossar

|   Wort   |    Bedeutung    |
| ------------- |:-------------:|
|  Linux |   ist ein Open Source Betriebssystem. Die Vorteile von Linux liegen darin, dass jeder den Code einsehen und benutzen kann. So können Sicherheitslücken besser geschlossen werden und es kann viel optimiert werden. |
|  Virtualisierung | soll die Wartung von Arbeitsplätzen oder Servern vereinfachen. Anstelle von Vielen Servern, werden nur weniger eingesetzt. Es wird also weniger Hardware gebraucht. Auf den Servern ist ein Programm für die Virtualisierung installiert. Nun lassen sich auf diesem Server mithilfe der Virtualisierung Virtuele Server, Clients und Netze installieren. |
|  Vagrant |  ist eine Freie Software für das erstellen von Virtuellen Maschinen. Mit Vagrant lassen sich auch einige Arbeitsschritte automatisieren. |
|  Git |  ist eine Freeware welche zur Pensionierung und Veröffentlichung/Verteilung von Programmen gebraucht wird. |


# LB02

In diesem Abschnitt befindet zeige ich auf, was ich alles gelernt habe in der LB02. Es geht um die Themen Container, Docker, Sicherheit.

## Was versteht man genau unter Containerisierung?

Bei der Containerisierung handelt es sich um eine Art Virtualisierung auf Anwendungsebene, bei der mehrere isolierte Userspace-Instanzen auf einem einzelnen Kernel ausgeführt werden können. Diese Instanzen werden Container genannt. Container bieten eine Standardmethode um Anwendungscode, Laufzeitumgebung, Systemwerkzeugen, Systembibliotheken und Konfigurationen in einer Instanz zusammenzufassen. Container teilen sich einen Kernel (Betriebssystem), der auf der Hardware installiert ist.

Hier ein Beispiel, wie das aussieht:

![Containerisierung](https://github.com/YangGorgoni/M300/blob/main/pictures/container.png)

### Welche Vorteile gibt es?

* Performance Bei hohen, konkurrierenden Ressourcenanforderungen ist die Leistung von Anwendungen die aus einer Containerumgebung ausgeführt werden weitaus besser als bei der Ausführung in einer virtuellen Maschine.

* Resourcenbedarf Container benötigen auf dem Server weniger Ressourcen als virtuelle Maschinen und sind normalerweise innerhalb weniger Sekunden gestartet.

* Elastizität Container sind hochelastisch und müssen nicht mit einer bestimmten Menge an Ressourcen ausgestattet werden. Dies bedeutet, dass Container die Ressourcen des Servers effizienter und dynamischer nutzen können.

## Docker

Bei Docker geht es primär um das Verteilen von Anwendungen und Diensten, das sogenannte Deployment. Doch wie wurde das eigentlich früher gemacht? Nehmen wir an, ein Entwickler will seine frisch erstellte .NET-Webapplikation einer Kollegin zum lokalen Testen geben. Ganz früher war das noch so, dass die Kollegin zur Installation eine Anleitung mit Voraussetzungen und ggfs. auch manuelle Skripts bekam. Da stand dann z. B. in der Anleitung, dass Windows als Betriebssystem benötigt wird, dass das .NET Framework in einer bestimmten Version installiert sein muss, dass zur Ausführung eine bestimmte Datenbank benötigt wird usw. Es wird also für die Kollegin ein mühsames und aufwändiges Unterfangen, die Webapplikation lokal zum Laufen zu bekommen.

Docker vereinfacht die Bereitstellung von Anwendungen, weil sich Container, die alle nötigen Pakete enthalten, leicht als Dateien transportieren und installieren lassen. Container gewährleisten die Trennung und Verwaltung der auf einem Rechner genutzten Ressourcen. Das beinhaltet laut Aussage der Entwickler: Code, Laufzeitmodul, Systemwerkzeuge, Systembibliotheken – alles was auf einem Rechner installiert werden kann.

Vorteile der Containerisierung mit Docker Die Containerisierung mit der frei verfügbaren Software bietet zahlreiche Vorteile. Sie benötigt weniger Ressourcen als virtuelle Maschinen, schottet die Anwendungen aber dennoch sicher untereinander und vom Host-System ab. Ein Container lässt sich in Form einer Image-Datei einfach auf andere Systeme übertragen. Es ist keine neue Installation der Anwendung und ihrer Laufzeitumgebung notwendig.

### Vorteile

* die gute Skalierbarkeit durch die Nutzung vieler weiterer Container,
* die einfache Verwaltung vieler Container über Orchestrierungs-Tools wie Kubernetes,
* das schnelle Starten von Containern

![Docker](https://github.com/YangGorgoni/M300/blob/main/pictures/docker.png)

Mein Wissen: Ich habe noch nie was von Docker oder Containerisierung gehört. Mit Inputs von meinem Lehrer habe ich verstanden, was das ungefähr ist. Ich konnte mir jedoch aber noch nicht richtig vorstellen, wie alles funktioniert. Ich habe angefangen dies umzusetzen und konnte einiges lernen. Jetzt ist mein Verständnis dafür mehr da.

### Bestehende Container als Backend, Desktop-App als Frontend  einsetzen

1. Als erstes muss man auf den eigenen Server über VPN zugreifen können über CMD.
2. Korrektes Passwort eingeben.
3. Man erstellt ein Dockerfile.
4. Dort drin steht 'FROM httpd'
5. Das Image bilden mit dem Befehl 'docker build -t webserver'
6. schauen ob es erstellt ist 'docker images'
7. Image starten 'docker run -dit --name webserver -p 5050:80 webserver' NICHT 8080, da der schon vergeben ist und das zu Konflikten kommen kann.

### Bestehende Docker-Container kombinieren

1. Man soll sich sicher sein, dass man einen SQL Container am laufen hat, dass osTicket es zum speichern seiner  Daten verwenden kann.

````
docker run --name osticket_mysql -d -e MYSQL_ROOT_PASSWORD=secret \
 -e MYSQL_USER=osticket -e MYSQL_PASSWORD=secret -e MYSQL_DATABASE=osticket mariadb
````
Nun bringen wir das image zum laufen und linken den MySQL Container:
````
docker run --name osticket -d --link osticket_mysql:mysql -p 3030:80 osticket/osticket
````
### Volumes zur persistenten Datenablage eingerichtet

Verwenden Sie ein schreibgeschütztes Volume, was zur Sicherheitsmassnahme dient.

1. Den Befehl eingeben, dass Volume schreibgeschützt bereitgestellt wird:
````
$ docker run -d \
  --name=nginxtest \
  --mount source=nginx-vol,destination=/usr/share/nginx/html,readonly \
  nginx:latest
````
2. Um es zu überprüfen schaut man es sich mit diesem Befehl an:
````
docker inspect nginxtest
````
3. Da wo Mounts steht sollten diese Einstellungen vorhanden sein - RW muss auf false eingestellt sein:

````
"Mounts": [
    {
        "Type": "volume",
        "Name": "nginx-vol",
        "Source": "/var/lib/docker/volumes/nginx-vol/_data",
        "Destination": "/usr/share/nginx/html",
        "Driver": "local",
        "Mode": "",
        "RW": false,
        "Propagation": ""
    }
],
````
4. Man kann auch noch das Volumen überprüfen, dass ich bereitgestellt habe:
````
docker volume inspect nginx-vol
````
![Volume](https://github.com/YangGorgoni/M300/blob/main/pictures/überprüfung-volumen.PNG)

### Sichern von einem Datenvolumen

1. Erstellen von einem neuen Container z.B den Namen dbstore:
````
$ docker run -v /dbdata --name dbstore ubuntu /bin/bash
````
2. Im nächsten Befehl wird ein neuer Container gestartet und das Volume dbstore angehängt, dann mountet man ein lokales Hostverzeichnis als /backup und Inhalt dbdata Volume wird an eine backup.tar Datei im backup Verzeichnis.
````
$ docker run --rm --volumes-from dbstore -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
````
3. Wenn der Befehl abgeschlossen ist und der Container stoppt, wird eine Sicherungskopie unseres dbdataVolumes erstellt.

### Monitoring mit cAdvisor

1. Mit dem Befehl kann man dieses Tool starten und man sieht dann auch schon das Ganze Monitoring.
````
docker run -d --name cadvisor -v /:/rootfs:ro -v /var/run:/var/run:rw -v /sys:/sys:ro -v /var/lib/docker/:/var/lib/docker:ro -p 2020:8080 google/cadvisor:latest
````
![cadvisor](https://github.com/YangGorgoni/M300/blob/main/pictures/monitoring.PNG)

## Testfälle

Zugriff testen über den Webbrowser http://IPVONSERVER:5050

![Apache](https://github.com/YangGorgoni/M300/blob/main/pictures/apache.PNG)

Testergebnis: erfolgreich

Funktioniert Whalesay?

![whalesay](https://github.com/YangGorgoni/M300/blob/main/pictures/whalesay.PNG)

Testergebnis: erfolgreich

Zugriff testen auf das Ticketsystem über http://10.2.45.17:3030:

![ticket](https://github.com/YangGorgoni/M300/blob/main/pictures/ticket.PNG)

Testergebnis: erfolgreich

Monitoring Zugriff:
![Monitoring](https://github.com/YangGorgoni/M300/blob/main/pictures/monitoring.PNG)

Testergebnis: erfolgreich

## Netzwerkplan

![netplan](https://github.com/YangGorgoni/M300/blob/main/pictures/Netplan.PNG)


## Befehle

|   Befehle   |    Bedeutung    |
| ------------- |:-------------:|
|  docker version |  zeigt die Version an |
|  docker run -dit --name imagename | startet das Image |
|  docker images|  listet die images auf |
|  docker ps |  zeigt aktive und beendete Containers an |
|  docker build -t NAME |  bildet ein image |
|  docker stop ID |  stoppt das image |
|  docker rm ID |  löscht das image |
|  docker rm ID --force |  löscht das image zwingend, auch wenn gestartet |

## Sicherheiten

Das Überwachen und Protokollieren von laufenden Containern ist sehr wichtig. Be den Microservices ist es wegen der höheren Zahl von Rechnern noch wichtiger.

### Logging

Die Logs können über den Befehl ````docker logs```` abgerufen werden. Es gibt mehrere Werte, die man über das Argument von ````docker````auswählen kann:

* json-file (Das Standard-Logging)

Ausgaben abholen:
````
$ docker run --name logtest ubuntu bash -c 'echo "stdout"; echo "stderr" >>2'
$ docker logs logtest
$ docker rm logtest
````
Laufende Ausgaben:
````
$ docker run -d --name streamtest ubuntu bash -c 'while true; do echo "tick"; sleep 1; done;'
$ docker logs streamtest
$ docker logs streamtest | wc -l
$ docker rm streamtest
````

* syslog (Der Syslog-Treiber des Hosts)

Protokollierung in das System-Log des Hosts:
````
$ docker run -d --log-driver=syslog ubuntu bash -c 'i=0; while true; do i=$((i+1)); echo "docker $i"; sleep 1; done;'
$ tail -f /var/log/syslog
````

* none (Schaltet die Protokollierung ab)

### Aspekte
An was für Sicherheitsprobleme soll man denken?

Kernel Exploits:

Sollte ein Container eine Kernel Panic verursachen, zieht das den ganzen Host mit herunter. In VMs ist die Situation viel besser – ein Angreifer müsste einen Angriff sowohl durch den VM-Kernel als auch den Hypervisor leiten, bevor er an den Host-Kernel kommt.

Denial-of-Service-(DoS-)Angriffe:

Kann ein Container den Zugriff auf bestimmte Ressourcen ganz für sich beanspruchen – auch so etwas wie den Speicher oder esoterischere Ressourcen wie User IDs (UIDs) –, kann er die anderen Container auf dem Host verhungern lassen.

Container-Breakouts:

Ein Angreifer, der Zugriff auf einen Container erhält, sollte nicht dazu in der Lage sein, auf andere Container oder den Host zuzugreifen. Da die Benutzer nicht über Namensräume getrennt sind, bekommen alle Prozesse, die aus dem Container ausbrechen, auf dem Host die gleichen Privilegien wie im Container – ist man im Container root, so wird man auch root auf dem Host sein.

Vergiftete Images:

Man sollte sich sicher sein, dass die Images nicht manipuliert wurden, sondern sicher sind.

Verratene Geheimnisse:

Greift ein Container auf eine Datenbank oder einen Service zu, muss er sehr wahrscheinlich ein Geheimnis wie einen API-Schlüssel oder Benutzernamen und Passwort kennen.

### Least Privilege

Jeder Prozess und Container sollte nur mit so viel Zugriffsrechten und Ressourcen laufen, wie er gerade braucht, um seine Aufgaben zu erfüllen.

Möglichkeiten:

* Prozesse in Containern nicht als root laufen
* Dateisysteme schreibgeschützt einsetzen
* Kernel-Aufrufe, die Container ausführen kann, einschränken
* Ressoucen begrenzen, um DoS-Angriffe zu verhindern

### Container absichern

Hier einige Absicherungsmethoden:

* Container laufen in VM
* Der Reverse-Proxy ist der einzige Container, der Port nach aussen freigibt
* Alle Images laufen nicht als root
* Images werden über eigenen Hash runtergeladen
* Anwendung wird überwacht und es wird Alarm ausgelöst
* Aktuelle Software

### Weitere Sicherheitstipps

* User setzen
````
$ RUN groupadd -r user_grp && useradd -r -g user_grp user
$ USER user
````
* Netzwerkzugriff beschränken
* setuid/setgid-Binaries entfernen
* Speicher begrenzen
````
$ docker run -m 128m --memory-swap 128m amouat/stress stress --vm 1 --vm-bytes 127m -t 5s
````

* CPU beschränken
````
$ docker run -d --name load3 -c 512 amouat/stress
````
* Neustarts begrenzen
````
$ docker run -d --restart=on-failure:10 my-flaky-image
````
* Zugriffe aus Dateisysteme begrenzen
````
$ docker run --read-only ubuntu touch x
````
* Capabilities einschränken
````
$ docker run --cap-drop all --cap-add CHOWN ubuntu chown 100 /tmp
````
* Ressourcenbeschränkungen anwenden
````
$ docker run --ulimit cpu=12:14 amouat/stress stress --cpu 1
````


## Kubernetes

Kubernetes ist ein Open-Source-System zur Automatisierung der Bereitstellung, Skalierung und Verwaltung von Container-Anwendungen.

### Merkmale

* Immutable (Unveränderlich) statt Mutable.
* Deklarative statt Imperative (Ausführen von Anweisungen) Konfiguration.
* Selbstheilende Systeme - Neustart bei Absturz.
* Entkoppelte APIs – LoadBalancer / Ingress (Reverse Proxy).
* Skalieren der Services durch Änderung der Deklaration.
* Anwendungsorientiertes statt Technik (z.B. Route 53 bis AWS) Denken.
* Abstraktion der Infrastruktur statt in Rechnern Denken.

### Objekte

* Pod - repräsentiert eine Gruppe von Anwendungs-Containern und Volumes, die in der gleichen Ausführungsumgebung laufen
* ReplicaSet - bestimmen wieviele Exemplare eines Pods laufen und stellen sicher, dass die angeforderte Menge auch verfügbar ist
* Deployment - erweitern ReplicaSets um deklarative Updates
* Service - steuert den Zugriff auf einen Pod
* Ingress - ermöglicht den Zugriff auf einen Service über einen URL

### Kubernetes Cluster

Bei einem Cluster wird ein Kubernetes Master und mehrere Worker erzeugt.

Voraussetzungen sind genügend RAM für alle VM's.

Die wichtigsten Konfigurationen:

````
master:
  count: 1
  cpus: 2
  memory: 5120
worker:
  count: 2
````
Es wird ein Master und zwei Worker Nodes erstellt. Der Master und die Worker Nodes werden während der Installation automatisch miteinander gejoint.

````
use_dhcp: false  
# Fixe IP Adressen mit welchen die IP fuer Master und Worker beginnen sollen
ip:
  master:   192.168.137.100
  worker:   192.168.137.111
# Netzwerk "private_network" fuer Host-only Netzwerk, "public_network" fuer Bridged Netzwerke
net:
  network_type: private_network
````
Die restlichen Standardeinstellungen wie Host-only Netzwerk mit fixen IP-Adressen kann 1:1 verwendet werden.

## Vergleich Wissenszuwachs

Mein Wissen von jetzt zu vorher hat sich massiv  gestiegen. Ich wusste vorher gar nichts über diese Themen Container, Docker etc. Jetzt kann ich mir darunter was vorstellen und kenne auch die wichtigsten Befehle für docker.

## Reflexion

In dieser Lb02 Übung, habe ich einiges lernen können. Ich muss zugeben anfangs war mein Verständnis nicht so da, weil es ein bisschen kompliziert war. Mit einigen Übungen habe ich dann das Ganze mehr verstanden. Ich bin zwar noch kein Profi, aber ich kann einiges mitnehmen. Die Dokumentationen waren für mich nicht so hilfreich. Im Kompetenzraster wusste ich am Anfang nicht genau was erwartet wird von mir. Ich bin die einzelnen Punkte dann durchgegangen und habe immer etwas dazu probiert. Ich finde es war anpruchsvoller als die LB01.
