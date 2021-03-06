# BLS Signature Scheme over BLS12-381 pairing-friendly curve

[![Build Status: Travis](https://img.shields.io/travis/status-im/nim-blscurve/master?label=Travis%20%28Linux%20x86-64%2FARM64%2C%20MacOS%20x86-64%29](https://travis-ci.org/status-im/nim-blscurve)
[![Build status](https://ci.appveyor.com/api/projects/status/6l1il60ljfbtxw3g/branch/master?svg=true)](https://ci.appveyor.com/project/nimbus/nim-blscurve/branch/master)
[![Build Status: Azure](https://img.shields.io/azure-devops/build/nimbus-dev/0c305144-232d-4f3e-ba77-93e4e81182da/4/master?label=Azure%20%28Linux%2064-bit%2C%20Windows%2032-bit%2F64-bit%2C%20MacOS%2064-bit%29)](https://dev.azure.com/nimbus-dev/nim-blscurve/_build?definitionId=4&branchName=master)

This library implements:
- The BLS signature scheme (Boneh-Lynn-Shacham)
- over the BLS12-381 (Barreto-Lynn-Scott) pairing-friendly curve

Cipher suite ID: BLS_SIG_BLS12381G2-SHA256-SSWU-RO-\_POP\_

## Installation

You can install the developement version of the library through nimble with the following command
```
nimble install https://github.com/status-im/nim-blscurve
```

## Implementation stability

This repo follows Ethereum 2.0 requirements.

Besides the standardization work described below, no changes are planned upstream
for the foreseeable future.

### Standardization

Currently (Jun 2019) a cross-blockchain working group is working to standardize BLS signatures
for the following blockchains:
- Algorand
- Chia Network
- Dfinity
- Ethereum 2.0
- Filecoin
- Zcash Sapling

#### Signature scheme

- IETF draft submission: https://tools.ietf.org/html/draft-boneh-bls-signature-00
- Repo for collaboration on the draft: https://github.com/cfrg/draft-irtf-cfrg-bls-signature

#### Hashing to curve

- https://tools.ietf.org/html/draft-irtf-cfrg-hash-to-curve-05

#### Curve implementation

- https://tools.ietf.org/html/draft-irtf-cfrg-pairing-friendly-curves-00

## Backend

This library uses sources from [AMCL (Apache Milagro Crypto)](https://github.com/apache/incubator-milagro-crypto-c).

### Keeping track of upstream

To keep track of upstream AMCL:

- Update the submodule.
- Execute `nim e milagro.nims amcl blscurve/csources`
- Test
- Commit

### Executing the test suite

We recomment working within the nimbus build environment described here:
https://github.com/status-im/nim-beacon-chain/

To execute the test suite, just navigate to the root of this repo and execute:

```
nimble test
```

> Please note that within the nimbus build environment, the repository will
  be located in `nim-beacon-chain/vendor/nim-blscurve`.

### Executing the fuzzing tests

Before you start, please make sure that the regular test suite executes
successfully (see the instructions above). To start a particular fuzzing
test, navigate to the root of this repo and execute:

```
nim tests/fuzzing/run_fuzzing_test.nims <test-name>
```

You can specify the fuzzing engine being used by passing an additional
`--fuzzer` parameter. The currently supported engines are `libFuzzer`
(used by default) and `afl`.

All fuzzing tests are located in `tests/fuzzing` and use the following
naming convention:

```
fuzz_<test-name>.nim
```

## License

Licensed and distributed under either of

* MIT license: [LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT
* Apache License, Version 2.0, ([LICENSE-APACHEv2](LICENSE-APACHEv2) or http://www.apache.org/licenses/LICENSE-2.0)

at your option. This file may not be copied, modified, or distributed except according to those terms.
