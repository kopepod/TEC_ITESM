# Reading From Parser


```python
import argparse
import itertools
import numpy

def GenerateTable():
	Values = numpy.arange(0,98,2);
	for x in itertools.permutations(Values,3):
		if x[1] > 50 or x[2] > 24:
			continue

def main():
	parser = argparse.ArgumentParser('Reading arguments from parser')
	parser.add_argument('--Path', type=str, default='./DATA', required = True, help = 'Path to Files');
	args = parser.parse_args()
	Path = args.Path
	print(Path)


if __name__ == '__main__':
	main()

```
