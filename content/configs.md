## Declarative Configurations
{:#configs}

Components.js depends on two levels of configuration for enabling the wiring of software components.
The first level is the creation of *components* files,
which are the semantic representation of component (or class) constructors,
and can usually be automatically generated.
The second level is the creation of *configuration* files,
which represent the actual instantiation of components
based on the generated components files.

In this section, we discuss the two main vocabularies that are used within these component files,
and show how configuration files can refer to them for instantiation.
Next, we explain how URLs can be minted for software components, so that they become fully dereferenceable.
Finally, we explain how these component files can be generated automatically from existing TypeScript code.

### Object-Oriented Components Vocabulary

Components.js distinguishes between three main concepts:

Module
: a software package containing zero or more components. For example, this is equivalent to a module within Node.js.

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
The parameters to construct the component can therefore be defined as a property having that component as its domain.

Note that the vocabulary does not contain an _interface_ class,
because this notion does not exist in JavaScript,
and it can exist in TypeScript code but, only before transpilation to JavaScript.
Instead, we only define `oo:AbstractClass`,
as both abstract classes and interfaces can be considered equivalent at the level of dependency injection.

We illustrate the usage of this vocabulary with an example in [](#module-oo) using the [JSON-LD](cite:cites jsonld) serialization.
This listing shows the definition of a new module (`oo:Module`) with compact IRI `ex:MyModule`.
The name of the module is set with the compact IRI `requireName`, which expands to `doap:name` from the [Description of a Project (DOAP) vocabulary](cite:cites link:web:doap).
Furthermore, our module contains a single class component (`oo:Class`) with compact IRI `ex:MyModule/MyComponent`.
Since this is a class component (subclass of `oo:Component`), this means that this component is instantiatable based on parameters.
Each component can refer to its path within a module using the `oo:componentPath` predicate (compacted as `requireElement`).
Finally, our single component has a parameter (`oo:Parameter`) with compact IRI `ex:MyModule/MyComponent#name`
that can be set when instantiating this component.

<figure id="module-oo" class="listing">
````/code/module-oo.txt````
<figcaption markdown="block">
A description of a module `ex:MyModule` with a single component using the JSON-LD serialization,
compacted with the `https://linkedsoftwaredependencies.org/bundles/npm/componentsjs/^4.0.0/components/context.jsonld` context.
</figcaption>
</figure>

Since components and parameters are defined as RDFS vocabulary,
we can instantiate components easily using the `rdf:type` predicate,
and by using parameters as predicates on such new instances, as shown in [](#instance-oo).
Instead of passing literals as values to parameters, it is also possible to pass _other component instances_ as values,
thereby allowing nested component instantiations to be defined.

<figure id="instance-oo" class="listing">
````/code/instance-oo.txt````
<figcaption markdown="block">
Instantiation of `ex:MyModule/MyComponent` using a value for the parameter `ex:MyModule/MyComponent#name`.
</figcaption>
</figure>

<div class="printonly" style="height: 50px;">&nbsp;</div>

### Object Mapping Vocabulary

As shown in the previous section, the OO vocabulary allows modules, components, and parameters to be defined,
so that instances of components can be declared.
However, this vocabulary only defines parameter values for component instances,
but it does not define how these parameter values are used to invoke the constructor of this component.
To enable this, we introduce the accompanying [_Object Mapping vocabulary (OM)_](cite:cites link:web:om).
[](#voc-om-diagram) shows an overview of all its classes and predicates.

<figure id="voc-om-diagram">
<img src="img/voc-om-diagram.svg" alt="[Object Mapping vocabulary diagram]">
<figcaption markdown="block">
Classes and properties in the [_Object Mapping_ vocabulary](cite:cites link:web:om), with as prefix `om`.
</figcaption>
</figure>

The OM vocabulary makes use of the `oo:constructorArguments` predicate for the domain `oo:Class`,
and thereby builds upon the OO vocabulary via the `oo:constructorArguments` extension point to define the class constructor's behaviour.
Concretely, this new vocabulary defines a mapping between the component parameters as defined using the OO vocabulary,
and the raw objects that are passed into the constructor during instantiation.

In essence, this vocabulary enables an (RDF) list of `om:ObjectMapping`'s to be passed to the `oo:constructorArguments` of an `oo:Class`.
An `om:ObjectMapping` represents an object containing zero or more key-value pairs, which are represented by `om:ObjectMappingEntry`.
`om:ArrayMapping` is a special type of `om:ObjectMapping` that represents an array, where its elements can be other `om:ObjectMapping`'s.

Building upon the OO example from [](#module-oo), we illustrate the usage of this vocabulary with an example in [](#module-om), again using the JSON-LD serialization.
The only difference with the previous example, is the addition of the `constructorArguments` block,
which expands to `oo:constructorArguments` that is configured to always contain an RDF list.
The constructor arguments contain a single `om:ObjectMapping`, which is implied by the presence of `field`, which expands to `om:field`.
Since the field array contains just a single element (`om:ObjectMappingEntry`),
it represents an object with a single key and value.
The key is defined by `keyRaw` (expands to `om:fieldName`), which contains the constant `name`.
The value is defined by `value` (expands to `om:fieldValue`), which refers to the `ex:MyModule/MyComponent#name` parameter.

<figure id="module-om" class="listing">
````/code/module-om.txt````
<figcaption markdown="block">
A description of a module `ex:MyModule` with a single component having constructor arguments using the JSON-LD serialization,
compacted with the `https://linkedsoftwaredependencies.org/bundles/npm/componentsjs/^4.0.0/components/context.jsonld` context.
</figcaption>
</figure>

The addition of an object mapping to a component requires no changes as to how a component is instantiated,
which means that our component from [](#module-om) can still be instantiated in the exact same way as the one from [](#module-oo).
The only difference now, is that we are able to determine how exactly the parameter values are to be used for invoking the component constructor.
For example, the instantiation of [](#instance-oo) corresponds to the following code in JavaScript: `new MyComponent({ name: 'Some name' })`

A real-world example of the combined usage of the OO and OM vocabularies can be found at [https://linkedsoftwaredependencies.org/bundles/npm/%40comunica%2Fcore/1.21.1/components/Actor.jsonld](https://linkedsoftwaredependencies.org/bundles/npm/%40comunica%2Fcore/1.21.1/components/Actor.jsonld).

### Dereferenceability

In [previous work](cite:citesAsAuthority van2017describing)
we introduced the [Linked Software Dependencies (LSD) service](cite:cites link:web:lsd),
which makes all resource URLs within components files fully dereferenceable.

Since our current focus is on enabling dependency injection for JavaScript,
this LSD service provides Linked Data subject pages for _all_ packages within the [npm package manager](cite:cites link:web:npm) for JavaScript.
For example, the URL [`https://linkedsoftwaredependencies.org/bundles/npm/@comunica/core/1.21.1`](https://linkedsoftwaredependencies.org/bundles/npm/@comunica/core/1.21.1)
is an identifier for the `@comunica/core` package at version `1.21.1`.
[](#lsd-snippet) shows a snippet of the JSON-LD contents when dereferencing this URL.

<figure id="lsd-snippet" class="listing">
````/code/lsd-snippet.txt````
<figcaption markdown="block">
Part of the JSON-LD contents of [`https://linkedsoftwaredependencies.org/bundles/npm/@comunica/core/1.21.1`](https://linkedsoftwaredependencies.org/bundles/npm/@comunica/core/1.21.1).
</figcaption>
</figure>

This LSD service allows creators of components files to automatically mint LSD-based URLs for their packages,
which will automatically become dereferenceable as soon as these packages are published to npm.
The LSD service thereby removes the dereferenceability responsibility from package developers that want to use dependency injection via Components.js,
but do not have the will or ability to make their component files dereferenceable themselves.
The LSD service is not required for the functioning of the Components.js framework,
so developers are not obligated to publish their package to npm or mint their own URLs if they do not have this desire.
But since publishing packages to npm in a common practise within the JavaScript community, we consider this a low barrier to entry.

This dereferenceability is beneficial for enabling querying execution within and across component files.
For example, it enables using the follow-your-nose principle to analyze class inheritance chains of certain modules.
Another example in the domain of reproducibility is the ability to analyze which config parameters had the largest influence on the performance of a system,
assuming that the experimental results have also been linked to the semantic configuration.

The long-term sustainability of the LSD service and its minted URLs is guaranteed by Ghent University,
[which places a strong emphasis](https://www.ugent.be/en/research/datamanagement) on ensuring that data is preserved in the long term.
In the unlikely event that the LSD service would experience downtime,
all applications that make use of Components.js will still remain functional,
because the Components.js framework does not rely directly on the dereferenceability of these URLs.

### Generation from TypeScript

For larger projects, the manual creation of components files for all classes in the project can require significant manual effort, and can therefore become error-prone.
For projects that make use of a strongly-typed language, such as TypeScript,
all required information to create such components files is in fact already available implicitly via the source code files.
In order to minimize manual effort for such projects, we provide the open-source tool [_Components-Generator.js_](cite:cites link:docs:componentsjsgenerator)
([Zenodo](cite:cites link:zenodo:componentsjsgenerator)) for TypeScript projects.

Concretely, this tool can be installed into any TypeScript project.
When its command-line script is invoked, it scans all exported TypeScript classes within this project,
and generates corresponding components files for them.
In doing so, it preserves information that is important for dependency injection,
such as component extensions via class inheritance relationships and
parameter types with constructor arguments mapping via class constructors.

For example, assuming an npm package named `my-package` containing the single TypeScript class from [](#generator-ts),
Components-Generator.js will generate the components file in [](#generator-out).

<figure id="generator-ts" class="listing">
````/code/generator-ts.txt````
<figcaption markdown="block">
TypeScript class that is used as input to Components-Generator.js.
</figcaption>
</figure>

<figure id="generator-out" class="listing">
````/code/generator-out.txt````
<figcaption markdown="block">
Components file that is generated by Components-Generator.js from the TypeScript file from [](#generator-ts).
</figcaption>
</figure>

A real-world example of such conversion can be seen in the [Community Solid Server](cite:cites link:github:css) project.
For example, the `CorsHandler` TypeScript class <br /> ([https://github.com/solid/community-server/blob/9b6eab27bc4e5ee25d1d3c6ce5972e83db90c650/src/server/middleware/CorsHandler.ts#L31](https://github.com/solid/community-server/blob/9b6eab27bc4e5ee25d1d3c6ce5972e83db90c650/src/server/middleware/CorsHandler.ts#L31)) is converted to the components file at <br /> [https://linkedsoftwaredependencies.org/bundles/npm/%40solid%2Fcommunity-server/2.0.0/dist/server/middleware/CorsHandler.jsonld](https://linkedsoftwaredependencies.org/bundles/npm/%40solid%2Fcommunity-server/2.0.0/dist/server/middleware/CorsHandler.jsonld).
