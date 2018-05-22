## Pierwsza część
Plik oceny.txt:
```
imie i nazwisko Oceny
Anna Nowak 4,5,4,3.5,2,5,4,5
Jaroslaw Zimek 3,4,3,2,5,4.3,3,4
Maria Modrzejewska 2,3,4,3
```
#### Zadanie 01
W pliku oceny.txt znajduja sie oceny studentow w formacie Imie i Nazwisko a nastepnie podane sa oceny oddzielone przecinkami, nalezy wyswietlic plik zawartosc pliku z ocenami tak aby najpierw być nazwisko a dopiero pozniej imie i to w kolejnosci alfabetycznej najpierw wzgledem nazwiska, a nastepnie wzgledem imienia, oraz aby nie pojawila sie wyswietlana linia naglowka.

```
cat oceny.txt | awk '{print $2" "$1" "$3}' | sort
```

#### Zadanie 02
Wpisujac oceny mozna czasem poeplnic blad wpisujac niepoprawna wartosc, to tez ma miejsce w przypadku danych z zadania 001. Jenda z ocen jest niepoprawna. Jak za pomoca komend wydanych w jednej linii odnalezc wpis w ktorym  jest niepoprawna ocena.
```
 cat oceny.txt | egrep -v '(2,|3,|3\.5|4,|4\.5|5,)(2|3|3\.5|4|4\.5|5)$' | awk '{print $2" "$1" "$3}'
```

#### Zadanie 03
Lista ocen to bardzo wa¿na rzecz wiec warto zrobic jej kopie bezpieczenstwa. Proszê o napisanie komendy która z pliku oceny.txt stworzy plik oceny.{aktualna data}.txt
```
cp oceny.txt oceny_$(date +"%Y_%m_%d").txt
```

#### Zadanie 04
Rozszerzenie pliku txt, ktore otrzymalismy w ostatnim zadaniu nie jest najlepsze, gdyz nie sugeruje, ze utworzony plik jest kopia (z reguly takie kopie maja rozszerzenie bak). Prosze zatem zmienic rozszerzenie utowrzonego pliku na bak, jednak aby nie wpisywac za duzo polecen, to nalezy wykorzystac mechanizmy historii.
```
!!.bak
```

#### Zadanie 05
Umieść plik oceny.txt z ocenami w katalogu wyniki. A następnie udostępnij zawartość tego pliku wszytkim zainteresowanym osobom, w taki sposób aby nie mogły przeglądać zawartości katalogu wyniki, a jedynie  zawartość tego pliku.
```
mkdir -m 711 oceny
mv oceny.txt oceny
chmod 644 oceny.txt
```

#### Zadanie 06
Utworz grupe student oraz grupe nauczyciel (obcięty do 8 znaków) do grupy studentow nalezy dodac 2 osoby Anne Nowak, Jaroslawa Zimka, Marie Modrzejewska. Jako login nalezy podac 8 pierwszych liter nazwiska. Podobnie do grupy nauczyciel dodaj osoby Stefan Kaczka, Leszek Jastrzab.

#### Zadanie 07
Studenci nie powinni miec zbyt wielkich mozliwosci operowania na koncie. Zrób tak aby przy logowaniu studenta, uruchamiał się jedynie edytor vi.

#### Zadanie 08
Oczywistym jest, ze w dobie informatyzacji, wszytkie prace studentow trzyma sie na dyskach twardych, najlepiej w oddzielnych katalogach i podkatalogach np. wyniki dla poszczegolnych studentow:
```
wyniki
-->Anna Nowak 
-->-->zad.001
-->-->zad.002
-->Jaroslaw Zimek 
-->-->zad.001
-->-->Zad.002
-->Maria Modrzejewska
-->-->Zad.001
-->-->Zad.002
```
chcialoby sie miec jednak rowniez mozliwosc zgrupowania wynikow studentow rowniez po zadaniach, czyli 
```
wyniki
-->zad.001
-->-->Anna Nowak 
-->-->Jaroslaw Zimek 
-->-->Maria Modrzejewska
-->zad.002
-->-->Anna Nowak 
-->-->Jaroslaw Zimek 
-->-->Maria Modrzejewska
```
oczywiście bezsensem jest powielanie całej zawartości katalogów, zatem dobrze by było aby kartoteki zgrupowane po zadaniach byly jedynie podlinkowane do kartotek zgrupowanych po studentach.

#### Zadanie 09
Niektorzy studenci to leserzy, napisz komende, która spowoduje wyswietlenie osob, ktore jeszcze sie nie logowaly do systemu. Umiesc ta komende w pliku .bashrc tak aby była uruchamina przy kazdym logowaniu root'a.

#### Zadanie 10
Przy jednych z nastêpnych zadañ przyda siê nam oprogramowanie do tworzenia tzw. analizatorów leksykalnych flex. Proszê zatem o zainstalowanie takiego oprogramowania.

## Druga część
Plik Zadania.005.txt:
```
awk0
# Kto by chcial ogladac puste linie, aby AWK takich lini nie przepuscil
# to program ma tylko 4 (slownie 4 znaczki )

awk1
# Kto by chcial ogladac puste linie, aby AWK takich lini nie przepuscil
# to program ma tylko 4 (slownie 4 znaczki )

awk2 
# Poprzednio wykasowalismy wszystkie puste linie, jednak czasem linie puste
# moga sie przydac aby oddzielic jeden blok od drugiego, jednak zwykle do tego
# celu wystarcza jedna linia separujaca. Ponizszy przykladowy programik 
# pozostawia tylko po jednej pustej lini pomiedzy blokami

awk3
# Jesli chcemy policzyc ilosc lini danego pliku, to w AWK'u jest to
# tylko jedna linijka, gdy sie skorzysta z wbudowanych zmiennych, lub
# dwie gdy sie pisze wszystko samemu

awk4
# Czesto w zyciu codzeinnym wystepuje potrzeba zliczenia ilosci obiektow
# AWK nadaje sie jak nie mozna lepiej do zliczania ilosci wystapien slow 
# w podanym pliku

awk5
# Podczas startu systemu sa uruchamiane pewne programy w zaleznosci
# od poziomu startu. Zadanie polega na stwierdzeniu na jakim poziomie 
# startuje system i ile uruchamia programow

awk6
# AWK moze sie przydac nie tylko do przetwarzania tekstu, umie on rowniez
# dosc dobrze liczyc. Jest w stanie np. stwierdzic czy podany rok jest 
# przechodni czy nie
```

#### AWK0 & AWK1
Kto by chcial ogladac puste linie, aby AWK takich lini nie przepuscil to program ma tylko 4 (slownie 4 znaczki).
```bash
dos2unix na pliku Zadania.005.txt
awk 'NF>0 {print}' Zadania.005.txt
```
#### AWK2
Poprzednio wykasowalismy wszystkie puste linie, jednak czasem linie puste moga sie przydac aby oddzielic jeden blok od drugiego, jednak zwykle do tego celu wystarcza jedna linia separujaca. Ponizszy przykladowy programik pozostawia tylko po jednej pustej lini pomiedzy blokami.
```bash
awk '{if (/^a/ && NR>1) printf "\n" ; print}' Zadania.005a.txt
```

#### AWK3
Jesli chcemy policzyc ilosc lini danego pliku, to w AWK'u jest to tylko jedna linijka, gdy sie skorzysta z wbudowanych zmiennych, lub
dwie gdy sie pisze wszystko samemu.
```bash
wc -l Zadania.005.txt
awk 'END {print NR}' Zadania.005.txt
```
#### AWK4
Czesto w zyciu codzeinnym wystepuje potrzeba zliczenia ilosci obiektow AWK nadaje sie jak nie mozna lepiej do zliczania ilosci wystapien slow w podanym pliku.
```bash
grep -n "awk " Zadania.005.txt
awk 'END{print NR-1}' RS="awk " Zadania.005.txt 
#spacja po solowie gwarantuje znalezienie samego slowa zamiast fragmentu
```
#### AWK5
Podczas startu systemu sa uruchamiane pewne programy w zaleznosci od poziomu startu. Zadanie polega na stwierdzeniu na jakim poziomie startuje system i ile uruchamia programow
```bash
runlevel | awk '{print | "ls -1 /etc/rc" $2 ".d"}' | awk 'END {print "Ilosc uruchominych uslug: "NR-2}'
```
#### AWK6
AWK moze sie przydac nie tylko do przetwarzania tekstu, umie on rowniez dosc dobrze liczyc. Jest w stanie np. stwierdzic czy podany rok jest przechodni czy nie.
```bash
awk '{if( ($1%4==0 && $1%100!=0) || $1%400==0) print "przechodni"; else print "nieprzechodni"}' putYear 
#w pliku putYear jest tylko jeden rok
awk 'BEGIN {RS=" "} {if( ($1%4==0 && $1%100!=0) || $1%400==0) print $1 " - przechodni"; 
else print $1 " - nieprzechodni"}' putYear
```
Dla pliku w formacie: 2008 2009 2010 2011 2012;
```
Result:
2008 - przechodni
2009 - nieprzechodni
2010 - nieprzechodni
2011 - nieprzechodni
2012 - przechodni
```
