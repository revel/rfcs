Start Date: 2015-04-03
RFC PR: (leave this empty)
Revel Issue: (leave this empty)

# Summary
We want to refactor Revel to be more modular and extensible. We want Revel to expose its `net.http` handler to the app developer. We want Revel to be less monolithic and magical. This is related to the `code-generation` RFC.

# Motivation
We've had many issues in the past and recently that are highlighting certain architectural deficiencies in Revel's design. For example, developers want to be able to use Revel in conjunction with other `net.http` handling code. Our current design does not support this task in a clear and obvious manner.

Further, our current design has a unique advantage of modular app code via Revel Modules, but this relies on the `revel` command to dynamically parse `conf/app.conf` and `conf/routes` and then compile the Revel app as if it were all a single code base. This adds a certain layer of complexity and abstraction, such as auto generating `main.go` instead of it being managed by the developer. We need to explore alternative designs to enable modules while allowing greater control of individual Revel apps.

# Detailed design

We will retain the existing `app` file structure.

# Drawbacks


# Alternatives


# Unresolved questions
How can we support modules?

# References
