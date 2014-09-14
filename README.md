Flora Pac for NodeJS [![NPM version](https://badge.fury.io/js/flora-pac.png)](http://badge.fury.io/js/flora-pac)
====================

A NodeJS port of [Flora PAC] generator.
 

## Installation / Usage

1. Install from npm
    ````bash
    $ sudo npm install -g flora-pac
    ```` 

2. Create your own `pac-config.json` first (see next chapter)

3. Run (the default output file is `flora.pac`)
    ````bash
    $ flora-pac
    ```` 

    or to get some command-line help
    ````bash
    $ flora-pac -h
    ````


## Configurations

make a config file `pac-config.json` like this

```json
{
    "proxy"         : "SOCKS5 127.0.0.1:7070; SOCKS 127.0.0.1:7070",
    "normalDomains" : [
        "baidu.com", "v2ex.com"
    ],
    "walledDomains" : [
        "google.com", "youtube.com", 
        "twitter.com", "facebook.com"
    ],
    "fakeIps" : [
        "211.98.70.194", "211.98.70.195"
    ]
}
```

check [src/pac-config.js](src/pac-config.js) for more config options available.

INI format is also supported, check [this sample](pac-config.ini) for more details


All things done with only one command
```bash
$ node <path_to_this_project_root>
```

## Tests

You could run a simple test (assume that `flora.pac` is already generated)
```bash
$ npm install
$ ./pacTest flora.pac twitter.com
$ node test/pacTest flora.pac twitter.com
```

Or run batch tests
```bash
$ npm install
$ node test/test
```


## Speed up the generation time

The CHN IP is requested from apnic

There is approximate 1.6 MB data to download.

You can do it yourself using this command

```bash
$ curl http://ftp.apnic.net/apnic/stats/apnic/delegated-apnic-latest -O
```

If you need to generate multiple files, this will help generating speed up much faster.


## Performance

The Performance test code is just copied from [clowwindy's gfwlist2pac][gfwlist2pac]

An example of generated PAC file is [here](test/flora.pac)

Flora Pac uses `dnsResolve` which makes the execution time very unpredictable.

The test code is modified that **return a random IP every time while lookup any host**.

Here is the test result:

```
Testing pac generated by FloraPacNJS
   size: 49324 bytes
  total: 105.797055 ms
average: 1.528859176300578 ns

Testing pac generated by gfwlist2pac
   size: 54800 bytes
  total: 27.962916 ms
average: 0.40408838150289017 ns

Testing pac generated by switchysharp
   size: 506472 bytes
  total: 41940.2284 ms
average: 606.0726647398843 ns
```


## TODO:
- [X] Add tests
- [X] Add command-line: `--help / --proxy / --internal-proxy / --file / ...`
- ~~Generate minimal pac file, etc: `flora.min.pac` (meaningless, cancelled)~~
- [X] Add supports for INI config file rather than general json
- [ ] Add supports for import domains from [GFW whitelist]: `whitelist.pac` (smaller)
- [ ] Add supports for import domains from [fqdns]: `china_domains.txt` (much bigger)
- [ ] Add supports for import domains from [gfwlist.txt] (blacklist, much bigger)


## See also
* [Python original Flora Pac][Flora Pac]
* [Python fork by usufu](https://github.com/usufu/Flora_Pac)
* [clowwindy's gfwlist2pac][gfwlist2pac]
* [GFW whitelist]
* [fqrouter/fqdns][fqdns]

[Flora Pac]:     https://github.com/Leask/Flora_Pac
[gfwlist2pac]:   https://github.com/clowwindy/gfwlist2pac
[gfwlist.txt]:   https://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt
[GFW whitelist]: https://github.com/n0wa11/gfw_whitelist
[fqdns]:         https://github.com/fqrouter/fqdns

