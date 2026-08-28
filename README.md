# claude-tax-skills

Claude-Skills für die tägliche Arbeit in der Steuerkanzlei. Jeder Skill ist ein
eigenes Plugin unter `plugins/` mit einer `SKILL.md`, die Claude als
Arbeitsanweisung lädt.

## Enthaltene Skills

| Skill | Zweck |
|---|---|
| `belegpruefung` | Eingangsbelege gegen die Pflichtangaben nach § 14 UStG prüfen und Rückfragen an den Mandanten formulieren |
| `umsatzsteuer-voranmeldung` | UStVA aus Buchungsdaten vorbereiten, Kennzahlen plausibilisieren, Abgabefrist bestimmen |
| `mandantenanfrage-beantworten` | Mandantenfragen strukturiert beantworten: Sachverhalt, Rechtsgrundlage, Antwort, offene Punkte |

## Installation

### Als Marketplace (empfohlen)

Das Repo ist ein Claude-Code-Marketplace. Einmal hinzufügen, danach lässt sich
jeder Skill einzeln installieren und wieder entfernen:

```bash
claude plugin marketplace add bluebatch/claude-tax-skills
claude plugin install belegpruefung@bluebatch-tax
```

In der Desktop-App dasselbe über `/plugin`. Verfügbar sind `belegpruefung`,
`umsatzsteuer-voranmeldung` und `mandantenanfrage-beantworten`.

Aufgerufen wird ein Skill danach als `/<plugin>:<skill>`, also
`/belegpruefung:belegpruefung`, oder Claude zieht ihn selbst heran, wenn die
Anfrage zur `description` passt. Nach dem Aktivieren lädt Claude die Skills
erst nach `/reload-plugins` oder einem Neustart.

### Von Hand

Repo klonen und den einzelnen Skill in das Skill-Verzeichnis des Projekts oder
des Nutzers verlinken:

```bash
git clone git@github.com:bluebatch/claude-tax-skills.git
ln -s "$(pwd)/claude-tax-skills/plugins/belegpruefung/skills/belegpruefung" \
      ~/.claude/skills/belegpruefung
```

Alternativ die Skill-Ordner direkt nach `.claude/skills/` im Projekt kopieren.

## Aufbau

```
.claude-plugin/
└── marketplace.json              ← Katalog, listet jeden Skill als eigenes Plugin
plugins/<name>/
├── .claude-plugin/plugin.json    ← Name, Version, Beschreibung des Plugins
└── skills/<name>/
    └── SKILL.md                  ← Frontmatter (name, description) + Arbeitsanweisung
```

Der Unterordner `skills/` ist Pflicht. Eine `SKILL.md` direkt im
Plugin-Wurzelverzeichnis lädt zwar die CLI, die Desktop-App meldet dazu aber
„Dieses Plugin hat keine Skills oder Agents".

Ein neuer Skill braucht beides: den Ordner unter `plugins/` **und** einen Eintrag
in `marketplace.json` mit `"source": "./plugins/<name>"`.

Konventionen: Ordnernamen klein und mit Bindestrichen, deutsche Texte mit echten
Umlauten, `description` im Frontmatter so formuliert, dass Claude erkennt, wann
der Skill greift.

## Hinweis

Die Skills sind Arbeitshilfen und ersetzen keine steuerliche Beratung. Ergebnisse
werden immer von einem Berufsträger geprüft, bevor sie an Mandanten oder das
Finanzamt gehen.
