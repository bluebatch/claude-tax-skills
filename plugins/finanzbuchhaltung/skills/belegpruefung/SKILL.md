---
name: belegpruefung
description: Belegprüfung — Prüft Eingangs- und Ausgangsrechnungen auf die Pflichtangaben nach § 14 UStG, erkennt fehlende oder unplausible Angaben (Steuernummer, Leistungszeitpunkt, Steuersatz, Reverse-Charge) und formuliert eine Rückfrage an den Mandanten. Nutzen, wenn Rechnungen, Belege oder Kassenbelege auf Vorsteuerabzugsfähigkeit geprüft werden sollen.
---

# Belegprüfung — Rechnungen nach § 14 UStG

Du prüfst Belege daraufhin, ob sie zum Vorsteuerabzug berechtigen, und meldest
zurück, was fehlt.

$ARGUMENTS

---

## ARGUMENTE

- `<pfad>` — einzelner Beleg (PDF, Bild) oder Ordner mit Belegen
- `--mandant <name>` — Mandant, für den geprüft wird (steuert Ansprache der Rückfrage)
- `--kleinbetrag` — Beleg als Kleinbetragsrechnung (bis 250 € brutto) behandeln
- ohne Argumente: fragen, welcher Beleg oder Ordner geprüft werden soll

---

## PFLICHTANGABEN (§ 14 Abs. 4 UStG)

Für jeden Beleg prüfen:

1. Vollständiger Name und Anschrift des leistenden Unternehmers
2. Vollständiger Name und Anschrift des Leistungsempfängers
3. Steuernummer **oder** USt-IdNr. des Leistenden
4. Ausstellungsdatum
5. Fortlaufende, einmalig vergebene Rechnungsnummer
6. Menge und handelsübliche Bezeichnung der Lieferung / Art und Umfang der Leistung
7. Zeitpunkt der Lieferung oder Leistung (bzw. Leistungsmonat)
8. Nach Steuersätzen aufgeschlüsseltes Entgelt, jede Minderung im Voraus vereinbart
9. Anzuwendender Steuersatz und darauf entfallender Steuerbetrag **oder** Hinweis
   auf eine Steuerbefreiung

**Kleinbetragsrechnung bis 250 € brutto (§ 33 UStDV):** es genügen Name und
Anschrift des Leistenden, Ausstellungsdatum, Menge/Bezeichnung, Bruttobetrag und
Steuersatz bzw. Hinweis auf die Steuerbefreiung.

**Zusätzliche Pflichthinweise, wenn einschlägig:**

| Fall | Erwarteter Hinweis |
|---|---|
| Reverse Charge (§ 13b UStG) | "Steuerschuldnerschaft des Leistungsempfängers" + USt-IdNr. beider Seiten |
| Innergemeinschaftliche Lieferung | "Steuerfreie innergemeinschaftliche Lieferung" + beide USt-IdNr. |
| Gutschrift | Ausdrücklich "Gutschrift" |
| Differenzbesteuerung (§ 25a) | "Gebrauchtgegenstände/Sonderregelung", kein gesonderter USt-Ausweis |
| Bauleistung an Privatperson | Hinweis auf Aufbewahrungspflicht (§ 14b Abs. 1 S. 5 UStG) |

---

## ABLAUF

0. **Bei mehr als einem Beleg aufteilen.** Für jeden Beleg im Ordner einen
   eigenen Aufruf des Subagenten `finanzbuchhaltung:beleg-pruefer` starten, alle
   parallel. Jeder Agent liest genau einen Beleg und gibt einen kompakten
   Prüfblock zurück. Grund: Ein Stapel von zweihundert Scans passt nicht in einen
   Kontext, und ein unlesbarer Beleg soll die übrigen nicht mitreißen. Die Blöcke
   sammelst du ein und baust daraus die Ausgabe unten. Bei einem einzelnen Beleg
   lohnt der Umweg nicht, dann selbst prüfen.
1. **Beleg lesen.** PDF oder Bild öffnen und die neun Pflichtangaben einzeln
   heraussuchen. Nichts raten: was nicht lesbar ist, gilt als "unklar", nicht als
   "fehlt".
2. **Rechnerisch prüfen.** Netto + Steuerbetrag = Brutto. Steuerbetrag =
   Netto × Steuersatz. Abweichungen über 0,02 € melden.
3. **Plausibilität prüfen.**
   - Steuersatz passt zur Leistung (7 % nur bei Katalog des § 12 Abs. 2 UStG)
   - Leistungszeitpunkt liegt nicht nach dem Rechnungsdatum
   - Leistungsempfänger ist tatsächlich der Mandant, nicht eine Privatperson
   - Bei Reverse Charge: kein zusätzlicher Umsatzsteuerausweis
4. **Einordnen.** Jeder Beleg bekommt genau einen Status:
   - `ok` — alle Pflichtangaben vorhanden, Vorsteuerabzug möglich
   - `mangel` — Pflichtangabe fehlt oder ist falsch, Rechnungskorrektur nötig
   - `unklar` — Beleg nicht ausreichend lesbar oder Sachverhalt offen
5. **Ausgeben** (siehe unten).

---

## AUSGABE

Erst eine Tabelle über alle geprüften Belege:

```
| Beleg | Datum | Betrag brutto | Status | Fehlende Angabe |
|---|---|---|---|---|
| RE-2026-0412.pdf | 14.03.2026 | 1.428,00 € | mangel | Leistungszeitpunkt fehlt |
```

Danach je Beleg mit Status `mangel` oder `unklar` ein kurzer Block:

- **Was fehlt:** konkrete Pflichtangabe mit Fundstelle (z. B. § 14 Abs. 4 Nr. 6 UStG)
- **Folge:** ob der Vorsteuerabzug daran scheitert oder nur formell nachzubessern ist
- **Nächster Schritt:** Rechnungskorrektur anfordern, Nachweis nachreichen oder Rücksprache

Zum Schluss eine sammelnde **Rückfrage an den Mandanten** als fertiger E-Mail-Text:
locker und knapp formuliert, keine Gedankenstriche, alle offenen Punkte als Liste,
mit Belegnummer und Datum, damit der Mandant sie zuordnen kann.

---

## REGELN

- Keine Aussage ohne Beleg im Dokument. Steht die Steuernummer nicht drauf, ist sie
  nicht da, auch wenn der Lieferant bekannt ist.
- Zweifelsfälle nicht wegentscheiden, sondern als `unklar` mit konkreter Frage melden.
- Keine abschließende steuerliche Beurteilung. Das Ergebnis ist ein Prüfvermerk für
  den Berufsträger.
- Beträge immer in der Belegwährung mit zwei Nachkommastellen.
