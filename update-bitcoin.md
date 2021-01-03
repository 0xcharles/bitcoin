# Updating Bitcoin Core on a Debian Linux server

These instructions explain how to update to the latest version of Bitcoin Core. As of writing that is Bitcoin Core 0.20.1. You may want to replace this with the actual latest version if you're reading this after the release of an even newer version and this guide hasn't been updated to account for the newest version yet.

## Download update file

`cd Downloads`

`wget https://bitcoincore.org/bin/bitcoin-core-0.20.1/bitcoin-0.20.1-x86_64-linux-gnu.tar.gz`

## Verify download

`wget https://bitcoincore.org/bin/bitcoin-core-0.20.1/SHA256SUMS.asc`

`sha256sum --ignore-missing --check SHA256SUMS.asc`

You should see a message that says:

`bitcoin-0.20.1-x86_64-linux-gnu.tar.gz: OK`

If you do then proceed. If not, then you downloaded the wrong file and need to start over and double-check your work.

`gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 01EA5486DE18A882D4C2684590C8019E36C2E964`

`gpg --verify SHA256SUMS.asc`

You should see a message that says `gpg: Good signature` and `Primary key fingerprint: 01EA 5486 DE18 A882 D4C2  6845 90C8 019E 36C2 E964`.

If you do then proceed. If not, then something went wrong. Either the file is corrupt or the signature came from the wrong person. You'll need to investigate online to find out what's going on.

## Unpack the update file

`tar xzf bitcoin-0.20.1-x86_64-linux-gnu.tar.gz`

## Enter Bitcoin Core directory

`cd bitcoin-0.20.1`

`cd bin`

## Install bitcoin  

`sudo install -m 0755 -o root -g root -t /usr/local/bin *`

## Start bitcoin

`bitcoind --daemon`

## Stop bitcoin  

`bitcoin-cli stop`

## Create a cron job to keep bitcoin running

`crontab -e`

Scroll to the bottom of the file and type:

`@reboot bitcoind -daemon`

Then save and exit the file. This will ensure bitcoin restarts when you shut down and restart your node.

Repeat the above, up to the part where you create the cron job, each time you udate your Bitcoin Core version.
