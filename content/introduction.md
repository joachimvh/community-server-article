## Introduction
{:#introduction}

<span class="comment" data-author="RV">TODO: the socio-economic problem Solid is solving (see my blog posts for inspiration)</span>

[Solid](cite:cites solid) is many things.
<span class="comment" data-author="RV">I think that conventions are not enough; technical specifications to achieve the aforementioned goal?</span>
At the core it is a set of [API conventions](https://solid.github.io/specification/) to facilitate
built upon the [Linked Data Platform](cite:cites ldp) (LDP) specification.
<span class="comment" data-author="RV">Before describing what it adds, explain the needs of _why_ this is added</span>
It adds, among other things, components such as identity, authentication and authorization.
<span class="rephrase" data-author="RV">But that is just the server component.</span>

Besides the servers, there are also the Solid applications,
which are client applications that effectively use Solid servers as a backend through the Web.
The idea there is that multiple applications can independently make use of the same server,
while still interacting with the same data.
<span class="comment" data-author="RV">Yes, make the point a bit more explicitly: the apps conform to the spec, the server conforms to the same spec, so any app works with any server. The browser/Apache comparison might be useful; here or already earlier.</span>
This way a person only needs to store their personal data in a single place
which can then be reused by all applications that have need of this information.

Solid is deeply a community effort: all layers influence each other.
<span class="comment" data-author="RV">Which layers?</span>
The server API and specification naturally influence how the applications have to be developed.
On the other hand, the actual experiences of application developers
and how they experience interacting with the server
is vital in ensuring a healthy development of the environment.

Due to the open-source nature of Solid development,
both in available tooling and discussions being had,
everyone can cooperate to improve what is available,
which again emphasizes the community aspect of Solid.

The Community Solid Server was built from the ground up to support this community aspect.
Starting from the design phase, 
the idea was always that it could be used by a multitude of users:
ranging from people who want try out this Solid thing,
to application developers that want to test out their new app against a certain setup,
to backend developers that want to set up Solid servers with specific requirements.

