Testing and analysis
--------------------

## Scripts

* `test.include`: Constants and helper functions for test scripts.

* `test_bug_mining.sh`: Tests the
  [bug-mining](https://github.com/rjust/defects4j/blob/master/framework/bug-mining) infrastructure.

* `test_export_command.sh`: Tests the
  [export](https://github.com/rjust/defects4j/blob/master/framework/bin/d4j/d4j-export) command.

* `test_fix_test_suite.sh`: Tests the
  [fix_test_suite.pl](https://github.com/rjust/defects4j/blob/master/framework/util/fix_test_suite.pl) script.

* `test_gen_tests.sh`: Tests the
  [gen_tests.pl](https://github.com/rjust/defects4j/blob/master/framework/bin/gen_tests.pl) script.
  Specifically, this script tests the integration of all supported test
  generators and the compatibility of the generated test suites with the
  coverage, mutation, and bug detection analyses.

* `test_mutation_analysis.sh`: Tests various options for the mutation analysis.

* `test_sanity_check.sh`: Checks out each buggy and fixed project version and
  checks for compilation and required properties.

* `test_tutorial.sh`: Runs the tutorial described in the top-level
   [README](https://github.com/rjust/defects4j#using-defects4j).

* `test_verify_bugs.sh`: Reproduces a bug, or a set of bugs, and verifies that
   the observed set of triggering tests matches the expected set of triggering
   tests.

## CI testing
See [`.github/workflows/ci.yml`](../../.github/workflows/ci.yml) for the set of
tests that currently run in CI.

## Local testing
Some tests take a long time to run and usually only need to be run for major
version updates (e.g., bumping the Java version or adding new defects).

### Export command and exported properties
The `test_export_command.sh` test takes a long time as it checks out every
single defect and checks whether the exported paths, files, etc. make sense.

### Reproducing all bugs (parallel)
Reproducing all bugs is the most time-consuming test. To speed it up, we use
GNU parallel (`-j` gives the number of parallel processes):
```
./jobs_verify_bugs.pl | shuf > jobs.txt
parallel -j20 --progress < jobs.txt
```
