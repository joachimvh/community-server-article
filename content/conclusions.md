## Future Work & Conclusions
{:#conclusions}

We have achieved our initial goal of creation a server that has uses for a wide target audience,
as can be seen by the interest of both hobby and expert users. 

In the future we want to keep making sure the server adheres to the Solid specification,
but also keep extending its functionality so it becomes both more user-friendly
and has a wide array of different features it supports.

One of the big challenges for the server is versioning.
We follow the [semantic versioning](https://semver.org/) guidelines to make sure
we do not break any server installation.
For each new release, notes are added indicating both the new features 
and how configurations of older versions can be upgraded to the newer version.
Since all classes and configurations are part of the public API of the package,
most changes immediately require a major version increase,
which causes a faster upgrade cycle.

Due to the modular nature of the components,
it is not required for all new features to be added to the main repository.
This makes it possible for companies to develop the features that they require
and then link them to the main server,
thereby becoming the maintainers of that specific feature,
which could be part of their business model.
