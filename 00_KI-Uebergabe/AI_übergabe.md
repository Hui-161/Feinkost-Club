# AI-Übergabe — zentrale Kontextdatei für alle KI-Sitzungen

Diese Datei ist der **gemeinsame Gedächtnisspeicher aller KI-Chats** zu diesem
Projekt. Jede neue Sitzung liest **zuerst** diese Datei, bevor sie arbeitet, und
trägt am Ende ihren eigenen Abschnitt unter §6 nach. So weiß jede Sitzung, was
vorher passiert ist, welche Regeln gelten und wo die Stolperfallen liegen.

_Letzte Änderung: 2026-07-29_

---

## 1. Repo(s) und ihre Rolle

- **Repo:** `Hui-161/Feinkost-Club` (Remote `origin`).
- **Rolle:** Enthält die komplette **statische Website** für den *Feinkost Club*
  (Techno-Veranstaltungen in Ballenstedt). Es gibt nur dieses eine Repo —
  Arbeits- und Veröffentlichungsstand sind identisch.
- **Hauptbranch:** `main`. Was auf `main` liegt, ist live.
- **Zielumgebung / Auslieferung:** **GitHub Pages**, gebunden an die eigene
  Domain **`feinkost-club.de`** (siehe Datei `CNAME`). Ein Push auf `main`
  veröffentlicht die Seite automatisch — es gibt keinen separaten Deploy-Schritt.
- **Domain / DNS / SSL (Stand Juli 2026, in dieser Sitzung geklärt):**
  - **DNS** wird bei **Hetzner** verwaltet (konsoleH → DNS-Verwaltung).
  - **Hosting** der Seite läuft über **GitHub Pages** (nicht Hetzner-Webhosting).
  - **HTTPS/SSL:** GitHub Pages stellt automatisch ein **Let's-Encrypt**-Zertifikat
    aus und erneuert es selbst (Voraussetzung: „Enforce HTTPS" aktiv). Es muss
    **nirgends** manuell ein Zertifikat gepflegt werden — weder bei Hetzner
    (SSL-Manager bleibt leer) noch sonst wo.
  - **Namecheap** ist der **alte Hoster**. Dessen SSL-Zertifikat wird nicht mehr
    benutzt und kann ignoriert werden (Auto-Renew des SSL-Produkts dort
    deaktivieren, damit keine Kosten entstehen). Ob die **Domain-Registrierung**
    noch bei Namecheap liegt → **offene Frage**, bitte nicht kündigen ohne Klärung.

## 2. Was ist hier drin

| Ordner / Datei            | Zweck                                                              | Stand |
|---------------------------|-------------------------------------------------------------------|-------|
| `index.html`              | Startseite „Feinkost Club \| Techno in Ballenstedt"; enthält u. a. Sektion **„Nächste Raves"** (Event-Termine 2026). | aktiv |
| `legal.html`              | Impressum & Datenschutz.                                           | aktiv |
| `CNAME`                   | `feinkost-club.de` — bindet GitHub Pages an die Domain. **Nicht löschen.** | aktiv |
| `robots.txt`              | SEO: erlaubt alles, verweist auf Sitemap.                          | aktiv |
| `sitemap.xml`             | SEO: listet `/` und `/legal.html`.                                 | aktiv |
| `images/`                 | `hero-bg.webp` (Hero-Hintergrund), `logo.png` (freigestelltes Logo). | aktiv |
| `fonts/`                  | Lokal gehostete Schriften (Inter, Space Grotesk) als `.woff2` — **bewusst lokal statt Google-Fonts-CDN (DSGVO).** | aktiv |
| `00_KI-Uebergabe/AI_übergabe.md` | Diese Übergabe-Datei.                                       | aktiv |

## 3. Verbindliche Regeln

- **Sprache der Website:** Deutsch (`<html lang="de">`). Alle Nutzertexte auf Deutsch.
- **Kein Build, kein Framework-Build-Schritt:** reine statische Dateien. Was im
  Repo liegt, wird 1:1 ausgeliefert. Nichts „kompilieren".
- **Styling:** **Tailwind via CDN** (`https://cdn.tailwindcss.com`), direkt im
  HTML per Utility-Klassen. Kein separater CSS-Build.
- **Schriften lokal lassen** (DSGVO). Keine Google-Fonts-/Fremd-CDN-Einbindung für
  Fonts hinzufügen.
- **`CNAME` niemals entfernen oder ändern** — sonst bricht die Domain-Anbindung
  und die Seite ist unter `feinkost-club.de` nicht mehr erreichbar.
- **SEO konsistent halten:** Bei neuen Seiten `sitemap.xml` mitpflegen; bei
  inhaltlichen Änderungen `lastmod` in `sitemap.xml` aktualisieren.
- **`main` ist live.** Direkt auf `main` gepushte Änderungen gehen sofort online —
  entsprechend sorgfältig committen.
- **Vor dem Commit:** Da es keine Testsuite gibt → HTML im Browser sichten
  (Startseite + Termine + Legal), auf offensichtliche Darstellungsfehler und
  korrekte Event-Daten/Ticket-Links prüfen.

## 4. Arbeitsweise, die sich bewährt hat

- **Kleine, klar beschriebene Commits.** Die Historie zeigt inhaltliche Commits
  wie „Update event schedule", „Add hero background image and logo",
  „Freistellen des Logos".
- **Prüfen statt raten:** Der Live-Zustand von Domain/HTTPS lässt sich real
  verifizieren — z. B. im Browser das Zertifikat ansehen (Schloss → Zertifikat;
  erwartet: Aussteller **Let's Encrypt**, gültiges Datum). Achtung: Aus der
  Sandbox heraus scheitern DNS-/HTTPS-Abfragen am Proxy (Zertifikate werden
  re-signiert, `dig` fehlt) — für harte Fakten den Nutzer/Browser einbeziehen.
- **Tests:** Es gibt **keine automatisierte Testsuite** und **keine CI** im Repo.
  „Test des betroffenen Bereichs" = manuelle Sichtprüfung im Browser.

## 5. Aktueller Gesamtstand / offene Punkte

- **Läuft:** Website ist live über GitHub Pages unter `feinkost-club.de`, HTTPS
  via automatischem Let's-Encrypt-Zertifikat (verifiziert am 2026-07-29:
  ausgestellt für `feinkost-club.de`, Aussteller Let's Encrypt, gültig bis
  24.09.2026 — wird von GitHub automatisch erneuert).
- **Bewusst nicht umgesetzt:** Kein eigenes SSL bei Hetzner, kein Namecheap-SSL —
  wird nicht gebraucht.
- **Offene Punkte / Fragen:**
  - Wo liegt die **Domain-Registrierung** aktuell (Namecheap oder Hetzner)? Vor
    Kündigungen bei Namecheap klären.
  - **Auto-Renew des SSL-Produkts bei Namecheap** deaktivieren (Aufgabe des
    Nutzers, außerhalb des Repos).
  - **Event-Termine** in `index.html` sind bis Ende 2026 gepflegt; laufend aktuell
    halten. (Hinweis: parallele Sitzung `claude/website-image-schedule-update-hhh4xu`
    arbeitet an Bildern/Terminen — deren Details trägt jene Sitzung selbst unter §6 ein.)

## 6. Register der Sitzungen / Branches

### claude/namecheap-ssl-after-migration-2c9d8l — SSL nach Hoster-Migration (Namecheap → Hetzner/GitHub Pages)
- **Status:** abgeschlossen, **0 Commits Code-Änderung** (reine Beratungssitzung).
  Der Remote-Branch wurde bereits gelöscht; der lokale Branch stand exakt auf `main`.
- **Zeitraum/Thema:** 2026-07-29. Frage des Betreibers: „Namecheap-SSL läuft
  ab — kann mir das egal sein?" nach Umzug vom alten Hoster (Namecheap) auf
  Domain-bei-Hetzner + Website auf GitHub Pages.
- **Wesentliche Ergebnisse:**
  - Geklärt: **Ja, die Namecheap-SSL-Ablaufmail kann ignoriert werden.** HTTPS
    läuft über ein **automatisch verwaltetes Let's-Encrypt-Zertifikat von GitHub
    Pages**. Per Live-Zertifikat bestätigt (Aussteller Let's Encrypt, gültig bis
    24.09.2026).
  - Rollen sauber getrennt: **Hetzner = nur DNS**, **GitHub Pages = Hosting + SSL**,
    **Namecheap = alter Hoster, nur noch ggf. Domain-Registrar**.
  - **Diese Übergabe-Datei** (`00_KI-Uebergabe/AI_übergabe.md`) neu angelegt.
- **Wichtig für Nachfolger / Stolperfallen:**
  - Nicht durch die Namecheap-/Hetzner-SSL-Oberflächen verwirren lassen: Der
    Hetzner-SSL-Manager ist **korrekterweise leer** und muss leer bleiben —
    das Zertifikat kommt von GitHub, nicht von Hetzner.
  - `CNAME` ist die Lebensader der Domain-Anbindung — nicht anfassen.
  - Aus der Entwicklungs-Sandbox lassen sich DNS/HTTPS **nicht** zuverlässig
    prüfen (Proxy re-signiert Zertifikate, `dig` fehlt) → für Netz-/Domain-Fakten
    den Browser des Nutzers heranziehen.

## 7. Arbeitsauftrag für JEDE Sitzung

1. **Orientieren:** `git remote -v`, aktueller Branch (`git branch --show-current`),
   Hauptbranch ist **`main`**. Diese Datei komplett lesen. Repo ist eine statische
   GitHub-Pages-Website (kein Build, keine Tests).
2. **Branch klären:** `git fetch origin --prune`, dann
   `git rev-list --count origin/main..origin/<dein-branch>`.
   - **0** → Arbeit ist schon in `main`; dem Nutzer Bescheid geben (Branch kann weg).
   - **>0** → betroffenen Bereich prüfen (hier: Browser-Sichtprüfung, da keine
     Testsuite). Wenn fertig und in Ordnung → in `main` mergen und pushen. Wenn
     nicht fertig → **nicht** mergen, unter §6 dokumentieren, was fehlt und warum.
3. **Diese Datei pflegen:** Nur den **eigenen** Abschnitt unter §6 ergänzen
   (neueste oben). **Fremde Abschnitte und fremde Branches nicht anfassen.**
4. **Committen & nach `main` pushen.** Bei abgelehntem Push wegen paralleler
   Sitzung: `git fetch`, per Rebase den eigenen Commit obendrauf setzen, Konflikt
   so lösen, dass **alle fremden Abschnitte erhalten** bleiben, dann erneut pushen.
5. **Kurz an den Nutzer melden:** Branch-Status, was gemergt wurde (oder warum
   nicht), was in dieser Datei eingetragen wurde.
