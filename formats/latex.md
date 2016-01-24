# LATEX

### Eigene Klassen und Pakete: `.cls` und `.sty` Dateien

[Info](https://tug.org/pracjourn/2005-3/asknelly/nelly-sty-&-cls.pdf)

Classfiles (`*.cls`) und Stylefiles (`*.sty`) können zur Kapselung von Makros
und anderen Informationen in Tex verwendet werden:
* `.cls` Dateien werden Klassen genannt;
* `.sty` Dateien Stylefiles oder Pakete.

Classfiles werden mit `\documentclass{<filename>}` geladen;
Stylefiles mit `\usepackage{<filename>}`

Beide Formate können beliebigen Tex und Latex Code enthalten;


Laden einer Klasse mit `\documentclass` genau einmal in jedem Latex-Dokument;
Pakete sind optional, es können beliebig viele geladen werden.

Idealerweise definiert eine Klasse die Struktur eines Dokuments;
Pakete ergänzen diesen Funktionsumfang dann.

### Eigene Pakete und Klassen schreiben

[Link](http://tutex.tug.org/pracjourn/2005-4/hefferon/hefferon.pdf)
