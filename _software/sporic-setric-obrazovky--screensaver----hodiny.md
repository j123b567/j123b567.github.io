---
title: Spořič/Šetřič obrazovky (screensaver) - Hodiny
date: 2013-11-05
excerpt_separator: <!--more-->
---
![](/images/scr-hodiny.jpg)

## Hodiny (Clock)

This screensaver is clone of kclock.kss originally created by Melchior Franz
from KDE. It is written from scratch without any code from original project
because it is written in Delphi. This release is only in Czech localization.

[Download](https://github.com/j123b567/hodiny/releases/latest)

License: BSD 2-Clause

Source: [https://github.com/j123b567/hodiny](https://github.com/j123b567/hodiny)

<!--more-->

## Hodiny

[Stažení](https://github.com/j123b567/hodiny/releases/latest)

Jedná se o klon kclock.kss, jehož původním autorem je Melchior Franz z projektu KDE.

### verze 1.3/2013–11

 - Odstraněna podpora OpenGL
 - Vyřešení několika bugů
 - Podpora více obrazovek – hodiny se zobrazí na všech obrazovkách
 - Přechod na EZLines

### verze 1.2/2008-?
 
 - TODO: přidat podporu pro GNU gettext, aby byly možné lokalizované verze
	do jiných jazyků.


### verze 1.1.189/2008–1

 - Experimentální podpora OpenGl
 - V nastavení vyberte, že chcete používat OpenGL vykreslování.

### verze 1.1/2007-? Stále se připravuje a je ve stádiu návrhu

 - Bude umožňovat vykreslování hodin pomocí DirectX nebo OpenGL, čímž se zatížení procesoru sníží z asi 20% na 0% (testováno na AMD Sempron @1600MHz)

### verze 1.0.187/2007–7

 - Opravena podpora pro počítače s více monitory. Nyní se černá plocha roztáhne na všechny a hodiny se zobrazí na jednom náhodně vybraném monitoru.

### verze 1.0.183/2006–12

 - Volba antialiasingu – vyhlazování (bez, 2×, 4×)
 - Změnu barev ručiček, pozadí, …
 - Uložení nastavení
 - Režim s náhodným pohybem po obrazovce a režim vycentrovaně

### předchozí verze

 - zobrazení bílých hodin na černém pozadí bez možnosti nastavení parametrů
 - o této verzi se pravděpodobně mluví na blogu [http://lukasjankovic.blog.sme.sk/c/82556/Kde-hladat-kvalitne-setrice-obrazovky.html](http://lukasjankovic.blog.sme.sk/c/82556/Kde-hladat-kvalitne-setrice-obrazovky.html) Díky za reklamu ;)

Ještě musím uvést klíčové slovo „zdarma“ abych se umisťoval ve
vyhledáváčích výš ;)

Nejsem správný obchodník a proto zveřejňuji odkaz na konkurenční port
stejného spořiče na windows – [Klock od Oskara](https://web.archive.org/web/20080225073018/http://shell.sh.cvut.cz/~oskar/blog/index.php?entry=entry061014-132530) A další konkurence, tentokrát na MacOS X [http://clocksaver.sourceforge.net/](http://clocksaver.sourceforge.net/)
Zatím uvažuji, jak se mám postavit ke zdrojáku, protože jsem použil volně
dostupnou komponentu, kterou jsem ale od základu přepsal a opravil, takže
nezbyl ani její název, jen komentáře uvnitř zdrojáku. Takže níže je
odkaz a zatím bez licence (zasloužilo by si GPL nebo BSD)

## Co je dobré vědět při vytváření vlastního spořiče

Spořič obrazovky je obyčejný EXE soubor, pouze má příponu .scr a
řídí se příkazy z příkazové řádky.

 - `/A` se týká hesel
 - `/S` spustí samotný screensaver
 - `/P` spustí režim náhledu (předá v druhém parametru handle okna, kam se má náhled vykreslovat)
 - `/C` spustí režim nastavování parametrů (tento parametr spouští Windows XP ve tvaru `/C:223424` takže je potřeba testovat jen první dvě písmena na správný parametr, to číslo by mohl být handle rodičovského okna, abysme mohli dialog pěkně vycentrovat)

## Odkazy:

 * [1] [http://www.mindspring.com/~cityzoo/scrnsavr.html](https://web.archive.org/web/20200613222454/http://www.mindspring.com/~cityzoo/scrnsavr.html)
 * [2] [http://community.borland.com/article/0,1410,19534,00.html](https://web.archive.org/web/20061007004837/http://community.borland.com/article/0,1410,19534,00.html)
 * [3] [http://nono40.developpez.com/tutoriel/delphi/screensaver/](http://nono40.developpez.com/tutoriel/delphi/screensaver/)

