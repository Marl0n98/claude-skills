---
name: divergence
description: >-
  Verweigert generische KI-Ideen. Erzeugt nicht-offensichtliche kreative Winkel für Content, Ads,
  Kampagnen, Hooks, Videos, Posts und Positionierung, indem es die eigenen ersten Entwürfe angreift
  und Reframes erzwingt. Nutzen beim Brainstormen, Ideensammeln oder wenn nach Winkeln, Konzepten
  oder Ideen gefragt wird, besonders wenn die ersten Ideen offensichtlich, sicher oder wie etwas
  klingen, das jede KI sagen würde. Auslösen mit /divergence, "gib mir Winkel zu X", "brainstorm X",
  "Ideen für X", "Angles für X" oder "mach das weniger generisch".
---

# Divergence: die Anti-Slop-Schicht für *Ideen*

Das meiste KI-Brainstorming ist Slop. Frag nach zehn Ideen und du bekommst die zehn statistisch offensichtlichsten, dieselben zehn, die die KI von allen anderen auch ausgespuckt hat. Das ist keine Ideenfindung, das ist Autovervollständigung.

Divergence löst das mit einem einzigen Zug: **generieren, dann den eigenen Output angreifen, dann alles reframen, was durchfällt.** Nie den ersten Entwurf abgeben.

> Der `humanizer`-Skill bereinigt *Sprache*. Divergence greift *Ideen* an. Zwei verschiedene Jobs. Beide nutzen.

## Die Regel, die alles trägt

**Dem Nutzer nie eine Liste von Formaten oder Beispiel-Winkeln zur Auswahl zeigen.** Beispiele im Prompt werden zur Decke, nicht zum Boden. In dem Moment, in dem du anbietest "du könntest ein Listicle, ein Vorher/Nachher oder ein Testimonial machen", hast du das Denken auf das begrenzt, was es schon gibt.

Wenn du dich dabei ertappst, nach "du könntest versuchen…" zu greifen oder ein bekanntes Format aus dem Gedächtnis zu ziehen: Stopp. Das ist die Slop-Falle.

---

## Prozess

### Schritt 1: Kandidaten mit vollem Spielraum erzeugen

Erzeuge 10 Kandidaten-Winkel zum Thema. Nutze jeden Kontext, den du hast: die Marke, die Zielgruppe, das Produkt, die Daten, das, was tatsächlich wahr ist. **Null Beispiel-Formate. Keine Genre-Listen. Kein "hier sind ein paar beliebte Ansätze".**

Wenn `brand.json` in diesem Skill-Ordner existiert und ausgefüllt ist, lade sie. Echter Markenkontext macht die Winkel schärfer. Ist sie leer, arbeite mit dem Thema und dem, was der Nutzer dir gesagt hat. Nicht daran aufhalten.

### Schritt 2: Jeden Kandidaten gegen den Slop-Boden prüfen

Jeder Kandidat läuft durch diese Liste. Jeder Treffer bekommt das Tag `slop`:

- Ist es ein Talking-Head-Testimonial? → **slop**
- Ist es ein Vorher/Nachher? → **slop**
- Ist es ein Listicle ("3 Dinge, die ich gern früher gewusst hätte")? → **slop**
- Beginnt es mit "POV:" / "Stell dir vor" / "Hast du dich je gefragt" / "Wusstest du"? → **slop**
- **Könnte genau dieser Winkel von jedem Wettbewerber in der Kategorie stammen?** → **slop** (das ist der schärfste Test, am härtesten anwenden)
- Stützt es sich auf einen abgenutzten Trope: "Morgenroutine", "Was ist in meiner Tasche", "Get ready with me", "Ein Tag in meinem Leben"? → **slop**
- Taucht die Marke/das Produkt auf, bevor die Zielgruppe irgendetwas von Wert bekommen hat? → **slop**
- Ist es Aspirational Lifestyle, der leise signalisiert "das wirst du nie haben"? → **slop**
- Behauptet es ein Ergebnis ohne jede Spezifik? → **slop**
- Wäre diese Idee jedem genauso offensichtlich gewesen, der 15 Sekunden über das Thema nachgedacht hat? → **slop**

Sei gnadenlos. Die meisten Erstentwurf-Kandidaten *sind* Slop. Das ist erwartbar und genau der Punkt.

### Schritt 3: Reframes für alles Getaggte erzwingen

Für jeden Slop-Kandidaten 3 Reframes mit diesen Transformationen erzeugen. Das sind **Regeln zum Anwenden**, keine Beispiele zum Kopieren:

- **Inversion**: die Annahme umdrehen. Wenn die offensichtliche Version sagt "so machst du es", sagt die invertierte "deshalb funktioniert das, was du bisher machst, tatsächlich, und wann nicht".
- **Kontra**: die unpopuläre Position vertreten. Wenn alle bei X einig sind, finde den echten Fall, in dem X falsch ist.
- **Fachfremde Metapher**: das Thema mit einem völlig anderen Feld verbinden. Architektur, Wetter, Kochen, Musik, Sprache, Sport. In der Kollision steckt die Idee.
- **Spezifik-Bohrung**: statt zu verallgemeinern, in einen ultra-spezifischen Fall bohren, den die Zielgruppe sofort wiedererkennt. Je enger, desto mehr Leute fühlen sich gesehen.
- **Direkter Blickkontakt**: aufhören zu senden. Schreiben, als würdest du mit einer konkreten Person sprechen, die du vor Augen hast, über etwas, das nur sie bemerken würde.

Reframes müssen nicht perfekt sein. Sie müssen das Muster brechen und dem Nutzer echtes Material geben.

### Schritt 4: Ehrlich bewerten und streichen

Jeden Kandidaten und jeden Reframe auf drei Achsen mit 1 bis 10 bewerten:

- **Slop-Resistenz**: wie unähnlich ist das generischem KI-Output, wirklich?
- **Passung**: funktioniert das tatsächlich für diese Marke, Zielgruppe und dieses Produkt?
- **Spezifik**: steckt eine echte, konkrete Beobachtung drin, oder ist es eine Form ohne Inhalt?

**Alle drei müssen 6 oder höher sein.** Ein Winkel mit 9 bei Spezifik und 4 bei Passung ist tot. Streichen. Nach dem *niedrigsten* der drei Werte ranken, nicht nach dem Durchschnitt. Eine großartige Idee, die auf einer Achse durchfällt, ist eine schlechte Idee.

Die Top 3 zurückgeben.

### Schritt 5: Die Emotion benennen

Jeder Winkel muss eine dieser Emotionen auslösen, und du musst benennen können, welche:

**Wiedererkennung** ("das bin ich") · **Neugier** (ein offener Loop) · **stille Bestätigung** ("ich war nicht verrückt") · **leichte Überraschung** (eine kleine Umkehr) · **geteilte Beschwerde** ("endlich sagt es mal jemand") · **Spannung** (etwas steht auf dem Spiel)

Wenn du die Emotion nicht benennen kannst, ist der Winkel nicht fertig. Zurück.

---

## Output-Format

```markdown
# Divergence: {Thema}

## Top 3 Winkel

### 1. {kurzer Name}
**Der Winkel:** {ein oder zwei Sätze}
**Warum es nicht generisch ist:** {ein Satz, konkret}
**Emotion:** {Wiedererkennung / Neugier / stille Bestätigung / leichte Überraschung / geteilte Beschwerde / Spannung}
**Werte:** Slop-Resistenz {n}/10 · Passung {n}/10 · Spezifik {n}/10

### 2. {...}
### 3. {...}

## Gestrichen (der Prüfpfad)
- {Kandidat}: {warum es Slop war}
- {Kandidat}: {warum es Slop war}
```

**Immer die Streichliste zeigen.** Sie beweist, dass die Arbeit passiert ist, und verhindert, dass der Nutzer Ideen erneut vorschlägt, die du schon verworfen hast.

---

## Harte Regeln

1. **Keine Format-Hinweise beim Generieren.** Marke, Zielgruppe, Thema, Wahrheit. Sonst nichts. Nie "hier sind ein paar Formate zum Überlegen".
2. **Selbstangriff vor dem Output.** Nie einen Kandidaten zurückgeben, der nicht durch den Slop-Boden gelaufen ist.
3. **Alle drei Werte ≥ 6.** Keine Ausnahmen. Nach dem Minimum ranken, nicht nach dem Durchschnitt.
4. **Emotion benennen oder es ist nicht fertig.**
5. **Streichliste zeigen.**
6. **Die fünf Transformationen nutzen.** Keine neuen mitten im Lauf erfinden.

## Was dieser Skill nicht tut

- Er schreibt nicht das fertige Skript, den Post oder die Ad. Er liefert den *Winkel*. Den Winkel an `script-writing` (Videoskripte) oder an den `humanizer` (Text) weitergeben, um ihn auszuformulieren.
- Er repariert keine Sprache. Das macht der `humanizer`.
- Er hält keine Bibliothek "guter Formate". So eine Bibliothek gibt es hier absichtlich nicht.

## Optional: Markenkontext

`brand.json` in diesem Ordner ist optional. Ausgefüllt werden die Winkel spürbar schärfer, weil der Skill nicht mehr raten muss, mit wem du sprichst. Leer gelassen funktioniert er trotzdem mit dem, was du ihm im Chat sagst.
