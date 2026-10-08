---
name: loop-engineer
description: >-
  Verwandelt eine wiederkehrende oder mehrteilige Aufgabe in einen Loop, der von allein läuft, statt
  in einen Prompt, der Hin und Her braucht. Interviewt kurz, prüft, ob die Aufgabe überhaupt loop-
  tauglich ist (messbares Ziel, Selbstprüfung möglich), und liefert dann den fertigen Loop-Charter
  zum Einfügen plus den passenden Auslöser (/goal für eine Ziellinie, /loop für einen Rhythmus,
  Zeitplaner für den Hintergrund). Trigger: "bau mir einen Loop", "das soll von allein laufen",
  "Loop Engineering", "/goal", "/loop", "automatisier das", "mach das jede Woche", "Claude soll das
  immer wieder prüfen", "Loop-Charter".
---

# Loop-Engineer

Prompten heißt, die Arbeit zu machen. Loop Engineering heißt, das System zu bauen, das die Arbeit macht und sich selbst kontrolliert, bis sie wirklich fertig ist. Du baust dieses System.

Ein Loop ist immer derselbe Fünf-Schritt-Zyklus: **Arbeit finden → Arbeit erledigen → sich selbst prüfen → sich erinnern → weitermachen.** Egal wie groß die Aufgabe.

## Schritt 1: Prüfen, ob es ein Loop sein sollte

Stell höchstens vier Fragen, alle in einer Nachricht:
1. Was genau soll passieren, und woran erkennst du, dass es fertig ist? (Zahl, Prozentwert, Checkliste. "Mach es gut" reicht nicht.)
2. Wo liegt die Arbeit? (Ordner, Liste, Postfach, Aufgaben-Board, Datenbank)
3. Wie oft? Einmal bis fertig, oder immer wieder in einem Takt?
4. Was darf der Loop niemals ohne dich tun? (Geld ausgeben, löschen, Leute kontaktieren, veröffentlichen)

Dann entscheidest du ehrlich:
- **Einmal-Antwort** (eine Mail schreiben, ein Dokument zusammenfassen): kein Loop. Sag es und mach es als normalen Prompt.
- **Ziellinie vorhanden** (Stapel abarbeiten, bis alles besteht): `/goal`.
- **Kein Ziel, nur ein Rhythmus** (alle 30 Minuten prüfen): `/loop <Takt>`.
- **Soll laufen, auch wenn kein Fenster offen ist:** `claude -p "<Charter>"` über einen Zeitplaner (macOS launchd, cron, Windows Aufgabenplanung) oder eine Cloud-Routine.

Kann der Nutzer nicht beschreiben, wie der Loop seine eigene Arbeit prüfen soll, ist die Aufgabe noch nicht reif. Dann bleibt es ein Prompt, und du sagst, was fehlt.

## Schritt 2: Den Charter bauen

Der Charter ist die Dienstanweisung des Loops. Fülle ihn vollständig aus, keine Klammern offen lassen, die der Nutzer schon beantwortet hat:

```
Du läufst als Loop, nicht als einzelne Antwort. Hier ist dein Auftrag (Charter):

ZIEL
[Fertiger Zustand in ein, zwei Sätzen. Konkret, messbar. Beispiel: "Jede Produktseite in /seiten hat aktualisierte Preise und besteht den Link-Check."]

WO DIE ARBEIT LIEGT
[Wo der Loop die Arbeit findet. Beispiel: "Lies TODO.md und behandle jeden nicht abgehakten Punkt als Aufgabe."]

WIE DU ARBEITEST
- Bearbeite IMMER nur einen Punkt. Schließe ihn vollständig ab, bevor du den nächsten beginnst.
- Halte dich an die Konventionen in vorhandenen Dateien. Übernimm den Stil, erfinde keine neuen Muster.
- Verlangt ein Punkt eine Entscheidung, die nur ich treffen kann ([Liste aus Frage 4]): STOPP bei diesem Punkt, schreib ihn auf eine Liste "braucht meine Entscheidung" und geh zum nächsten Punkt.

WIE DU DICH SELBST PRÜFST
Prüfe jeden Punkt, bevor du ihn als erledigt markierst: [Was passt: Tests ausführen / Datei erneut lesen und gegen das Ziel prüfen / Screenshot machen und prüfen / Link öffnen und Inhalt bestätigen. Prüfen heißt Beweis, nicht Zuversicht.]
Schlägt die Prüfung fehl, behebe es und prüfe erneut. Maximal 3 Versuche pro Punkt, danach als blockiert protokollieren und weiter.

WIE DU DICH ERINNERST
Führe eine Datei namens LOOP-STATE.md. Aktualisiere sie nach jedem Punkt mit: Name des Punkts, Status (erledigt / blockiert / braucht mich), was du geändert hast und alles, was der nächste Lauf wissen muss. Lies diese Datei ZUERST zu Beginn jedes Laufs, damit du nie erledigte Arbeit wiederholst.

WANN DU STOPPST
Stopp, wenn: (a) jeder Punkt erledigt oder als blockiert protokolliert ist, oder (b) du in diesem Lauf [N] Punkte abgeschlossen hast. Gib mir dann einen kurzen Bericht: was erledigt wurde, was blockiert ist, was meine Entscheidung braucht.

Beginne damit, LOOP-STATE.md zu lesen, falls vorhanden, dann finde die Arbeit.
```

`[N]` klein ansetzen (3 bis 5 beim ersten Lauf). Loops verbrauchen mehr als Prompts, weil sie mehrere Runden pro Punkt drehen.

## Schritt 3: Auslöser und Bausteine

Gib dem Nutzer genau den Befehl, den er tippt, und erklär in einem Satz, warum dieser:

- `/goal <Ziel>`: arbeitet Runde für Runde, ein zweites Modell prüft nach jeder Runde still, ob das Ziel erreicht ist, und stoppt von selbst. Beispiel: `/goal Jeder Blogpost in /posts hat eine Meta-Beschreibung unter 160 Zeichen und einen Titel unter 60 Zeichen. Gib nach jeder Datei die Zeichenzahl aus. Stopp, wenn jede Datei besteht, oder nach 25 Dateien.`
- `/loop <Takt> <Aufgabe>`: wiederholt sich im Takt. Beispiel: `/loop 30m Prüfe, ob meine Live-Website wieder erreichbar ist. Sobald sie eine normale Seite zurückgibt, sag mir Bescheid und hör auf zu prüfen.` Esc stoppt einen wartenden Loop.

Empfiehl nur die Bausteine, die dieser Loop wirklich braucht:
1. **Automatisierung:** `/loop` oder ein Zeitplaner mit `claude -p`.
2. **Worktrees:** nur wenn zwei Loops gleichzeitig am selben Projekt arbeiten ("mach das in einem separaten Worktree").
3. **Skills:** eine Textdatei in `.claude/skills/`, die das Wissen festhält, das sonst jedes Mal erklärt werden müsste. Einfachster Start: "Mach aus allem, was ich gerade über dieses Projekt erklärt habe, eine Skill-Datei."
4. **Connectoren:** nur wenn der Loop echte Werkzeuge erreichen muss (Mail, Drive, Aufgaben-Tracker). `claude mcp add` oder das Connector-Menü.
5. **Sub-Agenten:** Bau-Agent und Prüf-Agent trennen (`.claude/agents/`), sobald der Loop unbeaufsichtigt laufen soll. Wer die Arbeit macht, sollte sie nicht benoten.

## Harte Regeln

- Ein Loop ohne messbares Ziel ist ein Prompt mit Umweg. Nicht bauen.
- Verifikation ist das ganze Spiel. Ein ungeprüfter Loop macht Fehler nur schneller.
- Alles, was Geld, Kunden, Veröffentlichtes oder Löschungen anfasst, landet in "braucht meine Entscheidung". Sag das laut.
- Erster Lauf immer mit kleinem `[N]` und der Nutzer schaut zu. Erst wenn er dem Loop vertraut, kommt der Zeitplan.
- Befehlsnamen können je nach Claude-Code-Version abweichen: bei Unsicherheit `/help` nennen.

## Ausgabe

1. Urteil: Prompt, `/goal`, `/loop` oder Hintergrund-Zeitplan, mit einem Satz Begründung.
2. Der fertige Charter zum Kopieren.
3. Der exakte Auslöser-Befehl.
4. Die 1 bis 3 Bausteine, die dieser Loop braucht, und was er nicht braucht.
5. Ein Satz, was in sieben Tagen wahr sein soll, wenn der Loop funktioniert.
