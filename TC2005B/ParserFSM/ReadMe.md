# Reading From Parser and Finite State Machine

Code:

```python
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
	S = [];
	for _, row in DF.iterrows():
		H = row["Humidity"]
		T = row["Temperature"]
		D = row["Hour"]

		if Irrigacion.CurrentState == "Cerrado":
			if T < Inputs.TemperatureLow and D not in range(Inputs.DateStart,Inputs.DateEnd) and H < Inputs.HumidityLow:
				Irrigacion.CurrentState = "Abierto";
				S.append("Abierto");
				continue
			else:
				S.append("Cerrado");
		if Irrigacion.CurrentState == "Abierto":
			if T > Inputs.TemperatureHigh or D in range(Inputs.DateStart,Inputs.DateEnd) or H > Inputs.HumidityHigh:
				Irrigacion.CurrentState = "Cerrado";
				S.append("Cerrado");
				continue
			else:
				S.append("Abierto");			
			

	DF = DF.assign(Salida = S)
	DF.to_csv("FSM.csv", index = False)
	
	

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

Run as:

```bash
python StateDiagramExample.py --TemperatureHigh 35 --TemperatureLow 25 --HumidityHigh 50 --HumidityLow 10 --DateStart 6 --DateEnd 19 --Crop Beans
```
