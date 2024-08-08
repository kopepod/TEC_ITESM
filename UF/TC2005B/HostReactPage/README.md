# Deploy a React page on gitpages


Create the React APP

```bash
npx create-react-app testpage
```

Move into directory and edit _package.json_
```bash
cd testpage
nano package.json
```

Add this line
```bash
"homepage": "https://<github-username>.github.io/<repo-name>/"
```
and these to scripts:
```bash
"scripts": {
   "predeploy": "npm run build",
   "deploy": "gh-pages -d build"
}
```

Run

```bash
npm test
npm run build
git init
git remote add origin https://github.com/<github-username>/<repo-name>.git
```

Enable a token to create site:

Click your Avatar (top right) → Settings → Developer settings → Personal access tokens → Tokens (classic). -> Only repo should be fine

```bash
git remote set-url origin https://<token>@github.com/<username>/<repo>
```



Deploy via

```bash
npm install --save-dev gh-pages
git add .
git commit -m "comments ..."
git push origin master
npm run deploy
```

Your site should be at 

```bash
firefox https://<github-username>.github.io/<repo-name>/
```

