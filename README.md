New project template - task runner for each new project

Include "devDependencies":  :

    "autoprefixer": "^10.2.4",
    "browser-sync": "^2.26.3",
    "eslint": "^8.46.0",
    "html-validate": "^2.8.0",
    "mkdirp": "^0.5.1",
    "npm-run-all": "^4.1.5",
    "onchange": "^5.2.0",
    "postcss": "^8.2.6",
    "postcss-cli": "^8.3.1",
    "sass": "^1.44.0"

"scripts":

    "init-project": "npm install && npm-run-all init:*",
    "init:dirs": "mkdirp sass css vendor images js",
    "init:files": "touch README.md index.html sass/style.scss js/script.js",
    "init:gitignore": "curl https://raw.githubusercontent.com/github/gitignore/master/Node.gitignore -o .gitignore",
    "test": "npm run test:*",
    "test:html": "html-validate *.html",
    "test:js": "eslint js/",
    "build": "npm-run-all build:* test",
    "build:sass": "sass --style=compressed --no-source-map sass:css",
    "build:autoprefixer": "postcss css/*.css --use autoprefixer -d css",
    "build-dev": "npm-run-all build-dev:sass build:autoprefixer",
    "build-dev:sass": "sass --style=expanded --source-map sass:css",
    "watch": "npm-run-all build:* build-dev -p watch:*",
    "watch:browsersync": "browser-sync start --server --files \"css/*.css\" \"*.html\" \"js/*.js\"",
    "watch:sassprefixer": "onchange sass/*.scss -- npm run build-dev"