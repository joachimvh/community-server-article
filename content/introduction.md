## Introduction
{:#introduction}

[Solid](cite:cites solid) is many things.
At the core it is a set of [API conventions](https://solid.github.io/specification/) to facilitate
built upon the [Linked Data Platform](cite:cites ldp) (LDP) specification.
It adds, among other things, components such as identity, authentication and authorization.
But that is just the server component.

Besides the servers, there are also the Solid applications,
which are client applications that effectively use Solid servers as a backend through the Web.
The idea there is that multiple applications can independently make use of the same server,
while still interacting with the same data.
This way a person only needs to store their personal data in a single place
which can then be reused by all applications that have need of this information.

Solid is deeply a community effort: all layers influence each other.
The server API and specification naturally influence how the applications have to be developed.
On the other hand, the actual experiences of application developers
and how they experience interacting with the server
is vital in ensuring a healthy development of the environment.

Due to the open source nature of Solid development,
both in available tooling and discussions being had,
everyone can cooperate to improve what is available,
which again emphasizes the community aspect of Solid.

The Solid Community Server was built from the ground up to support this community aspect.
Starting from the design phase, 
the idea was always that it could be used by a multitude of users:
ranging from people who want try out this Solid thing,
to application developers that want to test out their new app against a certain setup,
to backend developers that want to set up Solid servers with specific requirements.

