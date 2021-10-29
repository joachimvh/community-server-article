## Architecture
{:#architecture}

The architecture of the server heavily makes use of dependency injection:
every class is independent of the other classes and only depends on interfaces.
This allows us to easily swap out classes for other implementations,
as long as they follow the same interface,
which provides the required flexibility mentioned in [](#requirements).
How we link those components together is covered in [](#configuration).

One related aspect is that every component is responsible for solving a small problem
while being mostly unaware of the bigger picture.
This makes it so small parts get chipped of the problem of resolving a request 
until there is nothing left and the answer has been output.

### Reductive Request Processing(tm)
<figure id="architecture-diagram" class="listing">
````/figures/architecture-diagram.md````
<figcaption markdown="block">
The path an HTTP request takes through the server.
</figcaption>
</figure>

Markdown lists seem to not render as expected so should use a different format.
{:.todo}

[](#architecture-diagram) shows a simplified overview of how an LDP request gets resolved by
being passed through several components.
It starts as an HTTP request and ends as the output is written as an HTTP response.
The steps are as follows:
1. The request is parsed into an easy-to-use Operation object 
   containing all the parsed essentials of the request.
2. We extract the credentials from the request. 
   Generally this will either be blank or the WebID identifying who is doing the request.
3. From the Operation we extract which CRUD permissions are required to resolve the request.
4. The permission reader determines what the request owner is allowed to do on the target resource.
5. The authorizer determines if the request can proceed based on the output from step 3 and 4.
6. The Operation handler resolves the Operation and generates a Response Description,
   containing everything needed to write a valid response.
    - In case any of the previous steps failed, 
      a Response Description will be generated based on the error thrown.
7. The Response Description is used to write a response.

Backend data access is hidden behind a Resource Store.
This interface has functions corresponding to all the CRUD requirements.
The Operation handler in step 6 then calls the corresponding function based on the HTTP method.

<figure id="store-diagram" class="listing">
````/figures/store-diagram.md````
<figcaption markdown="block">
The stores an operation passes through before reaching the backend.
</figcaption>
</figure>

In practice, the Resource store is actually several store implementations all chained together,
as can be seen in [](#store-diagram).
Each store again handles a specific a part of the complete behaviour that is expected from the store:
* The Locking store prevents multiple operations from writing to a resource at the same time.
* The Patching store handles PATCH requests.
* The Converting store converts representations to support content negotiation.
* The Data Accessor store supports LDP behaviour by calling a Data Accessor class,
  which is a simple interface to support a specific storage method.
  E.g., file based, memory based, etc.

### PATCH
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
