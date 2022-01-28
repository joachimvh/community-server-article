## Architecture
{:#architecture}

[](#requirements) explained that there is a strong need for flexibility in the server.
We want it to be possible for anyone to set up the server tailored specifically tot their needs.
We enabled this by making the codebase completely modular:
all classes are completely independent of each other and only define which interfaces they expect.
This allows anyone to easily swap out any implementation without impacting other components,
as long as they follow those same interfaces.

### Dependency Injection
This entire subsection seems to not really fit here and should perhaps be moved somewhere else.
Components.js should also have been partially described in related work already.
{:.todo}

To combine all our classes and inject their dependencies,
we make use of a Dependency Injection (DI) framework.
Such a framework injects actual implementations of the expected interfaces into the classes.
This way the actual class chains are configured externally to our implementations,
making these much easier to change.
We specifically use the [Components.js](cite:cites componentsjs) DI framework,
which uses declarative RDF configuration files to link everything together.
How this works in practice is covered in [](#configuration).

### Components
Due to the nature of our DI-based architecture,
every component is mostly unaware of what its own role is in the grand scheme of things.
For example, there is a component that converts authentication headers into a usable identifier,
not knowing which component will make use of it.
There is component that converts thrown errors to serializable output,
and another simply takes incoming RDF serializations and converts them to quad objects.

The combination of this architecture, combined with the DI framework, 
brings many advantages for both developers and users.

#### Making sure the server correctly implements the Solid protocol
The Solid protocol is defined in a specification that is still evolving.
We know that it is not final and future changes are still planned.
It is important that the impact of such changes impacts a minimal amount of components.
On the one hand this makes it much easier for developers to keep the server in line with the specification.
On the other hand, this also reduces the chances of breaking any extensions
that might have been created for the server.

#### Extending the server features
Components.js does not require the components it links together to be in the same repository.
It can import components from other projects.
This means anyone can easily extend the features of the server by writing their own modules.
In case multiple ideas need to be compared it only requires a configuration change
to set up multiple different versions of the server.
This is highly useful when doing research to evaluate different aspects,
or even as part of discussions on the Solid specification to immediately see certain suggestions in practice.

#### Components and configurations can be reused
While it is possible to extend the server with custom components,
the reverse is also true: individual components of the server can be reused.
All the components are exposed through the project,
so it is possible to include only a few of them specifically if preferred.
The configurations provided with the server can also be reused,
allowing the reuse of partial blocks without having to reconfigure them completely.

### High-level Architectural View
Should cover some parts of how a Solid server works in the related work as we don't want to cover all of it here?
Should also use references instead of just links.
{:.todo}

The goal of the server is to accept incoming HTTP requests
and send a correct response based on what is defined in the Solid specification.
The specification consists of several core parts.
The community server supports these by having different components for each of them.
These can then be consecutively applied to the incoming request to reach the final result,
with each of them potentially stopping the request in case of an invalid request.
Below we cover some of these major core components.

#### Authentication
Authentication in Solid is part of the [Solid-OIDC](https://solid.github.io/solid-oidc/) specification.
The authentication block of the server will parse the relevant headers of an incoming request
to identify the agent calling the server.
It will output the correct identifier to be used by other components.

#### Authorization
For authorization, the [Web Access Control](https://solidproject.org/TR/wac) specification is used.
There are multiple components at work here as handling this requires several steps.
The sever has to determine which permissions are required based on the kind of request.
It also has to determine which permissions are allowed on the target resource.
A request is only valid if required permissions are allowed.

#### Solid Protocol
The main Solid specification is the [Solid Protocol](https://solidproject.org/TR/protocol).
It is based on the [Linked Data Platform](cite:cites ldp) specification
and determines how different possible HTTP methods should be interpreted by the server.
There are many relevant components here as there are many possibilities here,
but the end goal is always to perform the necessary data action and return the result.

### Reductive Request Processing
As we mentioned before,
all the components in the server solve a specific problem
and are mostly unaware of the grander scheme of what is going on.
Requests to the server are solved by letting each component
handle a small part of the problem,
so the next component can continue and do the same,
until it has been completely solved.

<figure id="architecture-diagram" class="listing">
````/figures/architecture-diagram.md````
<figcaption markdown="block">
The path an HTTP request takes through the server.
</figcaption>
</figure>

[](#architecture-diagram) shows a simplified overview of how a request gets resolved.
It starts as an HTTP request and ends as the output is written as an HTTP response.
The steps are as follows:

1. The request is parsed into an <span class="rephrase" data-author="RV">easy-to-use</span> Operation object 
   containing all the parsed essentials of the request.
2. We extract the credentials from the request. 
   Generally this will either be blank or the WebID identifying who is doing the request.
3. From the Operation we extract which CRUD permissions are required to resolve the request.
4. The permission reader determines what the request owner is allowed to do on the target resource.
5. The authorizer determines if the request can proceed based on the output from step 3 and 4.
6. The Operation handler resolves the Operation and generates a Response Description,
   containing everything needed to write a valid response.
7. In case any of the previous steps failed, 
   a Response Description will be generated based on the error thrown.
8. The Response Description is used to write a response.

### Data storage
Solid does not specify how data should be stored,
only how it should be returned.
Internally we have done the same by abstracting data access with a Resource Store.
This allows us to have different stores for different storage methods,
such as in-memory, file-based or with a SPARQL endpoint.
This interface has functions corresponding to all the CRUD requirements.
In the previous subsection, the Operation handler of step 6
calls the corresponding function based on the HTTP method.

<figure id="store-diagram" class="listing">
````/figures/store-diagram.md````
<figcaption markdown="block">
The stores an operation passes through before reaching the backend.
</figcaption>
</figure>

In practice, the Resource Store is actually several store implementations all chained together,
as can be seen in [](#store-diagram).
Each store again handles a specific a part of the complete behaviour that is expected from the store:
<ul>
    <li>The Locking store prevents multiple operations from writing to a resource at the same time.</li>
    <li>The Patching store handles PATCH requests.</li>
    <li>The Converting store converts representations to support content negotiation.</li>
    <li>The Data Accessor store supports LDP behaviour by calling a Data Accessor class,
      which is a simple interface to support a specific storage method.
      E.g., file based, memory based, etc.</li>
</ul>

### Example Request Runthrough: `PATCH`
One specific example of how the server makes use of smaller independent tools to solver a bigger problem
can be seen in how it handles PATCH requests.
Currently, Solid servers generally only accept PATCH request 
that contain a [SPARQL UPDATE](https://www.w3.org/TR/sparql11-update/) body
to edit `RDF` resources.

One solution for this would be to support these queries
in the same component that also handles storing the data,
seeing as we have direct access to the data there.
The disadvantage is that such an implementation 
would be required for every different storage method used,
thus also providing extra work for developers that want to
support a new storage method on the server.

Our server handles this differently.
As can be seen in [](#store-diagram),
we have a component specifically for handling PATCH requests.
This store first checks of the next store supports a PATCH by itself,
as could for example be the case if the storage method is a SPARQL endpoint.
But if this is not the case, this store provides a fallback method:
1. Create a new internal request to acquire the data,
   using content negotiation to request triple data.
2. Execute the SPARQL UPDATE query on the received triple data in memory.
3. Create a another internal request to write the resulting data to the resource,
   again using content-negotiation to convert back to the original media type.

The converting component in this story is unaware that a PATCH request is using it,
it simply knows that it first gets a request to convert an RDF serialization to triples,
and then another request to convert triples into a serialization again.
Likewise, the backend storage only knows that it first has to return a data stream,
and afterwards has to overwrite the resource data.
On the other hand, the patching component does not know what the original data serialization was,
or how it was stored,
it can only apply a SPARQL UPDATE query on a set of triples.
