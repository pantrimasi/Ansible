# Ansible Playbook

*Ein Ansible-Projekt zur automatisierten Konfiguration von Servern mit eigenem Playbook und modularen Rollen.*

## Überblick

Dieses Projekt enthält ein selbst erstelltes **Ansible-Playbook**, das verschiedene Dienste und Anwendungen auf einer frischen VM automatisch installiert und konfiguriert. Das Playbook ist modular aufgebaut und nutzt Rollen für Common-Settings, Apache, virtuelle Hosts, Firewall, Netzwerkanalyse (Nmap) sowie zwei wählbare Applikationen. Das Projekt befindet sich aktuell in Entwicklung.

## Was passiert, wenn du UFW aktivierst, bevor du SSH erlaubt hast? 

Wenn ich UFW aktiviere, bevor SSH erlaubt worden ist, kann ich **mich selber** aus der VM **aussperren**.

## Ausführung

Vor der Ausführung müssen die Variablen in **group_vars/all.yml** angepasst werden:

- `server_name` – Hostname der VM  
- `web_root` – Verzeichnis, in dem die HTML-Dateien abgelegt werden
- `web_files` – HTML-Dateien, die man hochladen will

Um das Playbook auf einer frischen VM auszuführen, genügt ein Befehl:

ansible-playbook -i inventory/hosts.ini site.yml

## Wahlapplikationen

### Wahlapplikation 1: PostgreSQL
**Funktion:** Datenbank  
**Warum gewählt:** Da eine PostgreSQL-Datenbank gut zu einem Webserver passt und es mich interessiert hat, wie ich User und Datenbanken erstellen kann.  
**Konfiguration:**
1. Installation mit Ansible per apt
2. Servicestarten und Autostart aktivieren
3. Datenbank und Benutzer erstellen
4. Konfiguration mit einem Template angepasst

### Wahlapplikation 2: fail2ban
**Funktion:** Sicherheit  
**Warum gewählt:** Da es mich auch interessiert hatte, wie bei der ersten Auswahl. Dazu ist es auch allgemein nützlich, wenn man Server Sicherheit verbessern will.  
**Konfiguration:**
1. Installation von fail2ban
2. Autostart aktivieren
3. erstellt eine Grundkonfiguration

## nmap-Ergebnis
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-04-08 09:01 CEST
Nmap scan report for zli-VMware-Virtual-Platform (192.168.146.154)
Host is up (0.0000020s latency).
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 0.06 seconds
```
Port 443 war zuerst nicht offen, weil kein Dienst auf diesem Port aktiv war, obwohl er in der Firewall erlaubt wurde. Ich habe danach **SSL in Apache aktiviert**, damit der Server auf Port 443 hört und der Port im Scan sichtbar wird.

### Das habe ich gemacht mit folgenden Commands:
```
sudo a2enmod ssl
sudo a2ensite my_site-ssl.conf
sudo systemctl reload apache2
```

# Reflexion
## Tag 1
### Was war für dich neu?
Natürlich war mir das ganze Thema Ansible neu, und auch die verschiedenen neuen Begriffe wie Roles, Tasks, Handler und Templates haben am Anfang ein bisschen verwirrt. Es war auch neu, dass ich wirklich mit YAML‑Files gearbeitet habe, da ich es mir früher mal angeschaut habe, aber nicht richtig. Ich habe den Zweck und Vorteile von Ansible gelernt. Also, dass es für die Automatisierung ist, man Konfigurationsdateien machen und hochladen kann oder dass es Agentenlos ist.

### Wo bist du nicht weitergekommen und wie hast du den Blocker gelöst?
Zuerst hatte ich ein bisschen Probleme, das ganze Thema zu verstehen, vor allem mit dem Aufbau eines Playbooks. Nach einiger Zeit, nach ein bisschen Informieren und selber Ausprobieren, ging es dann wieder. Auch am Anfang von der 2. Aufgabe hatte ich ein bisschen Probleme, da ich nicht wirklich wusste, wie ich jetzt anfangen sollte. Auch hier habe ich versucht, mich möglichst gut zu informieren. Schlussendlich konnte ich dann auch bei der 2. Aufgabe Apache etc. installieren.

### Wo hast du KI eingesetzt und was hättest du ohne KI selbst herausgefunden?
Ich habe KI direkt schon am Anfang benutzt, nämlich für die Erstellung eines README. Da wir irgendwann schon mal einen README-Prompt machen mussten, benutzte ich den, um eine Vorlage zu generieren. Was mir auch geholfen hat, ist KI für die Erklärung verschiedener Funktionen, der Struktur und Bedeutung zu helfen. Dazu benutzte ich KI auch während der Aufgaben, wenn Fehlercodes unverständlich waren oder wenn ich nicht mehr weiterkam.

## Tag 2
### Was war für dich neu?
Heute konnte ich natürlich mehr lernen über Ansible allgemein, wenn auch nicht so viel wie gestern. Heute konnte ich vor allem nochmal spüren, dass Schreibfehler und die Reihenfolge von Tasks sehr wichtig sind. Allgemein verstehe ich das System viel klarer und genauer, womit ich heute je nachdem ein bisschen effizienter arbeiten konnte.

### Wo bist du nicht weitergekommen und wie hast du den Blocker gelöst?
Bei PostgreSQL hatte ich viel und lange Probleme mit allem. Die Installation hatte Probleme mit dem Cluster und dazu hatte ich auch Berechtigungsprobleme. Ich habe viel Zeit damit verbracht, das zu lösen, und habe auch ein bisschen weggelassen, damit es schlussendlich funktionierte.

### Wo hast du KI eingesetzt und was hättest du ohne KI selbst herausgefunden?
Ich habe KI heute vor allem zum Debuggen benutzt, da, wie gesagt, PostgreSQL viele Probleme hatte. Dazu habe ich KI auch wieder gebraucht, um verschiedene Funktionen zu verstehen. 

## Lizenz & Credits

Dieses Projekt wurde von **PantriMasi** erstellt.  
Verwendete Technologien: **Ansible**, **community.general Collection**

## Zusätzliche Links

- Offizielle Ansible-Dokumentation: https://docs.ansible.com/
