---
description: Evaluation of the user tests
---

# User tests

{% hint style="info" %}
This page describes the results of the user tests.
{% endhint %}

## Introduction

To test the implemented abstractions more widely, we performed user tests. Our probands were all students who program on a daily basis and are typical users of implementations like the one we implemented.

We have created a JavaScript file for this purpose, which contains some prepared tasks. Dazu wurde im Code ein Grundgerüst einer Applikation erstellt und da wo der Proband etwas ergänzend programmieren musste war eine Aufgabe mit einem TODO markiert und beschrieben.

Anschliessend zum Programmieren mussten die Probanden einen Fragebogen ausfüllen. Einschätzungen über die Verständlichkeit und der Sinnhaftigkeit der Frameworks wurden nebst Grundsätzlichen Ansichten abgefragt. Die Resultate werden in diesem Dokument nachfolgend erörtert.

## Evaluation

Die Feedbacks wurden nach den implementierten Abstraktionen unterteilt. Am Ende des Fragebogens durften die Probanden noch angeben, ob sie sich für erfahrene Programmierer halten und ob sie Kenntnisse der Funktionalen Programmierung haben. Dabei denkt ungefähr drei viertel, dass sie erfahren sind und fast alle sind mit der funktionalen Programmierung vertraut.

### Range

Allgemein hat ein Range bei den Probanden keine grösseren Probleme oder Unverständlichkeiten hervorgerufen. Dies ist vermutlich darauf zurück zu führen, dass ein Range auch von anderen Programmiersprachen bekannt ist. So denken die meisten Probanden, das ein Range in einem Projekt durchaus zum Einsatz kommen könnte. Für die meisten war auch klar, dass ein Range als Iterable weiter prozessiert werden kann. So gehen die meisten davon aus, dass map, filter oder auch drop Verfügbar sind.

### Focusring

Die Mehrheit der Probaneden haben den Fokusring als einfache Datenstruktur empfunden und denken, dass sie mit der Funktionsweise dieser Datenstruktur nach der Durchführung des Tests vertraut sind. Alle Teilnehmer sehen Vorteile darin, dass der Focusring immutable ist. Fast alle könnten sich ein Einsatz dieser Datenstruktur in einem zukünfigen Projekt vorstellen.

### Logging Framework

Die Grundfunktionalitäten des Logging-Frameworks war den Probanden klar. Einfache Fragen zur Handhabung wurden von allen Probanden richtig beantwortet. Die meisten denken auch, dass sie das Framework schnell verstanden haben. Etwas differenzierter sieht es bei der Konfiguration des Loggers mittels curried-style aus. Hier haben einige den Vorteil dieser impementation nicht erkennen können und empfinden dies als unnötig kompliziert. Jedoch sind sich alle einig, dass der gewonnene Nutzen das etwas kompliziertere Setup rechtfertigt. Die meisten könnten sich auch einen Einsatz des Logging-Framework in einer eigenen Applikation vorstellen.

## Fazit

Grundsätzlich sind wir mit dem Resultat sehr zufieden. Die meisten konnten die Aufgaben ohne grössere Probleme lösen. Etwas mehr mühe hatten die Teilnehmer wenn sie Vorteile von angewendeten Prinzipien erkennen sollten. Wir führen dies zurück auf die ungewohnte programmierweise, die zum Beispiel im curried-style angewendet wird. Diese Art der funktionalen Programmierung ist für viele eher ungewohnt. Erschwerden kommt dazu, dass die IDE nicht die gleiche unterstützung bietet und man gewzugen ist, tieferes Verständnis des Codes zu erlangen oder die Dokumentation zu studieren. Allgemein ist aufgefallen, dass eine gute Code-Dokumentation für die Verwendung eines Frameworks oder Datenstruktur zentral ist. So ist auch zum Vorschein gekommen, dass Probanden ohne gute Integrierung der jsDoc in der IDE mehr Aufwand betreiben müssen um eine Aufgabe zu lösen.
