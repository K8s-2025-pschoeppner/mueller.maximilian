# DHBW Kubernetes Klausur 2025

## Name

**Ihr Name hier**

## Ablauf

1. Klonen Sie das Repository
    ```bash
    git clone git@github.com:K8s-2025-pschoeppner/klausur.git
    cd klausur
    git remote remove origin
    ```
2. Erstellen Sie in der GitHub Organisation ein Repository mit dem Namen **\<vorname>.\<nachname>**
3. Laden Sie den Stand in das Repository hoch
   ```bash
   git remote add origin <url Ihres Repositories>
   git push -u origin master
   ```
4. Erstellen Sie einen Branch für die Bearbeitung
   > Vergessen Sie am Ende nicht Ihre Bearbeitung hochzuladen

* Bearbeiten Sie die Aufgaben der Reihe nach, da sie aufeinander aufbauen.
* Es wird nur der Stand in Ihrem Git Repository bewertet!
* Ob Ihre Abgabe funktioniert fließt in die Bewertung mit ein, aber auch nicht funktionierende Manifeste werden bewertet.

## Punkte

00 / 20

## Aufgaben

### Webserver (10 Punkte)

Sie finden in diesem Verzeichnis eine `index.html` Datei. Ihre Aufgabe ist es, einen Webserver ihrer Wahl auf Kubernetes zu erstellen, welcher diese zur Verfügung stellt. Dieser soll folgende Anforderungen erfüllen:

* Hochverfügbar: Er soll auf mindestens zwei Nodes laufen
* Updates: Er soll über `kubectl rollout restart` neugestartet werden können. Dabei dürfen nicht alle Instanzen gleichzeitig neustarten.
* Quality of Service: Er soll mit der QoS Klasse `Burstable` laufen
* Er soll nicht den `default` Service Account nutzen

### Networking (4 Punkte)

Der Webserver soll natürlich auch von "außen" erreichbar sein. Ihnen steht hierfür ein Ingress Controller zur Verfügung. Erstellen Sie keinen externen LoadBalancer.

* Die Domain `*.k8s.schoeppi5.de` ist für dieses Cluster konfiguriert. Nutzen Sie Ihr Studentenkürzel als Subdomain
* Die Website soll mittels HTTP ohne Angabe eines Ports erreichbar sein.

### Deployment (6 Punkte)

Der Webserver soll mittles der Blue/Green Deployment Strategie geupdatet werden können. Stellen Sie alle dafür notwendigen Manifeste bereit. Beschreiben Sie hier folgend, wie ein Upgrade durchgeführt werden kann. Stichpunkte sind ausreichend:



### Zusatzaufgaben

Sollten Sie noch Zeit haben, können Sie die folgenden Fragen noch beantworten:

* Was ist ein `ReplicaSet` und wofür wird es verwendet? (1 Punkt)
* Welche Auswirkungen hat die `Quality of Service` Klasse eines Pods und wie wird sie bestimmt? (1 Punkt)
* Was ist die Aufgabe des `CNI` in Kubernetes? (1 Punkt)
