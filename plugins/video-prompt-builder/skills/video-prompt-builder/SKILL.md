---
name: video-prompt-builder
description: >-
  Erstellt detaillierte Shot-für-Shot-Videoprompts für Seedance 2.0 aus einem Creative Brief. Nutze
  diesen Skill immer, wenn der Nutzer einen Videoprompt erstellen, eine Shotlist schreiben, eine
  Videosequenz planen, ein Videokonzept für KI-Generierung beschreiben will oder Seedance erwähnt.
  Auch auslösen, wenn der Nutzer eine Szene, ein Werbekonzept, einen Brand Film, ein Produktvideo
  oder irgendeine visuelle Sequenz beschreibt, die in strukturierte Prompts übersetzt werden soll,
  selbst wenn er nicht ausdrücklich "Videoprompt" sagt. Trigger sind Sätze wie "schreib mir einen
  Videoprompt", "Seedance-Prompt", "Shotlist", "plan ein Video", "Videokonzept", "erstell eine
  Sequenz", "Brand-Film-Prompt", "Ad-Prompt" oder jedes Mal, wenn der Nutzer beschreibt, was in
  einem Video passieren soll, und das in generierungsfertige Prompts übersetzt werden muss.
---

# Video Prompt Builder für Seedance 2.0

Baut cineastische Shot-für-Shot-Videoprompts aus einem Creative Brief. Jeder Output folgt einem festen Effekt-Breakdown-Format, das Seedance 2.0 maximale Details zu Kameraarbeit, Effekten, Übergängen, Tempo und Energiebogen liefert.

## So funktioniert der Skill

1. Der Nutzer liefert einen **Creative Brief**. Das kann so knapp sein wie "ein Läufer im Stadion für eine Werbung im Nike-Stil" oder so ausführlich wie eine komplette Storyboard-Beschreibung. Dazu können ein Referenzvideo, eine Stimmung, Markenkontext oder konkrete gewünschte Effekte kommen.
2. Lies die Referenzdatei unter `references/effects-breakdown-reference.txt`, um Struktur und Detailtiefe zu verinnerlichen.
3. Erzeuge einen vollständigen Videoprompt als reinen Text, gegliedert in die vier Pflichtabschnitte unten.

## Erwarteter Input

Der Brief kann eine beliebige Kombination davon enthalten:
- Beschreibung von Subjekt/Talent (wer oder was ist im Bild)
- Setting/Umgebung
- Stimmung, Ton, Energielevel
- Marken- oder Produktkontext
- Konkrete Effekte oder Kamerabewegungen
- Ziel-Dauer
- Verweise auf bestehende Werbungen, Filme oder visuelle Stile
- Farbpalette oder Grading-Wünsche

Ist der Brief zu vage für einen vollständigen Prompt (z.B. "mach irgendwas Cooles"), stell genau eine gezielte Rückfrage, bevor du loslegst. Nicht ausfragen: Arbeite mit dem, was da ist, und triff kreative Entscheidungen, wo der Nutzer nichts vorgegeben hat.

## Output-Struktur

Gib IMMER ALLE VIER Abschnitte in genau dieser Reihenfolge aus. Nie einen Abschnitt auslassen.

### Abschnitt 1: SHOT-FÜR-SHOT EFFEKT-TIMELINE

Das ist der Kern des Prompts. Jeder Shot bekommt einen eigenen Block nach diesem Muster:

```
SHOT [N] ([Zeitstempel]) — [Shot-Name / Beschreibung]
• EFFEKT: [Primärer Effekt] + [weitere Effekte, falls gestapelt]
• [Detaillierte Beschreibung, was visuell passiert]
• [Kameraverhalten: Winkel, Bewegung, ggf. Objektiv]
• [Geschwindigkeit/Timing]
• [Wie dieser Shot in den nächsten übergeht: Übergangstyp]
```

Richtlinien für die Shots:
- Jeder Shot dauert 1 bis 4 Sekunden, außer der Brief verlangt längere Halte
- Effekte präzise benennen: "Speed Ramp (Verlangsamung)" statt nur "Speed Ramp"; "Digitalzoom (Scale-in)" statt nur "Zoom"
- Gestapelte Effekte ausdrücklich beschreiben: Passieren drei Dinge gleichzeitig, alle drei auflisten
- Übergangslogik einbauen: Wie geht dieser Shot RAUS und wie kommt der nächste REIN?
- Sprache verwenden, die Seedance 2.0 interpretieren kann: das visuelle Ergebnis beschreiben, nicht die Technik im Schnittprogramm. Also "das Bild skaliert schnell nach innen" statt "keyframed Scale-Effekt in After Effects anwenden"
- Den wirkungsvollsten oder markantesten Shot mit einem Hinweis wie "Das ist der SIGNATURE VISUAL EFFECT" markieren
- Bei Slow-Motion konkrete Prozentwerte nennen (z.B. "etwa 20 bis 25 % Geschwindigkeit")
- Motion Blur, Lichtverhalten und atmosphärische Effekte beschreiben, wo relevant

### Abschnitt 2: MASTER-EFFEKT-INVENTAR

Eine nummerierte Liste jedes einzelnen Effekts im gesamten Prompt, mit:
- Effektname
- Wie oft er vorkommt (z.B. "3x verwendet")
- In welchen Shots er auftaucht
- Ein Satz zu seiner Rolle im Schnitt

Dieser Abschnitt zeigt dem Nutzer (und dem Generator) die komplette Technik-Palette auf einen Blick. Ähnliche Effekte gruppieren. Typische Kategorien: Geschwindigkeitsmanipulation, Kamerabewegung, digitale Effekte, Übergänge, Compositing, optische Effekte.

### Abschnitt 3: EFFEKT-DICHTE-KARTE

Die Timeline in Segmente aufteilen (etwa 3 bis 6 Sekunden) und jedes bewerten als:
- **HOHE DICHTE**: 4+ Effekte gestapelt oder in schneller Folge
- **MITTLERE DICHTE**: 2 bis 3 Effekte
- **NIEDRIGE DICHTE**: 1 Effekt oder sauberes, einfaches Material

Format:
```
[Zeitbereich] = [DICHTE-LEVEL] ([kurze Effektliste] — [Anzahl] Effekte in [Dauer])
```

### Abschnitt 4: ENERGIEBOGEN

Die Energiestruktur des Videos als erzählerischen Bogen beschreiben. Die Referenz nutzt ein Drei-Akt-Modell:
- **Akt 1**: Eröffnungsenergie, wie das Video Aufmerksamkeit greift
- **Akt 2**: Mittelteil, wie es sich entwickelt und was die Signature-Momente sind
- **Akt 3**: Auflösung, wie die Energie sich auflöst und landet

Die Anzahl der Akte an Länge und Struktur des Videos anpassen. Ein 5-Sekunden-Clip braucht vielleicht nur zwei Beats, ein 30-Sekunden-Brand-Film vier.

## Kreative Prinzipien

Diese Prinzipien leiten jeden Prompt:

1. **Kontrast erzeugt Wirkung.** Momente mit hoher und niedriger Dichte abwechseln. Ein Slow-Motion-Shot nach einem Speed Ramp trifft härter als zwei Speed Ramps hintereinander.
2. **Signature-Momente zählen.** Jedes Video braucht mindestens einen "Hero"-Effekt, etwas visuell Eigenständiges, das hängen bleibt. Ausdrücklich benennen.
3. **Übergänge sind Shots.** Übergänge nicht als Wegwerf-Verbindungen behandeln. Ein Whip Pan, ein Bloom Flash, ein Motion-Blur-Schmier: Das sind kreative Momente, keine bloßen Schnitte.
4. **Konkret statt vage.** "Das Bild rotiert im Uhrzeigersinn um etwa 15 bis 20°" ist besser als "die Kamera kippt". "Etwa 20 bis 25 % Geschwindigkeit" ist besser als "Slow Motion".
5. **Energie muss sich auflösen.** Egal wie intensiv der Anfang, das Video muss landen. Die letzten Momente sollen gewollt wirken, nicht so, als wäre das Effektbudget aufgebraucht.

## Ton und Stil

- Direkt und technisch schreiben, wie Shot-Notizen eines Regisseurs, nicht wie ein Marketing-Brief
- Innerhalb jedes Shot-Blocks Aufzählungspunkte für Klarheit nutzen
- Knapp, aber vollständig: Jedes Detail muss sich seinen Platz verdienen
- Keine Hype-Sprache, kein "atemberaubend" oder "beeindruckend". Beschreiben, was passiert, und die Bilder sprechen lassen

## Kalibrierung nach Dauer

Anzahl der Shots und Effektdichte an die Ziel-Dauer anpassen:
- **5 bis 10 Sekunden**: 4 bis 7 Shots, schlank und knackig, 1 Signature-Effekt
- **10 bis 20 Sekunden**: 8 bis 14 Shots, Raum für Kontrast und Aufbau, 1 bis 2 Signature-Effekte
- **20 bis 30 Sekunden**: 12 bis 20 Shots, voller Drei-Akt-Bogen, 2 bis 3 Signature-Effekte
- **30+ Sekunden**: Entsprechend skalieren, aber den Dichte-Kontrast halten. Nicht jede Sekunde mit Effekten füllen

Nennt der Nutzer keine Dauer, sind 15 bis 20 Sekunden der Standard (ein guter Bereich für KI-Videogenerierung).

## Beispiel-Workflow

**Der Nutzer sagt:** "Ich will einen dramatischen Brand Film für einen Trailrunning-Schuh. Berge, goldene Stunde, ein einzelner Läufer. Soll episch wirken, aber nicht übertrieben. Etwa 15 Sekunden."

**Du machst:**
1. `references/effects-breakdown-reference.txt` lesen, um die Detailtiefe zu kalibrieren
2. Den vollständigen Vier-Abschnitt-Output erzeugen: Shot-für-Shot-Timeline (8 bis 12 Shots), Master-Effekt-Inventar, Dichte-Karte und Energiebogen
3. Als reinen Text im Chat ausgeben
