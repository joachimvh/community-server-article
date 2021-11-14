## Usage & Impact
{:#usage}

### Repository
Update numbers when finished
{:.todo}

At the time of writing, the [repository](https://github.com/solid/community-server)
has 200 stars and 50 forks.
The corresponding [gitter](https://gitter.im/solid/community-server) chatroom has 55 people.

### Maintenance
During the development of the server
we have always focused on making sure the code bases remained of high quality.
One way we did this is by enforcing all new code to be added through pull requests,
which always require at least one code review before being able to be merged.
This means that all code is seen by multiple people before being added.

Another requirement of new code being added is that unit tests
always have 100% code coverage on all code in the project.
<span class="comment" data-author="RV">Would list this one first</span>
While this is not immediately an indication of everything working as intended,
it does make sure that a developer checks that new classes output data as expected.

Besides the unit tests, we also have extensive integration tests covering the larger parts of the server.
These, for example, test all the entire Identity Provider procedures
and all the supported LDP actions.

### Projects
Some projects that other people have already made with the server:
 * Reading calendar data using a Solid server: https://github.com/KNowledgeOnWebScale/solid-calendar-store/
 * Operating Philips Hue lamps through a Solid server: https://github.com/RubenVerborgh/solid-hue/
 * Data-Kitchen, a desktop app combining local files and Solid pods: https://github.com/solid/data-kitchen/

<span class="comment" data-author="RV">And all apps that work on the server?</span>

Do we explicitly have to say which projects are related to our lab?
{:.todo}

Any companies/large projects we should add? Digita? Cern? ...?
{:.todo}
