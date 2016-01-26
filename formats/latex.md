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

* [Link](http://tutex.tug.org/pracjourn/2005-4/hefferon/hefferon.pdf)
* [Link](https://www.sharelatex.com/learn/Writing_your_own_class)

#### Klasse oder Paket?

* [Link](https://www.sharelatex.com/learn/Understanding_packages_and_class_files)

Wann ist es besser Funktionalität in einer Klasse zu kapseln, wann in einem Paket?

Daumenregel:
* Wenn eine Datei Makros enthält, die das Aussehen einer bestimmten Dokumentart 
  verändern, dann sollten sie in eine Klasse ausgelagert werden.
* Wenn eine Datei Makros enthält, die unabhängig vom Dokumenttyp sind,
  dann sollten sie in ein Paket ausgelagert werden.

#### Pakete

* [Link](https://www.sharelatex.com/learn/Writing_your_own_package)

Im Prinzip gleich wie Klassen nur ein paar andere Befehle; Todo.

#### Klassen

* [Link](https://www.sharelatex.com/learn/Writing_your_own_class)

Die Struktur einer Klassendatei (`*.cls`):

1. Identifikation: Name des Pakets.
2. (Initialisierende) Deklarationen: 
   Importieren der externen Pakete die für die Klasse gebraucht werden.
3. Optionen: Angabe und Verarbeitung der Optionen.
4. Weitere Deklarationen: 
   Das 'Fleisch' der Klasse; hier werden die eigentlichen Änderungen vorgenommen.


##### 1. Identifikation

Diese zwei Befehle müssen in jeder Klasse enthalten sein:

    \NeedsTeXFormat{LaTeX2e}
    \ProvidesClass{exampleclass}[2013/08/12 Example Latex Class]

Das Datum sollte in der Form `YYYY/MM/DD` sein.

##### 2. Initialisierende Deklarationen

Die meisten Klassen bauen auf existierenden Standardklassen auf,
und haben Abhängigkeiten zu weiteren externen Paketen.

    % 1. Identification
    \NeedsTeXFormat{LaTeX2e}
    \ProvidesClass{exampleclass}[2013/08/12 Example Latex Class]

    % 2. Preliminary Declarations
    \newcommand{\headlinecolor}{\normalcolor}
    \LoadClass[twocolumn]{article}
    \Requirepackage{xcolor}
    \definecolor{slcolor}{HTML}{882B21}

Die Befehle in diesem Abschnitt fallen in zwei Kategorien:

1. Definition von Makros zur Verarbeitung von Optionen (im nächsten Abschnitt)
2. Importe von Paketen deren Funktion in der Klasse benötigt werden

`LoadClass`:
Mit diesem Befehl wird die Klasse geladen die verändert werden soll.
Alle Befehle/Abstraktionen dieser Basisklasse stehen dann zur Verfügung.
Bei diesem Aufruf können der Basisklasse Parameter übergeben werden.

`RequirePackage`:
Dieser Befehl hat die gleiche Funktionalität wie der Befehl `\usepackage`;
auch hier können einem Paket Optionen übergeben werden.
Der einzige Unterschied: `\usepackage` kann nicht vor dem `\documentclass`
Befehl verwendet werden.


##### 3. Optionen

Die Klasse kann durch Optionen parametrisiert werden:

    % 1. Identification
    \NeedsTexFormat{LaTeX2e}
    \ProvidesClass{exampleclass}[2013/08/12 Example Latex Class]

    % 2. Preliminary Declarations
    \newcommand{\headlinecolor}{\normalcolor}
    \LoadClass[twocolumn]{article}
    \Requirepackage{xcolor}
    \definecolor{slcolor}{HTML}{882B21}

    # 3. Optionen
    \DeclareOption{onecolumn}{\OptionNotUsed}
    \DeclareOption{green}{\renewcommand{\headlinecolor}{\color{green}}}
    \DeclareOption*{\PassOptionsToClass{\CurrentOption}{article}}
    \ProcessOptions\relax

`DeclareOption`:
Dieser Befehl verarbeitet eine übergebene Option. Zwei Parameter:

1. Name der Option
2. Code der ausgeführt wird wenn die Option übergeben wurde.

`DeclareOption`:
Dieser Befehl verarbeitet unbekannte übergebene Optionen. Ein Parameter:

1. Code der ausgeführt wird wenn eine unbekannte Option übergeben wurde.
   (In diesem Fall Weiterleitung and die unterliegende Klasse.)

`PassOptionsToClass{}{}`:
Gibt die Optionen in der ersten Klammer an die Klasse in der zweiten Klammer 
weiter (hier `article`).

`CurrentOption`: speichert die Namen der Übrigen Optionen.

`ProcessOptions\relax`:
Führt die Verarbeitung der Optionen aus und muss am Ende der Befehle zur 
Verarbeitung von Optionen stehen.


##### 4. Weitere Deklarationen

Jetzt folgen weitere Deklarationen. Beispiel:
    
    \renewcommand{\maketitle}{%
    \twocolumn[%
        \fontsize{50}{60}\fontfamily{phv}\fontseries{b}%
        \fontshape{sl}\selectfont\headlinecolor
        \@title
        \medskip
        ]%
    }
 
Alle Klassen müssen folgende vier Befehle enthalten:

1. Den Defaultwert von `normalsize` (default font size)
2. Den Defaultwert von `textwidth`
3. Den Defaultwert von `textheight`
4. Die Spezifikation des `page numbering`.

Beispiel:

    \renewcommand{\normalsize}{\fontsize{9}{10}\selectfont}
    \setlength{\textwidth}{17.5cm}
    \setlength{\textheight}{22cm}
    \setcounter{secnumdepth}{0}

##### Fehlerbehandlung

Todo


#### Key-Value Paare als Optionen übergeben

* [Link](https://tex.stackexchange.com/questions/34312/how-to-create-a-command-with-key-values)

Ein bißchen Einabreitung aber es schein sich zu lohnen: `pgfkeys`.

### FAQ
* [Welche Pakete standardmäßig laden?](https://tex.stackexchange.com/questions/823/remove-ugly-borders-around-clickable-cross-references-and-hyperlinks)
* [`\include` vs `\input`](https://tex.stackexchange.com/questions/246/when-should-i-use-input-vs-include)
* [`\makeatletter` und `makeatother`](https://tex.stackexchange.com/questions/246/when-should-i-use-input-vs-include)
