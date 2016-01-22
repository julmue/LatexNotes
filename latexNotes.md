# LATEX




---
## Kompilation

### Wichtige Optionen beim Kompilieren

Wichtige Optionen beim kompilieren

------------------------+-------------------------------------------------------
Flag 			| Semantik
------------------------+-------------------------------------------------------
-halt-on-error		| latex stoppt die kompilatin nach dem ersten Fehler
-file-line-error	| eine bessere Anordnung der Informationen zu den 
                          Fehlern im Logfile
-synctex=1		| eine Datei <file_name>.synctex.gz wird generiert welche
			  informationen enthält, welcher Teil des Sourcecodes zu
			  welchem Output geführt hat.
------------------------+-------------------------------------------------------

### Kompilieren mit Propstscript

Wenn das Programm PostScript Commands enthält ist folgende Reihenfolge einzuhalten:

1. `latex [options] <file_name>.tex`: tex -> dvi 
2. `dvips [options] <file_name>.div`: dvi -> ps
3. `ps2pdf [options] <file_name>.ps`: ps -> pdf


### Dateiformate und Dateiendungen 

Wichtige Dateiformate und -endungen bei Latex:

* DVI: Device Independent File Format (`*.dvi`)
    * Seitenbeschreibungssprache
    * Vektorbasiert
    * ähnliche Formate: PDF, PostScript, SVG 
    * verwendete Zeichensätze werden von der Dati nur referenziert und müssen 
      auf dem Zielsystem vorhanden sein
    * DVI ist das Ausgabeformat des Textsatzsystems Tex
    * DVI kann in viele weitere Formate umgewandelt werden

* PS: PostScript (`*.ps`)
    * Seitenbeschreibungssprache
    * Vektorbasiert
    * Entwickelt von Adobe
    * turingvollständige Stackorientierte Programmiersprache
    * üblicherweise für Vektrografiken verwendet
    * Bei unixoiden Betriebssystemen ist es üblich, 
      das Druckaufträge an den Druckserver in PS gesendet werden

* EPS: Encapsulated PostScript (`*.eps`)
    * Datei zur Beschreibung von Grafiken

* GS: GhostSrcipt
    * Freier Interpreter der Seitenbeschreiungssprache GhostScript und PDF
    * Rasterung von PDF oder PostScript Dateie

* PDF: Portable Document Format
    * Entwickelt von Adobe


### Was sind .cls und .sty files?

[Info](https://tug.org/pracjourn/2005-3/asknelly/nelly-sty-&-cls.pdf)

Classfiles (`*.cls`) und Stylefiles (`*.sty`) können zur Kapselung von Makros
und anderen Informationen in Tex verwendet werden.

Classfiles werden mit `\documentclass{<filename>}` geladen;
Stylefiles mit `\usepackage{<filename>}`

`.cls` Dateien werden Klassen genannt;
`.sty` Dateien Stylefiles oder Pakete.

Beide Formate können beliebigen Tex und Latex Code enthalten;
Sie werden allerdings unterschiedlich verwendet:

Laden einer Klasse mit `\documentclass` genau einmal in jedem Latex-Dokument;
Pakete sind optional, es können beliebig viele geladen werden.

Idealerweise definiert eine Klasse die Struktur eines Dokuments;
Pakete ergänzen diesen Funktionsumfang dann.



### Schriftbeschreigungssprachen

* METAFONT
    * Abstrakte Beschreibungssprache zur Definition von Vektorschriften
    * von Donald E Knuth Entwickelt
    * rationale Kurven höhren Grades
    * Bei Metafont-Schriften muss für jedes Gerät ein angepasster Satz an 
      Bitmap-Schriften erstellt werden. Der DVI Treiber erstellt dann die 
      optimal angepassten Schriften für das jeweilige Gerät

* TrueType/FreeType
    * rationale Kurven zweiten Grades

* PostScript-Type-1Font
    * Dateiendung .pfb
    * rationale Kurven dritten Grades
	* Eingeschfränkter ISO Standardisierter Sprachanteil aus der PS-Sprache
	*  Bezierkurven dritten Grades


### Tex-Erweiterungen

Tex-Interpreter (mit erweitertem Funktionsumfang):
* Etex			
* pdflatex
* Luatex
* Xetex
* Omega
* Aleph


### Ergänzende Programme

Weiter Hilfsprogramme zur Verarbeitung von Dokumenten:
* bibtex, bibtex8:	bibliograpy support
* makeindex, xindy:	index support
* dvips	:		converts dvi to postscrpit
* dvipdfmx:		converts dvi to pdf
* tex4ht:		tex to html and xml converter (better use pandoc)


### Eigen Pakete und Klassen schreiben

[Link](http://tutex.tug.org/pracjourn/2005-4/hefferon/hefferon.pdf)



---
## TEXLIVE

Voraussetzung für die Verwendung von Latex ist eine funktionierende Latex
Distribution. Unter linux wird üblicherweise TexLive verwendet.

Texlive ist eine Tex-Distribution. Sie enthält grundsätzlich alle Pakete die
auch im Comprehensiv Tex Archive Network enthalten sind. Beschränkungen ergeben
sich für Pakete die unter keiner freien Lizenz verfügbar sind.

Seit Version 2008 verfügt die Distribution mit `tlmgr` über einen eigenen
Paketmanager.


### Installation und Verzeichnisse

#### Wie wird Texlive installiert

Texlive ist in den Paketquellen enthalten:

    sudo apt-get install texlive texlive-doc-de texlive-latex-extra texlive-lang-german

#### Wohin wird Texlive installiert
Die Distribution `texlive` wird nach `/usr/share/texlive` installiert;
die Hilfsdateien nach `/usr/share/doc/texmf`.


#### Lokaler Textree

Ein lokaler Textree ermöglicht es, `*sty` Stylefiles und `*.cls` Classfiles an
einem zentralen Punkt abzulegen, und sie gleichzeitig für alle Dokumente 
verfügbar zu machen.

##### Wo muss der lokale Textree abgelegt werden?
Das Verzeichnis an dem nach dem lokalen Textree gesucht wird ist vom 
Betriebssystem abhängig und kann wie folgt ermittelt werden:

    kpsewhich -var-value=TEXMFHOME
    > ~/texmf

https://www.tug.org/tds/tds.html#Top_002dlevel-directories


##### Wie ist der lokale Textree aufgebaut?

Der Aufbau des lokalen Textree entspricht der standard Tex Directory Structure 
[TDS](http://tug.ctan.org/tds/tds.html):
Eine Verzeichnishierarchie für
* Macros
* Schriften
* Bibtex Datenbanken
* ...

Jedes Paket (damit ist hier nicht nur eine sty-Datei gemeint)
muss in einem Eigenen Verzeichnis liegen.

Die Suche nach einer Datei im texmf Baum findet rekursiv statt.

Das Wurzelverzeichnis eines Textrees heisst `texmf` (Tex and Metafont).

Auf einer Maschine kann mehr als eine TDS installiert werden.
(genau das passiert hier ja)

Beispiel:
Die Datei `common.sty` soll (für den lokalen Benutzer) von überall 
zugänglich gemacht werden:
1. Ablegen der Datei in `~/texmf/tex/latex/common/common.sty`.
   Die entsprechenden Ordner müssen angelegt werden;
   es genügt nicht die Datei einfach nur in `~/texmf` abzulegen --
   hier wird sie nicht gefunden.
2. Die Datei kann jetzt benutzt werden. Überprüfung des Pfades:
   `kpsewhich common.sty`.

Anmerkung:
Es dürfen mehrere sty und cls Dateien in einem Ordner liegen;
Diese können direkt eingebunden werden.
Weiter muss der Ordnername und der Name des Stylefiles bzw.
des Classfiles nicht identisch sein.

Anmerkung:
Es ist nicht notwendig `mktexlsr` mit dem Argument `$TEXMFHOME` 
auszuführen

Anmerkung:
Texlive verwendet zur Suche die Bibliothek `kpathsea`.
Das Programm `kpsewhich` ist eine "kpsewhich - standalone path lookup 
and and expansion for kpathsea" für diese Biblothek.

### Hilfe in Texlive

Das Hilfsprogramm in Texlive heißt `texdoc`;
es ist das Latex-Pendant zu den manpages.

    texdoc [options] <name>

Beispiel:

    texdoc koma 

### Paketmanager in Texlive

Seit Version 2008 verfügt Texlive mit tlmgr über einen eigenen Paketmanager.



---
## MISC

### Schriften

Um weitere Schriften zu installieren auf http://www.tug.org/fonts/getnonfreefonts/
das Script herunterladen und dann die Installationsanweisung befolgen.
*noch aktuell?*


### Was ist das Comprehensive Tex Archive Network (CTAN)?
