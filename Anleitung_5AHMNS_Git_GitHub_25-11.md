# Git und GitHub · Skriptum für die 5AHMNS

**Mittwoch, 25.11.2026 · 3 Unterrichtseinheiten · Einzelarbeit im Repo `ID-gitbasics`**

**Stellt euch vor:** Gestern habt ihr für eure Diplomarbeit einen Spielprototyp getestet. Für jede Runde hatten die Testpersonen genau eine Minute Zeit. Heute öffnet ihr das Projekt für die nächste Testrunde und merkt: Der Timer läuft jetzt 90 Sekunden. Jemand aus dem Team hat das Zeitlimit beim Ausprobieren geändert. Eure Betreuung fragt, ob ihr den gestrigen Test unter denselben Bedingungen wiederholen könnt.

**Wie findet ihr heraus, welche Codezeile geändert wurde und welcher Projektstand beim gestrigen Test verwendet wurde?**

Mit **Versionierung** könnt ihr einen festgehaltenen Projektstand wiederfinden und mit dem aktuellen Stand vergleichen. Im Übungsrepo probierst du das mit `README.md` und `docs/Notizen.md` aus. Du änderst beide Dateien, hältst aber zunächst nur die Änderung am README in einem Commit fest. Am Ende ist dein Übungscommit auf GitHub sichtbar und im vierten Issue verlinkt.

## Fachbegriffe

| Begriff | Erklärung in einem Satz |
|---|---|
| **Versionierung** | Versionierung hält ausgewählte Projektstände fest, damit du sie später wiederfinden und vergleichen kannst. |
| **Git** | Git ist ein Versionsverwaltungssystem, mit dem du Projektstände und ihre Änderungen lokal festhältst. |
| **GitHub** | GitHub ist eine Online-Plattform, auf der du Git-Repositories bereitstellen und Aufgaben gemeinsam bearbeiten kannst. |
| **Repository (Repo)** | Ein Repository enthält die Versionsgeschichte deines Projekts. |
| **Lokales Repository** | Das lokale Repository ist die Git-Versionsgeschichte auf deinem Rechner. |
| **Remote** | Ein Remote ist eine benannte Verbindung zu einem anderen Repository, etwa zu deinem Repo auf GitHub. |
| **`origin`** | `origin` ist der Name, den Git beim Klonen üblicherweise für das Remote vergibt. |
| **Klonen** | Beim Klonen erstellt Git eine lokale Kopie des Repositories und richtet die Verbindung zum Remote ein. |
| **`.git`** | Der versteckte Ordner `.git` enthält unter anderem die lokale Versionsgeschichte, die Einstellungen dieses Repos und den Index. |
| **Arbeitsverzeichnis** | Im Arbeitsverzeichnis befinden sich die Dateien, die du im Editor ansiehst und bearbeitest. |
| **Staging Area (Index)** | Die Staging Area hält den Dateistand fest, den Git für den nächsten Commit vorbereitet. |
| **Commit** | Ein Commit speichert einen ausgewählten Stand der versionierten Dateien mit einer eindeutigen Kennung und einer Nachricht. |
| **Commit-Nachricht** | Die Commit-Nachricht beschreibt, welche Änderung du festgehalten hast. |
| **Diff** | Ein Diff zeigt die Unterschiede zwischen zwei Ständen, bei Textdateien zum Beispiel hinzugefügte und entfernte Zeilen. |
| **Branch** | Ein Branch ist ein Name, der auf einen Commit zeigt und beim Committen auf diesem Branch weiterrückt. |
| **`main`** | `main` ist in diesem Projekt der Name des Hauptbranches, von dem du startest. |
| **`HEAD`** | `HEAD` bezeichnet deinen aktuell ausgecheckten Stand, normalerweise über den aktiven Branch. |
| **Push** | Beim Push überträgt Git Commits an ein Remote und aktualisiert dort den angegebenen Branch. |
| **HTTPS** | HTTPS schützt die Übertragung zwischen deinem Rechner und GitHub durch Verschlüsselung. |
| **Authentifizierung** | Bei der Authentifizierung weist du GitHub nach, welches Konto auf das Repo zugreift. |
| **Git Credential Manager (GCM)** | Git Credential Manager übernimmt die GitHub-Anmeldung für Git über HTTPS und verwaltet die Zugangsdaten. |
| **Personal Access Token (PAT)** | Ein PAT ist ein geheimer Zugangsschlüssel, mit dem sich ein Tool bei GitHub authentifizieren kann. |
| **Git-Konfiguration** | Die Git-Konfiguration enthält Einstellungen wie Name und E-Mail, die in deine Commits geschrieben werden. |
| **Issue** | Ein Issue hält auf GitHub eine Aufgabe, einen Fehler oder einen Vorschlag fest. |
| **Akzeptanzkriterium** | Ein Akzeptanzkriterium beschreibt überprüfbar, wann eine Aufgabe erledigt ist. |

## Vor dem Start

Melde dich bei GitHub mit deinem Konto an, nimm gegebenenfalls die Einladung an und öffne dein persönliches Repo `ID-gitbasics`. Dort findest du unter **Issues** die vier Aufträge. Öffne auf deinem eigenen Rechner ein Terminal. Unter Windows kannst du **Git Bash** oder **PowerShell** verwenden, unter macOS oder Linux das **Terminal**.

## 1. EH · Git prüfen und Repo klonen

### Issue 1 · Git prüfen und bei Bedarf installieren

Öffne auf deinem Rechner ein Terminal und prüfe, ob Git bereits installiert ist.

~~~text
git --version
~~~

Wenn eine Versionsnummer erscheint, geh direkt zu **Issue 2**. Falls Git fehlt, folge der Anleitung für dein Betriebssystem.

#### Windows · Git for Windows

1. Lade den Installer für deinen Rechner von der offiziellen [Git-Downloadseite für Windows](https://git-scm.com/install/win) herunter. Wähle **x64** oder **ARM64** passend zu deinem Gerät.
2. Starte die heruntergeladene Datei und übernimm für diese Übung die Standardeinstellungen. Lass **Git Credential Manager** ausgewählt, falls der Installer danach fragt.
3. Öffne nach der Installation ein neues Fenster in **Git Bash** oder **PowerShell** und führe `git --version` erneut aus.

#### macOS · Apple Command Line Tools

1. Öffne **Terminal** und führe den folgenden Befehl aus. Falls macOS schon beim Versionscheck die Installation angeboten hat, kannst du direkt dort auf **Installieren** klicken.

   ~~~text
   xcode-select --install
   ~~~

2. Bestätige die Installation der **Command Line Tools** und warte, bis sie fertig ist.
3. Führe `git --version` erneut im Terminal aus. Die Versionsnummer kann den Zusatz `Apple Git` enthalten.

[Offizielle Git-Installationsanleitung für macOS](https://git-scm.com/install/mac)

**Akzeptanzkriterium**

- [ ] `git --version` gibt eine Versionsnummer aus.

### Issue 2 · Dein Repository klonen und Commit-Identität prüfen

Kopiere in deinem Repo unter **Code → HTTPS** die Adresse. Ersetze in den folgenden Befehlen den URL-Platzhalter und den Beispielordner durch deine eigenen Angaben. Falls eine Browser-Anmeldung erscheint, wähle dein GitHub-Konto. Für diesen Ablauf mit Git Credential Manager brauchst du keinen selbst erstellten Token.

~~~text
git clone "HTTPS-ADRESSE-HIER-EINFUEGEN"
cd 01-gitbasics
git status
~~~

**Ein sauberes Arbeitsverzeichnis** erkennst du an der Meldung `nothing to commit, working tree clean` oder ihrem deutschen Gegenstück. Es gibt keine Änderungen an versionierten Dateien, keine vorgemerkten Änderungen und keine neuen, noch unversionierten Dateien, die Git anzeigen würde. Absichtlich ignorierte Dateien, etwa Einträge aus `.gitignore`, zählen dabei nicht mit.

**Name und E-Mail auslesen:** Führe im Projektordner die folgenden beiden Befehle aus. Der erste gibt den Namen aus, der zweite die E-Mail-Adresse. Bleibt eine Ausgabe leer, ist der jeweilige Wert in der Git-Konfiguration noch nicht gesetzt.

~~~text
git config --get user.name
git config --get user.email
~~~

Mit `git config --list --show-origin` kannst du nachsehen, aus welchen Dateien Git seine Einstellungen liest. `--local` gilt für dein aktuelles Repo, `--global` für dein Benutzerprofil am Rechner. Falls Name oder E-Mail fehlen oder falsch sind, setze sie **im Projektordner**. Ersetze die Beispielwerte.

~~~text
git config --local user.name "Vorname Nachname"
git config --local user.email "EIGENE-COMMIT-ADRESSE"
~~~

**Akzeptanzkriterien**

- [ ] In deiner lokalen Kopie findest du `README.md` und `docs/Notizen.md`.
- [ ] `git status` zeigt den Branch `main` und ein sauberes Arbeitsverzeichnis.
- [ ] Git zeigt den vorgesehenen Namen und die vorgesehene E-Mail für deine Commits.

## 2. EH · Zwei Dateien ändern und gezielt eine committen

### Issue 3 · Nur die README-Änderung committen

Erstelle den Branch `uebung-git` und wechsle darauf.

~~~text
git switch -c uebung-git
~~~

Kopiere den jeweils vorgegebenen Satz als neue Zeile ans Ende der Datei.

| Datei | Satz zum Einfügen |
|---|---|
| `README.md` | In diesem Projekt übe ich die Versionsverwaltung mit Git und GitHub. |
| `docs/Notizen.md` | Heute übe ich, zwei Dateien zu ändern und nur eine davon zu committen. |

Speichere beide Dateien und führe die folgenden Befehle aus. Lies die Ausgabe von `git diff --staged`, bevor du den Commit erstellst.

~~~text
git status
git diff
git add README.md
git status
git diff
git diff --staged
git commit -m "Projektbeschreibung ergänzen"
git show --stat HEAD
git status
~~~

| Befehl | Worauf du in der Ausgabe achtest |
|---|---|
| `git status` | Welcher Branch ist aktiv und welche Dateien sind geändert oder vorgemerkt? |
| `git diff` | Welche Änderungen an bereits versionierten Dateien sind noch nicht vorgemerkt? |
| `git diff --staged` | Welche Änderungen sind gegenüber dem letzten Commit für den nächsten Commit vorgemerkt? |
| `git show --stat HEAD` | Welche Dateien hat der aktuelle Commit geändert? |

**Akzeptanzkriterien**

- [ ] Du arbeitest auf `uebung-git`.
- [ ] Vor dem Commit zeigt `git diff --staged` nur Änderungen an `README.md`.
- [ ] Der Commit ändert nur `README.md` und hat eine verständliche Nachricht.
- [ ] Nach dem Commit zeigt `git status` die Notizdatei weiterhin als lokal geändert und unvorgemerkt.

## 3. EH · Branch pushen und Commit prüfen

### Issue 4 · Deinen Commit auf GitHub nachweisen

~~~text
git push -u origin uebung-git
~~~

`-u` verbindet deinen lokalen Branch für nachfolgende Befehle mit dem zugehörigen Branch auf dem Remote. Wähle auf GitHub `uebung-git` aus, öffne deinen Commit und kontrolliere die geänderten Dateien. Kopiere die URL des Commits als Kommentar in dieses Issue.

**Akzeptanzkriterien**

- [ ] Auf GitHub ist in deinem Repo der Branch `uebung-git` sichtbar.
- [ ] Der Commit auf GitHub zeigt nur die README-Änderung.
- [ ] Im vierten Issue steht der direkte Link zum Commit.

**Wenn etwas hängt:** Bei „not a git repository“ prüfe, ob du im geklonten Projektordner bist. Bei Problemen mit dem Push zeigt `git remote -v` die Adresse der Gegenstelle. Prüfe außerdem, ob du mit dem richtigen Konto angemeldet bist und die Repo-Einladung angenommen hast.

**Abschlussfrage:** Warum ist die Änderung an `docs/Notizen.md` weiterhin in `git status` sichtbar, obwohl sie im Commit auf GitHub fehlt?

**Am 02.12.** verwenden wir den gepushten Branch für einen **Pull Request** (Vorschlag zum Übernehmen der Änderung), ein **Review** (Prüfung durch eine andere Person) und den **Merge** (Zusammenführen der Änderungen).

## Nachschlagen

- [Git – Arbeitsverzeichnis, Staging Area und Repository](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)
- [Git – Konfiguration](https://git-scm.com/docs/git-config)
- [Git – Diff](https://git-scm.com/docs/git-diff)
- [GitHub – Anmeldung mit Git Credential Manager](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git?platform=windows)
