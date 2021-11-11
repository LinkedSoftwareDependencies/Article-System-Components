## Introduction
{:#introduction}

Object-oriented (OO) programming is a highly popular paradigm within the domain of software engineering.
Considering _objects_ containing data and logic as primary software elements
makes it easy for developers to understand software,
as it makes software resemble real-world mechanisms with interacting physical objects.
<span class="comment" data-author="RV">Is it necessary here too make the inheritance versus composition argument? It might make it seem as if we are suggesting developers to write in a different way, whereas that is not really the case. Even code with inheritance will still have objects that require dependencies. I'd propose to just explain composition.</span>
Most OO languages allow objects to be instantiated from _classes_ that determine the object's type,
where _inheritance_ can be used to let classes extend from other classes,
and thereby inheriting their fields, methods, and type(s).
Unfortunately, [inheritance is often overused in places where _composition_ would be better suited](cite:cites designpatterns),
because composition of objects (containment within each other) leads to more flexibility in terms of object relationships,
and thereby leads to more loosely coupled objects.

<span class="comment" data-author="RV">Interestingly, I'm actually missing here what DI really is. DI, as I understand it, is the idea that an object _asks_ for components it will use, rather than _getting_ or _creating_ them itself. This, IMHO, is the more important point over inheritance versus composition, namely that the composition happens not by the component itself but by another instantiating it.</span>
<span class="comment" data-author="RV">Here is a Wikipedia copy/paste: <q>In software engineering, dependency injection is a technique in which an object receives other objects that it depends on, called dependencies. Typically, the receiving object is called a client and the passed-in ('injected') object is called a service. The code that passes the service to the client is called the injector. Instead of the client specifying which service it will use, the injector tells the client what service to use. The 'injection' refers to the passing of a dependency (a service) into the client that uses it.</q></span>
A popular technique to manage the composition of objects is called [_Dependency Injection_ (DI)](cite:cites DependencyInjection).
It assumes that objects are loosely coupled,
and that they only depend on each other via a minimal and generic interface,
without depending on concrete implementations of such interfaces.
<span class="comment" data-author="RV">So nearly the same, but not quite; it eliminates objects instantiating their own dependencies, but not objects that actively (know how to) retrieve their dependencies from somewhere else. [Breaking the Law of Demeter is Like Looking for a Needle in the Haystack](http://misko.hevery.com/2008/07/18/breaking-the-law-of-demeter-is-like-looking-for-a-needle-in-the-haystack/)</span>
In order to link these interfaces to concrete implementations,
a generic DI framework can provide specific implementations where needed based on some external configuration.
Since objects only communicate by strict interfaces,
and specific implementations are derived from an external configuration,
the specific wiring of a software application is not hard-coded anymore.
Instead, this wiring can be altered afterwards by modifying the configuration file,
which makes the application more flexible.

Configurations for existing DI frameworks
are either defined directly within a programming language,
<span class="comment" data-author="RV">contradicts the <q>hard-coded</q> above; I understand, but could be confusing</span>
or are defined declaratively within text files with a domain-specific language using syntaxes such as JSON and XML.
The latter type of configuration files is better suited for use cases where no changes can be made to existing code
(e.g., in the case of pre-compiled languages),
when the creators of these configuration files have no programming knowledge,
or when configuration files are created automatically from an external tool
(e.g., a visual drag-and-drop interface).
Such declarative configuration files typically have only <em>local</em> semantics,
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
