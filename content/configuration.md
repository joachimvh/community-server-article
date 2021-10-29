## Configuration
{:#configuration}

How much of components.js do we explain here compared to related work?
{:.todo}

talk about how imports match features to help users

To combine all the independent components discussed in [](#architecture)
we make use of the dependency injection framework [Components.js](https://componentsjs.readthedocs.io/),
which uses [JSON-LD](https://json-ld.org/) configuration files to link all the components together.

### Ease of use
Components.js is a very strong framework with much flexibility,
but it does have a steep startup curve before fully understanding how configuration works.
To this end we took several steps to make configuration as easy as possible for new users.

The server comes bundled with several default configurations that can be used out of the box.
These include different backends, such as file or memory based,
and examples on how to configure more complex features.

Since JSON-LD is used, it is possible to split the configuration up over multiple files
and then import them into a single file.
We strongly make use of this import behaviour to hide most of the configuration complexity from new users.
Specifically, we made it so a user can choose specific features based on the files being imported.
For example, the only difference between a configuration to set up a server with a memory backend
compared to one with a file backend is that the first one imports `/storage/backend/memory.json`
and the second one imports `/storage/backend/file.json`.
This is just one of the currently 29 lines of imports that users can modify to change behaviour.
To help with the choices there, all configuration subfolders contain documentation
explaining the options available.

When someone wants to develop a new component for the server,
adding Components.js configuration to link it correctly will be a requirement.
Components.js also requires configuration description files for every class,
describing the class parameters,
but the server is set up to generate those automatically using
[Components-Generator.js](https://github.com/LinkedSoftwareDependencies/Components-Generator.js),
saving developers much work.
Besides that, the many configurations included with the server
should help as examples of how to link components.
