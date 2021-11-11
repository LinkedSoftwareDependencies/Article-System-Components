## Abstract
<!-- Context      -->
A common practice within object-oriented software
is using _composition_ to realize complex object behavior
in a reusable way.
Such compositions can be managed by _Dependency Injection (DI)_,
a popular technique in which components only depend on minimal interfaces
and have their concrete dependencies passed into them.
Instead of requiring program code,
this separation enables describing the desired instantiations
in declarative configuration files,
such that objects can be wired together automatically at runtime.
Configurations for existing DI frameworks typically only have local semantics,
which limits their usage in other contexts.
<!-- Need         -->
Yet some cases require configurations outside of their local scope,
such as for the reproducibility of experiments, static program analysis, and semantic workflows.
As such, there is a need for globally interoperable, addressable, and discoverable configurations,
which can be achieved by leveraging Linked Data.
<!-- Task         -->
We created _Components.js_ as
an open-source semantic DI framework for TypeScript and JavaScript applications,
providing global semantics via Linked Data-based configuration files.
<!-- Object       -->
In this article, we report on the Components.js framework
by explaining its architecture and configuration,
and discuss its impact by mentioning where and how applications use it.
<!-- Findings     -->
We show that Components.js is a stable framework that has seen significant uptake during the last couple of years.
<!-- Conclusion   -->
We recommend it for software projects that require
high flexibility,
configuration without code changes,
sharing configurations with others,
or applying these configurations in other contexts such as experimentation or static program analysis.
<!-- Perspectives -->
We anticipate that Components.js will continue driving concrete research and development projects
that require high degrees of customization to facilitate experimentation and testing,
including the Comunica query engine and the Community Solid Server for decentralized data publication.
