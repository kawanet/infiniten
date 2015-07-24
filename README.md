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

## Initscripten

Infiniten works great with initscripten which is a support tool
to create SysV Init script with standalone program running inifiniten.

```sh
#!/usr/bin/env bash
# chkconfig: 35 85 15

USR="username"
CMD="path/to/command"

# re-launch itself with full path
[ "${0:0:1}" = "/" ] || exec -- "$0" "$@"

# re-launch itself with the user
[ "$UID" -eq "0" ] && exec -- su - "$USR" -c "nohup $0 $*"

# project home absolute path
PRJ=$(dirname $(readlink -f $0 2> /dev/null || echo $0))
PRJ=$(dirname $PRJ) # ..
PRJ=$(dirname $PRJ) # ..

# add local node_modules path
export PATH=$PATH:$PRJ/node_modules/.bin

# run this as a SysV Init script
. initscripten "$@"
shift
[ "$1" = "" ] && shift

# move to project home
cd $PRJ

# prepare node.js environment
[ -x ~/.nvm/nvm.sh ] && . ~/.nvm/nvm.sh

# launch standalone daemon
exec infiniten "$CMD" "$@"
```

Install the script above at `/etc/init.d/scriptname`.
It accepts `start`, `stop` and `restart` argument.

```sh
service scriptname start
service scriptname stop
service scriptname restart
```

## License

MIT http://rem.mit-license.org
