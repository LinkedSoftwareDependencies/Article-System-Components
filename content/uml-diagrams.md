## Architectural Diagrams
{:#uml-diagrams}

This appendix section contains the architectural diagrams that were discussed in [](#system-architecture).
[](#architecture-main) contains the main entrypoint of the framework,
[](#architecture-load) represents the loading phase,
[](#architecture-preprocess) represents the preprocessing phase,
and [](#architecture-construct) represents the construction phase.

<figure id="architecture-main">
<img src="img/architecture-main.svg" alt="[Components.js Architecture - Main package]">
<figcaption markdown="block">
UML diagram of the classes within the main package,
which contains the main entrypoint of the framework.
</figcaption>
</figure>

<figure id="architecture-load">
<img src="img/architecture-load.svg" alt="[Components.js Architecture - Load package]">
<figcaption markdown="block">
UML diagram of the classes within the load package,
which are responsible for loading components and configurations.
</figcaption>
</figure>

<figure id="architecture-preprocess">
<img src="img/architecture-preprocess.svg" alt="[Components.js Architecture - Preprocess package]">
<figcaption markdown="block">
UML diagram of the classes within the preprocess package,
which are responsible for preprocessing config parameters and constructor arguments.
</figcaption>
</figure>

<figure id="architecture-construct">
<img src="img/architecture-construct.svg" alt="[Components.js Architecture - Construct package]">
<figcaption markdown="block">
UML diagram of the classes within the construct package,
which are responsible for instantiating configs according to a certain strategy.
</figcaption>
</figure>
