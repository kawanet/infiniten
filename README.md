# infiniten

A tiny manager for production process running infiniten, such like forever, nodeman or pm2

## Installation

```sh
npm install infiniten --save
```

## Usage

```sh
export PATH=$PATH:./node_modules/.bin
infiniten ./server.js --port=3000 &
```

## Infiniten does

- restart the script when crashed automatically.
- use much smaller memory footprint compared to alternatives. Just 1MB!
- need zero configuration.

## Infiniten does NOT

- restart the script when files changed.
- be written in node.js, but in bash.

## License

MIT http://rem.mit-license.org
