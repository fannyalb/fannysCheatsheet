# 🦭 Podman Cheat Sheet (Schummelzettel)

Ein kompakter Leitfaden für die Arbeit mit Podman. Podman ist weitgehend kompatibel zu Docker, läuft aber "rootless" und ohne Daemon.

---

## 🏗️ Image-Verwaltung
*Bilder herunterladen, anzeigen und löschen.*

| Befehl | Beschreibung |
| :--- | :--- |
| `podman pull <image>` | Lädt ein Image aus einer Registry herunter (z.B. `python:3.11-slim`). |
| `podman images` | Listet alle lokal gespeicherten Images auf. |
| `podman rmi <image_id>` | Löscht ein lokales Image. |
| `podman build -t <name> .` | Erstellt ein Image aus einem Dockerfile im aktuellen Verzeichnis. |
| `podman image prune` | Löscht alle ungenutzten (dangling) Images. |

---

## 🚀 Container-Lebenszyklus
*Container erstellen, starten und stoppen.*

| Befehl | Beschreibung |
| :--- | :--- |
| `podman run <image>` | Erstellt und startet einen neuen Container. |
| `podman run -d <image>` | Startet den Container im Hintergrund (Detached Mode). |
| `podman run --name <name> <image>` | Startet einen Container mit einem spezifischen Namen. |
| `podman run --rm <image>` | Container wird nach dem Beenden automatisch gelöscht. |
| `podman ps` | Zeigt alle laufenden Container an. |
| `podman ps -a` | Zeigt alle Container an (auch gestoppte). |
| `podman stop <name_id>` | Stoppt einen laufenden Container sauber (SIGTERM). |
| `podman start <name_id>` | Startet einen bereits vorhandenen, gestoppten Container. |
| `podman rm -f <name_id>` | Stoppt und löscht einen Container sofort (force). |

---

## 🛠️ Interaktion & Debugging
*In den Container schauen und Befehle ausführen.*

| Befehl | Beschreibung |
| :--- | :--- |
| `podman exec -it <id> sh` | Öffnet eine interaktive Shell im laufenden Container. |
| `podman logs <id>` | Zeigt die Konsolen-Logs des Containers an. |
| `podman logs -f <id>` | "Folgt" den Logs in Echtzeit. |
| `podman inspect <id>` | Zeigt detaillierte JSON-Infos (Netzwerk, Mounts, etc.). |
| `podman stats` | Live-Stream der Ressourcen-Nutzung (CPU, RAM). |
| `podman cp <lokal> <id>:<pfad>` | Kopiert Dateien vom Host in den Container (und umgekehrt). |

---

## 🌐 Netzwerk & Volumes
*Daten speichern und Ports freigeben.*

| Befehl | Beschreibung |
| :--- | :--- |
| `podman run -p 8080:80` | Mappt Port 8080 des Hosts auf Port 80 des Containers. |
| `podman run -v /host:/cont:Z` | Mountet ein Verzeichnis. Das `:Z` ist wichtig für SELinux (z.B. auf Fedora/RHEL). |
| `podman network ls` | Listet alle verfügbaren Podman-Netzwerke auf. |

---

## 🧹 System-Aufräumen
*Platz schaffen.*

| Befehl | Beschreibung |
| :--- | :--- |
| `podman system df` | Zeigt die Speicherplatzbelegung durch Podman an. |
| `podman system prune` | Löscht ALLES Ungenutzte: gestoppte Container, ungenutzte Netzwerke und Images ohne Namen. |

---

## 💡 Profi-Tipp für Python-Devs
Wenn du dein `python:3.11-slim` Image zum Debuggen startest:
`podman run -it --rm python:3.11-slim python`
*(Dies startet direkt den interaktiven Python-Interpreter und löscht den Container beim Beenden sofort wieder.)*
