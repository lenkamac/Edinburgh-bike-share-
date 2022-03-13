# Edinburgh Bike-share datova analyza

Projekt pro engeto akademii - analyza Bikeshare v Edinburgu je provedena v jupyter notebook s pomoci knihoven pro python - folium,seaborn,matplotlib, pandas a geopy.
Upozorneni: Datove soubory vyuzite v teto analyze ve formatu CSV jsou zde do repozitatoru nahrane v podobe souboru Zip a to z toho duvodu, ze jsou prilis velke.

# Prehled
V tomto projektu pouzivame Python a jeho knihovny a ma nam vysvetlit system sdileni kol v Edinburgu, ktery probihal od podzimu 2018 kdy byl zahajen az do leta roku 2021,kdy byl ukoncen. V tomto projektu budeme odpovidat na par otazek a take tvorit deskritptivni statistiku.

# Nastroje potrebne k projektu
- Python 3 - projekt je zpracovan pomoci Python 3.9 a virtual enviroment (zde byla pouzita instalace Anaconda)
- jupyter notebook
- dam upozorneni, ze projekt je tvoren na systemu  Linux Ubuntu Server, bohuzel nektere pouzite knihovny jsou velmi narocne na vykon :-))

# Postup
Jako prvni importujeme vsechny potrebne knihovny, ktere bychom k analyze mohli potrebovat. Ja jsem vyuzila python 3.9 a k nemu knihovny - python Pandas, Folium, Geopy, Matplotlib, Numpy, Seaborn, Datetime a Math. Dale si naimportujeme nase soubory ve formatu CSV - edinburgh_bikes.csv a edinburgh_weather.csv. V repozitatoru jsou tyto dva soubory nahrane ve formatu ZIP.
Pri prvotnim pruzkumu datasetu edinburgh_bikes.csv vyplynulo, ze tento dataset obsahuje celkove 14 sloupcu a 438259 radku dat ruznych datovych typu. U datasetu edinburgh_weather.csv to je 11 sloupcu a 6336 radku.
Pro svou analyzu jsem si vybrala jako stezejni informaci sloupce, ktere obsahuji identifikacni cislo stanice. Kazda stanice ma sve vlastni unikatni identifikacni cislo a je mozno provest presnejsi analyzu.
U sloupcu v datasetu bikes, ktere mely nevhodny datovy typ jsem provedla pretypovani - tyka se to hlavne sloupcu s casovymi zaznamy, jako je datum, kdy vypujcka zacala a kdy skoncila. Po prevodu techto udaju jsem dostala vystup v podobe datoveho typu datetime, ktery nam nasledne umoznil ziskat mnohem vice hodnot souvisejicich prave s casovym udajem napr. mesic, rok, tyden, hodiny atd. U datasetu weather bylo vse trochu obtiznejsi, hodnoty obsahovaly jak numericky typ tak string a byly ulozeny v datovem typu object. Zde jsem to resila pomoci regulerniho vyrazu a nasledneho pretypovani, az jsem si vytvorila dataframe obsahujici jen hodnoty potrebne pro mou analyzu.

# Python Folium
K zobrazeni jednotlivych stanic, jejich identifikacniho cisla, popisku a take poctu, kolikrat byla stanice vyuzita jsem vyuzila python knihovnu folium, ktera mi umoznila stanice zobrazit na openstreet map. Vyuzila jsem moznosti DualMap, takze v leve casti pro stanice, kde byl pocatek vypujcky a v prave casti pro konecnou stanici vypujcky. Diky tomu jsme ziskali celkem rychly prehled kde se jaka stanice nachazi, cetnost stanic pro zacatek vypujcky a  naopak pro ukonceni vypujcky pro jednotlive mestske casti Edinburghu. Ke kazde stanici je vytvoren popisek, ve kterem je oznaceno identifikacni cislo stanice, jmeno konkretni stanice, popis ktery nam charakterizuje tuto stanice ( ne ve vsech pripadech - nekde tato hodnota chybi) a take pocet, kolikrat stanice byla vyuzita v prubehu celeho sledovaneho obdobi. Tento soubor ma format .html proto je nacten do repozitatoru samostatne. Python Folium a DualMap jsem vyuzila jeste i k interaktivnimu zobrazeni vypujcek v prubehu dne. Toto zobrazeni je take soubor .html a je take ulozen v repozitari. Ukazuje stanice a jejich uziti v prubehu denni doby. Z duvodu velikosti je tento soubor komprimovan do souboru ZIP. K vypoctu polohy stanic jsou vyuzity udaje o langtitude a longtitude pro kazdou stanici v nasem datasetu. 

# Distance - vzdalenost
V teto casti jsem se venovala vzdalenosti mezi jednotlivymi stanicemi. Pomoci langtitude,longtitude a matematicke haversinovy formule jsem mohla spocitat vzdalenosti mezi stanicemi po cele sledovane obdobi. Po provedeni prvni descriptivni statistiky se ukazalo, ze maximalni vzdalenost mezi stanicemi byla 285 km a tykalo se to tri datovych zaznamu. Pri blizsim zkoumani vyslo najevo, ze tyto udaje by mohly byt chybne - nejspis chybny zapis v hodnotach langtitude nebo longtitude, protoze udaje v techto radcich neodpovidali mozne realite (casovy udaj vychazel nerealne v souvislosti s touto vzdalenosti) a proto jsem tyto tri datove zaznamy z celkove analyzy vzdalenosti odstranila. Vzdalenost jsem pro snadnejsi predstavu pocitala v Kilometrech. Z descriptivni statitiky vyplyva, ze nejdelsi vzdalenost byla 18.4 km ze stanice Dalmeny Station do stanice Joppa.

![Distance_graf_png](https://user-images.githubusercontent.com/72987557/158071182-d8979332-52d3-4930-bbe8-5822eb10db91.png)

Vyse uvedene grafy Distance nam ukazuji vzdalenost v souvislosti s jinymi promennymi. Frequency distance nam ukazuje cetnost vzdalenosti. Muzeme videt ze opravdu velke mnozstvi vypujcek je pro vzdalenost 0 az 2 Km. Cim delsi vzdalenost tim mensi pocet, kolikrat ta vzdalenost byla absolvovana. Take mame vzdalenost v pomeru ke dni v tydnu, ze ktereho vyplyva, ze o vikendu konkretne v sobotu byva vzdalenost delsi, kdezto uprostred tydne byva kratsi. Dale je zde graf vyvoje vzdalenosti v ramci celeho sledovaneho obdobi, tedy od podzimu 2018 do leta 2021. Celkem logicky je nejvyssi vzdalenost v letnich mesicich. Tento udaj jde lepe videt na poslednim grafu, kde je zobrazena vzdalenost pro jednotlive dny v tydnu. Vsechny hodnoty jsou brany jako prumer. V datasetu najdeme i 0 distanci, ale ve sloupci pro dobu trvani je uvedena casova hodnota - to by se dalo vysvetlit tim, ze si kolo pujcim i vratim na stejne stanici.

# Duration - doba trvani vypujcky
V teto casti analyzy se podivame na dobu trvani vypujcky. Uz na zacatku analyzy je upravena hodnota sloupce duration a to tak, ze je prepocitana na dobu vypujcky v minutach a ne sekundach. Pro cast analyzy tykajici se doby trvani vypujcky jsem vyfiltrovala udaje , kde vzdalenost je mensi nez 280 km, protoze jsou zde predpokladany chybne udaje. Z vypoctu descriptivni statistiku muzeme ve vztahu k dobe vypujcky konstatovat, ze prumerna doba vypujcky je zhruba 32 minut, minimalni doba vypujcky je 1 minuta = zde bych se priklanela k tomu, ze byla vypujcka provedena ale hned nasledne taky zrusena. Maximalni doba vypujcky je hodne velka, takze by se to dalo vysvetlit tim, ze byla vypujcka provedena, ale clovek kolo vratil az po delsi dobe. Pri grafickem zobrazeni jsem omezila dobu vypujcky na 120 minut.

![Duration-Bike_Share](https://user-images.githubusercontent.com/72987557/158072550-293061f5-9db4-4a95-a6c5-7fd30270602c.png)

V hornich grafech mame zobrazenou dobu vypujcky. Hranici vypujcky jsem urcila v interaval od 1 minuty do 120 minut, protoze moc delsich casovych intervalu vypujcky dataframe neobsahuje. Prumer vypujcky je kolem 30 minut. Delka trvani vypujcky je nejvyssi o vikendu v roce 2020 a 2019, ale je to ovlivneno tim, ze data pro rok 2018 a 2021 nejsou kompletni - zaznamy zacinaji na podzim v roce 2018 a konci v lete 2021. Z grafu muzeme vycist ze dlouha doba vypujcky je hlavne o vikendu, kde prevlada sobota a take v jarnich a letnich mesicich. V lete je prumer 40 minut na vypujcku nejmene je v zimnim obdobi a to kolem 25 minut na vypujcku. Nejcasteji se vyskytujici vypujcky v prubehu celeho roku trvaji 10 az 20 minut.

![Averige bike-share by month](https://user-images.githubusercontent.com/72987557/158073194-b773d9de-931a-4759-b8c8-9e7ede15dded.png)

- vyse uvedeny graf znazornuje prumerny pocet vypujcke pro jednotlive mesice. Z logiky veci samozrejme je jasne ze letni mesice maji prumerne mnohem vice vypujcek nez zimni mesice.

![Counts bike-share by date and hours](https://user-images.githubusercontent.com/72987557/158073268-65c7f00f-9f39-46b4-a427-c3772ca41880.png)

- tento graf ukazuje prumerny pocet vypujcek v souvislosti s denni dobou pro konkretni den v tydnu. Muzeme zodpovedet otazku, v kterou denni dobu probiha nejvice vypujcek pro jednotlive dny v tydnu. Da se predpokladat, ze o vikendu prevazuji vypujcky od 9 hodiny ranni do 15 hodiny odpoledni, v pracovni dny se do pohybuje vice v drivejsich rannich hodinach a nasledne kolem 17 hodiny odpoledni.

![counts bike-share by season,month,weekday and weekend](https://user-images.githubusercontent.com/72987557/158073750-0faedd46-da3c-4df0-b8e3-2cb753027926.png)

![bike-share for weekday](https://user-images.githubusercontent.com/72987557/158073824-d5a9a1f0-d67a-4e2f-95b3-e75ae8653a21.png)

![Counts by date and year](https://user-images.githubusercontent.com/72987557/158073885-453241ae-b297-4609-b8db-4d0e39fec2dd.png)

Ctyri liniove grafy ukazujici vyvoj vypujcek v prubehu jednotlivych let a k datu. Uz bylo zmineno,ze rok 2018 a 2021 jsou nekompletni. Pro rok 2020 si muzeme vsimnout ze zde mame atakovanou hranici 2000 vypujcek za den, o rok drive byla hranice 1000 vypujcek za den. Lze i odhadnout mnozstvi vypujcek pro jednotlive rocni obdobi.

# Grafy ukazujic stanice a jejich ID, ktere jsou nejvice a nejmene uzivane.

![Maximal and minimal frequence for start and end stations](https://user-images.githubusercontent.com/72987557/158073984-d379a971-9888-46fa-812f-09191ffce6e0.png)

Z vrchniho grafu muzeme vycist, ze stanice ze ktere je provedeno nejvice vypujcek ma ID 265 a jmeno Meadows East - celkovy pocet vypujcek na teto stanici presahl 17000, konkretne 17390. Nejmene vyuzite pocatecni stanice jsou 1857 City Chambers Launch Station a take 1740 Cycling Scotland Conference. U konecnych stanice je nejvice vyuzivana stanice ID 1728 Portobello-Kings Road, kdy pocet presahl 16000 a nejmene vyuzivane 1740 Cycling Scotland Conference a take 242 Virtual Depot.

Pri standartni descriptivni statistice zjistime, ze pocet start_stations podle jejich unikatniho Id je 198 a end_stations je 199.  U pocatku je nejmenis pocet stanice jedno pouziti uz konecne stanice 2.

# Bikes and Weather - souvislost a vliv pocasi na vypujcky
Jak uz bylo vyse uvedeno, dataset pro weather jsem musela upravit a ziskat odpovidajici hodnoty a spravny datovy typ. Abych mohla provadet nejakou analyzu, bylo potreba tyto dva datasety, tedy bike a weather spojit dohromady. Protoze casove udaje v datasetu bike neodpovidaly casovym udajum datasetu weather, pripravila jsem si oba datasety casovym ohranicenim - to znamena tak, aby datum v datasetu bike odpovidalo datu v datasetu weather. To znamena ze vypujcky provedene v konkretnim datu probihaly pri pocasi ve stejnem datu. U datasetu weather jsem vzala prumer pro vsechny hodnoty - tedy prumernou teplotu, jaka byla prumerna rychlost vetru ci prumerne mnozstvi srazek. Dataset bike jsem upravila tak, abych mela datum, pocet vypujcek, prumernou dobu trvani a prumernou vzdalenost. Po spojeni techto dvou dataframe vznikla nova dataframe, ktera obsahovala relevantni udaje pro nasledne vypocty.

Pro zjisteni zavislosti promnenych navzajem jsem vyuzila moznosti metody corr() na dataframe. Diky teto metode me vznikla dataframe s hodnotami,ktere rikaji, jaka je tesnost zavisle promenne pri zmene nezavisle promenne. Nize je uvedeny graf i s hodnotamy korelace.

![Correlation bike-share and weather](https://user-images.githubusercontent.com/72987557/158074779-8f00636b-bd23-4695-a157-3bf16e4aee49.png)

Nize uvedene grafy linearni regrese nam ukazuji zavislost mezi velicinamy. V kazdem grafu je znazornena jako velicina x jedna nase promenna napr.teplota a jako velicina y druha promena napr.distance. V nasem pripade muzeme rict, ze pravdepodobne na teplote je zavisla distance a ne naopak. Stejne tak to vypovida graf, ktery se tyka doby trvani vypujcky, ze ktereho muzeme vcelku zato rict, ze tam mame primou zavislost - hodnoty se vyskytuji podel primky. Kdezto u poctu vypujcek jsou hodnoty vice rozsete, a tak lze konstatovat, ze pocet vypujcek neni uplne zavisly na tom, jake je pocasi.

![Relationship between bikeshare and weather - part1](https://user-images.githubusercontent.com/72987557/158074811-bfbfac11-1bf0-4009-9121-e439d660ea66.png)

Jako posledni je graf, ktery znazornuje souvislost mezi vypujckami, vlhkosti vzduchu a oblacnosti. Hlavni vlivy pocasi byly zobrazeny pomoci linearni regrese v jinem grafu, pro prehlednost jsem to trochu rozdelila.

![Relationship betwen bikeshare and weather - part2](https://user-images.githubusercontent.com/72987557/158074895-3ec84598-cc53-4979-b8ad-3339b8fdb227.png)

# Zaver
Co rict na zaver. Z pruzkumu, vypoctu a zobrazeni datasetu vyplyva, ze lide si pujcuji kola vice o vikendu a to nejvice v sobotu, zaroven se lisi doba vypujcek mezi vikendem a pracovnim dnem. Mame zjisteny stanice, ze kterych lide kola vypujcovali nejvice ale take nejmene. Pocasi urcity vliv ma, ale tento vliv neni uplne zasadni. Nektere stanice jsou vyuzivane tak malo, ze by bylo mozne je zrusit. Take vime ve kterem roce bylo provedeno nejvice vypujcek v jeden den. Vcelku jasny vystup je pro vypujcky v ruznych rocnich obdobich - celkem logicky nejvice v lete, nasledne na jare a pak podzim a zima. Stejne tak je to jasne v pripade mesicu v roce. Je zajimave ze napriklad delka trvani vypujcky je prozmenu prumerne vyssi na jare nez v lete, ale samozrejmen o vikendu jsou vypujcky delsi. Nejvice frekventovane vypujcky maji dobu trvani do 20 minut a frekvence vzdalenosti se pohybuje do 1.5 km.


