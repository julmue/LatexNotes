# LATEX

---
---
## Eigene Makros und Environments

* [Link](https://en.wikibooks.org/wiki/LaTeX/Macros)


---
### Makros

#### Kommandos/Makros definieren: `newcommand`/`providecommand`


##### Befehlsstruktur

Neue Makros werden mit dem Befehl `newcommand` definiert:

    \newcommand{name}[num]{definition}

* `name`: Name des Makros
* `num`: (optional, default 0) Anzahl der Argumente (bis zu 9)
* `definition`: Definition des Makros

Beispiel

    % macro without arguments
    \newcommand{\eulerid}{\math{e^{ix} = cos x + i sin x}}

    % macro with 1 argument
    \newcommand{\important}[1]{\textbf{\color{red}#1}}

Ist ein Makro mit dem gleichen Namen bereits definiert bricht LaTeX
bei der Kompilation mit einem Fehler ab. Um Kommandos zu überschreiben siehe 
`renewcommand`.

`providecommand` gleicht `newcommand` mit einem Unterschied:
Ist ein Makro mit gleichem Namen bereits definiert wird dieses Makro verwendet,
kein Kompilierungsfehler wird ausgegeben.

##### Defaultwerte für die Parameter

Mit LaTeX2e ist es möglich dem ersten Parameter einen Defaultwert zuzuweisen:

    \newcommand{name}[num][default]{definition}

Wenn ein `default` Wert angegeben wird gilt dieser für das *erste Argument*
des Makros. Beispiel:

    \newcommand{\elr}[2][Raymond]{#2 loves #1}

Anwendung:

    \elr{Christine}             % -> Christine loves Raymond
    \elr[Charles]{Christine}    % -> Christine loves Charles

Frage: 
Ist es möglich für alle Werte einen Defaultwert anzugeben?
Siehe Übergabe von Key/Value - Paaren.


#### Kommandos/Makros überschreiben: `renewcommand`

Latex erlaubt nicht das bereits definierte Kommandos mit `newcommand` 
überschrieben werden; Überschreibungen werden mit `renewcommand` definiert:

    \renewcommand{name}[num]{definition}

Die Parameter des Befehls sind identisch mit denen von `newcommand`.


#### Robuste Kommandos: `DeclareRobustCommand`

* [Wann newcommand, wann DeclareRobustCommand?](https://tex.stackexchange.com/questions/61503/newcommand-vs-declarerobustcommand)

Todo: Was macht `DeclareRobustCommand` genau?



---
### Environments

Neue Environments werden mit dem Befehl `newenvironment` definiert:

    \newenvironment{name}[num]{before}{after}

* `name`: Name der Umgebung
* `num`: (optional) Anzahl der Parameter (default: 0)
* `before`: Befehle die ausgeführt werden bevor der Inhalt der Umgebung 
            verarbeitet wird
* `after`: Befehle die ausgeführt werden nachdem der Inhalt der Umgebung
           verarbeitet wurde

Beispiel:

    \newenvironment{king}
    {\hrule}
    {\hrule}

Anwendung:
   
    \begin{king}
    Humble Subjects!
    \end{king}


#### Unerwünschter Leerraum

Bei der Definition neuer Umgebungen müssen unerwünschte Leerräume vermieden 
werden:

    % Falsch
    \newenvironment{simple}
    {\noindent}
    {\par\noindent}

    % Richtig
    \newenvironment{correct}
    {\noindent\igonrespaces}
    {\par\noindent
    \ignorespacesafterend}

    % Application:
    \begin{correct}%
    \input{somefile.tex}
    \end{correct}


#### Makros in Umgebungen

Makros können innerhalb des Skopus einer Umbegung definiert werden:

    \newenvironment{topics}{%
        \newcommand{\topic}[2]{ \item{##1 / ##2} }%
        Topics:
        \begin{itemize}
    }{%
        \end{itemize}
    } 

Anwendung:

    \begin{topics}
    \topic{This}{That}
    \end{topics}



---
### Die Anzahl der Parameter erweitern / Key/Value-Paare übergeben

Beispiel `xkeyval`. Geht das auch mit `pgfkeys`?

Damit kann man vermutlich auch defaultwerte für alle übergebenen Parameter 
einrichten.



---
### Arithmetik

LaTeX kann Arithmetik.
Pakete: `calc` und `pfgmath`

Todo: Evaluieren welches der beiden Pakete besser ist.



---
### Konditionale

Siehe `etoolbox` Booleans



---
### Loops

#### Loops in etoolbox
* [Loops in etoolbox](https://tex.stackexchange.com/questions/140907/whats-the-difference-between-the-various-methods-for-producing-for-loops)

#### Loops in PGF

Paket `foreach`.
 


---
### Strings

Siehe `etoolbox` Strings.
Welches Paket ist besser `etoolbox`, `xstrings`, `pgf`?



---
### Latex Hooks

Standardmäßig bietet Latex zwei Hooks an:
* `\AtBeginDocument`: Kommandos die ausgeführt werden sobald `begin{document}`
   erreicht wird
* `\AtEndDocument`: Kommandos die ausgeführt werden sobald `end{document}`
   erreicht wird.

Funktioniert das wie Signals? Also kann mehr als ein Kommando da eingetragen
werden oder wird das überschrieben?



---
---
### Wichtige Pakete für die Latex-Programmierung


---
#### etoolbox

Viele wichtige Konstrukte:
* Hooks
* Booleans
* Flags
* Tests
* Counters
* Length Tests
* String Tests
* Arithmetic Tests
* Boolean Expressions
* ListProcessing
* Internal Lists
* Miscellaneous Tools

`etoolbox` sollte statt `ifthen` und verwandten Paketen verwendet werden.


#### pgf System

##### pgfkeys

##### pgfmath


---
---
## Eigene Klassen und Pakete: `.cls` und `.sty` Dateien

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


* [Link](http://tutex.tug.org/pracjourn/2005-4/hefferon/hefferon.pdf)
* [Link](https://www.sharelatex.com/learn/Writing_your_own_class)



---
### Klasse oder Paket?

* [Link](https://www.sharelatex.com/learn/Understanding_packages_and_class_files)

Wann ist es besser Funktionalität in einer Klasse zu kapseln, wann in einem Paket?

Daumenregel:
* Wenn eine Datei Makros enthält, die das Aussehen einer bestimmten Dokumentart 
  verändern, dann sollten sie in eine Klasse ausgelagert werden.
* Wenn eine Datei Makros enthält, die unabhängig vom Dokumenttyp sind,
  dann sollten sie in ein Paket ausgelagert werden.



---
### Pakete

* [Link](https://www.sharelatex.com/learn/Writing_your_own_package)

Im Prinzip gleich wie Klassen nur ein paar andere Befehle; Todo.



---
### Klassen

* [Link](https://www.sharelatex.com/learn/Writing_your_own_class)

Die Struktur einer Klassendatei (`*.cls`):

1. Identifikation: Name des Pakets.
2. (Initialisierende) Deklarationen: 
   Importieren der externen Pakete die für die Klasse gebraucht werden.
3. Optionen: Angabe und Verarbeitung der Optionen.
4. Weitere Deklarationen: 
   Das 'Fleisch' der Klasse; hier werden die eigentlichen Änderungen vorgenommen.


#### 1. Identifikation

Diese zwei Befehle müssen in jeder Klasse enthalten sein:

    \NeedsTeXFormat{LaTeX2e}
    \ProvidesClass{exampleclass}[2013/08/12 Example Latex Class]

Das Datum sollte in der Form `YYYY/MM/DD` sein.

#### 2. Initialisierende Deklarationen

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


#### 3. Optionen

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

##### `DeclareOption`
Dieser Befehl verarbeitet eine übergebene Option. Zwei Parameter:

1. Name der Option
2. Code der ausgeführt wird wenn die Option übergeben wurde.

##### `DeclareOption*`
Dieser Befehl verarbeitet unbekannte übergebene Optionen. Ein Parameter:

1. Code der ausgeführt wird wenn eine unbekannte Option übergeben wurde.
   (In diesem Fall Weiterleitung and die unterliegende Klasse.)

`PassOptionsToClass{}{}`:
Gibt die Optionen in der ersten Klammer an die Klasse in der zweiten Klammer 
weiter (hier `article`).

##### `CurrentOption`

In diesem Makro sind die Namen der übrigen Optionen gespeichert.

##### `ProcessOptions\relax`
Führt die Verarbeitung der Optionen aus und muss am Ende der Befehle zur 
Verarbeitung von Optionen stehen.


#### 4. Weitere Deklarationen

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

#### Fehlerbehandlung

Todo



---
### Key-Value Paare als Optionen übergeben

* [Link](https://tex.stackexchange.com/questions/34312/how-to-create-a-command-with-key-values)

Ein bißchen Einabreitung aber es schein sich zu lohnen: `pgfkeys`.



---
---
## FAQ
* [Welche Pakete standardmäßig laden?](https://tex.stackexchange.com/questions/823/remove-ugly-borders-around-clickable-cross-references-and-hyperlinks)
* [`\include` vs `\input`](https://tex.stackexchange.com/questions/246/when-should-i-use-input-vs-include)
* [`\makeatletter` und `makeatother`](https://tex.stackexchange.com/questions/246/when-should-i-use-input-vs-include)





