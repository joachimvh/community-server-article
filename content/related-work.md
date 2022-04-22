## Related Work
{:#related-work}

Many more references?
{:.todo}

### Linked Data Platform
[Linked Data Platform](cite:cites ldp) (LDP) is a set of rules to provide a RESTful API
to read/write Linked Data resources on the Web.
It introduces several concepts such as using URIs to identify resources
and using RDF standards to provide information and data.

### Solid
The [Solid](cite:cites solid) project is a combination of [specifications](https://solid.github.io/specification/)
with a focus on data ownership and data interoperability.
At its core is the [Solid Protocol](https://solidproject.org/TR/protocol) specification
which determines how Solid servers should behave.
It is built upon the LDP specification and has a stricter
and more well-defined expectation for each of the CRUD operations.

### Components.js
[Components.js](cite:cites componentsjs) is a Dependency Injection framework built specifically
for [TypeScript](https://www.typescriptlang.org/) projects.
It is non-invasive in that all of its configurations happens outside the source code in external configuration files,
which describe how classes are linked to each other and which parameters they require.
These descriptions are done in RDF, which means that those configuration files are valid RDF serializations.
Usually [JSON-LD](https://json-ld.org/) is used.

### OIDC
To handle authentication, the server implements the [Solid-OIDC](https://solid.github.io/solid-oidc/) specification,
which builds upon the [OAuth 2.0](cite:cites oauth) and 
[OpenID Connect Core 1.0](https://openid.net/specs/openid-connect-core-1_0.html) standards.
These are two widely adopted standards,
and the above specification extends them to solve problems specific for the Solid ecosystem.
