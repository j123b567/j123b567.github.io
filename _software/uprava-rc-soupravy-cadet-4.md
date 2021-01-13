---
title: Úprava RC soupravy CADET 4 (Protokol V3)
date: 2013-09-13
---
Jsem úplný začátečník s RC letadly a tak jsem musel řešit situaci,
jak se jednoduše naučit létat. Koupil jsem si školní model Beta 1400, ke
které je přibalena vysílačka CADET 4 (Protokol V3). Vysílačku jsem
rozebral a doplnil o potřebné části pro připojení k simulátoru.
Vysílačka po úpravách dále bez problémů plní svoji původní funkci.

## Rozebrání vysílačky

Rozebrání jde snadno, povolí se několik šroubů včetně těch malých
v držadle a vysílačka se rozloží na dvě části. Ve spodní části je
velký tištěný spoj s mikroprocesorem. Na druhé straně je RF modul.

<figure>
  <img src="/images/rc-cadet/img_j_str_164_1f14e39a344194fdfcdb8d2d097e2034.jpg" alt="" />
  <figcaption>Základní deska ve vysílačce</figcaption>
</figure>

<figure>
  <img src="/images/rc-cadet/img_j_str_164_41a162fcceeaed2940a71edfb98f371d.jpg" alt="" />
  <figcaption>Strana součástek, RF modul</figcaption>
</figure>

## Nalezení PPM výstupu<

Vývojáři asi předpokládali rozšiřování této vysílačky. I přes
to, že se signál PPM interně nepoužívá a do RF modulu se posílají data
v jiném formátu, má mikroprocesor na jednom pinu tento signál dostupný. Na
tišťáku je to označeno jako TRAINER.

<figure>
  <img src="/images/rc-cadet/img_j_str_164_43410ed6176605146df53b1e39f1ffbe.jpg" alt="" />
  <figcaption>Nalezení PPM výstupu</figcaption>
</figure>

Na PCB jsou dokonce vyvedeny i další dva kanály, takže se již nedivím,
proč je přijímač šestikanálový. Na obrázku jsou další dva dostupné
kanály označeny CH5 a CH6. Jeden z nich je pouze dvoupolohový spínač a na
druhý lze připojit potenciometr.

V čelním plastovém krytu je mnoho otvorů zalepených samolepkou, takže
v případě potřeby je možné tyto vstupy vyvést na povrch.

## Vyvedení PPM signálu

Abych si úplně vysílačku nezničil a netrčel z ní někde drát, vyvedl
jsem PPM signál do konektoru na přední část vysílačky. Při zapojení
konektoru jsem se inspiroval z projektu [crrcsim IFAudio](http://sourceforge.net/apps/mediawiki/crrcsim/index.php?title=IFAudio)

<figure>
  <img src="/images/rc-cadet/img_j_str_164_d5ae5a155ffe8c16dc8c2e2aed9ba7b2.jpg" alt="" />
  <figcaption>Zapojení děliče pro PPM signál</figcaption>
</figure>

Druhý odpor jsem nakonec volil trochu větší, aby nebylo potlačení tak
velké, ale při správném nastavení zesílení to funguje i takto.

<figure>
    <table>
    <tr>
    <td><img src="/images/rc-cadet/img_j_str_164_8ec968a6495765d7217745f032168b51.jpg" alt="" /></td>
    <td><img src="/images/rc-cadet/img_j_str_164_a53bc807170b1c26129411e87b86600b.jpg" alt="" /></td></tr>
    </table>
  <figcaption>Konektor v přední části vysílače</figcaption>
</figure>

Použil jsem otvor v plastovém krytu, pouze jsem vystříhal samolepku.
Konektor je upevněn za matku, asi by bylo dobré jej trochu lépe upevnit,
protože Jack 3.5 tam drží tak tak – průměr matky je téměř stejný
jako průměr celého otvoru, takže konektor má při špatné montáži
tendenci zapadnout dovnitř.

## Sestavení zpět

Sestavení zpět do původního stavu má pouze jeden háček a to je
správná orientace antény. Anténa se má otáčet pouze v úhlu 90°, takže
je třeba dbát na správné dosednutí do výlisku. Pokud se to nepovede,
anténa se bude protáčet dokola a bude zapadávat dovnitř.

## Testování

Testování jsem prováděl s programem [crrcsim](http://sourceforge.net/apps/mediawiki/crrcsim/index.php?title=Download).
Propojil jsem vysílač s počítačem pomocí kabelu Jack-Jack. Pro
připojení je využit linkový vstup. Přes mikrofonní by to také možná
nějak šlo, ale asi ne takto jednoduše. Nastavil jsem vstupní zesílení
zvukové karty. Vše ověřil v SW pro záznam zvuku (např. Audacity).

V programu crrcsim jsem vybral ovládání pomocí Audio a provedl jsem
kalibraci. Nejpodobnější letadlo mé Betě 1400 je asi Flexify XLM, takže
jsem jej zvolil a již se dalo létat.

<figure>
  <img src="/images/rc-cadet/img_j_str_164_caecef2264c84fbf6897fcfaec5b0e4b.jpg" alt="" />
  <figcaption>Létání v programu crrcsim</figcaption>
</figure>

## Další čtení

[https://docs.google.com/document/d/1oXhdEPzrDN5KuK5Me9V8KdsePNP5mduOCcoRUj7rb28/preview?pli=1](https://docs.google.com/document/d/1oXhdEPzrDN5KuK5Me9V8KdsePNP5mduOCcoRUj7rb28/preview?pli=1)
