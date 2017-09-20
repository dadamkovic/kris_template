# KRIS Template
A LaTeX template for the creation of BSc and MSc theses; dpt. KRIS.

# Návod

Vykompilovanú formu šablóny s návodom (nemusí ísť o najaktuálnejšiu verziu) je
možné [nájsť tu](https://www.dropbox.com/s/vn83egme6v8f54j/LaTeX_template.pdf?dl=0).

# Ako skompilovať

Kompilácia dokumentu sa dá realizovať štandardne. Môžeme však odporúčať použitie
nástroja latexmk – v tom prípade sa dajú použiť príkazy v nasledujúcom tvare:
```
mkdir -p auxfiles
latexmk -silent -bibtex -outdir=auxfiles -pdf -pdflatex="pdflatex -synctex=1 --shell-escape %O '\def\auxfiles{}\input{%S}'" main.tex
```

Prvý príkaz vytvorí pomocný adresár auxfiles (ak ešte neexistuje). Do tohto
adresára sa uložia pomocné súbory aj výsledný PDF súbor – inak by sa uložili
medzi zdrojové súbory, čo by bolo značne neprehľadné.

Ak sa kompilácia spúšťa z prostredia TeXStudio, dá sa tiež použiť latexmk.
Príkaz bude vyzerať nasledovne:
```
latexmk -silent -bibtex -outdir=auxfiles -pdf -pdflatex="pdflatex -synctex=1 --shell-escape %%O '\def\auxfiles{}\input{%%S}'" %
```

## Balíček encxvlna

Slovenská typografia je charakteristická mierne excentrickou požiadavkou, že
niektoré predložky a spojky sa nesmú sádzať na konci riadka. Ak sa tam
vyskytnú, musia sa už zalomiť do nasledujúceho riadka. Na realizáciu tejto
funkcionality v LaTeX-u je potrebné použiť balíček ``encxvlna``.

Tento balíček vyžaduje aktiváciu systému ``enctex``. V inštalácii TeXLive je
možné ``enctex`` aktivovať buď pre užívateľa, alebo pre celý systém. V oboch
prípadoch je na to vytvoriť súbor s názvom ``fmtutil.cnf``, ktorý bude
obsahovať:
```
pdflatex pdftex language.dat -enc -translate-file=cp227.tcx *pdflatex.ini
```
Kľúčová je časť ``-enc``, ktorá hovorí, že sa má povoliť ``enctex``.

### Aktivácia ``enctex``-u pre užívateľa

V prípade aktivácie pre užívateľa je súbor ``fmtutil.cnf`` potrebné umiestniť
do domovského adresára užívateľa, na cestu ``texmf/web2c``.

Následne treba z príkazového riadku spustiť príkaz:
```
fmtutil -user --all
```
ktorý nanovo prekompiluje užívateľské LaTeX formáty tak, že príkaz pdflatex
bude mať aktivovaný ``enctex``.

### Aktivácia ``enctex``-u pre celý systém

V prípade aktivácie pre celý systém sa súbor ``fmtutil.cnf`` umiestni do
adresára LaTeX-ovej inštalácie, na cestu ``texmf-local/web2c``. Následne
je znovu potrebné prekompilovať LaTeX formáty, lenže systémové. Používa
sa na to príkaz:
```
fmtutil -sys --all
```

Keďže príkaz modifikuje systémovú inštaláciu, môže byť potrebné spustiť ho
s administrátorskými privilégiami. Napr. na Ubuntu sa to dosiahne pomocou
príkazu ``sudo``.
