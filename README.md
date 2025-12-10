## 🔍 What is SmokeRand?

SmokeRand is a set of tests for pseudorandom number generators. Tested generators should return either 32-bit or 64-bit unsigned uniformly distributed unsigned integers.

### 📦 Compiling:

1. Download the latest [release](release/) archive file or clone the Git repo
2. Run the `make_pkg.sh` script in the root
3. The `smokerand` binary will be placed in the `bin/` directory

### 🔋 Batteries

Four primary batteries are implemented in SmokeRand:

- `express` - simplified battery that consists of 5 tests and can be
  rewritten for 16-bit platforms with 64KiB segments of data and code.
  Less powerful than `brief` but may be more sensitive than diehard
  or even dieharder.
- `brief` - a fast battery that includes a reduced set of tests, e.g.
  matrix rank tests and some tests for higher bits of generators
  are excluded.
- `default` - a more comprehensive but slower battery with extra tests
  for higher bits of generators and matrix rank tests. Other tests use
  larger samples that make them more sensitive.
- `full` - similar do default but uses larger samples.


 Battery | Number of tests | Bytes (32-bit PRNG) | Bytes (64-bit PRNG)
---------|-----------------|---------------------|---------------------
 express | 7               | 2^26                | 2^27
 brief   | 25              | 2^35                | 2^36
 default | 42              | 2^37                | 2^38
 full    | 46              | 2^40                | 2^41

### ✨ Usage:

    $ ./smokerand (battery) (path/to/rng.so) [--threads]

To test the lcg64 generator the next command can be used:

    $ ./smokerand default generators/lcg64.so --threads

Integration with PractRand:

    $ ./smokerand stdout generators/lcg64.so | RNG_test stdin32 -multithreaded

Getting PRNG input from stdin (multithreading is not supported in this case):

    $ ./smokerand stdout generators/lcg64.so | ./smokerand express stdin32

Integeration with TestU01 using the TestU01-threads plugin:

    $ ./smokerand s=libtestu01th_sr_ext.so generators/lcg64.so --batparam=SmallCrush --threads

### 🧰 Other tools similar to SmokeRand:

* [PractRand](https://pracrand.sourceforge.net/)
* [TestU01](https://simul.iro.umontreal.ca/testu01/)

### 📄 More information:

Want to learn how the SmokeRand works under the hood? Check our detailed [implementation information](implementation_detauls.md).
