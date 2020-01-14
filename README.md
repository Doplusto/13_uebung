
_Übungsaufgabe zur Veranstaltung [IT
Systeme](https://hsro-wif-it.github.io) im [Bachelorstudiengang
Wirtschaftsinformatik](https://www.th-rosenheim.de/technik/informatik-mathematik/wirtschaftsinformatik-bachelor/) an der [Hochschule Rosenheim](http://www.th-rosenheim.de)._

# 13 - Docker und Cloud

Diese Übung behandelt speziell das Thema _Amdahl's Law_, _Virtualisierung_ und _Docker_.

> Note: **Diesmal gibt es _teilweise eine_ Musterlösung!**

## Aufgabe 1: Amdahl's Law


### a)

Um welchen Faktor S (overall speedup) wird ein Programm schneller, wenn Sie 10% des Programms (paralleler Anteil) 90 mal (Prozessor N=90) schneller machen?

### b)
Um welchen Faktor S (overall speedup) wird ein Programm schneller, wenn 90% des Programms (paralleler Anteil) 10 mal (Prozessor N=10) schneller wird?

### c)
Ein bestimmtes Programm hat den in der Abbildung gezeigten Ablauf. Dabei stellt jedes Quadrat eine unteilbare Aufgabe
dar, die grau hinterlegten Quadrate stehen für nicht parallisierbare Aufgaben, die anderen sind parallelisierbar. Zur
Vereinfachung nehmen wir an, dass eine solche Aufgabe auf einem Prozessor exakt eine Zeiteinheit benötigt.

![Beispiel](./img/amdahl.png)

Bestimmen Sie mit Hilfe von Amdahl’s Law:
1. den parallelisierbaren Anteil des Programms,
2. den maximalen Speedup für die Prozessoranzahlen p = ∞, p = 5, p = 4, p = 3 und p = 2.

Kann der in 2. berechnete Speedup tatsächlich erreicht werden? Begründen Sie Ihre Aussage

## Aufgabe 2: Docker Installation

Verwenden Sie in dieser Übung das virtuelle Image (Linux), das Sie in der letzten Woche aufgesetzt haben.

Wenn Sie Linux auf ihrem Notebook verwenden, können Sie diese Übung auch auf ihrem Notebook durchführen. Sonst bitte die VM verwenden.

Warum? 
1. Wir werden mit Docker arbeiten und wollen nicht die ganze Zeit Images durch die Gegend schieben (Hochschulnetz).
2. Sie müllen sich ihren Windows-Rechner nicht mit Docker zu!

> Denken Sie daran, dass Sie weiterhin in ihrer Ressourcegruppe arbeiten!

1. Gehen Sie zum [Azure Portal](http://portal.azure.com)
2. Löschen Sie zunächst die VM, die Sie letzte Woche angelegt haben, auf der Windows als Gastsystem läuft! **Löschen Sie nicht das Linux VM Image!**
3. Starten Sie ihre Linux-VM 
4. Verbinden Sie sich entweder via ssh mit ihrer
5. Installieren Sie auf der VM Docker, in dem Sie folgende Schritte ausführen. 

Befehle auf der VM ausführen (kopieren und einfügen!):

- Aktualisieren Sie zunächst Ihre vorhandene Paketliste:
```
$ sudo apt update
```

- Als nächstes installieren Sie ein paar Voraussetzungpakete, mit denen apt Pakete über HTTPS verwenden kann:
```
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

- Fügen Sie dann den GPG-Schlüssel für das offizielle Docker-Repository zu Ihrem System hinzu:

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

- Fügen Sie das Docker-Repository zu den APT-Quellen hinzu

```
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```

- Aktualisieren Sie anschließend die Paketdatenbank mit den Docker-Paketen aus dem neu hinzugefügten Repo:

```
$ sudo apt update
```

- Stellen Sie sicher, dass Sie die Installation aus dem Docker-Repo statt aus dem standardmäßigen Ubuntu-Repo durchführen:

```
$ apt-cache policy docker-ce
```

- Sie werden die folgende Meldung sehen, obwohl die Versionsnummer für Docker unterschiedlich sein kann:

```
docker-ce:
  Installed: (none)
  Candidate: 18.03.1~ce~3-0~ubuntu
  Version table:
     18.03.1~ce~3-0~ubuntu 500
        500 https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
```

Beachten Sie, dass docker-ce nicht installiert ist, aber der Installationskandidat aus dem Docker-Repository für Ubuntu 18.04 (bionic) stammt.

- Installieren Sie schließlich Docker:

```
$ sudo apt install docker-ce
```

- Docker sollte nun installiert, der Daemon sowie der Prozess beim Booten gestartet werden. Überprüfen Sie, ob es funktioniert:

```
$ sudo systemctl status docker
```

Die Meldung sollte wie folgt aussehen und zeigen, dass der Dienst aktiv ist und läuft:

```
 docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2018-07-05 15:08:39 UTC; 2min 55s ago
     Docs: https://docs.docker.com
 Main PID: 10096 (dockerd)
    Tasks: 16
   CGroup: /system.slice/docker.service
           ├─10096 /usr/bin/dockerd -H fd://
           └─10113 docker-containerd --config /var/run/docker/containerd/containerd.toml
```

Die Installation von Docker gibt Ihnen nun nicht nur den Docker-Dienst (Daemon), sondern auch das docker -Befehlszeilenprogramm oder den Docker-Client. 


- Testen:
```
$ sudo docker pull hello-world
```

## Aufgabe 3: Docker Übung

Ihre VM mit dem installierten Docker kann nun verwendet werden, um einige Übungen mit Docker durchzuführen.

> Note: Sie müssen bei den folgenden Docker Commands stets ein `sudo` voranstellen. Oder Docker entsprechende Rechte geben. Hierzu könnten Sie folgendes ausführen:
```
$ sudo gpasswd -a ${USER} docker
$ sudo service docker restart
```
> Durch die Gruppenänderung muss man sich noch einmal ab- und anmelden, anschließend läuft Docker sudofrei

Anschliessend:

1. Bitte führen Sie folgende Übung aus "[Einführung in Docker-Container](https://docs.microsoft.com/de-de/learn/modules/intro-to-docker-containers/index)
2. Alternative können Sie auch diese Übung ausführen [Erstellen einer containerisierten Webanwendung mit Docker](https://docs.microsoft.com/de-de/learn/modules/intro-to-containers/index)

**Fertig!!!**