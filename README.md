#!/bin/bash

cartelle=`ls -d */`

ciclo=0


for i in $cartelle
do
	i=${i:0:${#i}-1}
	
	primaRiga=1
	while read -r linea
	do
		if [ $primaRiga -eq 1 ]
		then
			primaRiga=0
			if [ $ciclo -eq 0 ]
			then
				
				echo "${linea};filiale" > merged.csv
			fi
		else
			
			echo "$linea;$i"  >> merged.csv 
		fi
	done < $i/export.csv
	ciclo=$((ciclo+1))
done
