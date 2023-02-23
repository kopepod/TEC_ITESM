# Reading From Parser


```python
#Main.py

import argparse
import itertools
import numpy
import pandas

class Operation:
	CurrentState = "Cerrado"
	Temperature = 0
	Humidity = 0
	Hour = 0
	

def GenerateTable():
	#
	T = [] # Temperature
	H = [] # Humidity
	D = [] # Date (Hour)
	#
	Values = numpy.arange(0,98,2);
	for x in itertools.permutations(Values,3):
		if x[1] > 50 or x[2] > 24:
			continue
		T.append(x[1])
		H.append(x[0])
		D.append(x[2])
	DF = pandas.DataFrame()
	DF = DF.assign(Temperature = T)	
	DF = DF.assign(Humidity = H)	
	DF = DF.assign(Hour = D)	
	return DF

def Control(Irrigacion, DF, Inputs):
	for _, row in DF.iterrows():
		H = row["Humidity"]
		T = row["Temperature"]
		D = row["Hour"]
		
		S = [];
		
		if T > Inputs.TemperatureLow and D > Inputs.DateStart and D < Inputs.DateEnd and H > Inputs.HumidityHigh and Irrigacion.CurrentState == "Cerrado":
			S.append("Abrir");
			
			
	print(S)	
		
	

def main():
	parser = argparse.ArgumentParser(prog = 'Valvles control',
                    description = 'It controls the valvles operation')
	parser.add_argument('--TemperatureHigh', required = True, type = int, help = "Temperature High")
	parser.add_argument('--TemperatureLow', required = True, type = int, help = "Temperature Low") 
	parser.add_argument('--HumidityHigh', required = True, type = int, help = "Humidity High")
	parser.add_argument('--HumidityLow', required = True, type = int, help = "Humidity Low") 	
	parser.add_argument('--DateStart', required = True, type = int, help = "Start Hour")
	parser.add_argument('--DateEnd', required = True, type = int, help = "End hour") 	
	parser.add_argument('--Crop', required = True, type = str, help = "Crop sort") 		
		
	Inputs = parser.parse_args()

	Irrigacion = Operation() # Finite State Machine

	DF = GenerateTable()

	Control(Irrigacion, DF, Inputs);

if __name__ == "__main__":
	main();


```
