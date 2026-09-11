---
typ: spec
status: bereit-zur-umsetzung
erstellt: 2026-09-10
thema: Landingpage LifeStrings Timer auf naturalconsult.de
---

# Landingpage LifeStrings Timer – Spezifikation

Eine Seite auf naturalconsult.de, die den LifeStrings Timer erklärt, ihn zum Download
anbietet und eine freiwillige Update-Liste führt. Dieses Dokument ist zugleich der
Auftrag: Wer es liest, kann die Seite bauen.

**Arbeitsweise:** Bei Abweichungen von dieser Spec anhalten und fragen. Nichts behaupten,
was nicht ausgeführt wurde. Jeden Schritt committen, aussagekräftige Commit-Messages.

---

## 1. Rahmen

| | |
|---|---|
| URL | `naturalconsult.de/lifestrings-timer/` |
| Hosting | GitHub Pages, Repo `naturalconsult-de` |
| Technik | statisches HTML + CSS, eine Seite, kein Framework, kein Build-Schritt |
| Sprache | Deutsch |
| Responsiv | ja – vom iPhone bis zum großen Monitor |
| Zielgruppe | Mac-Nutzer, die Werkzeuge fürs Selbstmanagement suchen |
| Zweitwirkung | Beratungskunden und LinkedIn – die Seite muss sich teilen lassen |

---

## 2. Grundentscheidungen

**Offener Download, kein E-Mail-Gate.** Die Datei ist ohne Anmeldung erreichbar. Ein Gate
wäre auf einer statischen Seite ohnehin nur Fassade, kostet Installationen und erzeugt
über das Kopplungsverbot (Art. 7 Abs. 4 DSGVO) einen Nachweisaufwand, der zum Ertrag in
keinem Verhältnis steht.

**Download als GitHub-Release-Asset.** Die ZIP hängt an einem Release in einem eigenen,
öffentlichen Release-Repo. GitHub zählt jeden Download serverseitig; die Zahl ist über die
API abrufbar. Damit braucht die Seite kein Statistik-Skript. Der Quellcode der App bleibt
in seinem privaten Repo – öffentlich ist nur das Release-Repo.

**Update-Liste, freiwillig.** Ein Feld auf der Seite, Double-Opt-in über Brevo. Sie ist
kein Zugangsweg zum Download, sondern ein Angebot.

**Keine fremden Ressourcen im Normalbetrieb.** Schriften liegen lokal im Repo, kein
Analyse-Skript, keine Cookies, kein Einwilligungsbanner. Die Seite wirbt mit „keine Cloud,
kein Tracking" – sie hält das selbst ein.

**Kein eigener Server.** Alles läuft über GitHub Pages.

---

## 3. Aufbau der Seite

Von oben nach unten. Reihenfolge nach dem Muster vergleichbarer Indie-Mac-Apps
(Rectangle, Maccy): Nutzen vor Funktionen, Systemvoraussetzungen am Knopf, kein Scrollen
bis zum Download.

1. **Kopf.** App-Icon, Name, Einzeiler. Download-Knopf, darunter eine Zeile:
   Version · Dateigröße · ab macOS 14 · kostenlos · von Apple notarisiert. Darunter der
   Installationshinweis: „Nach dem Laden die App in den Ordner ‚Programme' ziehen. Beim
   ersten Start kommt der Hinweis, dass es sich um eine aus dem Internet geladene Datei
   handelt – einmal bestätigen." Nur hier, nicht am zweiten Knopf.
2. **Bewegtbild.** Tonlose Schleife, 8–15 Sekunden: die ablaufende Scheibe und das
   Mini-Fenster, das über einem anderen Fenster schwebt. Zeigt, was ein Standbild nicht
   kann.
3. **Wofür das gut ist.** Drei Sätze zum Rhythmus – 25 Minuten arbeiten, fünf Minuten
   Pause, nach vier Runden eine längere. Keine Aufzählung.
4. **Vier bis fünf Nutzenblöcke,** je ein Bild: schwebendes Mini-Fenster · Ziffern oder
   ablaufende Scheibe · Restzeit per Drehgeste · automatisch weiter · hell und dunkel.
   Überschrift benennt das Ergebnis, nicht die Funktion; ein bis drei Sätze je Block.
5. **Was er bewusst nicht tut.** Keine Konten, keine Cloud, keine Statistik, keine
   Streaks, kein Tracking – mit Begründung: Der Timer bewertet niemanden.
6. **Zweiter Download-Knopf** mit denselben Angaben wie im Kopf.
7. **Update-Liste.** Ein Feld, ein Satz, eine Einwilligung. Siehe § 6.
8. **Wer das gebaut hat.** Zwei Sätze, ohne Foto, mit Link auf das LinkedIn-Profil. Sobald
   der Artikel zur Entstehung existiert, wird er von hier verlinkt.
9. **Fußzeile.** naturalconsult.de, Impressum, Datenschutz, Kontakt, Markenhinweis (§ 4).

---

## 4. Sprache und Begriffe

**Pomodoro.** Der Begriff darf beschreibend im Fließtext stehen: „Der LifeStrings Timer
ist ein Pomodoro-Timer für macOS" und „angelehnt an die Pomodoro-Technik". Einmal
nachgestellt in der Meta-Description. **Nicht** im Seitentitel als Produktbezeichnung,
nicht in einer Überschrift, nicht im Namen der App, nicht in der Domain, keine Tomate im
Bild, keine Meta-Keywords. Kein ®-Zeichen – die EU-Marken für Software sind erloschen, ein
Schutzzeichen für ein nicht bestehendes Recht wäre selbst angreifbar. In der Fußzeile ein
unaufdringlicher Satz: „Pomodoro Technique ist eine Marke von Francesco Cirillo.
LifeStrings Timer steht in keiner Verbindung zu ihm."

**LifeStrings.** Ein Satz im Einstieg verortet den Timer: das kleinste Werkzeug aus
LifeStrings, es schützt den Fokus, nachdem die Entscheidung gefallen ist, woran gearbeitet
wird. Der Begriff „Jetzt-Fokus" fällt genau einmal. Kein Erklärabschnitt zu LifeStrings –
der Timer steht für sich.

**Nutzen statt Funktionen.** Prägnanter, sachlicher Text schlägt werblichen; jedes Bild
bekommt erklärenden Text. Keine Schlagworte ohne Inhalt.

---

## 5. Download-Artefakt

- Quelle ist der notarisierte Release-Build.
- ZIP ausschließlich mit `ditto -c -k --keepParent` erzeugen – erhält Signatur, erweiterte
  Attribute und Symlinks. Kein Finder-„Komprimieren", kein `zip -r`.
- Ablage als Asset an einem Release im öffentlichen Release-Repo, Tag = Versionsnummer.
- Version, Dateigröße und Mindest-macOS auf der Seite stammen aus dem `Info.plist` der
  gebauten App, nicht aus einer Annahme.
- Vor dem Live-Gang: ZIP über einen Browser-Download laden, entpacken, starten – die App
  muss ohne Gatekeeper-Dialog öffnen. Ist das nicht so, stimmt an der Notarisierung etwas
  nicht; dann anhalten.
- Die Downloadzahl wird über die GitHub-API am Release-Asset abgelesen.

---

## 6. Update-Liste

- **Zweck:** Nachricht, wenn eine neue Version erscheint. Sonst nichts.
- **Mechanik:** eigenes HTML-Feld auf der Seite, das direkt an den Formular-Endpunkt von
  Brevo postet – kein fremdes Skript im Normalbetrieb. Läuft das ohne Brevos JavaScript
  nicht sauber durch, ist der Rückfall das eingebettete Brevo-Formular.
- **Double-Opt-in** ist Pflicht: Bestätigungsmail, werbefrei, mit einem Knopf zur
  Bestätigung. Erst danach steht die Adresse in der Liste.
- **Am Feld:** Zweck in einem Satz, Link auf die Datenschutzerklärung, Hinweis auf
  jederzeitigen Widerruf. Kein vorangekreuztes Feld, keine Kopplung an den Download.
- **Nach dem Absenden:** eine schlichte Danke-Seite auf naturalconsult.de, die auf die
  Bestätigungsmail hinweist.

---

## 7. Rechtstexte

Zwei eigene Seiten, `/impressum/` und `/datenschutz/`, aus der Fußzeile **jeder** Seite
verlinkt – auch von der Startseite.

- **Impressum** nach § 5 DDG: Anbieter, Anschrift, Kontakt, USt-IdNr., Verantwortlicher.
- **Datenschutzerklärung**, Generator-Text als Basis, ergänzt um die tatsächliche Technik:
  GitHub Pages als Hoster (Server-Logs beim Seitenaufruf), GitHub als Auslieferer der
  Downloads, Brevo als Auftragsverarbeiter für die Update-Liste mit Zweck, Rechtsgrundlage,
  Speicherdauer, Widerruf und Beschwerderecht. Ausdrücklich: keine Cookies, keine
  Reichweitenmessung, keine Weitergabe an Dritte darüber hinaus.
- Schriften liegen lokal – es gehen keine Besucherdaten an Google.

---

## 8. Gestaltung

- Farbtoken aus `SPEC-v2.md` des Timer-Repos: Warmweiß `#faf8f5` / Warmdunkel `#1e1c19`,
  Akzent Amber `#d97706` / `#f59e0b`, Text `#1c1a17` / `#ede9e3`. Hell und Dunkel über
  `prefers-color-scheme`.
- **Plus Jakarta Sans, lokal** aus `assets/fonts/` – niemals von einem fremden Server.
- Ruhige Seite: viel Weißraum, keine Karten-Schatten, keine Zier-Animationen.
- Der Amber-Akzent trägt die Download-Knöpfe, sonst nichts.
- **Bewegtbild:** `autoplay muted loop playsinline`, Standbild als Poster, bei
  `prefers-reduced-motion` bleibt das Standbild stehen. MP4 plus WebM.
- **Bilder:** frisch aufgenommen aus der laufenden v2, hell und dunkel, mit
  beschreibendem Alternativtext.

---

## 9. Metadaten

- **Titel:** „LifeStrings Timer – Fokus-Timer für macOS"
- **Beschreibung:** ein menschenlesbarer Satz, der „Pomodoro-Timer" nachgestellt enthält.
- **Vorschaubild** 1200 × 630 mit Icon und Einzeiler, als Open Graph gesetzt – damit
  geteilte Links auf LinkedIn nicht kaputt aussehen.
- **`SoftwareApplication`-Auszeichnung** nach schema.org mit `name`, `operatingSystem`,
  `applicationCategory` und `offers.price` = 0.
- Kein FAQ-Schema – Google zeigt daraus seit Mai 2026 keine Rich Results mehr.

---

## 10. Arbeitspakete

**Paket 1 – Korrektur.** Bringt die bestehende Seite in einen wahren Zustand, unabhängig
vom Umbau.

1. Schriften lokal einbinden statt von Google Fonts laden. *(erledigt)*
2. Öffentliches Release-Repo anlegen, notarisierte ZIP als Release-Asset hochladen.
3. Download-Knopf auf das Release-Asset umhängen, Versionszeile richtigstellen.
4. Abschnitt „So öffnest du die App" ersatzlos entfernen – mit der Notarisierung
   gegenstandslos.
5. `/impressum/` und `/datenschutz/` anlegen und aus beiden Seiten verlinken.

**Paket 2 – Umbau.** Die neue Seite nach § 3, sobald die Aufnahmen vorliegen.

6. Bewegtbild und Screenshots einbauen.
7. Texte nach § 3 und § 4 schreiben.
8. Update-Liste nach § 6 einbauen, Brevo-Automation prüfen.
9. Metadaten nach § 9 setzen.
10. Installationshinweis unter den Download-Knopf setzen, Wortlaut nach § 3 Punkt 1.

---

## 11. Akzeptanzkriterien

Jedes einzeln belegen, nicht behaupten.

1. `naturalconsult.de/lifestrings-timer/` zeigt alle neun Abschnitte aus § 3.
2. Der Download liefert eine ZIP, aus der die App **ohne** Gatekeeper-Dialog startet –
   über einen echten Browser-Download geprüft.
3. Die Downloadzahl ist über die GitHub-API abrufbar; ein Beispielaufruf ist dokumentiert.
4. Eine Testadresse im Anmeldefeld erhält die Bestätigungsmail und steht nach dem Klick in
   der Zielliste – nicht vorher.
5. Im Netzwerk-Panel geht beim reinen Seitenaufruf **kein** Request an eine fremde Domain.
6. Hell- und Dunkelmodus sehen beide richtig aus.
7. Auf einem iPhone-schmalen Viewport bricht nichts.
8. Impressum und Datenschutz sind von jeder Seite aus in einem Klick erreichbar.
9. Ein geteilter Link zeigt auf LinkedIn Titel, Beschreibung und Vorschaubild.
10. Die Startseite naturalconsult.de bleibt inhaltlich unverändert – bis auf die neuen
    Fußzeilen-Links.

---

## 12. Nicht Teil dieser Seite

Download hinter Registrierung · Feedback-Funktion · englische Fassung ·
Reichweitenmessung oder Analyse-Skripte · Cookie-Banner · eigener Server ·
App-Store-Verweise · Changelog · Newsletter über die Update-Nachricht hinaus.

---

## 13. Offene Zulieferungen

- Name des Release-Repos
- Impressumsdaten: Anschrift, USt-IdNr., Verantwortlicher
- Bildschirmaufnahme für das Bewegtbild und frische Screenshots aus v2
- Zielliste in Brevo samt Double-Opt-in-Automation
