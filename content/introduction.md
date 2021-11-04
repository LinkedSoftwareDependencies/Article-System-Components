## Introduction
{:#introduction}

Object-oriented (OO) programming is a highly popular paradigm within the domain of software engineering.
Considering _objects_ containing data and logic as primary software elements
makes it easy for developers to understand software,
as it makes software resemble real-world mechanisms with interacting physical objects.
Most OO languages allow objects to be instantiated from _classes_ that determine the object's type,
where _inheritance_ can be used to let classes extend from other classes,
and thereby inheriting their fields, methods, and type(s).
Unfortunately, [inheritance is often overused in places where _composition_ would be better suited](cite:cites designpatterns),
where composition of objects (containment within each other) leads to more flexibility in terms of object relationships,
and thereby leads to more loosely coupled objects.

A popular technique to manage the composition of objects is called [_Dependency Injection_ (DI)](cite:cites DependencyInjection).
It assumes that objects are loosely coupled,
and that they only depend on each other via a minimal and generic interface,
without depending on concrete implementations of such interfaces.
In order to link these interfaces to concrete implementations,
a generic DI framework can provide specific implementations where needed based on some external configuration.
Since objects only communicate by strict interfaces,
and specific implementations are derived from an external configuration,
the specific wiring of a software application is not hard-coded anymore.
Instead, this wiring can be altered afterwards by modifying the configuration file,
which makes the application more flexible.

Configurations for existing DI frameworks
are either defined directly within a programming language,
or are defined declaratively within text files with a domain-specific language using syntaxes such as JSON and XML.
The latter type of configuration files is better suited for use cases where no changes can be made to existing code –e.g., in the case of pre-compiled languages–,
when the creators of these configuration files have no programming knowledge,
or when configuration files are created automatically from an external tool –e.g., a visual drag-and-drop interface–.
Such declarative configuration files typically have only local semantics,
which means that they are usually only usable within the DI framework for which they were created, and for the current application only.
With the power of [Linked Data](cite:cites linkeddata) and the [Semantic Web](cite:cites semanticweb) in mind,
these configurations could move _beyond_ their local scope,
and make them globally _interoperable_, _addressable_, and _discoverable_.

To this end, we present _Components.js_,
a semantic DI framework for TypeScript and JavaScript applications
that gives global semantics to software configurations, hence surpassing existing dependency injection frameworks.
Components.js thereby enables highly modular applications to be built that are dynamically wired based on semantic configuration files.
The framework is [open-source](cite:cites link:github:componentsjs),
is available on [npm](cite:cites link:npm:componentsjs),
and has extensive [documentation](cite:cites link:docs:componentsjs).
Furthermore, it is being actively used as core technology within popular tools such as
the [Solid Community Server](cite:cites link:github:css) and [Comunica](cite:cites comunica).
Within Components.js,
software configurations and modules are described as Linked Data using
the [_Object-Oriented Components vocabulary_](cite:citesAsAuthority van2017describing)
and the [_Object Mapping vocabulary_](cite:cites link:web:om).
By publishing such descriptions,
the composition of software (and parts thereof) can be _unambiguously identified_ by IRIs and 
retrieved through _dereferencing_.
Components.js automatically _instantiates_ such software configurations, including resolving the necessary dependencies.
As such, this (de)referenceability of software configurations by IRI could be beneficial in use cases such as:

Experimental research
: Providing the full provenance trail of used software configurations to produce experimental results for improving reproducibility.

Static program analysis
: Discovering conflicts or compatibility issues of different classes within software using RDF tools such as SPARQL query engines and reasoners.

Semantic workflows
: Automatic wiring of software using RDF tools to optimally address a specific need.

We consider this article an extension of our previous work involving [describing software as Linked Data](cite:citesAsAuthority van2017describing).
Concretely, the contributions of this work are:

* the Components.js dependency injection framework and its architecture;
* the Components-Generator.js tool for generating component descriptions for TypeScript projects;
* the Object-Oriented Components and Object Mapping vocabularies; and
* the Linked Software Dependencies (LSD) service that makes npm packages dereferenceable.

While Components.js can aid in the reproduction of experiments as one possible use case,
we consider full reproducibility of experiments out of scope for this work.
Instead, to enable full replication of experiments,
we refer to tools such as [NixOS](cite:cites link:web:nix) that can describe full experimental environments,
where Components.js can offer more granular software configuration descriptions.

In this article, we introduce the Components.js framework as follows.
In the next section ([](#related-work)), we discuss the related work.
Next, in [](#configs) we explain the declarative configuration files of Components.js,
followed by an architectural overview of the framework itself in [](#system).
Then, in [](#usage), we mention some applications where Components.js is being used.
Finally, we conclude in [](#conclusions).
