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

Repo klonen und den Ordner `skills/` in das Skill-Verzeichnis des Projekts oder
des Nutzers verlinken:

```bash
git clone git@github.com:bluebatch/claude-tax-skills.git
ln -s "$(pwd)/claude-tax-skills/skills/belegpruefung" ~/.claude/skills/belegpruefung
```

Alternativ die Skill-Ordner direkt nach `.claude/skills/` im Projekt kopieren.

## Aufbau eines Skills

```
skills/<skill-name>/
└── SKILL.md    ← YAML-Frontmatter (name, description) + Arbeitsanweisung
```

Konventionen: Ordnernamen klein und mit Bindestrichen, deutsche Texte mit echten
Umlauten, `description` im Frontmatter so formuliert, dass Claude erkennt, wann
der Skill greift.

## Hinweis

Die Skills sind Arbeitshilfen und ersetzen keine steuerliche Beratung. Ergebnisse
werden immer von einem Berufsträger geprüft, bevor sie an Mandanten oder das
Finanzamt gehen.
