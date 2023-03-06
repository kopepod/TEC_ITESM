# TC3004B

Code configuration

```yaml
name : bob
lastname : cruz
phone : 443612346
```

Load from code

```python
import yaml

def loadSettings(File):
	class Settings: pass
	with open(File) as f:
		docs = yaml.load_all(f, Loader=yaml.FullLoader)
		for doc in docs:
			for k, v in doc.items():
				setattr(Settings, k, v)
	return Settings;

```


