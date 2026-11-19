# BuUI: Basic Universal User Interface

Konzept und Mockup für eine universelle, MCP-gesteuerte Oberfläche. Das Beispiel ist der Kundenservice-Assistent.

**Lizenz:** Das Konzept (dieses README) steht unter [CC BY 4.0](LICENSE-CC-BY-4.0), © Abrad7. Das Mockup (`kundenservice-assistent.html`) steht unter der [MIT-Lizenz](LICENSE-MIT), © Abrad7. Bei Weiterverwendung bitte Urheber und Quelle nennen.

---

# Kundenservice-Assistent: Konzept und Mockup

Status: Klickbares Mockup (eine HTML-Datei, ohne Backend, ohne festgelegte Systemarchitektur)
Mockup-Datei: `kundenservice-assistent.html`
Zielgruppe: Entwicklerinnen und Entwickler sowie Designerinnen und Designer, die dieses Mockup in ein echtes Produkt überführen

---

## 1. Idee in einem Absatz

Servicemitarbeitende im Kundenservice bearbeiten viele verschiedene Anliegen (Neukunde anlegen, Rechnungsfrage, Korrektur, Rechnungshistorie, Umzug, Fahrkarte, Kundensuche). Heute verteilt sich das auf mehrere Systeme. Der Kundenservice-Assistent ist ein einziger Arbeitsplatz, an dem Mitarbeitende ein Anliegen im Chat beschreiben oder auswählen, der Assistent sie durch den Ablauf führt und die relevanten Kundendaten neben dem Gespräch angezeigt werden. Mitarbeitende sollen schnell zwischen Anliegen wechseln, die Kundendaten auf einen Blick sehen und Detailansichten (Rechnungen, Zählerstände) öffnen können, ohne den Arbeitsplatz zu verlassen.

Die UI ist eine **menschenorientierte Oberfläche ohne eigene KI**. Menschen interagieren nur über Sprache (getippt oder gesprochen) und über Textbausteine, nicht über tiefe Menüs. Die UI stellt eine MCP-Schnittstelle bereit, über die sie sich selbst beschreibt. Ein steuernder Partner sendet Antworten, Textbausteine und Daten und passt sich an diese Selbstbeschreibung an. Die UI stellt empfangene Inhalte dar und meldet jede Interaktion als Ereignis zurück.

Das Mockup zeigt nur **Layout und Bediengefühl**. Es ist nicht an MCP oder ein reales System angebunden. Alle Kunden-, Rechnungs- und Zählerdaten sind fiktiv, die Chat-Antworten sind feste Texte.

---

## 2. Nutzergruppen und Ziele

| Nutzergruppe | Ziel |
| --- | --- |
| Servicemitarbeitende | Ein Anliegen durchgängig bearbeiten, mit weniger Systemwechseln und weniger fehlenden Angaben |
| Teamleitung | Häufige Anliegen erkennen und sehen, wo der Prozess hakt (spätere Auswertung, nicht im Mockup) |

Erfolgskriterien für eine erste echte Version (Vorschlag):

- Ein Neukunde kann mit allen Pflichtangaben (Vorname, Nachname, Geburtstag, Adresse, Bankdaten, Tarif, Zustimmung) in einer Sitzung angelegt werden.
- Typische Anliegen (Rechnungsfragen, Rechnungshistorie, Zählerstände bei einem Umzug) lassen sich ohne Verlassen des Arbeitsplatzes beantworten.
- Eine neue Vorlage kann von Mitarbeitenden in unter 10 Sekunden ergänzt werden.

---

## 2A. Konzeptmodell: UI als MCP-orientierte Oberfläche

- **Menschen** sprechen oder tippen und klicken Textbausteine. Es gibt keine tiefen Menüs.
- **Informationen** erscheinen im Chat und zusätzlich als Checklisten, Tabellen, Grafiken und Verweise auf andere Dashboards.
- **Die UI hat keine KI und keine Entscheidungslogik.** Sie stellt dar, was sie erhält.
- **Selbstbeschreibung:** Über ihre MCP-Schnittstelle legt die UI offen, wie sie mit Menschen kommuniziert (Textbausteine, Formulierungen, Ablauf) und welche Datenform und Vorgaben (Presets) sie erwartet, z. B. Tabellenspalten.
- **Steuernder Partner:** Eine externe KI-Anwendung oder ein Backend (noch nicht entschieden) liest die Selbstbeschreibung und passt an, was sie sendet.
- **Ereignisse zurück:** Jede Interaktion geht als Ereignis an den steuernden Partner, z. B. Checkbox gesetzt, Textbaustein gewählt, Tabellenzeile geöffnet, Dashboard-Verweis genutzt, Text oder Sprache eingegeben, Datei hinzugefügt.

Noch nicht entschieden sind: wer steuert, das Format der Selbstbeschreibung und das Ereignisschema.

## 3. Bildschirmaufbau

Der Bildschirm hat vier Bereiche. Der Kopfbereich ist fest, die drei Spalten sind in der Breite veränderbar und einklappbar.

```
+-----------------------------------------------------------------------+
| Kopfzeile: Titel                    [Darkmode] [Nutzer] [Anmelden]    |
+-----------------+----------------------------------+------------------+
| LINKS           | MITTE                            | RECHTS           |
| Vorlagen        | Chat                             | Kundendaten      |
| - + eigene      | - Anrufleiste (bei Anruf)        | - Checkliste     |
| - Fragenliste   | - Nachrichten (mit Aktionen)     | - Fortschritt    |
| - Mülleimer je  | - Eingabe: + | Text | Mikro | Hörer | - Dashboard-Verweis |
|   Vorlage       |   | Senden                       |                  |
+-----------------+----------------------------------+------------------+
```

### 3.1 Linke Spalte: Vorlagen

- Ein Textfeld mit **+**-Button fügt eine neue Vorlage zur Liste hinzu.
- Jede Vorlage hat ein **Mülleimer-Symbol** zum Löschen.
- "Vorlagen zurücksetzen" stellt die sieben Standardvorlagen wieder her.
- Ein Klick auf eine Vorlage sendet sie als Nutzernachricht in den Chat.
- Standardvorlagen (wie in der Oberfläche):
  1. Anlegen eines Neukunden
  2. Kunde hat Fragen zur Rechnung
  3. Kunde möchte eine Korrektur
  4. Kunde will seine Rechnungshistorie
  5. Kunde zieht aus
  6. Kunde braucht eine Fahrkarte
  7. Suche was wir zu Kunde XYZ wissen

### 3.2 Mittlere Spalte: Chat

- Chat im Stil von KI-Assistenten: Nachrichten oben, Eingabe unten.
- Eingabeelemente von links nach rechts:
  - **+**: Dateien oder Bilder anhängen (PDF, Office-Dateien, CSV, TXT, Bilder). Vor dem Senden als Chips angezeigt.
  - **Textfeld**: Enter sendet, Umschalt + Enter fügt eine Zeile hinzu.
  - **Mikrofon**: schaltet die Spracheingabe ein und aus (Browser-Spracherkennung, Deutsch).
  - **Telefonhörer**: nimmt einen Anruf an. Wird rot, um aufzulegen. Eine Anrufleiste zeigt Status und Dauer.
  - **Senden**: sendet Text und/oder Anhänge.
- Assistenz-Nachrichten können **Textbausteine** enthalten. Im Zielmodell kommen sie vom steuernden Partner. Im Mockup sind es feste Buttons, die ein Popup öffnen (z. B. "Rechnungen anzeigen").

### 3.3 Rechte Spalte: Kundendaten

- Checkliste mit sieben Feldern: Vorname, Nachname, Geburtstag, Adresse, Bankdaten, Tarif, Zustimmung.
- Jeder Eintrag ist eine Checkbox: **grün mit Haken**, wenn erfasst, **rot mit X**, wenn offen.
- Fortschrittsanzeige ("x von 7 erfasst") und ein Zurücksetzen-Button.
- Ein Bereich **Kundendashboard** verweist auf das bestehende Kundendashboard (URL noch festzulegen).

### 3.4 Popups (Dialoge)

- Für Listen mit Details, z. B.:
  - **Rechnungshistorie**: Rechnungsnummer, Datum, Zeitraum, Betrag, Status. "Details" klappt Positionen, Gesamtbetrag und Zahlungsart auf.
  - **Zählerstände**: Zählerart, Nummer, Ablesedatum, Stand, Verbrauch. "Details" klappt vorherigen Stand, Ablesungsart, Zählerort und Eichdatum auf.
- Schließen über ×, Escape oder einen Klick außerhalb.

### 3.5 Visuelles Design

- Weißer Hintergrund mit grauen Linien. Darkmode verfügbar (folgt der Systemeinstellung, Umschalter im Kopf).
- Primärfarbe **#800000** (dunkles Bordeaux) für Hauptbuttons und Nutzernachrichten im Chat.
- Checkbox-Zustände: Grün (#2E7D32) für erfasst, Rot (#C62828) für offen.
- Bewegung ist bewusst weich: Leisten gleiten, Nachrichten und Dialoge blenden ein und heben sich leicht. Alle Bewegungen sind abgeschaltet, wenn "Bewegung reduzieren" aktiv ist.

---

## 4. Verhalten im Detail

| Bereich | Verhalten im Mockup |
| --- | --- |
| Vorlagen | Hinzufügen über + oder Enter; Löschen je Eintrag; Zurücksetzen auf Standard. Nicht gespeichert (Neuladen stellt Standard wieder her). |
| Chat-Antwort | Nur Mockup: feste deutsche Antworten je Vorlage. Im Zielmodell kommen alle Antworten, Textbausteine und Daten vom steuernden Partner. Die UI hat keine eigene KI. |
| Anhänge | Bilder als Vorschau, Dokumente mit Name und Größe. Entfernen über ×. Es wird nichts hochgeladen. |
| Spracheingabe | Browser-Spracherkennung mit Sprache de-DE. Der Button ist deaktiviert, wenn der Browser sie nicht unterstützt. |
| Anruf | Nur Annehmen und Beenden. Dauer in einer Leiste. Beginn und Ende werden im Chat vermerkt. Keine echte Telefonie. |
| Checkliste Kundendaten | Manuelles Abhaken. Nicht mit einer Datenquelle verbunden und nicht gespeichert. |
| Größenänderung | Trenner zwischen den Spalten ziehen oder Pfeiltasten nutzen (Umschalt für größere Schritte). Grenzen 200 bis 480 px. |
| Einklappen | Runder Button auf jedem Trenner klappt die Seitenleiste ein oder aus. |
| Anmeldung | Nur optisch. Keine Authentifizierung. |

---

## 5. Daten (nur Mockup)

Das Mockup enthält fest hinterlegte Beispieldaten. Vor einem produktiven Einsatz müssen sie durch echte Quellen ersetzt werden.

- **Rechnungen**: Nummer, Datum, Abrechnungszeitraum, Betrag, Status (Mockup: Bezahlt, Überfällig; die echte Statusliste kommt aus dem System), Zahlungsart, Positionen.
- **Zähler**: Art (Strom, Gas, Wasser), Zählernummer, Ablesedatum, Stand, Verbrauch, vorheriger Stand, Ablesungsart, Standort, Eichung gültig bis.
- **Kundenfelder**: Vorname, Nachname, Geburtstag, Adresse, Bankdaten, Tarif, Zustimmung.

Wichtig: Der Beispieltext in den Popups weist darauf hin, dass es sich um Beispieldaten handelt. Dieser Hinweis bleibt, bis echte Daten angebunden sind, und wird im Produktivbetrieb entfernt.

---

## 6. Schnittstellen (noch zu bauen)

Hier braucht das Mockup ein echtes Backend oder ein externes System.

1. **Kundenstammdaten**: Lesen und Schreiben der sieben Kundenfelder. Nötig für "Anlegen eines Neukunden" und für Korrekturen.
2. **Rechnungssystem**: Rechnungen und Positionen je Kunde. Nötig für das Rechnungs-Popup und Rechnungsfragen.
3. **Zählerdaten**: Ablesungen und Historie je Kunde. Nötig für Umzugsanliegen.
4. **Kundendashboard**: Ziel-URL des bestehenden Dashboards. Derzeit ein Platzhalter (`https://example.com/kundendashboard`) in der Konstante `CUSTOMER_DASHBOARD_URL`.
5. **Telefonie**: echte Anrufverarbeitung (eingehender Anruf, Anrufererkennung, Aufzeichnung oder Notizen). Das Mockup simuliert nur Annehmen und Auflegen.
6. **Dateiablage**: Speicherort der Anhänge, Aufbewahrungsregeln, Virenprüfung. Derzeit werden Anhänge nicht hochgeladen.
7. **Authentifizierung**: echte Anmeldung und rollenbasierter Zugriff (Mitarbeitende, Teamleitung). Derzeit nur optisch.
8. **Protokollierung**: jede Änderung (Korrekturen, Neukunden) mit Nutzer und Zeitpunkt festhalten.
9. **Steuernder Partner (MCP)**: Das Mockup nutzt feste Texte. Im Zielmodell sendet eine externe KI-Anwendung oder ein Backend (noch nicht entschieden) Antworten, Textbausteine und Daten über MCP und empfängt die Ereignisse der UI. Antworten müssen die verwendeten Quelldaten nennen.

---

## 7. Technische Hinweise zum Mockup

- Einzelne Datei: `kundenservice-assistent.html`. HTML, CSS und reines JavaScript, keine externen Bibliotheken, keine Netzwerkzugriffe.
- Kein Browserspeicher (kein localStorage oder sessionStorage), der Zustand lebt nur in der Seite.
- Dialoge verwenden das native Element `<dialog>`.
- Die Spracheingabe nutzt die Web Speech API (`SpeechRecognition` / `webkitSpeechRecognition`). Sie ist nicht in jedem Browser verfügbar.
- Das Layout nutzt CSS Grid mit CSS-Variablen (`--left-w`, `--right-w`, `--left-col`, `--right-col`). Einklappen setzt die Spaltenbreite auf 0.
- Ab 1000 px Breite werden die drei Spalten untereinander angeordnet, die Größenänderung ist dann deaktiviert.
- Farben sind als CSS-Variablen in `:root` (hell) und `:root[data-theme="dark"]` (dunkel) definiert.

### Vorschlag für die Überarbeitung vor einem Produktivbetrieb

- Datei in Komponenten aufteilen (Vorlagen, Chat, Kundendaten, Dialoge), falls ein Framework eingesetzt wird.
- Beispieldaten in eine Datenschicht mit klarer Schnittstelle auslagern, damit sie durch echte APIs ersetzt werden können.
- Texte in eine Übersetzungsdatei auslagern, falls weitere Sprachen nötig sind.

---

## 8. Barrierefreiheit

Bereits im Mockup:

- Bedienbar per Tastatur: Vorlagen, Chat, Buttons, Spaltentrenner (Pfeiltasten), Dialoge (Escape zum Schließen).
- Beschriftungen für Symbol-Buttons (`aria-label`, `title`).
- Chat-Nachrichten werden als Live-Protokoll angekündigt.
- Checkboxen haben Textbeschriftungen neben den Symbolen.
- Reduzierte Bewegung wird berücksichtigt.

Vor einem Produktivbetrieb zu prüfen:

- Kontrast der Bordeaux-Buttons in beiden Designs.
- Verhalten der aufklappbaren Detailzeilen in den Popups mit Screenreadern.
- Reihenfolge des Tastaturfokus über die drei Spalten.

---

## 9. Glossar

| Begriff | Bedeutung |
| --- | --- |
| Vorlage | Vordefiniertes Anliegen in der linken Spalte |
| Popup / Dialog | Modales Fenster mit Liste und aufklappbaren Details |
| Kundendashboard | Bestehende Übersicht eines Kunden, erreichbar per Verweis |
| Zählerstand | Ablesung eines Zählers (Strom, Gas, Wasser) |
| Teamleitung | Leitung eines Teams von Mitarbeitenden |
| MCP | Model Context Protocol, ein Standard, um Werkzeuge und Daten mit KI-Anwendungen zu verbinden |
| Selbstbeschreibung | Beschreibung der UI über sich selbst: wie sie mit Menschen spricht und welche Datenform sie erwartet |
| Textbaustein | Vordefinierte Formulierung oder Auswahl, die Menschen anklicken statt zu tippen |
| Steuernder Partner | Externe KI-Anwendung oder Backend, das Inhalte über MCP an die UI sendet (noch nicht entschieden) |
