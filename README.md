# AWS Webanwendungsarchitektur mit VPC, ELB, Auto Scaling und S3

## Ziel

Erstelle eine skalierbare und hochverfügbare Webanwendungsarchitektur auf AWS, die eine Virtual Private Cloud (VPC) mit mehreren Subnetzen, einem Elastic Load Balancer (ELB), Auto Scaling und eine S3-Bucket-Integration beinhaltet.

## Anforderungen

### 1. **VPC-Erstellung**
- Erstelle eine VPC mit einem CIDR-Block von `10.0.0.0/16`.

### 2. **Subnetze einrichten**
- Erstelle **zwei öffentliche Subnetze** in unterschiedlichen Verfügbarkeitszonen:
  - `10.0.1.0/24`
  - `10.0.2.0/24`
  
- Erstelle **zwei private Subnetze** in unterschiedlichen Verfügbarkeitszonen:
  - `10.0.3.0/24`
  - `10.0.4.0/24`
  
- Füge ein **Internet-Gateway (IGW)** zur VPC hinzu und verbinde es mit den öffentlichen Subnetzen.

### 3. **Route Tables konfigurieren**
- Weise den öffentlichen Subnetzen eine **Route Table** zu, die den gesamten ausgehenden Datenverkehr über das Internet-Gateway leitet.
- Erstelle eine private **Route Table** für die privaten Subnetze ohne Internetzugang.

### 4. **Sicherheitsgruppen**
- Erstelle eine **Sicherheitsgruppe für den Load Balancer**, die HTTP (Port 80) für alle Quellen (`0.0.0.0/0`) zulässt.
- Erstelle eine **Sicherheitsgruppe für die EC2-Instanzen**, die nur HTTP-Verkehr vom Load Balancer und SSH (Port 22) für die Verwaltung zulässt.

### 5. **Launch Template und Auto Scaling**
- Erstelle eine **Launch Template** für die EC2-Instanzen:
  - Verwende ein AMI, das ein Webserver-Setup (z. B. NGINX) enthält.
  - Stelle sicher, dass die EC2-Instanzen mit User Data eingerichtet werden, um eine einfache Webseite anzuzeigen.
  - Ordne die EC2-Instanzen den privaten Subnetzen zu und verwende die Sicherheitsgruppe für EC2-Instanzen, die nur den Load Balancer zulässt.

- Richte **Auto Scaling** ein:
  - Mindestanzahl der Instanzen: 2
  - Maximalanzahl der Instanzen: 4

### 6. **Elastic Load Balancer (ELB)**
- Erstelle einen **Application Load Balancer** in den beiden öffentlichen Subnetzen.
- Konfiguriere Listener für HTTP (Port 80) und leite den Datenverkehr an die EC2-Instanzen in den privaten Subnetzen.

### 7. **S3-Bucket zur Speicherung statischer Inhalte**
- Erstelle einen **S3-Bucket** und lade einige statische Inhalte (z. B. Bilder, CSS-Dateien) hoch.
- Konfiguriere den Bucket so, dass die Dateien öffentlich zugänglich sind, und füge eine **Bucket Policy** hinzu, die den öffentlichen Zugriff auf Objekte erlaubt.

### 8. **DNS-Integration (Optional)**
- Verwende **Route 53** zur Erstellung einer Domain oder Subdomain, die auf den Load Balancer verweist.
- Ordne die Domain dem Load Balancer zu, um über eine benutzerfreundliche URL auf die Anwendung zuzugreifen.

## Überprüfung

1. **Verbindungstests:**
   - Rufe die Domain oder die öffentliche IP-Adresse des Load Balancers auf und überprüfe, ob die Webseite korrekt angezeigt wird.
   - Überprüfe den S3-Bucket, indem du die URL einer hochgeladenen Datei im Browser öffnest und sicherstellst, dass sie erreichbar ist.

2. **Auto Scaling-Test:**
   - Simuliere Lasttests auf den EC2-Instanzen (z. B. durch viele Anfragen oder eine Traffic-Spitze) und überprüfe, ob Auto Scaling automatisch zusätzliche Instanzen hinzufügt oder entfernt.

## Bonusaufgabe: Monitoring und Alarme

- Konfiguriere Amazon **CloudWatch** zur Überwachung des Webanwendungs-Traffics und der Ressourcennutzung (z. B. CPU-Auslastung, Netzwerkverkehr).
- Erstelle **Alarme**, die dich benachrichtigen, wenn Schwellenwerte (z. B. hohe CPU-Auslastung oder Anstieg des Traffics) überschritten werden.

## Ziel der Übung

- Lerne, eine skalierbare und hochverfügbare Webanwendung mit AWS-Ressourcen zu erstellen.
- Verstehe die Funktionsweise von VPCs, Subnetzen, Elastic Load Balancing, Auto Scaling und S3 in einer realen Anwendungsarchitektur.
- Erhalte praktische Erfahrung im Umgang mit AWS-Services zur Verwaltung von Infrastruktur.

## AWS-Dienste, die verwendet werden

- **Amazon VPC** (Virtual Private Cloud)
- **Amazon EC2** (Elastic Compute Cloud)
- **Elastic Load Balancer (ELB)**
- **Amazon S3** (Simple Storage Service)
- **Auto Scaling**
- **Amazon Route 53** (DNS)
- **Amazon CloudWatch** (Optional für Monitoring)

## Quellen

- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/)
- [AWS Auto Scaling Documentation](https://docs.aws.amazon.com/autoscaling/)
- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/)
- [AWS ELB Documentation](https://docs.aws.amazon.com/elasticloadbalancing/)
- [AWS Route 53 Documentation](https://docs.aws.amazon.com/route53/)

