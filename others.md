Dodaj skrypt do transpozycji danych w plikach .txt
```bash
#!/bin/bash
dateNow=$(date "+%Y_%b_%d")
files=$( ls *.out ) 										#tabela z nazwami plikót o rzszerzeniu .out (mozna zastapic na .txt)
counter=0
for k in $files ; do 										#start petli w ktorej iterujemy po wszystkich elementach tablicy
	  let counter=$counter+1
	  echo "File_name : ""$k"$'\n'"$(cat -- "$k")" > "$k" 	#do każdego pliku .out dodajemy w pierwszej lini napis z nazwą pliku - nazwą analizowanego przypadku
	  if [[ $counter -eq 1 ]]
		then
		awk '{print $1}' $k |								#z pierwszego pliku bierzemy nagłówki do nazw kolumn
			awk '
			BEGIN{}
			{ 
			for (i=1; i<=NF; i++)  {
						a[NR,i] = $i
						}
			}
			NF>p { p = NF }
			END {    
				for(j=1; j<=p; j++) {
					str=a[1,j]
					for(i=2; i<=NR; i++){
						str=str" "a[i,j];
					}
					print str
				}
			}
			' >> transpond_$dateNow.txt						#nazwa pliku z wynikami	
		#sed 's/[^0-9]* //' $k |						
		awk '{print " "$3}' $k |							#zamiana kolumny z danymi z pierwszego pliku
			awk '
			BEGIN{}
			{ 
			for (i=1; i<=NF; i++)  {
						a[NR,i] = $i
						}
			}
			NF>p { p = NF }
			END {    
				for(j=1; j<=p; j++) {
					str=a[1,j]
					for(i=2; i<=NR; i++){
						str=str" "a[i,j];
					}
					print str
				}
			}
			' >> transpond_$dateNow.txt						#nazwa pliku z wynikami	
	else													#transponowanie kolumn z danymi do wierszy dla pozostałych plikow
		#sed 's/[^0-9]* //' $k |
		awk '{print " "$3}' $k |
			awk '
			BEGIN{}
			{ 
			for (i=1; i<=NF; i++)  {
						a[NR,i] = $i
						}
			}
			NF>p { p = NF }
			END { FILENAME   
				for(j=1; j<=p; j++) {
					str=a[1,j]
					for(i=2; i<=NR; i++){
						str=str" "a[i,j];
					}
					print str
				}
			}
			' >> transpond_$dateNow.txt						#nazwa pliku z wynikami	

		fi
done
echo "Finished"												#powiadomienie o zakończeniu działania skryptu
```
