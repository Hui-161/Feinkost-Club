# AI-Übergabe — zentrale Kontextdatei für alle KI-Sitzungen

Diese Datei ist der **gemeinsame Gedächtnisspeicher aller KI-Chats** zu diesem
Projekt. Jede neue Sitzung liest **zuerst** diese Datei, bevor sie arbeitet, und
trägt am Ende ihren eigenen Abschnitt unter §6 nach. So weiß jede Sitzung, was
vorher passiert ist, welche Regeln gelten und wo die Stolperfallen liegen.

_Letzte Änderung: 2026-09-22_

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
|---------------------------|-------------
------------------------------------------------------|-------|
| `index.html`              | Startseite „Feinkost Club \| Techno in Ballenstedt"; oben ein **Ticket-Kasten „Nächster Rave"** (direkter Ticket-Link), darunter Sektion **„Nächste Raves"** (Event-Termine 2026). | aktiv |
| `legal.html`              | Impressum & Datenschutz.                                           | aktiv |
| `CNAME`                   | `feinkost-club.de` — bindet GitHub Pages an die Domain. **Nicht löschen.** | aktiv |
| `robots.txt`              | SEO: erlaubt alles, verweist auf Sitemap.                          | aktiv |
| `sitemap.xml`             | SEO: listet `/` und `/legal.html`.                                 | aktiv |
| `images/`                 | `hero-bg.webp` (Hero-Hintergrund), `logo.png` (freigestelltes Logo), `favicon-32/192/512.png`, `apple-touch-icon.png` (Favicon-Set). | aktiv |
| `favicon.ico`, `site.webmanifest` | Favicon (16/32/48 px) und Web-Manifest (Name, Farben, Icons). | aktiv |
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
  inhaltlichen Änderung
en `lastmod` in `sitemap.xml` aktualisieren.
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
    halten. Vergangene Termine **entfernen** (Liste **und** JSON-LD) — Stand
    2026-09-21 stehen nur no
ch die 6 Termine ab 10.10.2026 drin.
  - **Ticket-Kasten „Nächster Rave"** oben auf der Startseite zeigt fest auf
    „Druckausgleich" (10.10.2026). Nach dem Event auf den nächsten Termin
    umstellen oder entfernen, sonst wirbt die Seite für eine vergangene Party.
  - Der Ticket-Link `https://toduu.de/events/druckausgleich` kam vom Betreiber und
    konnte aus der Sandbox nicht aufgerufen werden (Proxy) → im Browser prüfen.
  - Branch `claude/website-image-schedule-update-hhh4xu` ist gemergt und kann auf
    GitHub gelöscht werden.

## 6. Register der Sitzungen / Branches

### session/2026-09-22-foerderer-logos
- **Status:** gemerged — direkt auf `main` gepusht (kein Branch).
- **Zeitraum/Thema:** 2026-09-22. Mail von Hannes Herrmann (IEK)
  „Logo": zwei Förderer-Logos im Footer, jeweils auf die
  Förderer-Seite verlinkt, darüber der Hinweis „Gefördert von:".
- **Wesentliche Ergebnisse:**
  - `index.html`-Footer: Vollbreite-Zeile mit „Gefördert von:"
    und zwei Logos auf weißen Karten (Seite dunkel, Logos
    dunkel/farbig auf weiß):
    1. **Initiative Musik** -> https://www.initiative-musik.de/
       Bild: gstatic-Thumbnail-URL aus der Mail.
    2. **BKM** (Beauftragte der Bundesregierung für Kultur und
       Medien) -> https://www.kulturstaatsminister.de/, Bild:
       offizielle SVG-URL kulturstaatsminister.de/fileadmin/
       Logo/BKM_de_v2__Web_farbig.svg.
  - `sitemap.xml`: `lastmod` der Startseite auf 2026-09-22.
  - `legal.html` hat keinen Footer → dort nichts ergänzt.
- **Wichtig für Nachfolger / Stolperfallen:**
  - **Beide Logos sind Hotlinks** (nicht im Repo gehostet),
    weil die KI-Sandbox keine Binärdateien laden/pushen kann.
    Die gstatic-Thumbnail-URL ist **nicht dauerhaft stabil** →
    sobald eine offizielle Logo-Datei vorliegt, unter `images/`
    hosten und `src` ersetzen; BKM-SVG ebenfalls bei Gelegenheit
    lokal speichern.
  - **Datenschutz:** Hotlinks lösen beim Seitenaufruf Requests
    an Google (gstatic) und kulturstaatsminister.de aus. Prüfen,
    ob §7 „Externe Links" in `legal.html` ergänzt werden muss.
  - Chat-Uploads enthalten keine Binärdaten → Logo-Dateien müssen
    anders ins Repo (z. B. direkt über GitHub hochladen).
  - Erster Push-Versuch (Commit 3fbcfb9) enthielt durch die
    Tool-Übertragung eingeschleppte Zeilenumbrüche mitten in
    HTML-Attributen; wurde mit Folge-Commit aus dem Elter-Stand
    neu aufgebaut.

### claude/favicon-logo — Favicon aus dem quadratischen Feinkost-Logo
- **Status:** gemerged — Inhalt vollständig in `main`; Branch kann gelöscht werden.
- **Zeitraum/Thema:** 2026-09-21 (gleiche Sitzung wie `claude/druckausgleich-ticketlink`).
  Betreiber lieferte Logo-Zip (`FEINKOST.png/.jpg/.pdf` = Logo mit Rahmen, dunkle
  Schrift auf Weiß; `Insta_Profil-4.png` = quadratisch, weiße Schrift auf Dunkel).
- **Wesentliche Ergebnisse:**
  - Favicon-Set aus `Insta_Profil-4.png` (passt zum dunklen Seiten-Design), enger
    zugeschnitten (Schrift ≈ 81 % der Kantenlänge), damit „FEIN KOST" auch bei
    16 px erkennbar bleibt: `favicon.ico` (16/32/48), `images/favicon-32.png`,
    `images/favicon-192.png`, `images/favicon-512.png`, `images/apple-touch-icon.png` (180).
  - `site.webmanifest` (Name, `theme_color`/`background_color` `#050505`, Icons).
  - `<link rel="icon"…>`, `apple-touch-icon`, `manifest` und `theme-color` im
    `<head>` von `index.html` **und** `legal.html`.
- **Wichtig für Nachfolger / Stolperfallen:**
  - Neue HTML-Seiten brauchen denselben Link-Block im `<head>` (aus `index.html` kopieren).
  - Favicons wurden mit Pillow erzeugt (`pip install pillow` in der Sandbox nötig).
    Das Quell-Logo hat eine helle 1-px-Linie am linken Rand → beim automatischen
    Zuschnitt Randspalten ignorieren.
  - Ein `og:image` für Social-Sharing gibt es weiterhin **nicht** — Kandidat wäre
    `image
s/favicon-512.png` oder ein eigenes 1200×630-Bild.

### claude/druckausgleich-ticketlink — Ticket-Link „Druckausgleich" 10.10.2026, vergangene Termine raus
- **Status:** gemerged — Inhalt vollständig in `main`; Branch kann gelöscht werden.
- **Zeitraum/Thema:** 2026-09-21. Betreiber lieferte Plakat und direkten toduu-Link
  für „Druckausgleich" (Black Ego x Wasted Electronic Youth, Techno/House/DnB,
  Sa 10.10.2026, Start 22:00 Uhr). Auftrag: Link hinterlegen, „den Leuten es so
  einfach wie möglich machen", vergangene Veranstaltungen entfernen.
- **Wesentliche Ergebnisse:**
  - Neuer **Ticket-Kasten „Nächster Rave"** als erste Sektion in `<main>` (direkt
    unter der Laufschrift): Datum, Titel „Druckausgleich", Subline, Button
    „Tickets sichern" → `https://toduu.de/events/druckausgleich`. Grund: Das Plakat
    verweist auf `feinkost-club.de`, Besucher sollen ohne Scrollen zum Ticket kommen.
  - Karte 10.10. in „Nächste Raves" von „Wasted x Black Ego" auf **„Druckausgleich"**
    umbenannt, Uhrzeit + Subline ergänzt, eigener „Tickets sichern"-Button rechts.
  - **Vergangene Termine entfernt** (18.07. Classic Night, 04.09. Teenie-Party,
    12.09. Techno / House VA) — in der sichtbaren Liste **und** im Events-JSON-LD.
    Übrig: 6 Termine (10.10., 06.11., 07.11., 11.12., 12.12., 26.12.).
  - JSON-LD des 10.10.-Events: Name/Beschreibung auf Druckausgleich, `url` und
    `offers.url` auf den direkten Ticket-Link. Übrige Events behalten den
    toduu-Org-Link; der Sammel-Button „Tickets auf toduu sichern" unten bleibt.
  - `sitemap.xml`: `lastmod` der Startseite auf 2026-09-21.
- **Wichtig für Nachfolger / Stolperfallen:**
  - Events stehen **zweimal** in `index.html`: sichtbare Karten in „Nächste Raves"
    **und** als JSON-LD-Array im `<head>`. Immer beides ändern. Das JSON-LD wurde
    per `json.loads`/`json.dumps` (indent=2, ensure_ascii=False) neu geschrieben.
  - Der Ticket-Kasten oben ist **statisch** verdrahtet (kein JS) — nach dem
    10.10.2026 manuell auf
 den nächsten Termin umstellen.
  - Externe Links (toduu) sind aus der Sandbox **nicht** erreichbar (Proxy 403) →
    Link-Prüfung im Browser des Nutzers.

### claude/website-image-schedule-update-hhh4xu — Hintergrundbild, Logo, Termine 2026
- **Status:** gemerged — Inhalt vollständig in `main`; Branch kann gelöscht werden.
- **Zeitraum/Thema:** 2026-07-29. Neues Hintergrundbild, freigestelltes Logo und
  Event-Termine 2026 auf der Website.
- **Wesentliche Ergebnisse:**
  - Hero-Hintergrundbild `images/hero-bg.webp` als fixierter Ganzseiten-Hintergrund
    mit dunklem Overlay (Lesbarkeit) eingebaut.
  - Logo `images/logo.png` freigestellt: eng zugeschnitten, transparenter
    Hintergrund, Rahmen+Schrift weiß invertiert (statt weißer Box mit dunkler
    Schrift); sitzt direkt im Header auf dunklem Grund.
  - Sektion „Nächste Raves" komplett auf 9 Termine 2026 aktualisiert:
    Classic Night (18.07./07.11./26.12.), Teenie-Party (04.09./06.11./11.12.),
    Techno / House VA (12.09./12.12.), Wasted x Black Ego (10.10.). Bezeichnungen
    laut Betreiber („Classic Night" statt „Disco", „Teenie-Party" statt „Teenie",
    „Techno / House VA" statt „Techno").
  - schema.org-JSON-LD-Eventdaten passend auf alle 9 Termine aktualisiert;
    Ticket-Button vereinfacht (direkter Link zur toduu-Org-Seite, abgelaufene
    Deadline-Logik entfernt).
- **Wichtig für Nachfolger / Stolperfallen:**
  - GitHub-Pages-Deploy hakte mehrfach mit „Deployment failed, try again later",
    Re-Runs blieben in „queued" hängen — **Upstream-Störung von GitHub Pages**,
    nicht im Repo. Was half: **neuer leerer Commit auf `main`** stößt einen
    frischen Build/Deploy an, statt denselben Run endlos neu zu starten. Daher
    stehen zwei leere „Trigger GitHub Pages rebuild"-Commits in der Historie
    (harmlos).
  - Logo-Freistellung per Pillow/numpy in der Sandbox (Luminanz→Alpha, dunkle
    Pixel→weiß) aus dem gelieferten Logo mit weißem Hintergrund.
  - Tailwind kommt per CDN; in der Sandbox ist `cdn
.tailwindcss.com` durch den
    Proxy blockiert → lokale Vorschau wirkt ungestylt, ist aber **kein** Fehler.

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
   `git rev-list --count origin/main..origin/<dein-b
ranch>`.
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
