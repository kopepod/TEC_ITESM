# Vite React Launch Page Tutorial

1. Install npm

https://nodejs.org/en/download/

verify installation

```bash
node -v
```

2. create Vite React APP

```bash
npm create vite@latest
```

3. Run server launch page

```bash
cd <project_name>
npm install
npm run dev
```
4. Open localhost browser, e.g.:

```bash
firefox http://localhost:5173/
```

5. Edit jsx file

```bash
nano src/App.jsx
```
```javascript
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import './App.css'


function App() {

	const [units, setUnits] = useState(0)

	const readTxtBox = () => {
		if (isNaN(Number(units))){
			alert(`Only numbers`);
			setUnits(0)
		}
		else{
			var celsius = units;
			var farenheit = units * 9/5 + 32;
			var mssg = `${celsius} [°C] = ${farenheit} [°F]`;
			alert(mssg)
		}
	}

  const handleChange = event => {
    setUnits(event.target.value);
    console.log('value is:', event.target.value);
  };

  return (
    <div className="App">
      <div>
        <a href="https://vitejs.dev" target="_blank">
          <img src="/vite.svg" className="logo" alt="Vite logo" />
        </a>
        <a href="https://reactjs.org" target="_blank">
          <img src={reactLogo} className="logo react" alt="React logo" />
        </a>
      </div>
      <h1> Convert Celsius to Farenheit </h1>

	<div className="card">      
		<input 
			type="number" 
			id="units"
			name="units"
			onChange={handleChange}
			value={units}>
			</input> [°C]
	</div>

	<div className="card">
		<button onClick={() => { readTxtBox() }} > Convert </button>
	</div>
    
</div>
    
  )
}

export default App
```
