# DHBW Kubernetes Klausur 2025

## Name

**Müller, Maximilian**

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

**Antwort:**
Update Green Deployment  
```bash
kubectl set image deployment/nginx-webserver-green nginx=nginx:new-version -n mueller-maximilian
```
Green Deployment hochskalieren  
```bash
kubectl scale deployment nginx-webserver-green --replicas=2 -n mueller-maximilian
```
Green Deployment prüfen  
```bash
kubectl get pods -l version=green -n mueller-maximilian
```
Traffic auf Green umleiten  
```bash
kubectl patch service nginx-webserver-service -n mueller-maximilian
```
```

### Zusatzaufgaben

Sollten Sie noch Zeit haben, können Sie die folgenden Fragen noch beantworten:

* Was ist ein `ReplicaSet` und wofür wird es verwendet? (1 Punkt)
Ein ReplicaSet sorgt dafür, dass eine festgelegte Anzahl identischer Pods immer läuft, meist über ein Deployment verwaltet. Es überwacht den Zustand der Pods und erstellt neue Pods, wenn welche ausfallen, um den gewünschten Zustand aufrechtzuerhalten.

* Welche Auswirkungen hat die `Quality of Service` Klasse eines Pods und wie wird sie bestimmt? (1 Punkt)
Die QoS-Klasse eines Pods bestimmt dessen Priorität bei Ressourcenknappheit und basiert auf definierten Ressourcenanforderungen und -limits. Es gibt drei Klassen: Guaranteed, Burstable und BestEffort. Pods mit der niedrigsten Klasse (BestEffort) werden zuerst evakuiert. Die QoS-Klasse wird basierend auf den definierten Ressourcenanforderungen (requests) und -limits (limits) der Container im Pod festgelegt.

* Was ist die Aufgabe des `CNI` in Kubernetes? (1 Punkt)
Das CNI in Kubernetes verwaltet die Netzwerkkonfiguration, ermöglicht Pod-Kommunikation und vergibt eindeutige IP-Adressen.
CNI-Plugins erweitern die Netzwerkfunktionalität von Kubernetes und unterstützen verschiedene Netzwerktypen wie Overlay- oder Bridge-Netzwerke.

