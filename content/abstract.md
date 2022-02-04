## Abstract
Kept RV comments after update for reference
{:.todo}

<!-- Context      -->
<span class="comment" data-author="RV">We're gonna need a bit more context here 🙂 
Proposal: how Linked Data has a strong association with public data, 
but that it actually also can be used for private data and everything in between. 
That's the idea behind Solid: empower people and organisations 
with permissioned decentralized knowledge graphs.</span>
<span class="comment" data-author="RV">Also: Solid is a spec.</span>
The Solid project aims to empower people and organisations
by giving them control back over their own data.
It defines a specification that leverages the advantages of linked data
to provide all the necessary functionality needed to achieve such a goal.
The aim is to create an environment where there is clear interoperability
between all solutions that adhere to the defined specification.
<!-- Need         -->
<span class="comment" data-author="RV">There is a need for R&D on top of Solid Pods.
So just enterprise implementations of the spec won't cut it.
Need for modularity should be evident, so the task flows into it.</span>
There already exist several implementations of the protocol,
but due to the still evolving nature of Solid,
there is a strong need for an implementation that enables research into Solid features
and also allows developers to quickly set up a development environment.
<!-- Task         -->
To meet these demands,
we have created the Solid Community server,
a modular server that can be configured to suit many needs.
<!-- Object       -->
In this paper we give an overview of the server architecture,
and how it is situated within the Solid ecosystem.
<!-- Findings     -->
<span class="comment" data-author="RV">This is a hard one for a systems paper indeed; 
but we could describe some concrete cases here where the modularity has been leveraged.</span>
<span class="comment" data-author="RV">Spec-compliant solution, passes test suites.</span>
The server already supports many orthogonal feature combinations
on axes such as authorization, authentication and data storage,
and is fully spec-compliant.
<!-- Conclusion   -->
<span class="comment" data-author="RV">Ready for use in scenarios X and Y.</span>
The server achieves it goal of lowering the barrier of getting started with Solid.
It comes with several predefined configurations that allow developers
to quickly set up a server with different content and backends,
and can easily be modified to change many of the features.
<!-- Perspectives -->
The server will evolve together with the specification,
and we are still continuing work on adding more features that might be useful for the community,
such as adding support for cross-document queries.
<span class="comment" data-author="RV">Concrete needs include query.</span>
