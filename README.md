# bash

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
