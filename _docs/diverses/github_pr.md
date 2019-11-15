---
title: Github Pull-Request testen
authors:
  - bloep
prio: null
---

# Github Pull-Request testen

* [Beschreibung](github_pr.md#beschreibung)
* [Pull-Reuqest auschecken](github_pr.md#pr-auschecken)
* [Fehler mitteilen](github_pr.md#fehler-mitteilen)
  * [Codezeile kommentieren](github_pr.md#codezeile-kommentieren)
  * [Anderungen gutheißen](github_pr.md#aenderungen-gutheissen)

## Beschreibung

Nachfolgend möchte ich zeigen, wie einfach es ist, mit dem Tool [**hub**](https://hub.github.com/) Pull-Requests von Github in die lokale Entwicklungsversion von REDAXO zu laden, damit diese getestet werden können.

**Für die nächsten Schritte wird vorrausgesetzt, dass** [**hub**](https://hub.github.com/) **installiert ist.**

## Pull Request auschecken

In der Redaxo Entwicklungsversion folgenden Befehl im Terminal/Kommandozeile ausführen:

`git checkout https://github.com/<OWNER>/{REPOSITORY}/pull/{PRNUMMER}`

In diesem Beispiel: `git checkout https://github.com/redaxo/redaxo/pull/1835`

Diese URL kann auch aus der Browser Adresszeile kopiert werden, wenn der Pull-Request geöffnet ist.

![Checkout eines Pull-Requests](https://raw.githubusercontent.com/FriendsOfREDAXO/tricks/master/screenshots/github_pr/checkout-pr.gif)

**Das wars schon.**

Das Programm legt selbstständig alle notwendigen Einstellungen fest und macht einen checkout des Pull-Requests.

Im Anschluss kann direkt drauf los getestet werden.

## Fehler mitteilen

Es gibt mehrere Möglichkeiten gefundene Fehler in einem PullRequests mittzuteilen.

Wenn ein Fehler entdeckt wird, die Ursache aber unbekannt ist, kann einfach ein entsprechender allgemeiner Kommentar verfasst werden.

### Codezeile kommentieren

Wenn man jedoch eine Idee hat oder den genauen Fehler gefunden hat, bietet es sich an, direkt den Kommentar an die entsprechende Code-Zeile zu heften.

![Code-Zeile kommentieren](https://raw.githubusercontent.com/FriendsOfREDAXO/tricks/master/screenshots/github_pr/comment-line-plus.png)

Dies kann über den Reiter **Files changed** geschehen. Hier kann für die entsprechende Zeile mit dem Klick auf das "+" zeichen ein Kommentar-Bereich geöffnet werden. Hier können Probleme, die mit dieser Zeile enstehen genau diskutiert werden. Im optimalfall schlägt man direkt seine Korrektur vor.

![Code-Zeile kommentieren](https://raw.githubusercontent.com/FriendsOfREDAXO/tricks/master/screenshots/github_pr/comment-line-filled.png)

### Änderungen gutheißen

Wenn keine Fehler gefunden wurden kann ein Pull-Request approved werden. Dies gibt den Maintainer eine RÜckmeldung darüber, dass man mit dem PR einverstanden ist. Wenn man nicht nur den Diff nach Fehlern durchsucht hat und zusätzlich das hier beschriebene Auschecken und Testen durchgeführt hat, kann man als Kommentar für das "approven" dazu schreiben, dass man diese Änderungen getestet hat.

![&#xC4;nderungen approven](https://raw.githubusercontent.com/FriendsOfREDAXO/tricks/master/screenshots/github_pr/approve-pr.png)

