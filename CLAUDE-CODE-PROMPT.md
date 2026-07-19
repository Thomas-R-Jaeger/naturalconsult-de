# Aufgabe: naturalconsult.de via GitHub Pages live bringen

## Kontext

Thomas Jäger (thomas.jaeger@naturalconsult.de, GitHub: thomas-r-jaeger) hat eine 
fertige statische Website für naturalconsult.de. Dateien liegen lokal unter 
`~/Projects/naturalconsult-website/`.

## Was bereits erledigt ist

- ✅ Fertige Website (`index.html` + `assets/logo.png` + `assets/thomas.jpg`)
- ✅ `.gitignore` und `CNAME` (enthält `naturalconsult.de`) angelegt
- ✅ DNS bei Ionos gesetzt: A-Records für `@` und `www` zeigen auf GitHub Pages IPs

## Deine Aufgabe

### 1. GitHub Repo anlegen

Gehe zu https://github.com/new und lege an:
- Name: `naturalconsult-de`
- Public
- Kein README, keine .gitignore, keine License

### 2. Git initialisieren und pushen

```bash
cd ~/Projects/naturalconsult-website
git init
git branch -m main
git config user.email "thomas.jaeger@naturalconsult.de"
git config user.name "Thomas Jäger"
git add index.html assets/ .gitignore CNAME
git commit -m "Initial commit: naturalconsult one-pager"
git remote add origin https://github.com/thomas-r-jaeger/naturalconsult-de.git
git push -u origin main
```

### 3. GitHub Pages aktivieren

Im Repo: **Settings → Pages**
- Source: `Deploy from a branch`
- Branch: `main` / `/ (root)`
- Save
- Custom domain: `naturalconsult.de` eintragen
- "Enforce HTTPS" aktivieren sobald verfügbar

### 4. Verify

Nach DNS-Propagation (bis zu ein paar Stunden) prüfen:
- https://naturalconsult.de lädt die Seite
- HTTPS funktioniert (kein Zertifikats-Fehler)

## Hinweise

- E-Mail bei Ionos läuft über Microsoft 365 – DNS dafür wurde nicht angefasst
- Subdomains (wiki, crm, sil, stage) bleiben unverändert
- Kalenderlink auf der Seite: https://cal.eu/thomas-jaeger
