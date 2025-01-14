# split_tests

Fork of https://github.com/leonid-shevtsov/split_tests to support parsing JUnit XML reports generated by Gradle for JVM projects.

Splits a test suite into groups of equal time, based on previous tests timings.

This is necessary for running the tests in parallel. As the execution time of test files might vary drastically, you will not get the best split by simply dividing them into even groups.

## Usage

Download and extract the latest build from the releases page.

### Using a JUnit report

```
split_tests -junit -junit-path=report.xml -split-index=0 -split-total=2
```

### Development
### Build
```bash
go build main.go junit.go split_files.go
```

### Run/test
```bash
./main -junit-path="./test/**.xml" -split-index=1 -split-total=2 -glob="src/**/*.kt" -prefix="src/" -postfix=".kt"
```


## Deployment

- Install Go
- Checkout the code
- `make`

## Arguments

```plain
$./split_tests -help

  -glob 'pattern'
        Glob pattern to find test files (default 'spec/**/*_spec.rb'). Make sure to single-quote the pattern to avoid shell expansion.
  -prefix 'string'
        Glob pattern to find test files (default 'spec/**/*_spec.rb'). Make sure to single-quote the pattern to avoid shell expansion.
  -postfix 'string'
        Glob pattern to find test files (default 'spec/**/*_spec.rb'). Make sure to single-quote the pattern to avoid shell expansion.
  -exclude-glob 'pattern'
        Glob pattern to exclude test files. Make sure to single-quote as well.
  -help
        Show this help text
  -junit
        Use a JUnit XML report for test times
  -junit-path string
        Path to a JUnit XML report (leave empty to read from stdin; use glob pattern to load multiple files)
  -split-index int
        This test container's index (or set CIRCLE_NODE_INDEX) (default -1)
  -split-total int
        Total number of containers (or set CIRCLE_NODE_TOTAL) (default -1)
```

