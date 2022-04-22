## Requirements
{:#requirements}

See comunica paper for inspiration: https://comunica.github.io/Article-ISWC2018-Resource/
{:.todo}

As mentioned in [](#introduction) the goal of the Community Solid Server is to provide
a wide spectrum of possibilities for everyone that wants to get involved with Solid,
from starting hobbyists to Solid-focused research labs,
all this while still remaining maintainable for future work.

There are three different axes we wanted to cover during the design of the server,
which we will discuss below.

### Evolving Solid specification
The Solid specification is still a draft specification,
meaning it can and will change in the future.
A consequence of this is that any Solid server implementation that wants to stay relevant
has to be flexible enough, so it can be updated once spec changes occur.
Likewise, a modular server can be used to inform the specification:
if there is any doubt, a new module can quickly be added to assess the impact of a change.
<span class="comment" data-author="RV">That then ties into research, where we can look at designing completely different APIs and algorithms, and see how it behaves</span>

### Research
Solid is still growing as an ecosystem,
this includes the research that investigates all the possibilities of using Solid as a core part of a system.
This sometimes requires quickly setting up thousands of Solid servers for automation
and having flexibility in their configuration such as what storage method is used,
how authorization works,
or how user accounts are managed, for example.
<span class="comment" data-author="RV">A specific class of research (and perhaps this also ties into the next point) could be intermediaries, i.e., not just the clients and servers we're talking about today</span>

### Server Customization
No Solid server is ever going to fully support everything a user wants:
there are infinite possible combinations of features that could be required.
For this reason we wanted to ensure that the implementation allows for easy extension,
so that if, for example, a user wants the server to use their own custom backend,
they do not have to rewrite a significant part of the server logic.

### Application Development
There are many things that have to be checked and kept in mind when developing a new Solid client application.
As mentioned before, it is vital that the application correctly makes use of the Solid API,
but besides that there is also a need for test users, 
testing different authorization situations,
managing different error responses, etc.
This requires testing against an actual server that provides a quick setup and teardown,
and can easily emulate different situations.

### Existing implementations

Think it makes more sense here instead of in related work?
{:.todo}

use more complex request (PATCH) to explain why CSS handles this better?
- NSS would not be able to add ACP instead of ACL?

LDP is just an API, could also have SPARQL endpoint in addition?

#### Linked Data Platform
apache marmotta? virtuoso? trellis?mayktso?

<span class="comment" data-author="RV">More specifically: why off-the-shelf LDP solutions would not do</span>

#### Solid servers
There are already several existing Solid servers,
such as [Node Solid Server](https://github.com/solid/node-solid-server/),
[Enterprise Solid Server](https://github.com/solid/node-solid-server/),
[TrinPod](https://trinpod.us/),
[Reactive-Solid](https://github.com/co-operating-systems/Reactive-SoLiD),
and several others.
While they each have their own advantages and disadvantages,
none of these fulfils the requirements that we set up before though.
Specifically the customization and flexibility requirements that we have, are never fulfilled. 
