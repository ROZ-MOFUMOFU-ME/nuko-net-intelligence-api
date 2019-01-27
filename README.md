Nekonium Network Intelligence API
============
[![Build Status][travis-image]][travis-url] [![dependency status][dep-image]][dep-url]

This is the backend service which runs along with nekonium and tracks the network status, fetches information through JSON-RPC and connects through WebSockets to [nuko-netstats](https://github.com/ROZ-MOFUMOFU-ME/nuko-netstats) to feed information. For full install instructions please read the [wiki](https://github.com/ethereum/wiki/wiki/Network-Status).


## Prerequisite
* gnekonium or parity-nekonium
* node
* npm

## Installation as docker container (optional)

There is a `Dockerfile` in the root directory of the repository. Please read through the header of said file for
instructions on how to build/run/setup. Configuration instructions below still apply.

## Configuration

Configure the app modifying [processes.json](/eth-net-intelligence-api/blob/master/processes.json). Note that you have to modify the backup processes.json file located in `./bin/processes.json` (to allow you to set your env vars without being rewritten when updating).

```json
"env":
	{
		"NODE_ENV"        : "production", // tell the client we're in production environment
		"RPC_HOST"        : "localhost", // eth JSON-RPC host
		"RPC_PORT"        : "8293", // nuko JSON-RPC port
		"LISTENING_PORT"  : "", // nuko listening port (only used for display)
		"INSTANCE_NAME"   : "", // whatever you wish to name your node
		"CONTACT_DETAILS" : "", // add your contact details here if you wish (email/skype)
		"WS_SERVER"       : "wss://stats.mofumofu.me", // path to nuko-netstats WebSockets api server
		"WS_SECRET"       : "join Nekonium Discord and ask ROZ WS_SECRET", // WebSockets api server secret used for login
		"VERBOSITY"       : 2 // Set the verbosity (0 = silent, 1 = error, warn, 2 = error, warn, info, success, 3 = all logs)
	}
```

## Run

Run it using pm2:

```bash
cd ~/bin
pm2 start processes.json
```

## Updating

To update the API client use the following command:

```bash
~/bin/www/bin/update.sh
```

It will stop the current netstats client processes, automatically detect your ethereum implementation and version, update it to the latest develop build, update netstats client and reload the processes.

[travis-image]: https://travis-ci.org/ROZ-MOFUMOFU-ME/nuko-net-intelligence-api.svg
[travis-url]: https://travis-ci.org/ROZ-MOFUMOFU-ME/nuko-net-intelligence-api
[dep-image]: https://david-dm.org/ROZ-MOFUMOFU-ME/nuko-net-intelligence-api.svg
[dep-url]: https://david-dm.org/ROZ-MOFUMOFU-ME/nuko-net-intelligence-api
