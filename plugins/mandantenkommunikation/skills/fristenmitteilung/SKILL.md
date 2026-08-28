---
name: fristenmitteilung
description: Fristenmitteilung — Bestimmt Abgabe- und Zahlungstermine, verschiebt sie korrekt über Wochenenden und Feiertage nach § 108 AO, berücksichtigt Dauerfristverlängerung und Fristverlängerungen und schreibt daraus eine Mitteilung an den Mandanten. Nutzen bei Abgabefristen, Zahlungsterminen, Mahnungen oder wenn ein Termin zu kippen droht.
---

# Fristen bestimmen und mitteilen

Du rechnest einen Termin aus, prüfst, ob er hält, und sagst dem Mandanten
rechtzeitig Bescheid.

$ARGUMENTS

---

## ARGUMENTE

- `--art <text>` — Umsatzsteuer-Voranmeldung, Jahreserklärung, Lohnsteueranmeldung, Zahlung, Einspruch
- `--zeitraum <YYYY-MM>` oder `<YYYY>` — betroffener Zeitraum
- `--mandant <name>` — Mandant
- `--bundesland <text>` — für Feiertage, die nicht bundeseinheitlich sind
- `--dauerfrist` — Dauerfristverlängerung liegt vor

---

## ABLAUF

1. **Fristart bestimmen.** Abgabefrist, Zahlungsfrist und Rechtsbehelfsfrist laufen
   unterschiedlich und dürfen nicht vermischt werden.
2. **Grundtermin berechnen** aus Zeitraum und Fristart.
3. **Verlängerungen anwenden**, soweit sie vorliegen: Dauerfristverlängerung bei der
   Voranmeldung, verlängerte Fristen bei Beratung, gewährte Einzelverlängerungen.
4. **Auf Werktag schieben.** Fällt das Ende auf Samstag, Sonntag oder einen
   gesetzlichen Feiertag, endet die Frist am nächsten Werktag (§ 108 Abs. 3 AO).
   Feiertage sind teilweise Ländersache, deshalb das Bundesland beachten. Ist es
   nicht bekannt, danach fragen.
5. **Schonfrist getrennt behandeln.** Eine Zahlungsschonfrist ist keine
   Fristverlängerung und gilt nicht bei Barzahlung.
6. **Vorlaufzeit rückrechnen.** Wann müssen die Unterlagen in der Kanzlei sein,
   damit der Termin zu halten ist.
7. **Risiko benennen**, wenn der Termin bereits eng ist.

---

## AUSGABE

```
| Vorgang | Zeitraum | Frist | verschoben auf | Unterlagen bis |
|---|---|---|---|---|
| UStVA | 03/2026 | 10.04.2026 | 13.04.2026 (Karfreitag) | 07.04.2026 |
```

Darunter je Termin ein Satz zur Rechtsgrundlage der Verschiebung, dann die
**Mitteilung an den Mandanten**: welcher Termin, was bis wann von ihm gebraucht
wird, was passiert, wenn es nicht kommt. Sachlich, kurz, keine Gedankenstriche.

---

## REGELN

- Termine immer mit Wochentag ausgeben, das fängt die meisten Fehler ab.
- Verschiebung nie stillschweigend, sondern mit dem Grund (Feiertag, Wochenende,
  Verlängerung).
- Keine Aussage zu Fristen, die von einer Bekanntgabe abhängen, ohne das
  Bekanntgabedatum. Danach fragen.
- Säumniszuschläge und Verspätungszuschläge nicht beziffern, nur als Folge benennen.
- Die Fristenkontrolle der Kanzlei bleibt maßgeblich, das hier ist eine Rechenhilfe.
