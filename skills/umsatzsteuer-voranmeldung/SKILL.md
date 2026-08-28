---
name: umsatzsteuer-voranmeldung
description: Umsatzsteuer-Voranmeldung — Bereitet die UStVA aus Buchungs- oder Summen-/Saldenlisten vor, ordnet Umsätze den ELSTER-Kennzahlen zu, plausibilisiert gegen den Vormonat und bestimmt Abgabefrist samt Dauerfristverlängerung. Nutzen bei UStVA, Voranmeldungszeitraum, Zahllast, Vorsteuerüberhang oder Kennzahlen wie 81, 86, 66, 83.
---

# Umsatzsteuer-Voranmeldung vorbereiten

Du erstellst aus den Buchungsdaten eines Mandanten den Entwurf der UStVA und
prüfst ihn auf Auffälligkeiten, bevor er in ELSTER übertragen wird.

---

## ARGUMENTE

- `--mandant <name>` — Mandant
- `--zeitraum <YYYY-MM>` oder `<YYYY-Qn>` — Voranmeldungszeitraum
- `--datei <pfad>` — Summen-/Saldenliste oder Buchungsjournal als CSV
- `--vormonat <pfad>` — Vergleichszeitraum für die Plausibilisierung (optional)
- ohne Argumente: Mandant, Zeitraum und Datenquelle erfragen

**CSV-Dateien nie komplett in den Kontext laden.** Für Filtern, Summieren und
Gruppieren die CSV-CLI des Projekts verwenden und nur die Aggregate lesen.

---

## KENNZAHLEN-MAPPING

| Kz | Inhalt |
|---|---|
| 81 | Steuerpflichtige Umsätze zu 19 % (Bemessungsgrundlage) |
| 86 | Steuerpflichtige Umsätze zu 7 % (Bemessungsgrundlage) |
| 35 / 36 | Umsätze zu anderen Steuersätzen, Bemessungsgrundlage und Steuer |
| 41 | Innergemeinschaftliche Lieferungen an Abnehmer mit USt-IdNr. |
| 43 | Weitere steuerfreie Umsätze mit Vorsteuerabzug |
| 48 | Steuerfreie Umsätze ohne Vorsteuerabzug |
| 89 / 93 | Innergemeinschaftliche Erwerbe 19 % / 7 % |
| 46 / 47 | Leistungen nach § 13b UStG, Bemessungsgrundlage und Steuer |
| 66 | Abziehbare Vorsteuer aus Rechnungen anderer Unternehmer |
| 61 | Vorsteuer aus innergemeinschaftlichen Erwerben |
| 67 | Vorsteuer aus Leistungen nach § 13b UStG |
| 62 | Entrichtete Einfuhrumsatzsteuer |
| 83 | Verbleibende Umsatzsteuer-Vorauszahlung / Überschuss |

---

## ABLAUF

### 1. Datenbasis prüfen
- Zeitraum eindeutig? Monats- oder Quartalszahler?
- Sind alle Konten enthalten, insbesondere Erlöskonten, 13b-Konten und
  Vorsteuerkonten?
- Offene Posten aus dem Vormonat, die noch umzubuchen sind?

### 2. Umsätze zuordnen
Erlöse je Steuersatz summieren, Steuerbeträge separat ausweisen und **nicht** aus
dem Bruttobetrag zurückrechnen, wenn die Steuer gebucht vorliegt. Innergemein-
schaftliche Erwerbe und 13b-Fälle erscheinen doppelt: als Steuer (Kz 89/93 bzw. 47)
und als Vorsteuer (Kz 61 bzw. 67).

### 3. Vorsteuer zuordnen
Nur Vorsteuer aus Belegen, die die Pflichtangaben erfüllen. Bei Zweifeln den Skill
`belegpruefung` vorschalten. Nicht abziehbare Vorsteuer (§ 15 Abs. 1a UStG,
Bewirtung über 70 %, Geschenke über 35 €) herausnehmen und ausweisen.

### 4. Plausibilisieren
Auffälligkeit melden, wenn:
- Umsatz gegenüber dem Vergleichszeitraum um mehr als 30 % abweicht
- die rechnerische Steuerquote nicht zum Steuersatz passt (Steuer/Netto ± 0,5 %-Punkte)
- die Vorsteuerquote (Kz 66 / Umsatz) um mehr als 20 % vom Vorzeitraum abweicht
- erstmals ein Vorsteuerüberhang entsteht (Rückfrage vom Finanzamt wahrscheinlich)
- ein 13b-Umsatz ohne korrespondierende Vorsteuer gebucht ist
- Erlöse ohne Steuer gebucht sind, ohne dass eine Befreiung dokumentiert ist

### 5. Frist bestimmen
- Grundsatz: 10. Tag nach Ablauf des Voranmeldungszeitraums
- Mit Dauerfristverlängerung: einen Monat später, bei Monatszahlern zusätzlich
  Sondervorauszahlung von 1/11 der Vorjahressteuer (Anmeldung bis 10. Februar)
- Fällt die Frist auf Samstag, Sonntag oder Feiertag, verschiebt sie sich auf den
  nächsten Werktag (§ 108 Abs. 3 AO)
- Der berechnete Termin wird immer mit dem konkreten Datum genannt

---

## AUSGABE

1. **Kennzahlen-Übersicht** als Tabelle: Kz, Bezeichnung, Betrag, Vergleichswert
   Vorzeitraum, Abweichung in Prozent.
2. **Zahllast oder Überschuss** (Kz 83) mit Rechenweg in zwei Zeilen.
3. **Auffälligkeiten** als Liste, je Punkt: Beobachtung, mögliche Ursache,
   was zu klären ist.
4. **Frist**: Abgabetermin und Zahlungstermin mit Datum, Hinweis auf
   Dauerfristverlängerung und Lastschriftmandat.
5. **Offene Punkte für den Mandanten**, falls Belege oder Angaben fehlen.

---

## REGELN

- Nichts schätzen. Fehlen Daten, wird die betroffene Kennzahl als offen markiert.
- Beträge auf volle Euro abrunden, wie ELSTER es bei Bemessungsgrundlagen erwartet;
  Steuerbeträge mit zwei Nachkommastellen.
- Keine Übertragung nach ELSTER und keine Absendung. Der Skill liefert einen
  geprüften Entwurf, freigegeben wird er von einem Berufsträger.
