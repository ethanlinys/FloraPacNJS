Flora Pac for NodeJS
====================

A NodeJS port of [Flora PAC] generator.
 

## Requirement / Installation

* NodeJS of course

No any further installation is required

## Configuration / Usage

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


All things done with only one command
```bash
$ node .
```

the default output file is `flora.pac`

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


## To speed up the generation time

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
   size: 82658 bytes
  total: 106.53362299999999 ms
average: 1.5395032225433525 ns

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
- [X] Support tests
- [ ] Support `--proxy / --internal-proxy / --file` command-line arguments
- [ ] Command-line help
- ~~Generate minimal pac file liked `flora.min.pac`~~
- [ ] Support user rule text config file format (will import to `walledDomains / normalDomains`)
- [ ] Support gfw list file (pac will be much bigger)
- [ ] Sync China Domains (that is, `normalDomains`) from other where


## See also
* [Python original Flora Pac][Flora Pac]
* [Python fork by usufu](https://github.com/usufu/Flora_Pac)
* [clowwindy's gfwlist2pac][gfwlist2pac]


[Flora Pac]:   https://github.com/Leask/Flora_Pac
[gfwlist2pac]: https://github.com/clowwindy/gfwlist2pac
