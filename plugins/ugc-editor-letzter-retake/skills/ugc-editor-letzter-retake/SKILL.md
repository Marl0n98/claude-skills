---
name: ugc-editor-letzter-retake
description: >-
  Schneidet UGC-, Talking-Head-, Creator-, Tutorial- und Short-Form-Videos straff aus Rohmaterial in
  Palmier Pro. Use for UGC, talking-head, creator, tutorial, or social-video edits with raw
  recordings, repeated takes, scripted lines, filler words, and pauses — especially when the user
  provides a script, recorded retakes, or asks that only the last recording of each line remain.
  Always preserve only the final complete take of each semantically equivalent line or scene, even
  if wording varies; remove earlier retakes, partial repeats, filler words, and long pauses; deliver
  a clean vertical 9:16 social cut.
---

# UGC Editor – letzter Retake

## Editorial-Prinzip

Authentisch bedeutet nicht ungeschnitten. Baue einen schnellen, inhaltlich lückenlosen Cut mit natürlichem Sprachfluss.

Nicht verhandelbare Retake-Regel:
- Segmentiere das Rohmaterial in inhaltliche Einheiten: Hook, Satz, Schritt, Beispiel, CTA oder Szene.
- Gruppiere alle aufeinanderfolgenden Versuche als denselben Take, wenn sie offensichtlich dieselbe Aussage bzw. denselben Script-Beat behandeln — auch wenn einzelne Wörter fehlen, geändert werden, in anderer Reihenfolge stehen oder der Sprecher improvisiert.
- Behalte aus jeder solchen Gruppe ausschließlich den letzten vollständigen, verständlichen Take.
- Lösche alle vorherigen Versuche vollständig. Verwende nie eine frühere Teilversion als Ergänzung zu einem späteren vollständigen Take.
- Verwende nie Teile aus mehreren Retakes derselben Aussage, wenn dadurch ein Satz doppelt beginnt, einzelne Wörter wiederholt werden oder eine Teilversion vor dem vollständigen finalen Take stehen bleibt.
- Nur wenn der letzte Versuch nachweislich unvollständig, inhaltlich falsch oder technisch unbrauchbar ist, verwende den letzten vollständigen Vorgänger und dokumentiere die Ausnahme kurz.

## Inputs

- A-Roll: Rohaufnahme(n) mit Sprache; bei mehreren Kameras als Multicam oder synchronisierte Clips.
- Optional: Skript oder gewünschte Botschaften.
- Optional: B-Roll, Musik, Branding, Captions.

## Vorflug

1. `get_timeline` aufrufen. Bei einer neuen Version zuerst `create_timeline({from: ...})` verwenden, damit das Original erhalten bleibt.
2. Für eine vertikale Fassung vor dem Platzieren `set_project_settings({aspectRatio:"9:16", quality:"1080p"})` verwenden. Bestehende vertikale Auflösung nicht unnötig ändern.
3. `get_media` aufrufen. Keine Datei anhand ihres Namens beurteilen.
4. A-Roll zuerst mit `inspect_media({overview:true})` prüfen, danach mit `inspect_media({wordTimestamps:true, language:"de"})` bei deutschsprachigem Material oder ohne `language`, wenn die Sprache nicht genannt wurde.
5. Bei mehreren Kameras oder separatem Ton zuerst den Skill `multi-cam-editing` lesen und eine Multicam-Gruppe bzw. saubere Synchronisation herstellen.

## Retake-Analyse: erst lesen, dann schneiden

1. Lies Skript und Transkript parallel als Bedeutungseinheiten, nicht nur als exakten Wortlaut.
2. Erstelle für jede Script-Zeile bzw. jeden semantischen Beat eine Retake-Gruppe:
- gleicher Einstieg oder Schlüsselbegriff;
- gleiche Produktfunktion, Demonstration oder Begründung;
- erkennbarer Neustart nach Versprecher, Pause oder Blick weg;
- umformulierte Wiederholung mit gleichem Sinn.
3. Bestimme innerhalb jeder Gruppe die zeitlich letzte vollständige und flüssige Fassung.
4. Markiere alle früheren Gruppenmitglieder zum Entfernen. Markiere zusätzlich:
- Satzanfänge, die vor einem Neustart abgebrochen werden;
- Wiederholungen einzelner Wörter oder Halbsätze innerhalb desselben Versuchs;
- Brückenwörter, die nur in eine Wiederholung führen;
- falsche oder nicht zum Skript passende Varianten;
- lange Denkpausen, technische Unterbrechungen und Off-Camera-Momente.
5. Anti-Duplikat-Prüfung vor jedem Schnitt: Lies den verbleibenden Übergang. Ein finaler Cut darf nicht die Struktur „Teil-Take + kompletter Take", „Wort + gleiches Wort", „Satzanfang + gleicher Satzanfang" oder zwei Fassungen derselben Aussage enthalten.

## Aufbau der A-Roll

1. Neue A-Roll mit `add_clips` platzieren oder den vorhandenen Rohclip verwenden.
2. Bei 16:9-Material auf 9:16 mit `apply_layout({layout:"full", ...})` cover-croppen; niemals eine Social-Reframe-Komposition mit `set_clip_properties.transform` bauen.
3. Wenn das Rohmaterial bereits aus Sequenzen besteht, `insert_clips` nur für echte narrative Einfügungen nutzen. `add_clips` für gezieltes Überschreiben leerer oder bewusst ersetzter Abschnitte verwenden.

## Schnittreihenfolge

1. Retakes vor Pausen. Entferne zuerst frühere Versuche jeder Retake-Gruppe vollständig.
- Wenn die Auswahl als ganze, nicht wortgenaue Zeitspanne vorliegt, `ripple_delete_ranges` verwenden.
- Wenn sie anhand der Transkriptwörter eindeutig ist, `get_transcript` lesen und `remove_words` mit zusammenhängenden Wortbereichen verwenden.
- Nach jeder wortbasierten Mutation `get_transcript` neu lesen, da Indizes sich ändern.
2. Danach `remove_silence({minimumPauseSeconds:0.5, speechPaddingSeconds:0.08})` für ein schnelles UGC-Tempo verwenden. Bei einem ruhigeren Erklärformat `minimumPauseSeconds:0.65` und `speechPaddingSeconds:0.12` verwenden.
3. Danach Füllwörter und Stolperer entfernen. `remove_words` bevorzugen; Beispiele nur auf ausdrücklichen Wunsch global entfernen: um, äh, ähm, also.
4. Entferne keine bewusst gesetzten Pausen zwischen eigenständigen Gedanken. Halte Übergänge knapp, aber nicht maschinell.
5. Nach jedem Pass das gesamte `get_transcript` als Prosa lesen. Der resultierende Text muss ohne doppelte Takes, Wortschnipsel, verwaiste Satzanfänge oder Sinnsprünge funktionieren.

## Regeln für Skriptabweichungen

- Exakter Wortlaut ist zweitrangig gegenüber der inhaltlichen Entsprechung.
- Wenn eine spätere Version eines Satzes das Skript verständlich erfüllt, behalte sie auch bei geänderter Formulierung.
- Wenn die letzte Fassung nur einen Teil der Aussage enthält, darf sie nicht mit einer älteren Fassung zusammengesetzt werden. Suche stattdessen nach dem letzten vollständigen Take dieser Aussage.
- Wenn keine vollständige Fassung existiert, behalte die letzte kohärente Fassung und entferne nur klar fehlerhafte Wiederholungen.
- Bei mehreren verwandten Sätzen darf ein späterer Take nicht versehentlich eine vorherige Szene ersetzen; prüfe die Script-Reihenfolge Hook → Problem → Lösung → Schritte → Beispiele → CTA.

## Empfohlene UGC-Struktur

- Hook in den ersten 2–3 Sekunden.
- Problem oder Kontrast unmittelbar danach.
- Schritt-für-Schritt-Nutzen oder Demonstration im Mittelteil.
- Ein konkretes Beispiel je Feature.
- Ergebnis/Payoff, dann eindeutiger CTA.
- Kein Padding: alle 3–5 Sekunden sollte sich zumindest der sprachliche Beat, Schnitt oder visuelle Fokus ändern.

## B-Roll und Layout

### Full-frame Intercut (Standard)

- A-Roll bleibt die Erzählung.
- B-Roll nur als Beleg oder Retention einsetzen und auf demselben Story-Track über passende A-Roll-Spannen legen.
- B-Roll-Audio über die verschachtelte `audio.id` mit `set_clip_properties({volumeDb:-60})` stummschalten.

### Stacked Split

- Nur nutzen, wenn Sprecher und Beleg gleichzeitig sichtbar sein müssen.
- A-Roll an den B-Roll-Grenzen mit `split_clips` teilen.
- B-Roll auf einen neuen Track legen und nur die überlappenden A-Roll-Segmente mit `apply_layout({layout:"top_bottom", ...})` gestalten.
- Nicht die ganze A-Roll in die untere Hälfte legen, wenn B-Roll nur punktuell erscheint.

## Captions

1. Erst nach Abschluss aller Retake-, Filler- und Pausenschnitte captionieren.
2. Vor einem neuen Caption-Pass alte Caption-Tracks entfernen, damit Ripple-Schnitte nicht blockiert werden.
3. Den Skill `caption-templates` vor dem Hinzufügen oder Restyling von Captions lesen.
4. Für eine neutrale Standardfassung `add_captions` ohne erfundene Styles verwenden. Stil, Animation und Position nur anwenden, wenn Nutzer oder Vorlage sie vorgeben.
5. B-Roll-Ton vor `add_captions` stummschalten.

## Verifikation

1. `get_timeline` nach einer Schnittserie für Struktur und Track-Stack prüfen.
2. `inspect_timeline` am Hook, an mehreren Übergängen, in der Mitte und am CTA prüfen.
3. `get_transcript` vollständig als Prosa lesen und folgende Checkliste beantworten:
- Ist pro Script-Beat nur der letzte vollständige Retake übrig?
- Gibt es keinen Satz, der mit einem älteren Fragment beginnt und im finalen Take erneut startet?
- Gibt es keine doppelten Wörter, Halbsätze oder Wiederholungen der gleichen Aussage?
- Bleiben Script-Reihenfolge, Sinn und CTA erhalten?
- Sind Pausen kurz und natürlich?
4. Erst nach dieser Prüfung Captions und B-Roll finalisieren.

## Anpassung an neues Material

- Fix bleiben: Retake-Regel „letzter vollständiger Take", Anti-Duplikat-Prüfung, Retakes-vor-Pausen-Reihenfolge und Vertikal-Layout-Workflow.
- Neu ableiten: konkrete Script-Beats, sprachspezifische Füllwörter, Stille-Schwellen, B-Roll-Positionen, Caption-Stil, Markenfarben und CTA.
- Niemals annehmen, dass die sprachlich eleganteste oder erste Fassung die richtige ist: Bei semantisch gleichen Wiederholungen gewinnt immer die letzte vollständige Aufnahme.
