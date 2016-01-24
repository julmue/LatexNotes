# TEXLIVE

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





















Zuerst
	
	" irgend so ein kompressionstool
	sudo apt-get install xzdec

	" beim ersten mal machen:
	tlmgr init-usertree

	" dann
	tlmgr repository add http://www.komascript.de/~mkohm/texlive-KOMA KOMA
	tlmgr pinning add KOMA koma-script
	tlmgr install --reinstall koma-script

tlmgr verwenden:

	tlmgr update --all
	tlmgr update --list
	tlmgr update --self

