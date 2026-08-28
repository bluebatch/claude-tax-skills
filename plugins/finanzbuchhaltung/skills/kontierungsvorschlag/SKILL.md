---
name: kontierungsvorschlag
description: Kontierungsvorschlag — Schlägt zu Belegen oder Buchungszeilen die Konten nach SKR03 oder SKR04 vor, samt Steuerschlüssel und Begründung, und markiert alles, was ohne Rücksprache nicht entschieden werden kann. Nutzen beim Vorkontieren von Eingangs- und Ausgangsrechnungen, Kassenbelegen oder Kontoauszügen.
---

# Kontierungsvorschlag nach SKR03 / SKR04

Du kontierst Belege vor. Das Ergebnis geht in die Buchhaltung, nicht direkt in
die Bilanz: Jede Zeile muss von einem Buchhalter abgenommen werden können.

$ARGUMENTS

---

## ARGUMENTE

- `<pfad>` — Beleg, Belegordner oder CSV mit Buchungszeilen
- `--kontenrahmen <skr03|skr04>` — Kontenrahmen, ohne Angabe nachfragen
- `--mandant <name>` — Mandant, steuert bekannte Dauerbuchungen
- `--branche <text>` — Branche, wenn sie die Kontenwahl beeinflusst

---

## ABLAUF

1. **Kontenrahmen klären.** SKR03 und SKR04 haben unterschiedliche Nummern für
   dieselbe Sache. Ohne Angabe nicht raten, sondern fragen.
2. **Geschäftsvorfall bestimmen.** Was wurde geliefert oder geleistet, an wen,
   wofür. Der Belegtext allein reicht oft nicht, der Betrag und der
   Zahlungsweg helfen.
3. **Konto vorschlagen.** Aufwands- oder Ertragskonto, Gegenkonto (Bank, Kasse,
   Verbindlichkeiten), Steuerschlüssel.
4. **Sonderfälle erkennen** (siehe unten) und getrennt ausweisen.
5. **Ausgeben** als Tabelle plus Rückfragenliste.

---

## SONDERFÄLLE, DIE NIE STILL DURCHLAUFEN

| Fall | Warum |
|---|---|
| Bewirtung | 70 / 30 aufteilen, Eigenbeleg und Anlass nötig |
| Geschenke | Grenze je Empfänger und Jahr, darüber nicht abziehbar |
| Reisekosten | Verpflegungspauschale ist kein Vorsteuerfall |
| Pkw-Kosten | Privatanteil, Fahrtenbuch oder Ein-Prozent-Regel |
| Anschaffung über der GWG-Grenze | Anlagevermögen statt Aufwand |
| Reverse Charge, innergemeinschaftlicher Erwerb | eigener Steuerschlüssel, kein Vorsteuerabzug ohne Gegenbuchung |
| Privatentnahme, Gesellschafterkonto | nie als Betriebsausgabe |
| Kaution, Anzahlung, durchlaufender Posten | kein Aufwand |

---

## AUSGABE

```
| Beleg | Datum | Betrag | Soll | Haben | Steuerschlüssel | Sicherheit |
|---|---|---|---|---|---|---|
| RE-0412 | 14.03.2026 | 1.428,00 € | 4930 Bürobedarf | 1600 Verbindlichkeiten | VSt 19 % | sicher |
```

`Sicherheit` ist `sicher`, `plausibel` oder `offen`. Alles unter `sicher` bekommt
darunter eine Zeile mit der konkreten Frage, die den Fall entscheidet.

---

## REGELN

- Kontonummer **und** Kontobezeichnung nennen, sonst ist der Vorschlag nicht prüfbar.
- Bei `offen` keinen Vorschlag erzwingen. Eine ehrliche Rückfrage ist billiger als
  eine stille Fehlbuchung.
- Keine Kontonummer erfinden. Ist die passende Nummer nicht bekannt, den
  Kontenzweck beschreiben und nachfragen.
- Der Vorschlag ersetzt keine Buchung durch einen Berufsträger.
