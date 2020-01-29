## INTRO
_@TODO_

## TOP DOWN - APP DESIGN

### Common in Web Development

	Je najbežnejší prístup pri programovaní web stránok či web aplikácií.

### You get design, wireframe or some framework theme

	Často od dizajnérov dostanete ako má vyzerať výsledné dielo.

###  You start think in HTML structure
	Pri plánovaní vývoja začnete myslieť a rozoberať na štruktúru aplikácie podobne ako vyzerá štruktúra
	HTML dokumentu.

### Header, footer, body, sections of body
	Rozoberiete dizajn na sekcie ako sú záhlavie a päta, rozdelíte telo na sekcie atď.

	Nechcem povedať, že tento prístup je zlý, pretože u množstva projektov, hlavne jednoduchších má
	zmysel.

**Prináša ale tieto možné riziká:**

### Focus on bigger picture
	Sústredíte sa skôr na to čo má daný modul či sekcia robiť
	
### Leads to less attention to detail
	A menej pozornosti sa môže dostať k samotnej implementácii - ako to má robiť. Niektoré detaily pri
	prvotnom návrhu zanedbáte a vyplavú na povrch až neskôr.
	
### Less precise estimations
	To vedie k podceneniu pracnosti a nepresným odhadom na realizáciu či potrebné ľudské zdroje.
	
### Often leads to tight coupling
	Ďalším možným dôsledkom je, že časti sú pevne prepojené na nadradený celok alebo dokonca dochádza
	k duplicite keď nejaká časť je implementovaná viac krát v rôznych sekciách, hoci by stačila jedna
	univerzálnejšia. Nižšie časti vedia o vyšších a vznikajú závislosti.

## BOTTOM UP - APP DESIGN

### Opposite approach
	Je opačný prístup pri analýze projektu.

### Think first of small and reusable components of app
	Snažime sa najskôr identifikovať opakujúce sa prvky, atomické elementy a z nich sa postupne budú
	vyskladávať nadradené sekcie. Zo sekcií aplikačné moduly a nakoniec to zastreší vrchná vrstva
	aplikácie. Lego princíp.
	
	V našom prípade šlo o remake pôvodnej Flash aplikácie, ktorá vyzerala takto []. Takže z UI
	pohľadu môžme hneď identifikovať nejaké základné prvky, ktoré v React svete nazývame komponenty.
	
### Not only visual components, those can be viewed as components too:
	Taktiež je vhodné myslieť "komponentovo" aj pri nie-UI častiach systému. Sú to tiež kocky Lega,
	ktoré napriek svojej špecifickosti tvoria súčasť aplikácie, alebo su podporou pri vývoji a
	nasadení.
	
**Výhody Bottom up**
	
### Planning view - how many of components we need to build app
	Ak máme apku rozdelenú na komponenty vieme povedať, ktoré treba nakódiť, ktoré je možné použiť
	3rd party.

### Logistic view - better estimations and resource planning
	Vzhľadom na detailnejšiu analýzu vieme presnejšie alkovať potrebnch vývojárov, testerov a čas.

### Loose coupling
	Keďže je dôraz na reusability tak jednotlivé komponenty sa snažíme nakódiť ako izolované a
	ich väzby na nadradené časti sú len smerom zhora. Samotný komponent nevie o vyšších
	vrstvách nič.
	
**Nevýhody Bottom up**

### Prehľad
	Pri veľkých a dlho trvajúcich projektoch sa môžme "strácať" => použiť vhodné nástroje.

### Integrácia
	"Pre stromy nevidíme les", alebo základná poučka kybernetiky "Ak sú časti systému stabilné,
	neznamená to že máme stabilný systém" => CI, priebežné testy stability, výkonnosti, spätná
	väzba od užívateľov atď.

## ISOLATED COMPONENTS
_@TODO_
