# Ansible Playbook

*Ein Ansible-Projekt zur automatisierten Konfiguration und Verwaltung von Servern mit eigenem Playbook und modularen Rollen.*

## Überblick

Dieses Projekt enthält ein selbst entwickeltes **Ansible-Playbook** zur automatisierten Einrichtung und Verwaltung von Systemen. Der Fokus liegt auf einer klar strukturierten Rollenarchitektur, um verschiedene Dienste wie Apache, Firewall und Netzwerkanalyse effizient bereitzustellen. Das Projekt befindet sich aktuell in Entwicklung und kann flexibel um weitere Rollen und Anwendungen erweitert werden.

## Installation

1. Repository klonen: git clone [Repository-URL] und danach cd mein-playbook

2. Ansible installieren: sudo apt update und sudo apt install ansible -y

3. Collection installieren: ansible-galaxy collection install community.general

4. Inventory prüfen und anpassen: nano inventory/hosts.ini

5. Verbindung testen: ansible all -m ping

6. Playbook ausführen: ansible-playbook -i inventory/hosts.ini site.yml

## Beitrag leisten (Contributing)

Beiträge sind willkommen. Erstelle bei Änderungen einen Pull Request und beschreibe klar, was geändert wurde. Für Fehler oder Verbesserungsvorschläge bitte ein Issue erstellen. Achte darauf, dass neue Rollen sauber strukturiert und nachvollziehbar dokumentiert sind.

## Lizenz & Credits

Dieses Projekt wurde von **PantriMasi** erstellt und gepflegt.  
Verwendete Technologien: **Ansible**, **community.general Collection**

## Zusätzliche Links

- Offizielle Ansible Dokumentation: https://docs.ansible.com/
