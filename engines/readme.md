# TeX Engines/Interpreter


## Tex

*TeX* (nicht das Format/Makrosammlung *Plain TeX*) ist das Programm/
der Interpreter für TeX-Dateien:
* Umwandlung von TeX-Dateien in DVI-Dateien
* Maschinenbefehlssatz: die 300 Primitiven von Core-Tex
* ASCII-basierend
* Beschränkung der Register

Aufgrund des Alters und der damit einhergenden technischen Beschränkungen
des Programms neuere Iimplementierungen die in unterschiedlichem Umfang
diese Beschränkungen beseitigen.

### Ressourcen

Ressourcen zum TeX-Interpreter
* TexByTopic: Aufbau und Funktion des Interpreters

## XeTeX

* UTF8-Engine 
* Standardmäßige Einbindung von Systemschriften 

Beste Implementierung für Multi-Language-Support.

XeteX verarbeitet direkt TTF, OTF und TeX-Fonts 
(Paket `fontspec`).

### Ressourcen

Ressourcen zum XeTeX-Interpreter:
* https://tug.org/xetex/
*[What is XeTeX?](https://tex.stackexchange.com/questions/3393/what-is-xetex-exactly-and-why-should-i-use-it)
* [XeTex vs LuaTex](https://tex.stackexchange.com/questions/126206/why-choose-lualatex-over-xelatex)
* [Frequently loaded packages, difference pdfTex vs XeTeX](https://tex.stackexchange.com/questions/2984/frequently-loaded-packages-differences-between-pdflatex-and-xelatex?lq=1)
* [Frequently loaded packages, difference XeTeX vs LuaTex](https://tex.stackexchange.com/questions/87155/frequently-loaded-packages-differences-between-xelatex-and-lualatex)


## LuaTex

* UTF8-Engine 
* Standardmäßige Einbindung von Systemschriften 
* Einbindung der Lua-Programmiersprache in TeX-Document



