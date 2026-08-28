---
name: reisekosten-abrechnen
description: Reisekosten abrechnen — Rechnet eine Dienstreise ab: Verpflegungsmehraufwand nach Abwesenheitsdauer, Kürzung bei gestellten Mahlzeiten, Übernachtung, Fahrtkosten und Kilometerpauschale, Auslandspauschalen und die Dreimonatsfrist. Nutzen bei Reisekostenabrechnung, Spesen, Verpflegungspauschale oder Fahrtkostenerstattung.
---

# Reisekosten abrechnen

Du rechnest eine Dienstreise ab und trennst dabei sauber, was steuerfrei erstattet
werden kann und was nicht.

$ARGUMENTS

---

## ARGUMENTE

- `<pfad>` — Reisekostenformular, Belege oder Kalenderauszug
- `--mandant <name>` — Arbeitgeber
- `--ausland <land>` — Auslandsreise, dann gelten Länderpauschalen
- `--mahlzeiten <text>` — vom Arbeitgeber gestellte Mahlzeiten je Tag

---

## ABLAUF

1. **Reise abgrenzen.** Beginn und Ende, erste Tätigkeitsstätte, Zwischenziele.
   Ohne erste Tätigkeitsstätte gelten andere Regeln, das zuerst klären.
2. **Abwesenheitsdauer je Kalendertag** ermitteln. Bei mehrtägigen Reisen zählen
   An- und Abreisetag unabhängig von der Stundenzahl.
3. **Verpflegungspauschale ansetzen.** Inland nach Abwesenheitsdauer, Ausland nach
   Länder- und Ortspauschale. Die geltenden Beträge nicht aus dem Gedächtnis
   setzen, sondern aus der für das Reisejahr veröffentlichten Tabelle nehmen und
   im Ergebnis nennen, welche verwendet wurde.
4. **Mahlzeiten kürzen.** Vom Arbeitgeber gestellte Frühstücke, Mittag- und
   Abendessen kürzen die Tagespauschale anteilig, auch wenn sie in der
   Hotelrechnung stecken.
5. **Übernachtung.** Tatsächliche Kosten gegen Beleg. Frühstücksanteil
   herausrechnen. Keine Pauschale bei Übernachtung im eigenen Fahrzeug.
6. **Fahrtkosten.** Öffentliche Verkehrsmittel gegen Beleg, eigener Pkw über die
   Kilometerpauschale, Firmenwagen gar nicht.
7. **Dreimonatsfrist prüfen.** Bei längerer Tätigkeit an derselben auswärtigen
   Stelle entfällt die Verpflegungspauschale nach drei Monaten.
8. **Nebenkosten** einzeln erfassen: Parken, Maut, Gepäck, beruflich veranlasste
   Telefonate.

---

## AUSGABE

```
| Tag | Abwesenheit | Pauschale | Kürzung Mahlzeiten | Ansatz |
|---|---|---|---|---|
| 12.03. Anreise | 9 h | 14,00 € | Abendessen −5,60 € | 8,40 € |
```

Danach ein Block je Kostenart mit Summe, dann:

- **Steuerfrei erstattbar:** Betrag
- **Steuerpflichtig, weil …:** Betrag mit Begründung
- **Fehlende Belege:** Liste, was der Mitarbeiter noch nachreichen muss

---

## REGELN

- Pauschbeträge, Kürzungssätze und Kilometersätze immer aus der Tabelle des
  Reisejahres, nie aus dem Gedächtnis. Verwendete Werte ausweisen.
- Gestellte Mahlzeiten nicht übersehen: sie stecken oft unbemerkt in der
  Hotelrechnung.
- Fehlt ein Beleg, wird nicht geschätzt. Der Posten wird als offen ausgewiesen.
- Ergebnis ist ein Abrechnungsentwurf, kein Nachweis gegenüber dem Finanzamt.
