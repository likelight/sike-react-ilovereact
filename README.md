Sike.io Full-stack React Bootcamp 
=========================

# Create A New Project

## Use NPM to create a new project

- Upgrade node

```bash
$ npm install -g n
$ n stable
$ node -v
$ v4.0.0
```

- Use npm init to create the project

```bash
$ mkdir ilovereact
$ cd ilovereact
$ npm init # to create package.json
```

- Initialize Git repo and add the NodeJS specific .gitignore file

```bash
$ curl https://raw.githubusercontent.com/github/gitignore/master/Node.gitignore > .gitignore
```

- Create index.html from the [HTML5 boilerplate](https://github.com/h5bp/html5-boilerplate/blob/master/src/index.html)

## Live edit with BrowserSync

- Install [BrowserSync](http://www.browsersync.io/)

```bash
$ npm install browser-sync@2.9.3 --save -d # --save adds browser-sync to package.json
$ export PATH=$PATH:./node_modules/.bin # add that directory to the PATH variable
# to add it to ~/.bash_profile to make it stick
export PATH=$PATH:./node_modules/.bin
$ browser-sync --version
$ browser-sync start --server --files=index.html

# refer to [stackoverflow](http://stackoverflow.com/questions/17980759/xcode-select-active-developer-directory-error-on-osx-mavericks) for npm package build failure: xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance
```

- Create Makefile for tasks automation, for [more information](http://www.sitepoint.com/using-gnu-make-front-end-development-build-tool/)

```
# Makefile
.PHONY: server
server:
#   # WARNING: The indentation MUST be a tab. Spaces won't work.
	browser-sync start --server --files='index.html,bundle/app.css'
```

```bash
$ make server
```

## Create base CSS for the project with modern css build tools

- Install the [PostCSS](https://github.com/postcss/postcss) parser

```bash
$ npm install postcss-cli@2.1.0 --save-dev
```

- Install [autoprefixer](https://github.com/postcss/autoprefixer)

```bash
$ npm install autoprefixer@6.0.2 --save-dev
```

- Add [ReactNative flexbox settings](https://github.com/facebook/css-layout#default-values) to the css/app.css file

- Use PostCSS to transform (add prefixeres) the original css file

```bash
$ mkdir -p bundle
$ postcss --use autoprefixer css/app.css --output bundle/app.css
```

- Link to bundle/app.css in the head element

- Install [normalize.css](http://necolas.github.io/normalize.css)

```bash
$ npm install --save normalize.css@3.0.3
```

- Install [postcss-import](https://github.com/postcss/postcss-import) plugin to import normalize.css

```bash
$ npm install --save-dev postcss-import@7.0.0
$ postcss --use autoprefixer --use postcss-import css/app.css --output bundle/app.css
```

- Update the [Makefile](https://github.com/j1wu/sikeio-ilovereact/blob/bf98375b6d30878b9cb4cfd67e205fd98da1e7b0/Makefile)
	- Added `--watch` option to postcss, so it rebuilds css/app.css whenver you make changes
	- Added bundle/app.css to `--files`, so BrowserSync reloads whenever we rebuild