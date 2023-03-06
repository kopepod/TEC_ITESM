# TC3004B

Install PyYAML

```bash
pip install PyYAML
```

Code configuration

```bash
nano Settings.yml
```

```yaml
name : bob
lastname : cruz
phone : 443612346
```

Load from code

```bash
nano Main.py
```

```python
import yaml
import argparse

def loadSettings(File):
	class Settings: pass
	with open(File) as f:
		docs = yaml.load_all(f, Loader=yaml.FullLoader)
		for doc in docs:
			for k, v in doc.items():
				setattr(Settings, k, v)
	return Settings;


def main():
	parser = argparse.ArgumentParser('IEEE828 POC')

	parser.add_argument('--config_file', type=str, required = True, help = 'Configuration File Path');
	
	args = parser.parse_args()
	
	print(str(args))
	
	ConfigFile = args.config_file
	
	Settings = loadSettings(ConfigFile);
	
	print(Settings.name)
	print(Settings.lastname)
	print(Settings.phone)

if __name__ == '__main__':
	main()
```

```bash
python Main.py --config_file Settings.yml
```
