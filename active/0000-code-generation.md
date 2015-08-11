Start Date: 2015-03-23
RFC PR: (leave this empty)
Revel Issue: (leave this empty)

# Summary
This is a high level RFC that describes the use of `go generate` mechanism for code auto generation as a replacement of `harness`.

# Motivation
Right now Revel Framework has a monolithic command that's responsible for many things including generation of:
* `app/tmp/main.go`
* `app/routes/routes.go`
The idea behind this RFC is to replace it by small utilities. Every of them will be responsible for generation of its own part.
`revel` command will be used only for watching files, and running `go generate && go build && go run`.

Thus, it will be easier to support `revel/cmd` code base. And it will be possible to run Revel Framework applications as regular go language programs: `go run path/to/application`. I.e. they will not depend on `revel` command anymore.

# Detailed design
`app/init.go` includes comments that describe what commands and with what parameters should be executed.
Specific details and expected behaviour of the commands is TBD. Possible values are illustrated below:
```go
//go:generate revgen-controller -o main.go
//go:generate revgen-routes -o /app/routes/routes.go
```
So, every time `go generate path/to/appliation` is run the files we need will be generated. *The generated files should not be ignored by Version Control System* [1].
And it will be possible to run application without installation of `revel/cmd`.

`revel/cmd` will be used just as a helper that watches the changes in `app` directory and runs `go generate && go build && go run` if necessary.

# Drawbacks
User will have to install `revgen-controller`, `revgen-routes`, and other utilities. It is possible to implement all those programs as separate packages and use `revel generate cmdName` command as a wrapper though.

# Alternatives
Alternatively, we can try to refactor the code we have already had and try to make it modular. Otherwise, it will be difficult to maintain the code base and develop new features.

# Unresolved questions
Details of generator utils and their expected behaviour are still TBD.

# References
1. http://blog.golang.org/generate
