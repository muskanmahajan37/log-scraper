# OmniSci Log Scraper

A collection of utilities and libraries for parsing, collating and converting
OmniSciDB logs into a variety of different representations and formats.


## Install from Source

This is a two-step process of installing `cargo`, which will
install `omnisci-log-scraper` (by building from source, automatically downloaded from github).

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

cargo install --git https://github.com/omnisci/log-scraper
```

Then you can run `omnisci-log-scraper --help` to see usage.

Example output can be seen in [tests/gold/omnisci_server.INFO.csv](tests/gold/omnisci_server.INFO.csv).


## Building

To build, make sure you first [install rust](https://www.rust-lang.org/tools/install).
The rustup install can be run with `make deps`.

Then, clone the repo and run:

```
cargo build --release
```

The binary will be in `target/release`. 

Alternatively, build the Linux binary using Docker:

```
make build.docker
```

The [Makefile](Makefile) also provides targets for `test`, `run`, `install`, and `release`.


### Testing

`make test` runs rust/cargo tests and also command line tests by comparing output to "gold" files.


## Usage

```
omnisci-log-scraper 0.1.0
https://github.com/omnisci/log-scraper and https://community.omnisci.com/
Scrapes OmniSci DB logs for useful data

USAGE:
    omnisci-log-scraper [FLAGS] [OPTIONS] [INPUT]...

FLAGS:
        --createtable    Create table
        --dryrun         Do not execute anything
        --follow         Wait forever for appended data
    -h, --help           Prints help information
    -V, --version        Prints version information

OPTIONS:
        --db <DB>                OmniSci DB URL, like: omnisci://admin:HyperInteractive@localhost:6274/omnisci
    -f, --filter <FILTER>        Filter logs: all, sql, select
        --hostname <HOSTNAME>    Hostname to set for the hostname column (optional)
    -o, --output <OUTPUT>        Ouput file, or if a dir, then output files as OUTPUT/INPUT.csv
    -t, --type <TYPE>            Output format: csv, json, tsv, terminal, sql, execute, load (default: terminal)

ARGS:
    <INPUT>...    Input log files

EXAMPLES:
    omnisci-log-scraper /var/lib/omnisci/data/mapd_log/omnisci_server.INFO
    omnisci-log-scraper -t csv /var/lib/omnisci/data/mapd_log/omnisci_server.INFO.*.log > log.csv
    omnisci-log-scraper -f select -t sql /var/lib/omnisci/data/mapd_log/omnisci_server.INFO | omnisql
```
