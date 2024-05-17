# De-Optimizer
<div align="center">
  <img src=".github/img/banner.png">
  <br>
  <br>


  [![GitHub All Releases][release-img]][release]
  [![Build][workflow-img]][workflow]
  [![Issues][issues-img]][issues]
  [![Crates][crates-img]][crates]
  ![Docker Pulls][docker-pulls]
  [![License: MIT][license-img]][license]
</div>

[crates]: https://crates.io/crates/deoptimizer
[crates-img]: https://img.shields.io/crates/v/deoptimizer
[release]: https://github.com/EgeBalci/deoptimizer/releases
[release-img]: https://img.shields.io/github/v/release/EgeBalci/deoptimizer
[downloads]: https://github.com/EgeBalci/deoptimizer/releases
[downloads-img]: https://img.shields.io/github/downloads/EgeBalci/deoptimizer/total?logo=github
[issues]: https://github.com/EgeBalci/deoptimizer/issues
[issues-img]: https://img.shields.io/github/issues/EgeBalci/deoptimizer?color=red
[docker-pulls]: https://img.shields.io/docker/pulls/EgeBalci/EgeBalci?logo=docker&label=docker%20pulls
[license]: https://raw.githubusercontent.com/EgeBalci/deoptimizer/master/LICENSE
[license-img]: https://img.shields.io/github/license/EgeBalci/deoptimizer.svg
[google-cloud-shell]: https://console.cloud.google.com/cloudshell/open?git_repo=https://github.com/EgeBalci/deoptimizer&tutorial=README.md
[workflow-img]: https://github.com/EgeBalci/deoptimizer/actions/workflows/main.yml/badge.svg
[workflow]: https://github.com/EgeBalci/deoptimizer/actions/workflows/main.yml
[moneta-ref]: https://github.com/forrest-orr/moneta
[pe-sieve-ref]: https://github.com/hasherezade/pe-sieve
[insomnihack]: https://www.youtube.com/watch?v=Issvbst_89I


This tool is a machine code de-optimizer. By transforming/mutating the machine code instructions to their functional equivalents it makes possible to bypass pattern-based detection mechanisms used by security products.

## Why?
Bypassing security products is a very important part of many offensive security engagements. The majority of the current AV evasion techniques used in various different evasion tools, such as packers, shellcode encoders, and obfuscators, are dependent on the use of self-modifying code running on RWE memory regions. Considering the current state of security products, such evasion attempts are easily detected by memory analysis tools such as [Moneta](https://github.com/forrest-orr/moneta) and [Pe-sieve](https://github.com/hasherezade/pe-sieve). This project introduces a new approach to code obfuscation with the use of machine code de-optimization. It uses certain mathematical approaches, such as arithmetic partitioning, logical inverse, polynomial transformation, and logical partitioning, for transforming/mutating the instructions of the target binary without creating any recognizable patterns. The tool is capable of transforming the instructions of a given binary up to ~95% by using the mentioned de-optimization tricks.

**Watch the presentation for more...**

## Installation

**Download the pre-built release binaries [HERE](https://github.com/EgeBalci/deoptimizer/releases).**

[![Open in Cloud Shell](.github/img/cloud-shell.png)](google-cloud-shell)

***From Source***
```
cargo install deoptimizer
```

***Docker Install***

[![Docker](http://dockeri.co/image/egee/deoptimizer)](https://hub.docker.com/r/egee/deoptimizer/)

```bash
docker run -it egee/deoptimizer -h
```

## Usage

```
Machine code deoptimizer.

Usage: deoptimizer [OPTIONS]

Options:
  -a, --arch <ARCH>                     Target architecture (x86/arm) [default: x86]
  -f, --file <FILE>                     target binary file name [default: ]
  -o, --outfile <OUTFILE>               output file name [default: ]
  -s, --source <SOURCE>                 source assembly file [default: ]
      --syntax <SYNTAX>                 assembler formatter syntax (nasm/masm/intel/gas) [default: keystone]
  -b, --bitness <BITNESS>               bitness of the binary file (16/32/64) [default: 64]
  -A, --addr <ADDR>                     start address in hexadecimal form [default: 0x0000000000000000]
      --skip-offsets <SKIP_OFFSETS>...  File offset range for not deoptimizing (eg: 0-10 for skipping first ten bytes)
  -c, --cycle <CYCLE>                   total number of deoptimization cycles [default: 1]
  -F, --freq <FREQ>                     deoptimization frequency [default: 0.5]
      --transforms <TRANSFORMS>         allowed transform routines (ap/li/lp/om/rs) [default: ap,li,lp,om,rs]
      --allow-invalid                   allow processing of invalid instructions
  -v, --verbose                         verbose output mode
      --debug                           debug output mode
  -h, --help                            Print help
  -V, --version                         Print version
```

### Currently Supported Architectures

|  **Architecture** | **32** | **64** |
|:-----------------:|:------:|:------:|
|      **x86**      |   ✅   |   ✅   |
|      **ARM**      |   ❌   |   🚧   |
|     **RISC5**     |   ❌   |   🚧   |

## TO DO 
- [ ] PE file support.
- [ ] ELF file support
- [ ] Mach-O file support.
- [ ] ARM architecture support.
- [ ] RISC5 architecture support.
