# GEO

An easy way to manage all your Geo resources.

Support GeoIP/GeoSite code lookup and converting among all popular GeoIP/GeoSite databases.

## Install

Requirements:

- [Go](https://go.dev) 1.20+

```shell
go install -v github.com/devsolux/maxmind-geo/cmd/geo@master
```

## Usage

Type `geo help` for more details.

### Look up codes from existing Geo databases

The default directory to find Geo databases is
`~/.geo`. You can specify it through `-D` argument.

#### IP

```shell
geo look 223.5.5.5
```

```shell
geo look 2001:250::
```

#### Site

```shell
geo look example.com
```

```shell
geo look --no-resolve example.com
```

Supported databases for `look` command:

- MaxMind MMDB
- V2Ray dat GeoIP/GeoSite
- sing-geosite
- sing-geoip MMDB
- Meta-geoip MMDB

### Convert

#### IP

```shell
geo convert ip -i <input_type> -o <output_type> -f [output_filename] input_filename
```

```shell
geo convert ip -i v2ray -o meta ./geoip.dat
```

Available types:

- [MaxMind](https://github.com/Dreamacro/maxmind-geoip) (MMDB)
- [V2Ray-geoip](https://github.com/v2fly/geoip) (dat)
- [sing-geoip](https://github.com/SagerNet/sing-geoip) (MMDB)
- [Meta-geoip](https://github.com/MetaCubeX/meta-rules-dat) (MMDB)

Supported conversion pairs: (Column=From, Row=To)

|            | MaxMind | V2Ray-geoip | sing-geoip | Meta-geoip |
|------------|:-------:|:-----------:|:----------:|:----------:|
| MaxMind    |    -    |             |            |            |
| V2Ray      |         |      -      |            |            |
| sing-geoip |    ✅    |      ✅      |     -      |     ✅      |
| Meta-geoip |         |      ✅      |            |     -      |

Conversion to MaxMind is not available for legal reasons.  
Conversion to V2Ray is on the TODO list.

#### Site

```shell
geo convert site -i <input_type> -o <output_type> -f [output_filename] -c [country code] input_filename
```

```shell
geo convert site -i v2ray -o sing ./geosite.dat
```
