# Ansible Playbook

*Ein Ansible-Projekt zur automatisierten Konfiguration von Servern mit eigenem Playbook und modularen Rollen.*

## Überblick

Dieses Projekt enthält ein selbst erstelltes **Ansible-Playbook**, das verschiedene Dienste und Anwendungen auf einer frischen VM automatisch installiert und konfiguriert. Das Playbook ist modular aufgebaut und nutzt Rollen für Common-Settings, Apache, virtuelle Hosts, Firewall, Netzwerkanalyse (Nmap) sowie zwei wählbare Applikationen. Das Projekt befindet sich aktuell in Entwicklung.

## Was passiert, wenn du UFW aktivierst, bevor du SSH erlaubt hast? 

Wenn ich UFW aktiviere, bevor SSH erlaubt worden ist, kann ich **mich selber** aus der VM **aussperren**.

## Ausführung

Vor der Ausführung müssen die Variablen in **group_vars/all.yml** angepasst werden:

- `server_name` – Hostname der VM  
- `apache_ports` – Ports, die Apache nutzen soll  
- `ufw_allowed_ports` – Ports, die die Firewall freigeben soll  
- `wahlapplikation_1_config` / `wahlapplikation_2_config` – spezifische Einstellungen der Applikationen  

Um das Playbook auf einer frischen VM auszuführen, genügt ein Befehl:

ansible-playbook -i inventory/hosts.ini site.yml

## Wahlapplikationen

### Wahlapplikation 1: [Applikation 1 Name]
- **Funktion:** [Kurzbeschreibung, z. B. Datenbank, Monitoring etc.]  
- **Warum gewählt:** [Grund, z. B. praktische Anwendung für das Projekt]  
- **Konfiguration:** Die Rolle installiert die Applikation, richtet Benutzerrechte ein und passt die Konfigurationsdateien gemäß `group_vars/all.yml` an.

### Wahlapplikation 2: [Applikation 2 Name]
- **Funktion:** [Kurzbeschreibung, z. B. Web-App, Proxy etc.]  
- **Warum gewählt:** [Grund, z. B. Lernziel oder Projektanforderung]  
- **Konfiguration:** Die Rolle installiert die Applikation, konfiguriert Dienste automatisch und sorgt dafür, dass sie über die Firewall erreichbar ist.

## nmap-Ergebnis

# Beispielausgabe
Starting Nmap 7.93 ( https://nmap.org ) at 2026-04-07 10:00
Nmap scan report for 192.168.56.101
Host is up (0.0010s latency).
Not shown: 995 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
3306/tcp closed mysql
8080/tcp open  http-proxy

**Kommentar:** Die offenen Ports (22, 80, 443, 8080) entsprechen den freigegebenen Ports in unseren **UFW-Regeln**. Geschlossene Ports wie 3306 werden korrekt blockiert, sodass unautorisierte Zugriffe verhindert werden.

## Lizenz & Credits

Dieses Projekt wurde von **PantriMasi** erstellt.  
Verwendete Technologien: **Ansible**, **community.general Collection**

## Zusätzliche Links

- Offizielle Ansible-Dokumentation: https://docs.ansible.com/
