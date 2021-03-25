# SSH

To log in to the server we will use the secure shell network protocol and the command `ssh`. Authentication over SSH can be done using passwords but this is not safe over the internet since the password can be intercepted. Instead, we will use public-key cryptography to both authenticate and establish a secure connection to the server. For this to work the user generates a pair of keys, one *public* and one *private*. The public key can be thought of as an identity and can be shared with anyone and needs to be uploaded to the server, the private key is the secret part and should never leave the user's computer. Using the public-key anyone can encrypt a message, but only the holder of the private key can decrypt it. When we ask the server to log in, it encrypts a message using our public key which contains a login password. Using our private key we can decrypt it and get access to the server.

## Generating an ssh-keypair

Run `ssh-keygen` and follow the instructions. Leave the defaults to generate a key called `id_rsa`. It will be stored in the folder `~/.ssh`. The generator will ask you for a passphrase, you should chose a random combination of words or generate one [here](https://www.useapassphrase.com).

## Copying the key to the server

If you have access to the server over LAN or password-based ssh login you can copy over the key by running `ssh-copy-id -i ~/.ssh/id_rsa user@host` where `user` is your username on the server and `host` is the hostname or ip adress of the server.

## Logging in to the server

To log in using ssh enter `ssh -i ~/.ssh/id_rsa user@host`.

## SSH-config

By creating a file called `~/.ssh/config` we can assign default settings making ssh login a lot easier. Recommended file content:

```
Host *
    AddKeysToAgent yes
    UseKeychain yes
    IdentitiesOnly yes
    IdentityFile ~/.ssh/ida_rsa.pub

Host my-server
    HostName <server.url>
    User <user>
    ForwardAgent yes
```

Everything under `Host *` applies to all our confgurated servers. `Host my-server` on the other hand is the name we give to a specific server with the hostname (or IP-adress) `<server.url>` and username `<user>`. `ForwardAgent` is really useful but should only be used on servers that we trust since. It forwards our ssh-agent keys to the server so that we can login to another server (e.g. Github) directly from the server we are using.

With these settings in place we can just write `ssh my-server` to log in.

## SSH security

Ask your server admin to keep the following settings in the file `/etc/ssh/sshd_config`.

```
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
PermitRootLogin no
PermitRootLogin prohibit-password
```

## Adding the ssh-key to the agent

To avoid having to enter your passphrase every time, ssh-agent can keep track of it. On Mac the ssh-agent is most likely already running. If you run `ssh-add -l` you should see your key listed. If not, first start the ssh-agent by running `` eval `ssh-agent` ``.

## Using a proxy server

Logging in to the Stockholm University computing server from outside will require you to use a proxy server that forwards the request to the compute server. The following settings in `~/.ssh/config` should do the trick.

```
Host broker
    Hostname <broker-server.url>
    User <broker-user>

Host my-server_external
    HostName <server.url>
    ProxyCommand ssh broker nc %h %p
    User <server-user>
    ForwardAgent yes
```
