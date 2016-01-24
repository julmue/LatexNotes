# Trennung von logischer und typograpischer Auszeichnungssprache

Die Trennung von logischer und typographischer Auszeichnungssprache
ist ein wichtiges Ziel bei der Erstellung von Texten.

##### Warum?

Vorteile einer Trennung von Form und Inhalt:
* Einfachere Bearbeitung durch externe Werkzeuge (`pandoc`, Rechtschreibekorrektur, ...)
  und Transformation/Archivierung in anderen Dateiformaten
* Änderungen an einem zentralen Punkt

##### Was?

Einteilung nach Wortarten, Satzgliedtypen und Gliederungstypen.
Kategorisierung nach [Frege](http://plato.stanford.edu/entries/categories/#DumMetDisCat).

Abbildung von syntaktischen Kategorien in semantische Kategorien: 
* Unterscheidung der Sprachebenen: Objektsprache/Metasprache
    * Metasprache
    * Objektsprachliche Ausdrücke: 
         * Programmiersprachen
         * Mathematik (hat schon eine eigene Auszeichnun
         * Logik
         * Zitate
         * ...

* Konstituenten der logischen Form eines Satzes:
    * Objekte:
        * (Einführung eines) Konzepts (z.B.: ... ist eine weitere *Kausalbedingung* ...)
        * Referenzierung von (formalen) Objekten (z.B.: ... die Kategorie **SET** ...)
    * Prädikate
    * Relationen
    Idee: Könnte man nicht zu Beginn eine Ontologie 
    (also Diskursuniversen, Typen und Interpretationen) festlegen und diesen
    Entitäten dann Makros zuweisen (als Prädikat bzw. Referenz?):
    * Typen?
    
* Gliederungsebene:
    * Skopen: Teil, Kapitel, Abschnitt, ...
    * Definition (Definitionen bestimmen Teilmengen aus den Universen/Typen)
        * Formale/Mathematische Definition
        * Informale/Umgangssprachliche Definition
    * Beispiel (Definition, Beispiel)
    * Erläuterung (XXX, Erläuterung
    * Warnung (XXX, Warnung)


## Wie?

### Implementierung für Objektsprachen

Für die Einbettung von Objektsprachen (genauer Formale Sprachen):
im Prinzip für jede Objektsprache eine eigene Umgebung und ganze Abschnitte:
* Inline-Eingettungen: `\haskell{...}` implementiert als `\olang{haskell}` implementiert als ...
* Abschnitte: `begin{haskell} ... \end{haskell}` implementiert als ...
Darin kann dann festgelegt werden welches Symbol in welche Kategorie
fällt (vll kann man das auch iwi über Vererbung machen)
(Implementierung vll. durch das `listings` bzw. `minted` Paket);

### Implementierung für die Metasprache

Dieser Ansatz funktioniert natürlich nicht bei der Metasprache.
Hier brauch man einzelne Makros für die logischen Kategorien.

Vll. ist auch eine Mischung mit Typen möglich notwendig. Beispiel:

    \newcommand\object[1]{\textbf{#1}}
    \newcommand\int[1]{\textit{#1}}
    
    % can be combined
    \object{\int{3}}

Hätte den Vorteil, dass es kommutiert; hier aber iwi nicht notwendig ...
jede Instanz eines Typs ist ja auch ein Objekt.
Vll. ist das aber trotzdem irgendwo nützlich. 

#### Anmerkungen

##### Automatisches Generieren von Referenzen möglich?

Vermutlich kann man diesen Ansatz noch erweitern,
beispielsweise das automatische generieren von Referenzen
durch die Makros ...
