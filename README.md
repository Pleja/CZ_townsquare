# Grimoár a náměstí pro hru Krvavá hodina odbila

> :warning: **Tento projekt je nádstavbou původního projektu, ze kterého vznikl.** :warning:

![social](https://user-images.githubusercontent.com/325521/102897760-d1147b00-4468-11eb-9d7b-63a204bc9fc1.png)

Tohle je neoficiální online nástroj pro hraní hry Krvavá hodina odbila přes Discord nebo jiné digitální způsoby.
Je zamýšlen pro pomoc vypravěčům a hráčům tím, že jim umožňuje rychle připravit hru, hlasovat a mnoho dalšího.

[Můžete vyzkoušet online!](https://pleja.github.io/CZ_townsquare/)

Pokud chcete zjistit, jak používat originální aplikaci jako hráč, tak [JayBotC](https://www.youtube.com/channel/UCNZy-4Rp877XtTHaIZdWYFQ) byl tak laskav, aby pro veřejnost vytvořil dvě ukázková videa (videa jsou v angličtině).

### Jak hostovat hry
[![Jak hostovat hry](https://img.youtube.com/vi/lVRJPBXfqxg/0.jpg)](https://www.youtube.com/watch?v=lVRJPBXfqxg)

### Jak hrát hru
[![Jak hrát hru](https://img.youtube.com/vi/VCpFnJFiCbk/0.jpg)](https://www.youtube.com/watch?v=VCpFnJFiCbk)

## Funkce

- Veřejné náměstí a grimoár pro vypravěče (lze přepínat pomocí **klávesové zkratky \[G\]**)
- Podporuje vlastní skripty JSON generované [Skriptovacím nástrojem](https://bloodontheclocktower.com/script)
- Relace živě pro vypravěče / hráče, která podporuje hlasovat, chtít mluvit a rozeslat postavy. To vše živě!
- Obsahuje všechny 3 základní edice, Pocestné, Proslulé i Loriky, plus všechny ostatní oficiálně oznámené postavy!
- Tabulku nocí a připomínkový text pro každou schopnost postavy pro výpomoc vypravěčům
- Plná podpora pro zakládání a hrání her s vlastní sestavou postav
- A spousty dalších možností úprav!

### Podpora vlastních skriptů

Jakýkoliv vlastní skript vytvořený oficiálním [Skriptovacím nástrojem](https://script.bloodontheclocktower.com/) je již podporován
a vám ho pouze stačí nahrát, aby se vám zobrazily zvolené postavy v grimoáru. Pokud chcete upravit váš skript ještě více,
tak je zde dodatečný `"_meta"` objekt, který můžete přidat do skriptu stejně, jako kdyby jste přidávali normální postavu:

```json
[
  {
    "id": "_meta",
    "name": "Deadly Penance Day",
    "author": "TPI",
    "logo": "https://url.to/your/logo.png"
  }
]
```

Tohle poskytne vašemu lokálnímu Grimoáru (a i všem připojeným hráčům) více informací pro zobrazení ohledně vašeho
vlastního skriptu - například místo "Vlastní skript" se bude zobrazovat "Deadly Penance Day" na referenční tabulce
postav. Logo se hráčům zobrazí, jakmile budou mít povolené vlastní obrázky v menu Grimoáru.

### Podpora vlastních postav

Pro přidání vlastní postavy do vašeho lokálního Grimoáru je potřeba vytvořit JSON soubor s jejich definicí,
který bude podobný souboru [`roles.json`](https://github.com/Pleja/CZ_townsquare/blob/main/src/roles.json) pro 3 základní edice.
Zde je ukázka, jak by taková definice postavy mohla vypadat:

```json
[
  {
    "id": "acrobat",
    "image": "https://github.com/bra1n/townsquare/blob/main/src/assets/icons/acrobat.png?raw=true",
    "edition": "custom",
    "firstNight": 0,
    "firstNightReminder": "",
    "otherNight": 49,
    "otherNightReminder": "If either good living neighbor is drunk or poisoned, the Acrobat dies.",
    "reminders": ["Die"],
    "remindersGlobal": [],
    "setup": false,
    "name": "Acrobat",
    "team": "outsider",
    "ability": "Each night*, if either good living neighbor is drunk or poisoned, you die."
  },
  { 
    "id": "investigator" 
  },
  { 
    "id": "imp" 
  }
]
```

Tako JSON definice obsahuje vlastní postavu "Acrobat" a 2 postavy ze základní hry - Vyšetřovatele a Čerta.
U základních postav stačí pouze dodat jejich ID, podobně, jako tomu je u oficiálního skriptovacího nástroje.

**Povinné parametry:** `id`, `name`, `team`, `ability`

- **id**: vnitřní ID této postavy, bez mezer a speciálních znaků<br>
  _Pozn._: ID musí být originální a nesmí být stejné, jako nějaké již existující ID základní postavy, jinak by byla vlastní postava nahrazena základní!
- **image**: URL na PNG obrázek tokenu postavy (měl by mít průhledné pozadí!)<br>
  _Pozn._: vlastní obrázky jsou viditelné pouze pokud jsou povoleny v menu Grimoáru!
- **edition**: ID edice této postavy. Může zůstat prázdné pro "custom"
- **firstNight** / **otherNight**: pozice, kdy se tato postava probouzí v první / dalších nocích, v porovnání se všemi ostatními postavami<br>
  _Pozn._: musí být kladné číslo nebo nula, přičemž nula se považuje za "neprobouzí se v noci"
- **firstNightReminder** / **otherNightReminder**: text připomínky na první / další noci
- **reminders**: Připomínkové tokeny, mělo by být prázdné pole `[]`, pokud žádné
- **remindersGlobal**: Globální připomínkové tokeny, které budou dostupné, i když postava není přiřazená zádnému hráči
- **setup**: pokud tato postava ovlivňuje přípravu hry (oranžový lístek), jako Pijan nebo Baron
- **name**: Zobrazované jméno postavy
- **team**: tým postavy, musí být buď `townsfolk`, `outsider`, `minion`, `demon`, `traveler` nebo `fabled`<br>
  _Pozn._: pokud vytvoříte vlastní Proslulou postavu, tak bude automaticky přidána do hry po načtení skriptu
- **ability**: zobrazovaný text schopnosti postavy

## [Code of Conduct](CODE_OF_CONDUCT.md) (Originální text)

## [Přispívání k projektu](CONTRIBUTING.md) (Originální text)

## Zmíňky a copyright

* [Krvavá hodina odbila](https://bloodontheclocktower.com/) je obchodní značka od Steven Medway a [The Pandemonium Institute](https://www.thepandemoniuminstitute.com/)
* Noční připomínky a další pomocné texty v angličtině napsal [Ben Finney](http://bignose.whitetree.org/projects/botc/diy/)
* Ikonografie od [Font Awesome](https://fontawesome.com/)
* Na obrázek na pozadí udělil copyright a svolení [Ryan Maloney](https://www.artstation.com/maloney94)
* Webové fonty od [Google Fonts](https://fonts.google.com/) and [Online Web Fonts](https://www.onlinewebfonts.com/)
* Ikony postav z repozitáře od uživatele [tomozbot](https://github.com/tomozbot/botc-icons)
* Všechny další obrázky a ikony mají copyright na své vlastníky

Tento projekt a jeho webové stránky jsou poskytovány zdarma a nejsou nijak spojeny s The Pandemonium Institute.

## Poděkování
* Uživateli [Bra1n](https://github.com/bra1n) že vytvořil originální nástroj