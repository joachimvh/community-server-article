## Configuration
{:#configuration}

<span class="comment" data-author="RV">Suggestion: move this before architecture. Then we can talk about this on a high level: why are different configs so interesting? What can we do with them? Then the architecture section can explain how the configs actually work. I.e., use the configs as a starting point, as a necessity, and then the things the architecture needs to do to support this.</span>

As mentioned in [](#related-work),
the server makes use of the Dependency Injection framework [Components.js](cite:cites componentsjs)
This allows us to combine all the independent components discussed in [](#architecture).

It is a framework with much flexibility and options,
but it does have a steep startup curve before fully understanding how configuration works.
To this end we took several steps to make configuration as easy as possible for new users.

### Default configurations

Due to the external nature of the configurations,
Components.js allows us to provide many different versions of the server to the users.

The server comes bundled with several 
[default configurations](https://github.com/CommunitySolidServer/CommunitySolidServer/tree/main/config) 
that can be used out of the box.
These include different backends, such as file or memory based,
and examples on how to configure more complex features.

These default configurations cover the main use cases of many users,
and those who do want to configure a different experience can often achieve this by only making minor adjustments.


### Feature options

Since RDF is used, it is possible to split the configuration up over multiple files
and then import them into a single file.
We strongly make use of this import behaviour to hide most of the configuration complexity from new users.
Specifically, we made it so a user can choose specific features based on the files being imported.
For example, the only difference between a configuration to set up a server with a memory backend
compared to one with a file backend is that the first one imports `/storage/backend/memory.json`
and the second one imports `/storage/backend/file.json`.
This is just one of the imports that users can modify to change behaviour.
To help with the choices there, there is documentation explaining all the available options.


### Configuring extensions

When someone wants to develop a new component for the server,
adding Components.js configuration to link it correctly will be a requirement.
Components.js also requires configuration description files for every class,
describing the class parameters,
but the server is set up to generate those automatically using
[Components-Generator.js](https://github.com/LinkedSoftwareDependencies/Components-Generator.js),
saving developers much work.
Besides that, the many configurations included with the server
should help as examples of how to link components.

<span class="comment" data-author="RV">Walk us through some extensions; walk us through some recipes and briefly what they do.</span>
