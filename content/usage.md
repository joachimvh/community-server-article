## Usage & Impact
{:#usage}

### Repository
Update numbers when finished
{:.todo}

At the time of writing, the [repository](https://github.com/CommunitySolidServer/CommunitySolidServer)
has 288 stars and 72 forks.
The corresponding [gitter](https://gitter.im/CommunitySolidServer/community) chatroom has 32 people.

### Maintenance
During the development of the server
we have always focused on making sure the code bases remained of high quality.
One way we did this is by requiring the unit tests 
to always have 100% code coverage on all code in the project.
While this is not immediately an indication of everything working as intended,
it does make sure that a developer checks that new classes output data as expected.

Another requirement is that all new code needs to be added through pull requests,
which always require at least one code review before being able to be merged.
This means that all code is seen by multiple people before being added.

Besides the unit tests, we also have extensive integration tests covering the larger parts of the server.
These, for example, test all the entire Identity Provider procedures
and all the supported LDP actions.

### Projects
Some projects that other people have already made with the server:
<ul>
  <li>Reading calendar data using a Solid server: https://github.com/KNowledgeOnWebScale/solid-calendar-store/</li>
  <li>Operating Philips Hue lamps through a Solid server: https://github.com/RubenVerborgh/solid-hue/</li>
  <li>Data-Kitchen, a desktop app combining local files and Solid pods: https://github.com/solid/data-kitchen/</li>
  <li>Solid-Redis, a component for the server to use Redis as data storage: https://github.com/comake/solid-redis</li>
</ul>

[use.id](https://get.use.id/) is an example of a commercial product that was built using the server.

Make sure this URL (and many others) also appear in the printed version.
{:.todo}

<span class="comment" data-author="RV">And all apps that work on the server?</span>
<span class="comment" data-author="JVH">Do you mean Solid client apps? Will have to investigate which ones are up to date enough to work. Media Kraken and Mashlib are at least 2.</span>

Do we explicitly have to say which projects are related to our lab?
{:.todo}
