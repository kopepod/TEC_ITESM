# Reading From Parser


```python
import argparse


def main():
	parser = argparse.ArgumentParser('Reading arguments from parser')

	parser.add_argument('--Path', type=str, default='./DATA', required = True, help = 'Path to Files');
	
	args = parser.parse_args()
	
	Path = args.Path

	print(Path)


if __name__ == '__main__':
	main()

```
