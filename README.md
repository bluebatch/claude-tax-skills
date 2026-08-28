# claude-tax-skills

Claude-Skills für die tägliche Arbeit in der Steuerkanzlei, gebündelt in drei
Plugins nach Themengebiet. Jeder Skill ist ein Ordner mit einer `SKILL.md`, die
Claude als Arbeitsanweisung lädt.

## Plugins und Skills

| Plugin | Skill | Zweck |
|---|---|---|
| `finanzbuchhaltung` | `belegpruefung` | Belege gegen die Pflichtangaben nach § 14 UStG prüfen und Rückfragen formulieren |
| | `kontierungsvorschlag` | Konten nach SKR03/SKR04 vorschlagen, Sonderfälle herausziehen |
| | `umsatzsteuer-voranmeldung` | UStVA aus Buchungsdaten vorbereiten, Kennzahlen plausibilisieren |
| `lohnbuchhaltung` | `lohnabrechnung-pruefen` | Entgeltabrechnung nachrechnen und Abweichungen zum Vormonat erklären |
| | `minijob-pruefen` | Geringfügigkeit, Übergangsbereich und kurzfristige Beschäftigung abgrenzen |
| | `reisekosten-abrechnen` | Dienstreise abrechnen, Mahlzeiten kürzen, Dreimonatsfrist prüfen |
| `mandantenkommunikation` | `mandantenanfrage-beantworten` | Mandantenfrage einordnen: Vermerk für die Akte, Antwort für den Mandanten |
| | `unterlagen-anfordern` | Fehlliste in eine Nachforderung übersetzen, die der Mandant beantworten kann |
| | `fristenmitteilung` | Termine berechnen, über Feiertage schieben, Mandanten informieren |

## Installation

### Als Marketplace (empfohlen)

Einmal den Marketplace hinzufügen, danach die Plugins einzeln installieren:

```bash
claude plugin marketplace add bluebatch/claude-tax-skills
claude plugin install lohnbuchhaltung@bluebatch-tax
```

In der Desktop-App dasselbe über `/plugin`.

Aufgerufen wird ein Skill als `/<plugin>:<skill>`, also
`/lohnbuchhaltung:minijob-pruefen`, oder Claude zieht ihn selbst heran, wenn die
Anfrage zur `description` passt. Nach dem Aktivieren lädt Claude die Skills erst
nach `/reload-plugins` oder einem Neustart. Nach einer Änderung im Repo muss
zuerst der Marketplace aktualisiert werden, sonst arbeitet der Client mit dem
alten geklonten Stand weiter.

### Von Hand

```bash
git clone git@github.com:bluebatch/claude-tax-skills.git
ln -s "$(pwd)/claude-tax-skills/plugins/lohnbuchhaltung/skills/minijob-pruefen" \
      ~/.claude/skills/minijob-pruefen
```

Alternativ die Skill-Ordner direkt nach `.claude/skills/` im Projekt kopieren.

## Aufbau

```
.claude-plugin/
└── marketplace.json              ← Katalog, listet die drei Plugins
plugins/<plugin>/
├── .claude-plugin/plugin.json    ← Name, Version, Beschreibung
└── skills/<skill>/
    └── SKILL.md                  ← Frontmatter (name, description) + Arbeitsanweisung
```

Der Unterordner `skills/` ist Pflicht. Eine `SKILL.md` direkt im
Plugin-Wurzelverzeichnis lädt zwar die CLI, die Desktop-App meldet dazu aber
„Dieses Plugin hat keine Skills oder Agents".

Ein neuer Skill braucht den Ordner unter `plugins/<plugin>/skills/`. Ein neues
Plugin braucht zusätzlich einen Eintrag in `marketplace.json` mit
`"source": "./plugins/<name>"` und eine eigene `plugin.json`.

Konventionen: Ordnernamen klein und mit Bindestrichen, der Frontmatter-`name`
gleich dem Ordnernamen, deutsche Texte mit echten Umlauten, `description` so
formuliert, dass Claude erkennt, wann der Skill greift.

## Hinweis

Die Skills sind Arbeitshilfen und ersetzen keine steuerliche Beratung. Ergebnisse
werden immer von einem Berufsträger geprüft, bevor sie an Mandanten oder das
Finanzamt gehen. Steuersätze, Grenzwerte und Pauschalen ändern sich jährlich; die
Skills sind angewiesen, sie nicht aus dem Gedächtnis zu setzen, sondern
nachzufragen oder aus dem Beleg zu nehmen.
