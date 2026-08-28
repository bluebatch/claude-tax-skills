---
name: mandantenanfrage-beantworten
description: Mandantenanfrage beantworten — Strukturiert eine steuerliche Mandantenfrage in Sachverhalt, Rechtsgrundlage, Antwort und offene Punkte und formuliert daraus eine verständliche Antwortmail plus einen internen Prüfvermerk. Nutzen bei E-Mails oder Telefonnotizen von Mandanten, etwa zu Bewirtung, Firmenwagen, Homeoffice, Kleinunternehmerregelung oder Fristen.
---

# Mandantenanfrage beantworten

Du nimmst eine Mandantenfrage auf, ordnest sie steuerlich ein und lieferst zwei
Ergebnisse: einen internen Vermerk für die Akte und eine verständliche Antwort
an den Mandanten.

---

## ARGUMENTE

- `<text>` — die Frage direkt als Text
- `--datei <pfad>` — E-Mail, Telefonnotiz oder PDF mit der Anfrage
- `--mandant <name>` — Mandant, steuert Ansprache und bekannte Vorgeschichte
- `--nur-vermerk` — nur den internen Vermerk erzeugen, keine Antwortmail
- ohne Argumente: nach der Anfrage fragen

---

## ABLAUF

### 1. Sachverhalt herausschreiben
Was ist tatsächlich passiert, in eigenen Worten und in Stichpunkten. Getrennt
notieren:
- **gesichert**: steht so in der Anfrage
- **angenommen**: für die Antwort unterstellt, vom Mandanten zu bestätigen
- **unbekannt**: fehlt und ist entscheidungsrelevant

Wenn ein unbekannter Punkt das Ergebnis kippen kann, wird er nicht unterstellt,
sondern zur Rückfrage.

### 2. Steuerart und Frage bestimmen
Welche Steuerart ist betroffen (ESt, KSt, GewSt, USt, LSt, ErbSt)? Was ist die
eigentliche Rechtsfrage? Häufig fragt der Mandant nach dem Ergebnis ("kann ich das
absetzen?"), die Frage dahinter ist aber eine andere (Zuordnung zum Betriebs-
vermögen, Abzugsfähigkeit dem Grunde oder der Höhe nach, Zeitpunkt).

### 3. Rechtsgrundlage suchen
Konkrete Norm nennen, nicht nur das Gesetz: Paragraf, Absatz, Satz, Nummer. Wo
einschlägig zusätzlich Richtlinie, BMF-Schreiben oder BFH-Entscheidung mit
Aktenzeichen und Datum.

**Wenn du eine Fundstelle nicht sicher kennst, schreibst du das hin.** Keine
erfundenen Aktenzeichen, keine geratenen Absätze. Unsichere Fundstellen kommen mit
dem Vermerk "zu verifizieren" in die offenen Punkte.

### 4. Subsumtion
Sachverhalt unter die Norm ziehen, kurz und in ganzen Sätzen. Wenn die Rechtslage
strittig oder die Verwaltungsauffassung von der Rechtsprechung abweicht, beide
Positionen nennen und sagen, welche für den Mandanten das geringere Risiko trägt.

### 5. Betragsmäßige Auswirkung
Wenn möglich, die Auswirkung beziffern: Abzugsbetrag, Steuerersparnis, Zahllast.
Rechenweg zeigen. Steuersatz nur ansetzen, wenn er bekannt ist, sonst mit
Bandbreite arbeiten und das kenntlich machen.

---

## AUSGABE

### A) Interner Vermerk (Akte)

```
Mandant:        <name>
Datum:          <heute>
Anfrage vom:    <datum>
Steuerart:      <ESt / USt / ...>

1. Sachverhalt
   - gesichert / angenommen / unbekannt

2. Rechtsfrage

3. Rechtsgrundlage
   - Norm, Verwaltungsauffassung, Rechtsprechung

4. Würdigung

5. Ergebnis

6. Offene Punkte / zu verifizieren

7. Risiko: gering | mittel | hoch  (mit einem Satz Begründung)
```

### B) Antwort an den Mandanten

- Anrede wie in der bisherigen Korrespondenz mit dem Mandanten
- Antwort im ersten Absatz, nicht am Schluss
- Begründung in zwei bis vier Sätzen, ohne Paragrafenketten im Fließtext; höchstens
  eine Fundstelle in Klammern
- Was der Mandant konkret tun soll, als Liste
- Rückfragen gesammelt am Ende
- Kurze Sätze, keine Gedankenstriche, kein Kanzleideutsch. So schreiben, wie man
  es dem Mandanten am Telefon erklären würde.
- Abschluss: Hinweis, dass die Einschätzung auf den geschilderten Angaben beruht

---

## REGELN

- Der Vermerk darf technisch sein, die Mandantenantwort nicht.
- Keine abschließende Beratung ohne Freigabe. Beide Texte sind Entwürfe für den
  Berufsträger.
- Wenn die Anfrage außerhalb des Mandats liegt (Rechtsberatung, Sozialversicherung,
  Zoll), das sagen und auf die zuständige Stelle verweisen, statt zu improvisieren.
- Fristen, die aus der Anfrage folgen (Einspruch, Abgabe, Antrag), immer explizit
  mit Datum nennen, auch wenn der Mandant nicht danach gefragt hat.
