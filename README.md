# claude-tax-skills

Claude-Skills für die tägliche Arbeit in der Steuerkanzlei. Jeder Skill ist ein
Ordner unter `skills/` mit einer `SKILL.md`, die Claude als Arbeitsanweisung lädt.

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

Damit das funktioniert, muss `.claude-plugin/marketplace.json` im Wurzel-
verzeichnis liegen — ohne diese Datei meldet Claude
`no readable .claude-plugin/marketplace.json` und lädt gar nichts. Jeder
Skill-Ordner ist zugleich das Wurzelverzeichnis eines Plugins: liegt dort kein
`skills/`, lädt Claude die `SKILL.md` daneben als einzelnen Skill.

### Von Hand

Repo klonen und den Ordner `skills/` in das Skill-Verzeichnis des Projekts oder
des Nutzers verlinken:

```bash
git clone git@github.com:bluebatch/claude-tax-skills.git
ln -s "$(pwd)/claude-tax-skills/skills/belegpruefung" ~/.claude/skills/belegpruefung
```

Alternativ die Skill-Ordner direkt nach `.claude/skills/` im Projekt kopieren.

## Aufbau

```
.claude-plugin/
└── marketplace.json    ← Katalog, listet jeden Skill als eigenes Plugin
skills/<skill-name>/
└── SKILL.md            ← YAML-Frontmatter (name, description) + Arbeitsanweisung
```

Ein neuer Skill braucht beides: den Ordner unter `skills/` **und** einen Eintrag
in `marketplace.json` mit `"source": "./skills/<skill-name>"`.

Konventionen: Ordnernamen klein und mit Bindestrichen, deutsche Texte mit echten
Umlauten, `description` im Frontmatter so formuliert, dass Claude erkennt, wann
der Skill greift.

## Hinweis

Die Skills sind Arbeitshilfen und ersetzen keine steuerliche Beratung. Ergebnisse
werden immer von einem Berufsträger geprüft, bevor sie an Mandanten oder das
Finanzamt gehen.
