# Telegram MTProto Proxy (Alpine 3.7)

The Telegram Messenger MTProto proxy is a zero-configuration container that automatically sets up a proxy server that speaks Telegram's native MTProto.

## Quick reference
To start the proxy all you need to do is
`docker run -d -p8843:8843 --name=mtproxy --restart=always -v proxy-config:/data masterx46/mtproxy_l:latest`

The container's log output (`docker logs mtproxy`) will contain the links to paste into the Telegram app:

```
[+] Using the detected external IP: 1.2.3.4.
[+] Using the detected internal IP: 122.0.0.4.
[*] Final configuration:
[*]   Secret 1: super_secret
[*]   tg:// link for secret 1 auto configuration: tg://proxy?server=1.2.3.4&port=443&secret=super_secret
[*]   t.me link for secret 1: https://t.me/proxy?server=1.2.3.4&port=443&secret=super_secret
[*]   Tag: my_tag
[*]   External IP: 1.2.3.4
[*]   Make sure to fix the links in case you run the proxy on a different port.
```
The secret will persist across container upgrades in a volume. It is a mandatory configuration parameter: if not provided, it will be generated automatically at container start. You may forward any other port to the container's 8843: be sure to fix the automatic configuration links if you do so.

Please note that the proxy gets the Telegram core IP addresses at the start of the container. We try to keep the changes to a minimum, but you should restart the container about once a day, just in case.

## Registering your proxy
Once your MTProxy server is up and running go to [@MTProxybot](https://t.me/mtproxybot) and register your proxy with Telegram to gain access to usage statistics and monetization.

## Custom secret and how to set TAG from bot

Custom secret key can be set as you can see below:
`docker run -d -p8843:8843 -v proxy-config:/data -e SECRET=super_secret_key masterx46/mtproxy_l:latest`.

A custom advertisement tag may be provided using the TAG environment variable:
`docker run -d -p8843:8843 -v proxy-config:/data -e TAG=Your_TAG_Here masterx46/mtproxy_l:latest`.

Please note that the tag is not persistent: you'll have to provide it as an environment variable every time you run an MTProto proxy container (except when --restart=always option is used).

## Info and Authors
This image/repo is forked from @alexdoesh and then updated, Telegram MTProto Proxy repo [MTProxy](https://github.com/TelegramMessenger/MTProxy)
