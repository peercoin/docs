# Peercoin official documentation repository

----
#### Directly via Github:

1. Edit any of the [docs files](https://github.com/peercoin/docs/tree/master/app/assets/docs);
2. Submit a Pull Request with your changes.

#### Developing locally:

Make sure you have Node.js installed. If you don't, [**please follow this guide**](https://gist.github.com/kazzkiq/fe702215173e795d49d0c1ffbea363b5).

1. Clone this repo: `git clone https://github.com/peercoin/docs.git`;
2. Inside the cloned folder, run: `npm i -g brunch && npm i`; (skip the first command if you already have `brunch` installed);
3. Run: `npm start`.
4. Access http://localhost:3333/ in your browser.

Any changes in the project (both on docs and/or code) will be reflect automatically in the browser once you refresh it.

#### Deploying a public test version:

1. In your local project, run: `npm run deploy`.