# Updating go and toolchain versions at once

Sometimes we need to closely track the Go version that is used within a project, mostly because
some other tools like static scanners will use it to determine if there are any existing vulnerabilities.

Since Go 1.21, [reproducible builds][00] are possible. Since Go aims for build reproducibility, even when we specify
the _minimum go version_ with the `go` directive in the `go.mod` file, modules are downloaded from source code and
compiled on each host. This is why Go needs to keep track of which toolchain was used to compile those sources in
order to let others fully reproduce the same exact build, and it is the reason why other commands like `go get <module>`
also update the toolchain directive in go.mod: because they trigger compilation of the source code of other modules.

In most cases, what we typically want is to use a _minimum go version_ that contains all the language features that
we need for our project, and a _minimum toolchain version_ as recent as possible to get any vulnerabilities fixed as soon
as possible.

However, in collaborative projects where each developer may have a different toolchain versions, we typically do not want
to have a lot of churn in the `go.mod` file, and neither force developers to update the toolchain over and over again.

After reading the document about [toolchains][01] in go documentation, I found the incantation that we likely want to
use in these cases:

```console
GO_VERSION="1.22.12" # Change to whatever value we want to update
go get "go@${GO_VERSION}" toolchain@none
```

This command:
- Updates the go directive
- Removes the toolchain directive, forcing to implicit use of the same version indicated by the go directive
- Makes any adjustment to `go.mod` to satisfy such versions
    - This should only be relevant on version downgrades, which are unlikely

Actually, quoting the [toolchains document][01] (emphasis mine):

_Before Go 1.21, the suggested way to update a module to a new Go version (say, Go 1.22) was go mod tidy -go=1.22,
to make sure that any adjustments specific to Go 1.22 were made to the `go.mod` at the same time that the go line is
updated. That form is still valid, but **the simpler go get go@1.22 is now preferred**._

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://go.dev/blog/rebuild
[01]: https://go.dev/doc/toolchain
