# beetools

[![Go Report Card](https://goreportcard.com/badge/github.com/Pippolo84/beetools)](https://goreportcard.com/report/github.com/Pippolo84/beetools)
[![Go Reference](https://pkg.go.dev/badge/github.com/Pippolo84/beetools.svg)](https://pkg.go.dev/github.com/Pippolo84/beetools)

<div align="center">
<img widht="640" height="320" src="assets/logo.jpg">
</div>

<br />

beetools is a CLI application to manipulate torrent file in [bencode](https://en.wikipedia.org/wiki/Bencode) format.

It currently supports three subcommands:

- `decode` to decode data in bencode format and encode them in JSON format.

```
$ beetools decode debian-10.8.0-amd64-netinst.iso.torrent | jq .
{
  "announce": "http://bttracker.debian.org:6969/announce",
  "comment": "\"Debian CD from cdimage.debian.org\"",
  "creation date": "2021-02-06T13:59:34+01:00",
  "httpseeds": [
    "https://cdimage.debian.org/cdimage/release/10.8.0//srv/cdbuilder.debian.org/dst/deb-cd/weekly-builds/amd64/iso-cd/debian-10.8.0-amd64-netinst.iso",
    "https://cdimage.debian.org/cdimage/archive/10.8.0//srv/cdbuilder.debian.org/dst/deb-cd/weekly-builds/amd64/iso-cd/debian-10.8.0-amd64-netinst.iso"
  ],
  "info": {
    "length": 352321536,
    "name": "debian-10.8.0-amd64-netinst.iso",
    "piece length": 262144,
    "pieces": "..."
  }
}
```

- `encode` to decode data in JSON format and encode them in bencode format.

```
$ beetools encode debian-10.8.0-amd64-netinst.iso.json
d8:announce41:http://bttracker.debian.org:6969/announce7:comment35:"Debian CD from cdimage.debian.org"13:creation datei1612616374e9:httpseedsl145:https://cdimage.debian.org/cdimage/release/10.8.0//srv/cdbuilder.debian.org/dst/deb-cd/weekly-builds/amd64/iso-cd/debian-10.8.0-amd64-netinst.iso145:https://cdimage.debian.org/cdimage/archive/10.8.0//srv/cdbuilder.debian.org/dst/deb-cd/weekly-builds/amd64/iso-cd/debian-10.8.0-amd64-netinst.isoe4:infod6:lengthi352321536e4:name31:debian-10.8.0-amd64-netinst.iso12:piece lengthi262144e6:pieces26880:...
```

- `show` to show information extracted from the content of a valid .torrent file (filtering "pieces" data).

```
$ beetools show debian-10.8.0-amd64-netinst.iso.torrent 
{
  "announce": "http://bttracker.debian.org:6969/announce",
  "comment": "\"Debian CD from cdimage.debian.org\"",
  "creation date": "2021-02-06T13:59:34+01:00",
  "httpseeds": [
    "https://cdimage.debian.org/cdimage/release/10.8.0//srv/cdbuilder.debian.org/dst/deb-cd/weekly-builds/amd64/iso-cd/debian-10.8.0-amd64-netinst.iso",
    "https://cdimage.debian.org/cdimage/archive/10.8.0//srv/cdbuilder.debian.org/dst/deb-cd/weekly-builds/amd64/iso-cd/debian-10.8.0-amd64-netinst.iso"
  ],
  "info": {
    "length": 352321536,
    "name": "debian-10.8.0-amd64-netinst.iso",
    "piece length": 262144,
    "pieces": ""
  }
}
```