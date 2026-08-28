---
name: unterlagen-anfordern
description: Unterlagen anfordern — Stellt aus einer Lücke in der Buchhaltung oder einer Checkliste eine Nachforderung an den Mandanten zusammen, sortiert nach Dringlichkeit, mit fertiger E-Mail und einer Liste zum Abhaken. Nutzen, wenn Belege, Kontoauszüge, Verträge oder Nachweise fehlen und der Mandant sie liefern soll.
---

# Unterlagen beim Mandanten anfordern

Du machst aus einer Fehlliste eine Mail, die der Mandant ohne Rückfrage
beantworten kann.

$ARGUMENTS

---

## ARGUMENTE

- `<pfad>` — Fehlliste, offene Posten oder Buchhaltungsauszug
- `--mandant <name>` — steuert Ansprache und Anrede
- `--frist <datum>` — bis wann die Unterlagen da sein sollen
- `--anlass <text>` — Jahresabschluss, Voranmeldung, Betriebsprüfung, Nachfrage des Finanzamts

---

## ABLAUF

1. **Fehlendes sammeln** und je Posten festhalten: was genau, für welchen
   Zeitraum, warum es gebraucht wird.
2. **Zusammenfassen.** Fünf Zeilen zur selben Sache werden ein Punkt. Der Mandant
   soll eine Liste sehen, keine Buchhaltungssicht.
3. **Nach Dringlichkeit sortieren:**
   - **blockierend** — ohne das geht die Abgabe nicht
   - **wichtig** — führt sonst zu einer Schätzung oder einem verlorenen Abzug
   - **nachreichbar** — kann später kommen
4. **Übersetzen.** Kein Kontenrahmen, keine Belegnummern ohne Kontext. „Die
   Rechnung von Meyer über 1.428 € vom 14. März" statt „Beleg 4930/0412".
5. **Formulieren** (siehe Ausgabe).

---

## AUSGABE

Erst die interne Liste:

```
| Was fehlt | Zeitraum | Warum | Dringlichkeit |
|---|---|---|---|
| Kontoauszüge Sparkasse | Q1 2026 | Bank nicht abgestimmt | blockierend |
```

Dann die **E-Mail an den Mandanten**:

- Anrede passend zum bisherigen Umgang
- ein Satz zum Anlass, kein Vorwurf
- die Punkte als Liste, je Punkt eine Zeile, konkret genug zum Suchen
- eine Frist mit Begründung, warum sie so liegt
- ein Satz dazu, was passiert, wenn etwas nicht auftreibbar ist
- Grußformel

Stil: kurze Sätze, gesprochene Sprache, keine Gedankenstriche, kein
Behördendeutsch. So schreiben, wie man einem Bekannten schreibt, der einem einen
Gefallen tut.

---

## REGELN

- Keine Sammelbegriffe. „Belege für März" ist keine Anforderung, „die vier
  Tankbelege aus März" ist eine.
- Nie mehr anfordern als gebraucht wird. Jeder Punkt kostet den Mandanten Zeit.
- Wenn unklar ist, ob etwas überhaupt existiert, danach fragen statt es zu fordern.
- Keine Androhung von Konsequenzen, die die Kanzlei nicht ausspricht.
