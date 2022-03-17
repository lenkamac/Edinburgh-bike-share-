# Edinburgh Bike-share datova analyza
# Edinburgh Bikeshare analysis for Engeto Data Academy

Projekt pro engeto akademii - analyza Bikeshare v Edinburgu je provedena v jupyter notebook s pomoci knihoven pro python - folium,seaborn,matplotlib, pandas a geopy.
Upozorneni: Datove soubory vyuzite v teto analyze ve formatu CSV jsou zde do repozitatoru nahrane v podobe souboru Zip a to z toho duvodu, ze jsou prilis velke.

Analysis of Bikeshare in Edinburgh is done in jupyter notebook using Python libraries - Folium, Seaborn, Matplotlib, Pandas and GeoPy.
Note: The data files used in this analysis are in format Zip and they are uploaded here to the repository as Zip files for the reason that they are too large.

# Prehled
# Overview
V tomto projektu pouzivame Python a jeho knihovny a ma nam vysvetlit system sdileni kol v Edinburgu, ktery probihal od podzimu 2018 kdy byl zahajen az do leta roku 2021,kdy byl ukoncen. V tomto projektu budeme odpovidat na par otazek a take tvorit deskritptivni statistiku.

In this project we use Python and his libraries to explain the Edinburgh bikeshare system, which ran from autumn 2018 when it was launched until the summer of 2021 when it was closed. In this project, we will answer a few questions and create descriptive statistic.

# Nastroje potrebne k projektu
# Tools for project
- Python 3 - projekt je zpracovan pomoci Python 3.9 a virtual enviroment (zde byla pouzita instalace Anaconda)
- jupyter notebook
- dam upozorneni, ze projekt je tvoren na systemu  Linux Ubuntu Server, bohuzel nektere pouzite knihovny jsou velmi narocne na vykon :-))

- Python 3 - the project is developed using Python 3.9 and virtual environment (Anaconda installation was used here)
- jupyter notebook
- I will warn you that the project is created on Linux Ubuntu Server, unfortunately some of the libraries used are very performance intensive :-))

# Postup
# Working procedure
Jako prvni importujeme vsechny potrebne knihovny, ktere bychom k analyze mohli potrebovat. Ja jsem vyuzila python 3.9 a k nemu knihovny - python Pandas, Folium, Geopy, Matplotlib, Numpy, Seaborn, Datetime a Math. Dale si naimportujeme nase soubory ve formatu CSV - edinburgh_bikes.csv a edinburgh_weather.csv. V repozitatoru jsou tyto dva soubory nahrane ve formatu ZIP.
Pri prvotnim pruzkumu datasetu edinburgh_bikes.csv vyplynulo, ze tento dataset obsahuje celkove 14 sloupcu a 438259 radku dat ruznych datovych typu. U datasetu edinburgh_weather.csv to je 11 sloupcu a 6336 radku.
Pro svou analyzu jsem si vybrala jako stezejni informaci sloupce, ktere obsahuji identifikacni cislo stanice. Kazda stanice ma sve vlastni unikatni identifikacni cislo a je mozno provest presnejsi analyzu.
U sloupcu v datasetu bikes, ktere mely nevhodny datovy typ jsem provedla pretypovani - tyka se to hlavne sloupcu s casovymi zaznamy, jako je datum, kdy vypujcka zacala a kdy skoncila. Po prevodu techto udaju jsem dostala vystup v podobe datoveho typu datetime, ktery nam nasledne umoznil ziskat mnohem vice hodnot souvisejicich prave s casovym udajem napr. mesic, rok, tyden, hodiny atd. U datasetu weather bylo vse trochu obtiznejsi, hodnoty obsahovaly jak numericky typ tak string a byly ulozeny v datovem typu object. Zde jsem to resila pomoci regulerniho vyrazu a nasledneho pretypovani, az jsem si vytvorila dataframe obsahujici jen hodnoty potrebne pro mou analyzu.

First we import all the libraries we might need for the analysis. I used python 3.9 and its libraries - python Pandas, Folium, Geopy, Matplotlib, Numpy, Seaborn, Datetime and Math. Next we import our CSV files - edinburgh_bikes.csv and edinburgh_weather.csv. In the repository these two files are uploaded in ZIP format.
An initial examination of the edinburgh_bikes.csv dataset shows that it contains a total of 14 columns and 438259 rows of data of various data types. For the edinburgh_weather.csv dataset this is 11 columns and 6336 rows.
For my analysis, I chose the columns containing the station ID as the staging information. Each station has its own unique ID number and a more accurate analysis can be performed.
For the columns in the bikes dataset that had an inappropriate data type, I performed a retype - this mainly concerns columns with time records, such as the date when the rental started and when it ended. After converting these data, I got the output in the form of datetime data type, which then allowed us to get many more values related to the time, e.g. month, year, week, hours, etc. With dataset weather everything was a bit more difficult, the values contained both numeric type and string and were stored in data type object. Here I solved it with a regular expression and subsequent retyping until I created a dataframe containing only the values necessary for my analysis.

# Python Folium
K zobrazeni jednotlivych stanic, jejich identifikacniho cisla, popisku a take poctu, kolikrat byla stanice vyuzita jsem vyuzila python knihovnu folium, ktera mi umoznila stanice zobrazit na openstreet map. Vyuzila jsem moznosti DualMap, takze v leve casti pro stanice, kde byl pocatek vypujcky a v prave casti pro konecnou stanici vypujcky. Diky tomu jsme ziskali celkem rychly prehled kde se jaka stanice nachazi, cetnost stanic pro zacatek vypujcky a  naopak pro ukonceni vypujcky pro jednotlive mestske casti Edinburghu. Ke kazde stanici je vytvoren popisek, ve kterem je oznaceno identifikacni cislo stanice, jmeno konkretni stanice, popis ktery nam charakterizuje tuto stanice ( ne ve vsech pripadech - nekde tato hodnota chybi) a take pocet, kolikrat stanice byla vyuzita v prubehu celeho sledovaneho obdobi. Tento soubor ma format .html proto je nacten do repozitatoru samostatne. Python Folium a DualMap jsem vyuzila jeste i k interaktivnimu zobrazeni vypujcek v prubehu dne. Toto zobrazeni je take soubor .html a je take ulozen v repozitari. Ukazuje stanice a jejich uziti v prubehu denni doby. Z duvodu velikosti je tento soubor komprimovan do souboru ZIP. K vypoctu polohy stanic jsou vyuzity udaje o langtitude a longtitude pro kazdou stanici v nasem datasetu. 

I used python folium and DualMap. This allowed me to display two maps with start and end stations on the openstreet map. I used it to display the individual stations, their unique ID, description and also the number of counts the stations was used. In the left part for the stations, where the rental started stations and in the right part for rental end stations. This gave us a pretty quick overview of where each station was located, frequency of stations and frequency stations for the different city districts of Edinburgh. For each station is created a label, in which is marked the identification number of the station, the name of the specific station, a description that describe this station(not in all - somewhere this value missing) and also the number of counts the station was used during the whole monitoring period. This file is in .html format so it is uploaded to the repository separately. I also used Python Folium and DualMap to interactively display the rentals during the day. This view is also a .html file and is also stored in the repository. It shows the stations and their usage during the day. For size reasons this file is compressed into a ZIP file. To calculate the position of the stations, the longitude and latitude data for each station in our dataset are used.

# Distance - vzdalenost
V teto casti jsem se venovala vzdalenosti mezi jednotlivymi stanicemi. Pomoci langtitude,longtitude a matematicke haversinovy formule jsem mohla spocitat vzdalenosti mezi stanicemi po cele sledovane obdobi. Po provedeni prvni descriptivni statistiky se ukazalo, ze maximalni vzdalenost mezi stanicemi byla 285 km a tykalo se to tri datovych zaznamu. Pri blizsim zkoumani vyslo najevo, ze tyto udaje by mohly byt chybne - nejspis chybny zapis v hodnotach langtitude nebo longtitude, protoze udaje v techto radcich neodpovidali mozne realite (casovy udaj vychazel nerealne v souvislosti s touto vzdalenosti) a proto jsem tyto tri datove zaznamy z celkove analyzy vzdalenosti odstranila. Vzdalenost jsem pro snadnejsi predstavu pocitala v Kilometrech. Z descriptivni statitiky vyplyva, ze nejdelsi vzdalenost byla 18.4 km ze stanice Dalmeny Station do stanice Joppa.

![Distance_graf_png](https://user-images.githubusercontent.com/72987557/158071182-d8979332-52d3-4930-bbe8-5822eb10db91.png)

Vyse uvedene grafy Distance nam ukazuji vzdalenost v souvislosti s jinymi promennymi. Frequency distance nam ukazuje cetnost vzdalenosti. Muzeme videt ze opravdu velke mnozstvi vypujcek je pro vzdalenost 0 az 2 Km. Cim delsi vzdalenost tim mensi pocet, kolikrat ta vzdalenost byla absolvovana. Take mame vzdalenost v pomeru ke dni v tydnu, ze ktereho vyplyva, ze o vikendu konkretne v sobotu byva vzdalenost delsi, kdezto uprostred tydne byva kratsi. Dale je zde graf vyvoje vzdalenosti v ramci celeho sledovaneho obdobi, tedy od podzimu 2018 do leta 2021. Celkem logicky je nejvyssi vzdalenost v letnich mesicich. Tento udaj jde lepe videt na poslednim grafu, kde je zobrazena vzdalenost pro jednotlive dny v tydnu. Vsechny hodnoty jsou brany jako prumer. V datasetu najdeme i 0 distanci, ale ve sloupci pro dobu trvani je uvedena casova hodnota - to by se dalo vysvetlit tim, ze si kolo pujcim i vratim na stejne stanici.

# Duration - doba trvani vypujcky
V teto casti analyzy se podivame na dobu trvani vypujcky. Uz na zacatku analyzy je upravena hodnota sloupce duration a to tak, ze je prepocitana na dobu vypujcky v minutach a ne sekundach. Pro cast analyzy tykajici se doby trvani vypujcky jsem vyfiltrovala udaje , kde vzdalenost je mensi nez 280 km, protoze jsou zde predpokladany chybne udaje. Z vypoctu descriptivni statistiku muzeme ve vztahu k dobe vypujcky konstatovat, ze prumerna doba vypujcky je zhruba 32 minut, minimalni doba vypujcky je 1 minuta = zde bych se priklanela k tomu, ze byla vypujcka provedena ale hned nasledne taky zrusena. Maximalni doba vypujcky je hodne velka, takze by se to dalo vysvetlit tim, ze byla vypujcka provedena, ale clovek kolo vratil az po delsi dobe. Pri grafickem zobrazeni jsem omezila dobu vypujcky na 120 minut.

In this part of the analysis we look at the duration. At the beginning of the analysis, the value of the duration column is adjusted so that it is recalculated to the rental time in minutes instead of seconds. For the part of the analysis concerning the duration of the rental, I have filtered out the data where the distance is less than 280 km, because the data are assumed to be wrong. From the calculation of the descriptive statistics we can conclude in relation to the rental time that the average rental time is about 32 minutes, the minimum rental time is 1 minute = here I would lean towards the fact that the rental was carried out but immediately afterwards also cancelled. The maximum rental time is very long, so it could be explained by the fact that the rental was done but the person returned the bike after a longer time. In the graphic display I limited the rental time to 120 minutes.

![Duration-Bike_Share](https://user-images.githubusercontent.com/72987557/158072550-293061f5-9db4-4a95-a6c5-7fd30270602c.png)

V hornich grafech mame zobrazenou dobu vypujcky. Hranici vypujcky jsem urcila v interaval od 1 minuty do 120 minut, protoze moc delsich casovych intervalu vypujcky dataframe neobsahuje. Prumer vypujcky je kolem 30 minut. Delka trvani vypujcky je nejvyssi o vikendu v roce 2020 a 2019, ale je to ovlivneno tim, ze data pro rok 2018 a 2021 nejsou kompletni - zaznamy zacinaji na podzim v roce 2018 a konci v lete 2021. Z grafu muzeme vycist ze dlouha doba vypujcky je hlavne o vikendu, kde prevlada sobota a take v jarnich a letnich mesicich. V lete je prumer 40 minut na vypujcku nejmene je v zimnim obdobi a to kolem 25 minut na vypujcku. Nejcasteji se vyskytujici vypujcky v prubehu celeho roku trvaji 10 az 20 minut.

In the upper graphs we have the rental period displayed. I set the borrowing interval from 1 minute to 120 minutes, because the dataframe does not contain many longer borrowing intervals. The average time is around 30 minutes. The duration of the rental is highest on weekends in 2020 and 2019, but this is influenced by the fact that the data for 2018 and 2021 are not complete - the records start in autumn 2018 and end in summer 2021. From the graph we can see that the long rental time is mainly on weekends, where Saturday prevails, and also in spring and summer months. In the summer, the average is 40 minutes per rental, the lowest is in the winter period, around 25 minutes per rental. The most frequent rentals throughout the year last 10 to 20 minutes.

![Averige bike-share by month](https://user-images.githubusercontent.com/72987557/158073194-b773d9de-931a-4759-b8c8-9e7ede15dded.png)

- vyse uvedeny graf znazornuje prumerny pocet vypujcke pro jednotlive mesice. Z logiky veci samozrejme je jasne ze letni mesice maji prumerne mnohem vice vypujcek nez zimni mesice.

- The above chart shows the average number of rentals for each month. Logically, of course, as emerged from the analysis that the summer months have much more rentals on average than the winter months.

![Counts bike-share by date and hours](https://user-images.githubusercontent.com/72987557/158073268-65c7f00f-9f39-46b4-a427-c3772ca41880.png)

- tento graf ukazuje prumerny pocet vypujcek v souvislosti s denni dobou pro konkretni den v tydnu. Muzeme zodpovedet otazku, v kterou denni dobu probiha nejvice vypujcek pro jednotlive dny v tydnu. Da se predpokladat, ze o vikendu prevazuji vypujcky od 9 hodiny ranni do 15 hodiny odpoledni, v pracovni dny se do pohybuje vice v drivejsich rannich hodinach a nasledne kolem 17 hodiny odpoledni.

Counts bikeshare by date and hours - this chart shows the average number of rentals in relation to the time of day for a specific day of the week. We can answer the question at which time of day the most rentals take place for each day of the week. It can be assumed that on weekends, the majority of rentals take place from 9 a.m. to 3 p.m., while on weekdays the number of rentals is higher in the early morning hours and then around 5 p.m.

![counts bike-share by season,month,weekday and weekend](https://user-images.githubusercontent.com/72987557/158073750-0faedd46-da3c-4df0-b8e3-2cb753027926.png)

![bike-share for weekday](https://user-images.githubusercontent.com/72987557/158073824-d5a9a1f0-d67a-4e2f-95b3-e75ae8653a21.png)

![Counts by date and year](https://user-images.githubusercontent.com/72987557/158073885-453241ae-b297-4609-b8db-4d0e39fec2dd.png)

Ctyri liniove grafy ukazujici vyvoj vypujcek v prubehu jednotlivych let a k datu. Uz bylo zmineno,ze rok 2018 a 2021 jsou nekompletni. Pro rok 2020 si muzeme vsimnout ze zde mame atakovanou hranici 2000 vypujcek za den, o rok drive byla hranice 1000 vypujcek za den. Lze i odhadnout mnozstvi vypujcek pro jednotlive rocni obdobi.

Four line graphs showing the development of borrowings over the years and to date. It has already been mentioned that 2018 and 2021 are incomplete. For the year 2020 we can notice that the limit of 2000 rentals per day has been reached, a year later the limit was 1000 rentals per day. It is also possible to estimate the number of rentals for each year.

# Grafy ukazujic stanice a jejich ID, ktere jsou nejvice a nejmene uzivane.
# Frequency start and end stations

![Maximal and minimal frequence for start and end stations](https://user-images.githubusercontent.com/72987557/158073984-d379a971-9888-46fa-812f-09191ffce6e0.png)

Z vrchniho grafu muzeme vycist, ze stanice ze ktere je provedeno nejvice vypujcek ma ID 265 a jmeno Meadows East - celkovy pocet vypujcek na teto stanici presahl 17000, konkretne 17390. Nejmene vyuzite pocatecni stanice jsou 1857 City Chambers Launch Station a take 1740 Cycling Scotland Conference. U konecnych stanice je nejvice vyuzivana stanice ID 1728 Portobello-Kings Road, kdy pocet presahl 16000 a nejmene vyuzivane 1740 Cycling Scotland Conference a take 242 Virtual Depot.

From the above graph we can see that the station from the most rentals stations are made has the ID 265 and the name Meadows East - the total number of rentals at this station exceeded 17000, namely 17390. The least used initial stations are 1857 City Chambers Launch Station and 1740 Cycling Scotland Conference. For the most used end station is ID 1728 Portobello-Kings Road, with over 16000 and the least used are 1740 Cycling Scotland Conference and 242 Virtual Depot.

Pri standartni descriptivni statistice zjistime, ze pocet start_stations podle jejich unikatniho Id je 198 a end_stations je 199.  U pocatku je nejmenis pocet stanice jedno pouziti uz konecne stanice 2.

In standard descriptive statistics we find that the number of start_stations according to their unique Id is 198 and end_stations is 199.  For start, the smallest number of stations per use is 2.

# Bikes and Weather - souvislost a vliv pocasi na vypujcky
# Bikes and Weather - their relationship
Jak uz bylo vyse uvedeno, dataset pro weather jsem musela upravit a ziskat odpovidajici hodnoty a spravny datovy typ. Abych mohla provadet nejakou analyzu, bylo potreba tyto dva datasety, tedy bike a weather spojit dohromady. Protoze casove udaje v datasetu bike neodpovidaly casovym udajum datasetu weather, pripravila jsem si oba datasety casovym ohranicenim - to znamena tak, aby datum v datasetu bike odpovidalo datu v datasetu weather. To znamena ze vypujcky provedene v konkretnim datu probihaly pri pocasi ve stejnem datu. U datasetu weather jsem vzala prumer pro vsechny hodnoty - tedy prumernou teplotu, jaka byla prumerna rychlost vetru ci prumerne mnozstvi srazek. Dataset bike jsem upravila tak, abych mela datum, pocet vypujcek, prumernou dobu trvani a prumernou vzdalenost. Po spojeni techto dvou dataframe vznikla nova dataframe, ktera obsahovala relevantni udaje pro nasledne vypocty.

As mentioned above, I had to edit the dataset for weather and get the corresponding values and the correct data type. In order to perform some analysis, I needed to combine these two datasets, i.e. bike and weather, together. Because the time data in the bike dataset did not match the time data in the weather dataset, I prepared both datasets with a time limit - that is, so that the date in the bike dataset matched the date in the weather dataset. This means that the rentals made on a specific date were made on the same weather date. For the weather dataset I took the average for all values - i.e. the average temperature, the average wind speed or the average number of collisions. I modified the bike dataset to have the date, number of runs, average duration and average distance. After combining these two dataframes, a new dataframe was created that contained the relevant data for the subsequent calculations.

Pro zjisteni zavislosti promnenych navzajem jsem vyuzila moznosti metody corr() na dataframe. Diky teto metode me vznikla dataframe s hodnotami,ktere rikaji, jaka je tesnost zavisle promenne pri zmene nezavisle promenne. Nize je uvedeny graf i s hodnotamy korelace.

To find out the dependency of the variables on each other I used the corr() method on the dataframe. This method I got a dataframe with values that tell me how tight the dependent variable is when the independent variable is changed. Below is the graph with the correlation values.

![Correlation bike-share and weather](https://user-images.githubusercontent.com/72987557/158074779-8f00636b-bd23-4695-a157-3bf16e4aee49.png)

Nize uvedene grafy linearni regrese nam ukazuji zavislost mezi velicinamy. V kazdem grafu je znazornena jako velicina x jedna nase promenna napr.teplota a jako velicina y druha promena napr.distance. V nasem pripade muzeme rict, ze pravdepodobne na teplote je zavisla distance a ne naopak. Stejne tak to vypovida graf, ktery se tyka doby trvani vypujcky, ze ktereho muzeme vcelku zato rict, ze tam mame primou zavislost - hodnoty se vyskytuji podel primky. Kdezto u poctu vypujcek jsou hodnoty vice rozsete, a tak lze konstatovat, ze pocet vypujcek neni uplne zavisly na tom, jake je pocasi.

The linear regression plots below show us the dependence between the variables. In each graph, one of our variables, e.g. temperature, is marked as x and the other variable, e.g. distance, is marked as y. In our case, we can say that the distance is probably dependent on the temperature and not the other way around. Similarly, the graph concerning the duration of the loan, from which we can pretty much say that we have a prime dependence - the values occur along the prime. In the case of the number of rentals, the values are more spread out, and so we can conclude that the number of rentals is not completely dependent on the weather.

![Relationship between bikeshare and weather - part1](https://user-images.githubusercontent.com/72987557/158074811-bfbfac11-1bf0-4009-9121-e439d660ea66.png)

Jako posledni je graf, ktery znazornuje souvislost mezi vypujckami, vlhkosti vzduchu a oblacnosti. Hlavni vlivy pocasi byly zobrazeny pomoci linearni regrese v jinem grafu, pro prehlednost jsem to trochu rozdelila.

Last is a graph showing the relationship between rentals, humidity and cloud cover. The main effects of weather have been plotted using linear regression in another graph, for clarity I have split it up a bit.

![Relationship betwen bikeshare and weather - part2](https://user-images.githubusercontent.com/72987557/158074895-3ec84598-cc53-4979-b8ad-3339b8fdb227.png)

# Zaver
# Ende 
Co rict na zaver. Z pruzkumu, vypoctu a zobrazeni datasetu vyplyva, ze lide si pujcuji kola vice o vikendu a to nejvice v sobotu, zaroven se lisi doba vypujcek mezi vikendem a pracovnim dnem. Mame zjisteny stanice, ze kterych lide kola vypujcovali nejvice ale take nejmene. Pocasi urcity vliv ma, ale tento vliv neni uplne zasadni. Nektere stanice jsou vyuzivane tak malo, ze by bylo mozne je zrusit. Take vime ve kterem roce bylo provedeno nejvice vypujcek v jeden den. Vcelku jasny vystup je pro vypujcky v ruznych rocnich obdobich - celkem logicky nejvice v lete, nasledne na jare a pak podzim a zima. Stejne tak je to jasne v pripade mesicu v roce. Je zajimave ze napriklad delka trvani vypujcky je prozmenu prumerne vyssi na jare nez v lete, ale samozrejmen o vikendu jsou vypujcky delsi. Nejvice frekventovane vypujcky maji dobu trvani do 20 minut a frekvence vzdalenosti se pohybuje do 1.5 km.

What to say in conclusion. From the research, calculations and display of datasets, it is clear that people rent bikes more at the weekend and most on Saturdays, while the rental time between the weekend and the working day differs. We have found the stations from which people rented bikes the most but also the least. The weather has a certain influence, but this influence is not absolutely essential. Some stations are so little used that it would be possible to close them down. We also know in which year the most rentals were made in one day. There is a fairly clear pattern for rentals in different seasons - quite logically most in summer, followed by spring and then autumn and winter. It is equally clear for the months of the year. It is interesting that for example the length of the rental period is on average higher in spring than in summer, but of course at weekends the rentals are longer. The most frequented rentals have a duration of up to 20 minutes and the frequency of distance is up to 1.5 km.

