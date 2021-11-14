## Requirements
{:#requirements}

See comunica paper for inspiration: https://comunica.github.io/Article-ISWC2018-Resource/
{:.todo}

As mentioned in [](#introduction) the goal of the Solid Community Server is to provide
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
<span class="comment" data-author="RV">Also, the server can inform the implementation, thanks to its modularity and easy-to-plug-in code. If there's doubt, just write the CSS module, tweak it, spec it. (I am hereby trademarking _Write it, tweak it, spec it_)</span>
<span class="comment" data-author="RV">That then ties into research, where we can look at designing completely different APIs and algorithms, and see how it behaves</span>

### Research
We wanted to create a server that could be used to perform research on Solid servers,
<span class="comment" data-author="RV">well not just we hopefully 🙂 but phrase from the need, not the solution</span>
meaning it should be easy to automate setup with a variety of different features,
such as different backends, authorization schemes, identity options, etc.
<span class="comment" data-author="RV">A specific class of research (and perhaps this also ties into the next point) could be intermediaries, i.e., not just the clients and servers we're talking about today</span>

### Server <del class="comment" data-author="RV">Development</del> <ins class="comment" data-author="RV">Customization</ins>
No Solid server is ever going to fully support everything a user wants:
there are infinite possible combinations of features that could be required.
For this reason we wanted to ensure that the implementation allows for easy extension,
so that if, for example, a user wants the server to use their own custom backend,
they do not have to rewrite a significant part of the server logic.

### Application Development
<span class="comment" data-author="RV">Also write this in terms of needs, not solution (yet); also the need for test users, fake logins, fake failures, etc.</span>
As mentioned before, when developing a Solid application it is vital
that the application correctly makes uses of the Solid `API`.
One of the easiest ways to ensure this is to test the app against an actual server.
To this end, we wanted the server to also be easily usable by application developers:
easy to set up, easy to configure and easy to use for their test data.
