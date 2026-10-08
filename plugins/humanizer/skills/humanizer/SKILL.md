---
name: humanizer
description: >
  Vermenschlicht Text, damit er nicht nach KI klingt — entfernt typische LLM-Muster
  (Wortschatz, Satzbau, Formatierung, Ton). WICHTIG, immer anwenden, nicht nur auf
  explizite Anfrage. Bei jedem Text, den der Nutzer zum Umschreiben oder Prüfen schickt
  ("klingt das nach KI?", "mach das menschlicher", "check den Text"), UND
  standardmäßig auf jeden längeren Text, den Claude selbst für den Nutzer generiert
  (Reels-Skripte, Captions, DMs, E-Mails, Kommentare, LinkedIn-Nachrichten, Posts),
  bevor die finale Version ausgegeben wird. Gilt für Deutsch und Englisch.
---

# Humanizer

Der Nutzer will grundsätzlich keine Texte, die nach ChatGPT/Claude klingen — egal ob er selbst einen Entwurf schickt oder ob Claude den Text neu schreibt. Dieser Skill ist der Standardfilter für ausgehenden Text.

## Wann aktiv werden

- **Reaktiv**: Der Nutzer schickt Text und bittet um Umschreiben, Gegencheck oder Feedback ("klingt das nach KI?", "vermenschlich das").
- **Proaktiv (Standardfall)**: Immer wenn Claude selbst Fließtext für den Nutzer produziert, der nach außen geht — Captions, Skripte, DMs, Mails, Kommentare, Posts. Bei reinem Chat-Smalltalk mit dem Nutzer selbst (nicht für Weitergabe bestimmt) ist der Filter nicht nötig.
- Bei internen Arbeitsdokumenten (Tabellen, Code, Analysen für den Nutzer selbst) NICHT automatisch anwenden — nur wenn er explizit danach fragt. Der Filter ist für Text gedacht, der Leser:innen erreicht.

## Vorgehen

1. Text (eigenen Entwurf oder Text des Nutzers) gegen `references/patterns.md` prüfen — die fünf Kategorien: Wortschatz, Satz-/Rhetorikmuster, Formatierung, Ton, und was stattdessen menschlich klingt.
2. Umschreiben, nicht nur Wörter austauschen. Ziel ist eine echte Neuformulierung, keine Synonym-Suche — sonst bleiben die verräterischen Satzstrukturen (Dreier-Regel, angehängte Partizipien, Negativ-Parallelismen) erhalten, auch wenn die Wörter anders sind.
3. Bedeutung, Fakten und Kernaussage bleiben unangetastet. Es geht um Stil, nicht Inhalt.
4. Ton an den Kontext anpassen: Instagram-Caption darf locker/umgangssprachlich sein, eine E-Mail an eine Marke bleibt professionell — aber in beiden Fällen ohne KI-Tell.
5. Ausgabe: standardmäßig nur der fertige Text, ohne Meta-Kommentar ("Hier ist die menschlichere Version:") und ohne die gefundenen Muster aufzulisten — außer der Nutzer fragt explizit nach einer Erklärung oder einem Vorher/Nachher-Vergleich.

## Groblinien, worauf besonders zu achten ist

- Keine Em-Dash-Ketten, keine Dreier-Aufzählungen im Autopilot, keine "spielt eine entscheidende Rolle"-Floskeln.
- Keine generischen Superlative anstelle konkreter Zahlen/Fakten, die der Nutzer eigentlich hat (Followerzahlen, Ortsnamen, Zeiträume).
- Keine übertrieben höflichen Chat-Floskeln in DMs/Mails, die eigentlich direkt und persönlich klingen sollen.
- Volle Kategorienliste mit Beispielen: siehe `references/patterns.md`.

## Beispiel

**Vorher (klingt nach KI):**
"Content-Erstellung spielt eine entscheidende Rolle für nachhaltiges Wachstum auf Instagram. Es ist nicht nur wichtig, regelmäßig zu posten — es ist essenziell, eine authentische Verbindung zur Zielgruppe aufzubauen. Drei Schlüsselfaktoren sind entscheidend: Konsistenz, Qualität und Engagement."

**Nachher (menschlich):**
"Regelmäßig posten allein reicht nicht. Was bei mir wirklich zieht, sind die Reels, wo die Leute merken, dass da wirklich jemand dahintersteckt, der sich mit dem Thema auskennt — nicht irgendein durchgestyltes Content-Schema."
