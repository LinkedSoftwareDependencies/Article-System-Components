## Declarative Configurations
{:#configs}

Components.js depends on two levels of configuration for enabling the wiring of software components.
The first level is the creation of *components* files,
which are the semantic representation of component constructors,
and can usually be automatically generated.
The second level is the creation of *configuration* files,
which represent the actual instantiation of components
based on the generated components files.
Hereafter, we explain these two levels in more detail.

### Components files

Component files are used to semantically represent the constructors of software components.
For this, we make use of two vocabularies, which will be explained hereafter.
Next, we explain how URLs can be minted for software components, so that they become fully dereferenceable.
Finally, we explain how these component files can be generated automatically from existing TypeScript code.

#### Object-Oriented Components Vocabulary

Components.js distinguishes between three main concepts:

Module
: a software package containing zero or more components. This is equivalent to a Node module or npm package.

Component
: a class that can be instantiated by creating a new instance of that type with zero or more parameter values. Parameters are defined by the class constructor.

Configuration
: a semantic representation of an instantiation of a component into an object instance based on parameters.

These concepts are described in the programming language independent [_Object-Oriented Components vocabulary (OO)_](https://linkedsoftwaredependencies.org/vocabularies/object-oriented) [](cite:citesAsAuthority van2017describing).
This vocabulary enables software components to be instantiated based on certain parameters,
analog to constructor arguments in object-oriented programming.
This is interpreted in the broad sense: only _classes_, _objects_ and _constructor parameters_ are considered.
An overview is given in [](#voc-oo-diagram).

<figure id="voc-oo-diagram">
<img src="img/voc-oo-diagram.svg" alt="[description diagram]">
<figcaption markdown="block">
Classes and properties in the [_Object-Oriented Components vocabulary (OO)_](https://linkedsoftwaredependencies.org/vocabularies/object-oriented), with as prefix `oo`.
</figcaption>
</figure>

A module is considered a collection of components.
Within object-oriented languages, this can correspond to for example a software library or an application.
A component is typed as `oo:Component`, which is a _subclass_ of `rdfs:Class`.
The parameters to construct the component can therefore be defined as an `rdfs:Property` on a component.

<figure id="module-oo" class="listing">
````/code/module-oo.txt````
<figcaption markdown="block">
A description of a module `ex:MyModule` with a single component using the [JSON-LD](cite:cites jsonld) serialization,
compacted with the `https://linkedsoftwaredependencies.org/bundles/npm/componentsjs/^4.0.0/components/context.jsonld` context.
</figcaption>
</figure>

We illustrate the usage of this vocabulary with an example in [](#module-oo) using the [JSON-LD](cite:cites jsonld) serialization.
This listing shows the definition of a new module (`oo:Module`) with compact IRI `ex:MyModule`.
The name of the module is set with the compact IRI `requireName`, which expands to `doap:name` from the [Description of a Project (DOAP) vocabulary](https://github.com/ewilderj/doap/wiki).
Furthermore, our module contains a single class component (`oo:Class`) with compact IRI `ex:MyModule/MyComponent`.
Since this is a class component (subclass of `oo:Component`), this means that this components is instantiatable based on parameters.
Each component can refer to its path within a module using the `oo:componentPath` predicate (compacted as `requireElement`).
Finally, our single component has a parameter (`oo:Parameter`) with compact IRI `ex:MyModule/MyComponent#name`
that can be set when instantiating this component.

#### Object Mapping Vocabulary

Write me
{:.todo}

#### Dereferenceability

Write me: via LSD
{:.todo}

#### Generation from TypeScript

Write me
{:.todo}

### Configuration files

Write me
{:.todo}
