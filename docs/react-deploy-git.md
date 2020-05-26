# React Deploy Git


npm install gh-pages --save-dev

./package.json
- "homepage": "http://jihoonyou.github.io/______",
- "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build",
}
- 기존 프로젝트는 git에 연결되있다고 가정.

npm run deploy
