---
title: Nützliches für Developer
authors:
  - skerbis
prio: null
---

# Nützliches für Developer

* [Beschreibung](developer_resources.md#beschreibung)
* [Nützliche AddOns](developer_resources.md#addons)
  * [Adminer](developer_resources.md#adminer)
  * [Cheatsheat für Extensionpoints](developer_resources.md#cheatsheet)
  * [Demo-AddOn](developer_resources.md#demo)
  * [Developer - Module, Templates und Aktionen syncen](developer_resources.md#developer)
  * [Project - Schnell mal eine PHP-Class einbinden](developer_resources.md#project)
  * [Strukturierte Daten - HilfsAddOn für Jason-LD](developer_resources.md#strucdata)
  * [Theme - Verwalten aller Projektdateien für Frontend und Backend](developer_resources.md#theme)
  * [YConverter - Migration REDAXO 4.x zu 5.x](developer_resources.md#yconverter)
  * [YTraduko - Übersetzungshelfer](developer_resources.md#ytraduko)
  * [ZIP-Install](developer_resources.md#zip)
* [Software und Workflows](developer_resources.md#swork)
  * [REDAXO mit Bimmelbam](developer_resources.md#bimmelbam)
  * [REDAXO mit Docker](developer_resources.md#docker)
* [Nützliche Links](developer_resources.md)
  * [Front-End Checklist](https://github.com/thedaviddias/Front-End-Checklist)
  * Weitere AddOns 
    * [Addon Viewer - Durch AddOns browsen](https://github.com/gupi/addon_viewer)
    * [Addon Template - AddOn-Struktur Generator](https://redaxo.org/download/addons/template/)

## Beschreibung

Nachfolgend listen wir hier nützliche Informationen, AddOns und Links, die die Entwicklung eines AddOns oder des geplanten Projektes erleichtern. Wer mitmachen möchte, sendet bitte seine Ergänzungen als PR.

## AddOns

### Adminer

Adminer für REDAXO. Seit Version 1.3.0 kann der rex\_sql\_table code für die ausgewählte Tabelle in der Tabellenstruktur angezeigt werden. Sehr hilfreich bei der AddOn-Erstellung für die install.php.

**Installation per Installer**

[**Github-Repo**](https://github.com/FriendsOfREDAXO/adminer)

### Cheatsheet

Das Cheatsheet-AddOn scant die REDAXO-Installation nach Extension-Points im Core und den installierten AddOns und listet deren Position im Quellcode auf.

[**Installation aus Github-Repo:**](https://github.com/tbaddade/redaxo_cheatsheet)

### Demo-AddOn

Das Demo-AddOn zeigt wie AddOns entwickelt und dokumentiert werden. Gut kommentierter Quellcode, Hilfe und Hints im AddOn selbst helfen beim Verständnis der AddOn-Programmierung und der Dokumentation. Es liefert auch ein Doku-Plugin, das den Aufbau einer Hilfe für das eigne AddOn ermöglicht.

**Installation per Installer**

[**Github-Repo:**](https://github.com/FriendsOfREDAXO/demo_addon)

### Developer

Developer kopiert und synct Module, Templates und Aktionen zwischen Dateisystem und Datenbank, so werden diese leicht für externe Editoren und per FTP zugänglich.

**Installation per Installer**

[**Github-Repo**](https://github.com/FriendsOfREDAXO/developer)

### Project

In REDAXO bereits vorhanden, ist das Project-AddOn. Hier können einfach eigene PHP-Classes und Assets eingebunden werden, die nach einem Update nicht gelöscht werden. Man erspart sich so also die Entwicklung eines eigenen AddOns, wenn man das System einfach nur mit einer PHP-Class bereichern möchte.

**Installation in der AddOn-Verwaltungr**

### Strukturierte Daten \(JSON-LD\)

Gerne vergessen, von Google aber gern gesehen. JSON-LD - Informationen auf der Website. Dieses AddOn hilft bei der Erstellung.

[**Github-Repo**](https://github.com/eaCe/strucdata)

### Theme

Das Theme-AddOn erleichtert die Verwaltung aller für das Projekt erforderlichen Prajektdateien in einem zusätzlichen /theme-Ordner im Web-Root. Theme erlaubt es auch das System oder die Website mit zusätzlichen CSS, JS und PHP-Classes zu breichern. Ist das Developer-AddOn installiert, synct es sich mit diesem um die Modul- und Template-Dateien an einer zugänglicheren Stelle bereitzustellen.

**Installation per Installer**

[**Github-Repo**](https://github.com/FriendsOfREDAXO/theme)

### YConverter

Eine REDAXO 4.x - Datenbank kann mit Hilfe dieses AddOns für REDAXO 5.x vorbereitet werden und migriert werden. Hierbei werden bekannte Class- und Methodenaufrufe, REX\_VARS für REDAXO 5.x vorbereitet und sogar xform-Tabellen nach yform konvertiert.

[**Github-Repo**](https://github.com/yakamara/yconverter)

### YTraduko - Übersetzungshelfer

Ytraduko hilft bei der Übersetzung der eigenen AddOns. Anstelle selbst für die weiteren Sprachen neue .lang - Dateien anzulegen, erledigt dieses AddOn es selbst. Die Übersetzungen können übersichtlich und schnell eingepflegt werden.

[**Installation aus Github-Repo**](https://github.com/yakamara/ytraduko)

### ZIP-Install

Das ZIP-Install ermöglicht es gezippte AddOns ohne Umweg per FTP auf den Server zu laden und zu entpacken. Ganz praktisch vor allem, wenn es sich um AddOns handelt, die es nur als GitHub-Repo gibt und nicht im Installer zur Vefügung stehen.

**Installation per Installer**

[**GitHub-Repo**](https://github.com/FriendsOfREDAXO/zip_install)

## Software und Workflows

### REDAXO mit Gulp, Browserify, PostCSS und Bimmelbam

Ein Frontend-Workflow auch für REDAXO

Frontendentwicklung wird immer aufwändiger, SCSS wollen kompiliert werden, Bilder komprimiert werden, JS schöner werden, HTML-Prototypen wollen erzeugt werden. _**REDAXO mit Bimmelbam**_ zeigt hierfür einen ausbaufähigen Weg.

[**GitHub-Repo**](https://github.com/FriendsOfREDAXO/redaxo-mit-bimmelbam)

### REDAXO mit Docker

_**MAMP und XAMPP waren gestern!**_ REDAXO kann leicht, systemunabhängig mit Docker verwendet werden. Die Vorteile: Möglichkeit der zentralen Installation und Bearbeitung, Versionierbarkeit, Ausbaufähigkeit. REDAXO-mit-Docker liefert alle Ressourcen und eine einsteigergeignete Anleitung. Und damit man nicht bei Null anfangen muss, kann eine Demo gleich automatisiert installiert werden. _**REDAXO mit Docker und Bimmelbam**_ sind übrigens leicht miteinander kombinierbar. Weitere Infos in den jeweiligen REPOS.

[**GitHub-Repo**](https://github.com/FriendsOfREDAXO/redaxo-mit-docker)

