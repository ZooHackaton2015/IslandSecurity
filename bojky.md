# Problém
Pytláci chytají ptáky sbírají želví vajíčka. Přijíždějí v lodích, takže cíl je nějak poznat, že někam přijíždí loď a dát to vědět Rangerům. 

# Řešení
Technologická řešení narážejí hlavně na problém s napájením a přenosem informace v členitém terénu na delší vzdálenosti (až 10), špatných atmosferických podmínkách jako bouře, vlny, vysoká vlhkost. Pro dosažení řešení je tedy nutné eliminovat hlavně tyto problémy.

## Balóny s foto
První nápad byl (pravděpodobně nad nejvyšším místě uprostřed ostrova) upevnit balóny, které by pořizovaly 360° snímky z pobřeží. 
### Nevýhody: 
* rozlišení snímků by bylo nedostatečné
* vysoká pořizovací cena kvalitní elektroniky
* méně odolává povětrnostním vlivům jako bouře
* instalace (nedostupnost)

## Kamery na pobřeží
### Nevýhody: 
* množství kamer, pořizovací náklady

## Bóje
Rozmístit síť bójek kolem ostrova, které by detekovali přijíždějící lodě. Pokud by na některé z bójek detekovala připlouvající loď, pak by vyslala daný signál Rangerovi, který by věděl u které bójky se co děje.

### Nevýhody:
* rozeznávání rybářských lodí od lodí pytláků

Vzhledem k tomu, že větší problém než želví vajíčka jsou ptáci, větší důležitost má poznat lodě, který plují řekami do vnitrozemí. Z toho vyplývá, že bójky zachycující zvuk motorů je vhodné umístit do ústí řek. Nenastává problém s rozeznáním lodí rybářské od pytlácké.

Řešení pomocí bóji za ústím řek či v zálivech se nám zdá jako nejschůdnější varianta. Bóje samotná i technická řešení přenosu dat a rozpoznání nemusí být nákladné a je poměrně jednoduché. Během brainstormingu jsme navrhli několik různých variant, které vyžadují další zkoumání a praktické experiemnty (výdrž, dosah, ...). 

### Návrh
![model_buoy](https://raw.githubusercontent.com/ZooHackaton2015/IslandSecurity/master/imgs/boje.png)

Celý návrh se dá rozdělit na několik dílčích částí, které je možné řešit odděleně:

1. Provedení bóje - obalu pro celé zařízení a uchycení
2. Detekce lodi
3. Komunikační zařízení

Následuje komentář a varianty k jednotlivým částem.

#### Provedení bóje
Bóje musí dlouhodobě odolat slané vodě a vlnám (které by však v *řekách* měli být menší) - šlo by snad i levně vytisknout na 3D tiskárně, stejně tak jako krabičku na elektroniku. Varianty technického řešení detekce a komunikace jsou poměrně malé - orientačně kolem 15x8x5cm (bez baterie) - bóje tedy nemusí být o přiliš větší než klasické bóje. 

Dle velikosti vln v těchto zátokách musí být korektně vyřešené uchycení. Bóje by mohla být i pod vodou uchycená na tak dlouhém laně/řetězu, aby byla těsně pod hladinou a nebyla tak vidět. Zároveň tak, aby byla možná jednoduchá výměna. 

Ani tvar bóje nemusí být nutně klasický kulový. Například válec a nebo kvádr by měl výhodu plochého dna. To ulehčuje přichycení elektroniky a eventuálně i přístup. Nemluvně o jednodušší výrobě. Tvar určitě doporučujeme zvážit. 

*Pozn.*: Řešili jsme i variantu umístění "bóje" mimo vodu, ale varianta ve vodě nám přijde výhodnější. Za prvé je tam méně rušivých zvuků a dle dostupných informací se k nim lze jednoduše dostat. 

#### Detekce lodi
Na detekci jsme uvažovali:

* Mikrofony pod hladinou zaznamenávaly zvuk motorů, případně nějaký akcelerometr...
* Sonary pod vodou: malý dosah, cena
* Paprsky nad hladinou: Nemusí je protínat pouze loď, navíc provedení není jednodušší než mikrofony pod vodou.

Jako nejlepší se nám tedy zdá použití buď mikrofonu a nebo nějakého akcelerometru. Mikrofon by byl pravděpodobně jistější, má však větší spotřebu. Detekce by se zapínala například každých pár sekund (opět kvůli spotřebě). Pokud by zařízení detekovalo lodní motor, aktivovalo by hlavní jednotku a ta odeslala signál rangerovi. 

#### Komunikační zařízení
Toto je nejproblematičtější část. Bude nutné vše otestovat a vyzkoušet. Vzhledem k použití relativně nových technologií není dostupných příliš mnoho informací například o reálných testech spotřeby a dosahu.

Naše řešení předpokládá využití poměrně nové technologie Low-Power Wide-Area Network (respektive jejích reprezentantů). Aktuálně existují prakticky 2 řešení které přicházejí v úvahu. Prvním je SIGFOX, druhým je LoRa. Nebudeme je popisovat do detailů, ale zmíníme jejich výhody a nevýhody. Důvod proč nevybrat stávající technologie jako WiFi, GSM nebo Bluetooth je vysoká spotřeba a nebo nízké dosah (a nízké pokrytí GSM v lokalitě). 

##### Model SIGFOX
![SIGFOX](https://raw.githubusercontent.com/ZooHackaton2015/IslandSecurity/master/imgs/SIGFOX.png) 
##### Model LoRa
![lora](https://raw.githubusercontent.com/ZooHackaton2015/IslandSecurity/master/imgs/LoRa.png)

* [SIGFOX](http://www.sigfox.com/): K tomuto řešení je nutné mít pokrytí v dané lokaci od nějakého operátora se smlouvo s firmou SIGFOX. Jde o obdobu klasických GSM (mobilních) sítí, ale nejsou spolu kompatibilní. Bylo by tedy nutné postavit na ostrově jejich BTS (základovou stanici). Ta navíc momentálně musí být připojena k internetu. Od firmy SimpleCell máme informace, že SIGFOX momentálně vyvijí variantu s lokální sítí bez internetu, ale to je na úrovni státu jako pro Ruskou federaci nebo Jižní Ameriku. Nejsou známé informace o tom, že by bylo možné si vytvořit vlastní cloudy a tak mít lokální sigfox síť. Toto řešení má nicméně výhodu většího dosahu a menší spotřeby. Dále se musí platit měsíční či roční předplatné. Prý by se mohli v budoucnu objevit jakési *microBTS*, ale o tom opět nejsou žádné spolehlivé a dohledatelné informace a momentálně veřejně není dostupný jediný příklad použití této varianty (stejně jako lokální sítě).Byl-li by na ostrově dostupný internet a bylo by-li levné pořídit BTS (s nízkým napájením), pak by toto řešení bylo vhodné. 
* [LoRa](http://www.microchip.com/design-centers/wireless-connectivity/embedded-wireless/lora-technology): LoRa je varianta LPWAN, která není vázaná na jeden centrální cloud jako SIGFOX - lze tedy vytvořit i lokální síť bez nutnosti připojení k internetu. Má větší spotřebu a menší dosah, potenciálně však stále dostatečný. Dle našich informacích se pohybuje do 20 km na volném prostranství a 2 km v zástavbě. Demonstrace takových zařízení jsou dnes už běžně dostupné (existuje například LoRa Fabian - síť ve městech). LoRa mohou implementovat všichni, tudíž nehrozí že se v případě krachu jedné společnosti zažízení stanou nepoužitelná. Komunikace může být obousměrná a rychlejší (to však nepotřebujeme, ale je dobré to zmínit).

Testování bychom tedy doporučili za použití technologie LoRa, jelikož v cílové lokace je alespoň teoreticky její fungování možné ihned s dostupnými prostředky. Pokud by se varianta ukázala jako neprůchozí, stálo by za to zkusit SIGFOX.

#### Technické provedení komunikačního zařízení
U obou řešení je možné zakoupit vysílací jednotky v ceně asi 50 dolarů. K nim je potřeba přikoupit ještě nějakou řídící jednotku, do které se připojí. Takovou jednotkou může být například Raspberry Pi (kde je problémem velká spotřeba) a nebo mnohem jednodušší nějaká varianta Arduina. Do této jednotky by bylo zapojeno i detekční zařízení a po zaregistrování lodi by spustilo právě vysílací jednotku.

U LoRy je nyní dostupné i zařízení [http://www.froggyfactory.com/froggy/](Froggy), které nepotřebuje řídící jednotku - to by mohlo ušetřit na spotřebě. Cena je kolem 99 Euro. 

Jednotky by pravděpodobně vysílaly nějaký signál typu keep-alive - například každý den vyslali zprávu o tom, že jsou v pořádku. Jinak by ale byly v nečinnosti a byly by aktivované jen v případě aktivace detekčním zařízením. To ušetří celkovou spotřebu.

Rangerovo přijímací zařízení by mohlo být v obou případech notebook, minipočítač typu RPi (nizká spotřeba) a nebo nějaké obdoba konzole s mnohem jednodušším rozhraním a displejem (opět kvůli šetření energie). V případě LoRy jsou přijímače a vysílače stejné zařízení. U SIGFOXu jsou vysílače odlišné od přijímačů. 

Problémem je členitý terén ostrova, hlavně přijímač u rangera, který je dle informací na úrovni moře a kolem je sráz. To může být velký problém a pro funkční zařízení by bylo nutné umístit nějaké middle-pointy po ostrově a nebo alespoň použít nějaké antény. To je potřeba však skutečně vyzkoušet. 

# Cenový odhad
Cena se samozřejmě bude odvíjet od vybraných technologií. Zde je jejich přibližný přehled s příklady:

1. Mikrofon - $7 [1](http://www.banggood.com/5Pcs-KY-038-Microphone-Sound-Sensor-Module-For-Arduino-p-953185.html)
2. Raspberry Pi - $30 
3. Arduino - $10-30
4. Tisk bóje - $30 (za materiál)
5. LoRa shield - $55
6. SIGFOX shield - $50 (nižší při větších odběrech, řádově stovky až tisíce)
7. Uchycení, krabičky, drátky, pájení... - $20

Jedna bóje s jedním rangerovým přijímačem by se tedy mohlo pohybovat kolem $250. Každá další bóje pak kolem $100. 

# Poznámky
* Ke sbírání vajíček s loděmi nepřiplouvají až ke břehu, ke břehu pouze plavou. K chytání ptáků plují řekami do vnitrozemí.
* K napájení by se daly samozřejmě využít solární panely. To však značně stěžuje konstrukční provedení celého řešení a zvyšuje jeho cenu. Možná však, že to bude nevyhnutelné. V případě tvaru bóje do například válce nebo kvádru by to bylo poměrně jednoduché provést. Cena panelů se již pohybuje řádově v desítkách dolarů (např. [zde](http://www.ebay.co.uk/sch/items/?_nkw=40+watt+solar+panel&_sacat=&_ex_kw=&_mPrRngCbx=1&_udlo=&_udhi=&_sop=12&_fpos=&_fspt=1&_sadis=&LH_CAds=&clk_rvr_id=1012026245183&rmvSB=true), nebo pro [RPi](http://www.reuk.co.uk/Solar-Powered-Raspberry-Pi.htm))

# Zdroje
* [využití LoRa - froggy](http://www.froggyfactory.com/froggy/)
* [ceny desek LoRa - froggy](http://www.froggyfactory.com/froggy/shop.php#shop)
* [LoRa Things Network wiki](http://thethingsnetwork.org/wiki/)
* [DIY LoRa GateWay](http://cpham.perso.univ-pau.fr/LORA/RPIgateway.html)
* [LORAIOT](https://www.loriot.io/gateways.html)
* [Testing LoRa module for RPi/Arduino](https://www.cooking-hacks.com/documentation/tutorials/extreme-range-lora-sx1272-module-shield-arduino-raspberry-pi-intel-galileo/)
* [SIGFOX @ lupa.cz](http://www.lupa.cz/clanky/sigfox-internet-veci-bez-internetu-a-jen-pro-nektere-veci/)
