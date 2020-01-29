## INTRO
	Táto časť Geeky bude venovaná nášmu pohľadu na analýzu úlohy. Porovnáme si dve načastejšie
	prístupy pri v'voji frontendovej aplikácie a povieme si načo je dobrá izolácia komponentov
	v React apke.

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

	Pod pojomom "izolovaný komponent" máme na mysli, že komponent sám o sebe je funkčný aj bez
	pripojenia k aplikácii alebo jej reálnym dátam. Komponent má zvyčajne nejaké možné stavy.
	Cieľom izolovaného behu komponentu je preveriť, či reaguje na dané stavy a či jeho funkčnosť
	pre tieto rozličné stavy je správna.

	To môže prinášať nasledovné situácie a otázky.

### App as whole does not exist yet, you can't connect your component yet.
	V počiatočných fázach projektu nastáva situácia, že ešte nemáme kde komponent pripojiť.
	Na izolovaný beh budeme musieť použiť niečo iné.

### How to see those visual states immediatelly ?
	Chceme nástroj aby sme podľa možnosti vedeli hneď vidieť a otestovať všetky relevantné stavy
	komponentu hneď ako je naprogramovaný, podľa možnosti ešte na počítači vývojára bez nutnosti
	nejakého deploymentu.

### Write some mock wrapper ?
	Môžme si napísať nejaký ad-hoc kus kódu, ktorý pripojí komponent a vykreslí ho ?

### Will be mock reusable or thrown away when we are done ?
	Čo s tým ad-hoc kódom, bude sa dať využiť aj pre iné komponenty ? Bude využiteľný aj keď
	komponent bude hotový ?

### How to test code ? Regression ?
	Bude ten ad-hoc kód schopný slúžiť ako test ? Bude vedieť spozorovať regresné odchýlky ak sa
	niečo počas vývoja zmení ?

### Code struture
	V podstate ide o to aby všetky potrebné súbory komponentu boli na jednom mieste a v rámci
	reusability boli jednoducho prenositeľné do prípadného iného projektu.

	Pokec k scss, tsx a story
	Pokec k container, test a mock

## Example

### Vision
	Obrázok [] toto bola naša vízia ako pripraviť zoznam kanálov s eventami. Ako prvý
	znovupoužiteľný komponent bol identifikovaný ChannelNumber. Je prítomný v každom kanáli,
	je pomerne jednoduchý - jeho úlohou je len zobraziť číslo kanálu. Vizuálne stavy sú v podstate
	dva - číslo ak má kanál eventy, a číslo ak nemá eventy.

### ChannelNumber code
	easy

## HOW TO RUN COMPONENT IN ISOLATION	
	Komonent máme hotový, poďme teda k možnostiam izolovaného behu.

### all-by-my-self
	Môžme si napísať vlastnú mini apku, ktorá použije komponent a zavoláme ho s rozličnými
	parametrami. Emotikony hovoria asi sami za seba, že to nie je dobrý nápad a isto sa už daným
	problémom niekto zaoberal.

### React Styleguidist
	Jeden z prvých a najkomplexnejších nástrojov. Z nášho pohľadu šlo skôr o kanón na vrabce,
	pretože je to skór interaktívna dokumentácia ku komponentom. Jej využitie sa vyplatí až pri
	veľkých projektoch alebo v teamoch tvoriacich komplexné riešenia na Reacte a potrebujú mať
	knižnicu existujúcich komponentov s podrobným popisom. 
	Ukázať web []

### Storybook
	Pre nás zlatá stredná cesta. Jednoducho integrovateľný do React projektu, rýchla laerning
	curve, jednoduché použitie a možnosť napojenia na Jest test runner. S pomocou StoryShot
	pluginu jednoducho realizovateľné regresné testy. Stále sa bavíme o lokálnom počítači
	developera, žiadny deploy a v podstate bežateľné aj offline.

### ChannelNumber stories code
	easy - pozeráme na to aj testovacími očami, stavov je viac než dva. Ako zvládne vykreliť
	veľké číslo ? Čo ak chýba číslo ? Fungujú default hodnoty ?

### Isolation run in Storybook
	easy, Ukázať spustený []

### Code coverage
	easy

### Regression html aj css
	easy





