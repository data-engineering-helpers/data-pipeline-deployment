Getting started with Go for Data Processing Pipeline (DPP) CLI tool
===================================================================

# References

# Getting started

# First time
* Create the `dppctl` module:
```bash
$ mkdir -p dppctl
$ pushd dppctl
$ go mod init github.com/data-engineering-helpers/data-pipeline-deployment/go/dppctl
$ go mod tidy
$ popd
```

* Create a checker:
```bash
$ mkdir -p tests
$ pushd tests
$ got mod init check-dppctl
$ go mod edit -replace github.com/data-engineering-helpers/data-pipeline-deployment/go/dppctl=../dppctl
$ go mod tidy
$ go run .
$ go build
$ ./check-dppctl
$ popd
```

* Install the checker:
```bash
$ go list -f '{{.Target}}'
~/go/bin/check-dppctl
$ go install
$ ls -laFh ~/go/bin/check-dppctl
-rwxr-xr-x  1 user staff 2.1M Mar 17 16:23 /Users/DENIS/go/bin/check-dppctl*
```


