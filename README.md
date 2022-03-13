# Edinburgh Bikeshare datova analyza

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

Python Folium
K zobrazeni jednotlivych stanic, jejich identifikacniho cisla, popisku a take poctu, kolikrat byla stanice vyuzita jsem vyuzila python knihovnu folium, ktera mi umoznila stanice zobrazit na openstreet map. Vuzila jsem moznosti DualMap, takze v leve casti pro stanice, kde byl pocatek vypujcky a v prave casti pro konecnou stanici vypujcky. Diky tomu jsme ziskali celkem rychly prehled kde se jaka stanice nachazi, v ktere casti Edinburgu jsou cetnost stanic pro zacatek vypujcky a v ktere casti zase naopak pro ukonceni vypujcky. Ke kazde stanici je vytvoren popisek, ve kterem je oznaceno identifikacni cislo stanice, jmeno konkretni stanice, popis ktery nam charakterizuje tuto stanice ( ne ve vsech pripadech - nekde tato hodnota chybi) a take pocet, kolikrat stanice byla vyuzita v prubehu celeho sledovaneho obdobi. Tento soubor ma format .html proto je nacten do repozitatoru samostatne. Python Folium a DualMap jsem vyuzila jeste i k interaktivnimu zobrazeni vypujcek v prubehu dne. Toto zobrazeni je take soubor .html a je take ulozen v repozitari. Ukazuje stanice a jejich uziti v prubehu denni doby.
