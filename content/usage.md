## Usage
{:#usage}

The usage of an open-source project without the use of any tracking software is a picture that is always incomplete.
Nevertheless, we analyze the usage of Components.js in this section on two aspects:
empirical usage via available metrics, and in-use analysis of specific projects.
We discuss these two aspects hereafter.

### Usage Metrics

As the source code of Components.js is hosted on [GitHub](https://github.com/LinkedSoftwareDependencies/Components.js){:.mandatory},
it is possible to inspect the usage of this project within other projects hosted on GitHub.
As of August 2 2021, there are 9 GitHub projects that depend on Components.js directly, and 268 that depend on it indirectly via transitive dependencies.
This shows that Components.js is primarily used as a core library to support larger projects that have a broad usage.

The [npm package manager](https://www.npmjs.com/package/componentsjs){:.mandatory} from which Components.js can be installed offers us additional insights.
For the week of July 26 2021 until August 1 2021 there were 5.351 downloads, which is an average number when comparing it to previous weeks.
However, there are outliers that have weekly downloads peak up to around 200.000 downloads.

While these GitHub and npm metrics give us _some_ insight into the usage of Components.js,
they are incomplete, as projects may be hosted on other source code platforms such as GitLab, Bitbucket, or even private instances.
Furthermore, direct downloads from npm are also incomplete, as downstream users may use bundling tools such as [Webpack](https://webpack.js.org/)
to incorporate the Components.js source code directly within their library, which makes downloads of that library not go via the the Components.js npm package anymore.
Therefore, we conclude that the metrics reported here are merely a lower limit,
and the actual usage is expected to be higher.

### In-use Analysis

In the previous section, we provided an informed estimate as to _how much_ Components.js is being used.
In this section, we provide an analysis of _in what way_ Components.js is being used in four real-world projects:
Solid Community Server, Handlers.js, Digita Identity Proxy, and Comunica.

#### Solid Community Server

The Solid Community Server ([https://github.com/solid/community-server/](https://github.com/solid/community-server/))
is a server-side implementation of the [Solid specifications](cite:cites solidspec),
which provides a basis for the Solid decentralization effort.
When such a server is hosted, it allows users to create their own personal storage space (pod) and identity,
so that this data can be used within any external Solid application.
This server is written in TypeScript, and is being developed by [Inrupt](https://inrupt.com/) and [imec](https://www.imec-int.com/en),
which includes authors of this article.

This server makes use of dependency injection because a primary goal of the server is to be as flexible as possible,
so that developers can easily modify the capabilities of the server, or even add additional capabilities.
This is especially useful in the context of research, where new components can be added to the server for experimentation,
before they are standardized and become a part of the Solid specifications.
To enable this level of flexibility, all components within this server are loosely coupled,
and are wired via customizable Components.js configuration files.

Since the Solid Community Server makes use of TypeScript, it is able to make use of the Components-Generator.js tool as explained before in [](#configs),
which avoids the need to manually create components files, and thereby significantly simplifies the usage of Components.js within this project.
At the time of writing, this server contains 246 components that can be customized via specific parameters, and wired together to form a server instance with specific capabilities.

#### Handlers.js

[Handlers.js](https://github.com/digita-ai/handlersjs){:.mandatory} aims to provide a comprehensive collection of generic logic classes,
that can be wired together via the composition pattern.
While this project is still under development, it already provides numerous handlers and services pertaining to
data flows, storage, logging, error handling, as well as logic about serving data over HTTP (routing, CORS, content negotiation ...).
This project is written in TypeScript, and is being developed by [Digita](https://www.digita.ai/).

In contrast to the Solid Community Server, Handlers.js is not meant to be usable by itself as standalone tool.
Instead, it is an accompanying library that can be used by other tools.
The components within Handlers.js are meant to capture common patterns within projects that depend on composition-based components,
so that they can be reused by other projects that make use of DI frameworks such as Components.js.
While Components.js is the primary DI framework this library was designed for,
it does not strictly depend on it thanks to the loosely coupling of the Components.js DI layer and software implementations.

Handlers.js also make use of the Components-Generator.js tool to convert TypeScript classes into components files.
At the time of writing, this project exposes 40 components that range from abstract logic flows to specific ones for setting up a simple HTTP server.
Since components within Components.js have global semantics, these components can be easily reused across projects.

#### Digita Identity Proxy

The Digita Identity Proxy (not public at the time of writing) is a [Solid-OIDC](https://solid.github.io/authentication-panel/solid-oidc/){:.mandatory}-compliant proxy server
that acts as a modular, and easily configurable compatibility layer for classic [OIDC](https://openid.net/connect/){:.mandatory} Identity Providers.
It enables Solid apps to authenticate at Solid pod servers with these existing identity services, without any necessary modification.
This project is also written in TypeScript, and is under development by [Digita](https://www.digita.ai/).

Several components exists that enable additional functionality of Solid-OIDC,
which can be plugged into the proxy when the need exists.
With Components.js, these components can be easily configured and plugged in via a configuration file.

#### Comunica

[Comunica](cite:cites comunica) is another project that makes use of Components.js at its core.
Comunica is a highly modular SPARQL query engine
that has been designed to be a flexible research platform for SPARQL query execution.
It has been written in TypeScript, and is developed by Ghent University, by authors of this article.

The modular nature of Comunica calls for a dependency injection framework due to its [actor-mediator-bus paradigm](https://comunica.dev/docs/modify/advanced/architecture_core/).
All logic within Comunica is placed within small actors,
which are registered on task-specific buses following the publish-subscribe pattern.
In order to select a certain actor on a bus for achieving a certain task,
the mediator pattern is applied, which allows different actors to be selected based on different actions.
These actors, buses, and mediators are loosely coupled with each other,
and are wired together via Components.js configuration files.
For example, this allows users of Comunica to create and plug in a different algorithm for resolving a certain SPARQL query operator.

At the time of writing, Comunica does not yet make use of the Components-Generator.js tool,
as it was developed before Components-Generator.js was created.
Therefore, all components files within Comunica are created manually,
which shows that Components.js is flexible in this regard.

As Comunica is a research platform for research around query execution,
the ability to _reproduce_ experiments is crucial.
This is where the benefit of Components.js becomes especially apparent.
It is often the case that research articles with experimental results only report on the used software,
without mentioning the exact version and configuration that was used.
When using a Components.js configuration file,
the necessary semantics for accurately replicating such experiments are available as Linked Data.
The reproducibility of [experimental results is often considered to be even more important than the research article itself](cite:cites WaveLab),
as the article can be considered to be merely _advertising of the scholarship_.
