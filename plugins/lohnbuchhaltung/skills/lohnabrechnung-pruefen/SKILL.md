---
name: lohnabrechnung-pruefen
description: Lohnabrechnung prüfen — Prüft eine Entgeltabrechnung auf Plausibilität: Steuerklasse und Freibeträge, Sozialversicherungsbeiträge gegen die Bemessungsgrenzen, Umlagen U1/U2/Insolvenzgeld, Sachbezüge und Einmalzahlungen, und meldet Abweichungen zum Vormonat. Nutzen bei Entgeltabrechnungen, Lohnjournalen oder Rückfragen von Arbeitnehmern zur Abrechnung.
---

# Lohnabrechnung prüfen

Du prüfst eine Entgeltabrechnung nach, bevor sie an den Arbeitnehmer geht oder
nachdem er sich beschwert hat.

$ARGUMENTS

---

## ARGUMENTE

- `<pfad>` — Abrechnung als PDF, oder Lohnjournal als CSV
- `--vormonat <pfad>` — Abrechnung des Vormonats für den Vergleich
- `--mandant <name>` — Arbeitgeber
- `--frage <text>` — konkrete Rückfrage des Arbeitnehmers, auf die geantwortet werden soll

---

## ABLAUF

1. **Stammdaten lesen.** Steuerklasse, Kinderfreibeträge, Konfession, Krankenkasse
   samt Zusatzbeitrag, Beitragsgruppenschlüssel, Eintrittsdatum, Befristung.
2. **Bruttoblock nachrechnen.** Laufendes Entgelt, Zuschläge, Sachbezüge,
   Einmalzahlungen. Steuer- und beitragsfreie Bestandteile getrennt halten,
   sie werden unterschiedlich behandelt.
3. **Steuerabzug plausibilisieren.** Lohnsteuer, Solidaritätszuschlag,
   Kirchensteuer. Einmalzahlungen laufen über die Jahrestabelle, nicht über
   die Monatstabelle.
4. **Sozialversicherung prüfen.** Je Zweig: Bemessungsgrundlage, Grenze,
   Beitragssatz, Arbeitnehmer- und Arbeitgeberanteil. Beitragsbemessungsgrenzen
   und Sätze ändern sich jährlich, deshalb immer die für den Abrechnungsmonat
   geltenden Werte heranziehen und im Ergebnis nennen, welche verwendet wurden.
5. **Umlagen prüfen.** U1 (Entgeltfortzahlung, nur bei umlagepflichtigen
   Betrieben), U2 (Mutterschaft, immer), Insolvenzgeldumlage.
6. **Netto nachrechnen** und mit dem ausgewiesenen Auszahlungsbetrag vergleichen.
   Abzüge nach dem Netto (Pfändung, Darlehen, Vorschuss) getrennt ausweisen.
7. **Mit dem Vormonat vergleichen**, wenn vorhanden. Jede Abweichung über 5 %
   oder 50 € braucht eine Erklärung.

---

## AUSGABE

Erst eine Übersicht:

```
| Position | Abrechnung | Nachgerechnet | Abweichung |
|---|---|---|---|
| Lohnsteuer | 412,58 € | 412,58 € | – |
| KV Arbeitnehmer | 289,40 € | 296,10 € | 6,70 € |
```

Dann je Abweichung ein Block mit **Beobachtung**, **wahrscheinlicher Ursache** und
**nächstem Schritt**. Zum Schluss, wenn `--frage` gesetzt war, eine verständliche
Antwort an den Arbeitnehmer: kurze Sätze, keine Paragrafenkette, keine
Gedankenstriche.

---

## REGELN

- Beitragssätze, Bemessungsgrenzen und Freibeträge nie aus dem Gedächtnis setzen.
  Entweder stehen sie im Beleg, oder es wird danach gefragt. Verwendete Werte immer
  mitschreiben.
- Rechenwege zeigen, damit die Lohnbuchhaltung nachvollziehen kann, woher eine
  Abweichung kommt.
- Eine Abweichung ist ein Hinweis, kein Urteil. Der Fehler kann in der Abrechnung
  liegen oder in den Stammdaten.
- Keine arbeitsrechtliche Bewertung, keine Aussage zur Wirksamkeit von Kürzungen.
