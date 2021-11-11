## Related Work
{:#related-work}

### Dependency Injection
{:#related-work-di}

**Inversion of Control**

[Inversion of Control (IoC)](cite:cites DependencyInjection) is a general principle within software engineering
that inverts the usual flow of control within software architectures.
This is mostly done to reduce coupling between software components, and make the overall architecture more modular and extensible.
On the one hand, traditional procedural programming gives the developer direct control of the flow of logic, where code directly invokes other code.
IoC on the other hand implies the use of a framework that manages this flow,
and allows custom code –that is supplied by the developer–
to be invoked when the frameworks deems it necessary.
This concept is typically referred to as _"The Hollywood Principle: Don't call us, we'll call you"_.

A specific technique to achieve IoC is [_Dependency Injection_ (DI)](cite:cites DependencyInjection),
where the framework calls constructors and methods with the right parameters.
<span class="comment" data-author="RV">So I disagree with the next sentence</span>
As mentioned before, DI is based on the _composition_ of objects to enable relationships between them (as opposed to _inheritance_).
These composed objects are tied to each other only by a lightweight interface,
where different implementations may be possible for each interface.
Using a DI framework, specific implementations for such interfaces can be configured,
after which they can be instantiated into objects,
and are injected into each other using the DI framework's _assembler_ to complete the wiring of the software application.

The configuration of such a wiring of objects
can either be done in code, or via external configuration files.
The main motivations for configurations are the strict boundaries between configuration and logic,
enabling non-developers to configure the code,
and taking away the need to recompile the code for pre-compiled languages.
However, when dependencies are defined based on some logic such as external conditions,
configuration via code may be better suited,
as this can become too complex to define in declarative configuration files.

**Forms of Injection**

In practice, three main forms of DI exist through which dependencies can be injected into an object:

Constructor injection
: Dependency objects are passed via a class constructor.

Setter injection
: Dependencies are passed to an object by invoking setter methods.

Interface injection
: The interface of dependencies expose a method that, when invoked, injects this dependency into an object that is passed to it. Such passed objects will typically be a setter method for this.

Constructor injection is the simplest and most popular form.
It requires all dependencies to be wired at construction time,
which usually leads to immutable wiring.
Setter injection is more flexible as wiring can be changed afterwards,
but could lead to problems where not all dependencies have been fully configured yet.
Interface injection is more complex, and is mainly useful if bidirectional links between dependencies and dependents need to be configured.

**Advantages and Disadvantages**

To end this section, we summarize the main [advantages](https://betterprogramming.pub/the-6-benefits-of-dependency-injection-7802b207ec69)
and [disadvantages](https://www.professionalqa.com/dependency-injection) of DI.

Advantages:

* Classes are loosely coupled, which leads to **lower maintenance** effort.
* Loose coupling also leads to better **testability**, as dependencies with lightweight interfaces can easily be mocked.
* Classes have a single responsibility, which leads to **better understandable** code.
* Applications are more **flexible**, as they can be wired differently by changing a configuration file.
* Applications are more **extensible**, as different interface implementations can be created, and swapped in or out easily.
* Since classes are coded against interfaces of dependencies, they lead to more **independent** code, which is beneficial in large teams that work in parallel.

Disadvantages:

* Defining the wiring of an application via **configurations can be complex**, so good defaults must be available.
* Logic **flow is harder to follow** when debugging, which leads to the need of good documentation.
* DI frameworks can lead to **overhead** in terms of understandability, execution time and software size.

### Semantic Software Description
{:#related-work-software-description}

Configuration-based DI frameworks make use of some form of software description.
Therefore, we introduce the related work around semantic software descriptions.

Software can be described on several levels of granularity,
going from a high-level package overview to a low-level description of the actual code.
The [Software Ontology (SWO)](cite:cites malone2014software) and [Description of a Project (DOAP)](cite:cites doap) ontology focus on the high-level management of software development,
enabling the description of tools, resources, contributors and tasks. 
At a slightly lower level, SWO includes interfaces, algorithms, versions, and the associated provenance data, but does not reach the level of detail to describe operational code.

Ontologies that describe software configuration from a research workflow perspective are [LODFlow](cite:cites Rautenberg:2015:LWM:2814864.2814882), [Workflow-Centric Research Objects](cite:cites Belhajjame2015) with the <cite><a href="https://w3id.org/ro/">Wf4Ever Research Object Model</a></cite> and the [Ontologies for Describing the Context of Scientific Experiment Processes](cite:cites Mayer2014) with the <cite><a href="http://www.timbusproject.net/portal/publications/ontologies/">TIMBUS Context Model</a></cite> to compliment the Research Objects model. 
From a more generic perspective, there exist the [PROV Ontology](cito:citesAsAuthority PROVO), the [OPMW-PROV Ontology](cito:citesAsAuthority OPMWPROV), and the [DDI-RDF Discovery Vocabulary](cito:citesAsAuthority DDIRDF).
However, these efforts can only cover (parts of) the connection between research and software, which is insufficient for dependency injection.
Such descriptions are moreover interpretive in that any given tool is subject to having multiple descriptions by different users.
In contrast to the human-driven descriptions, our work both enables and accelerates the generation of machine-driven Linked Data descriptions of software modules, their components, as well as their configurations to be uniformly created.
Consequently, this makes it possible to accurately describe and instantiate software experiments that can be reused and compared with unambiguously.

Much more low-level and exact is the [Core Software Ontology (CSO)](cite:cites oberle2009ontology),
which provides a foundational vocabulary that is designed for extensibility.
This includes the distinctive concepts to describe software as code, software as object to computational hardware, and software as a running computational activity,
but also Interfaces, Classes, Methods, the relationships between them, and workflow information on their invocation.
Its extension, the Core Ontology of Software Components (COSC), moves closer to the topic of this article by describing interfaces and protocols of objects.
Similar in scope is the [Software Engineering Ontology Network (SEON)](cite:cites ruy2016seon), which consolidates multiple ontologies for the Software Engineering field.
It includes a higher Core and Foundational layer, as well as multiple domain-specific ontologies.
Of particular interest is their Software Ontology (SwO) that captures the different artifacts in software.
More recently, the [GraphGen4Code toolkit](cite:cites GraphGen4Code) has been introduced,
which provides an ontology to capture code semantics to represent classes, functions and methods.
In general, these ontologies (or suites) view software from a <q>network of communicating concepts</q> perspective.
This allows for exhaustive descriptions of complex software systems, but is not suited for describing class instances or aspects of modular programming (e.g., package dependencies).
As such, the vocabularies that we introduced do not make use of these existing ontologies,
but they do make use of parts of them where possible.

### Dependency Injection Frameworks
{:#related-work-di-frameworks}

The large spectrum of existing dependency injection frameworks indicates a high demand for such systems.
Java likely contains the largest collection of dependency injection frameworks.
Much of this stems from the strict typing,
which makes it difficult to create mock objects when required for testing
if the dependencies are nested in the implementation.

One of the biggest Java frameworks is [Spring](cite:cites link:web:spring),
which amongst many things, also provides dependency injection.
That is one of its advantages though:
many projects already use Spring for other reasons,
reducing the jump required to add the dependency injection framework.
It supports two ways to do the injection.
The first one is through an external XML configuration file
which defines all the classes and how they are linked together.
The other one is with annotations in the actual code
that define how the interlinking of classes should work.
Google's [Guice](cite:cites link:web:guice) is a more lightweight alternative to Spring;
[Dagger](cite:cites link:web:dagger) was created to be even more lightweight than Guice.

In JavaScript, 
dependency injection frameworks tend to be less common because of its flexible nature.
However, with the increasing popularity of TypeScript –which provides strict typings for JavaScript–,
the need for dependency injection is increasing.
Still, multiple frameworks are available, such as [BottleJS](cite:cites link:web:bottlejs), [Wire](cite:cites link:web:wire), and [Electrolyte](cite:cites link:web:electrolyte), all backed by rather small communities.
One of the biggest ones, [InversifyJS](cite:cites link:web:inversifyjs),
uses annotations similar to Java frameworks to define possible injections.
Unlike standard JavaScript,
it requires the developer to define interfaces and types via TypeScript,
thereby allowing it to make use of this extra information to correctly handle the linking.
Like Guice, it also has a bindings file to link classes to interfaces.

Components.js differs from the aforementioned frameworks on different aspects.
First, Components.js decouples the dependency injection layer from the software implementation via **separate configuration files**,
while the other JavaScript DI frameworks use code-based configuration and thereby have a stronger coupling of these layers.
Is is thereby more similar to the Java-based DI frameworks that tend to rely more on external configuration files.
This is the primary reason why we opted to create a new framework, instead of extending an existing one.
Second, Components.js is the only framework that makes use of **RDF-based configuration files**,
which makes these configurations globally _interoperable_, _addressable_, and _discoverable_.
Third, regarding the form of dependency injection, Components.js makes use of **constructor injection**,
just like all other discussed frameworks.
Only the Spring also provides the option to make use of the other forms of injection,
but constructor injection is the most popular option.

### JavaScript Runtime Environments
{:#related-work-js-runtime-environments}

The most popular runtime environment for JavaScript is [Node.js](cite:cites link:web:node),
which allows JavaScript code to be executed outside of a Web browser.
Node.js is based on the highly performant [V8 engine](cite:cites link:web:v8) that is also used within the Chrome browser. 
Even though Node.js can not directly execute TypeScript code,
TypeScript code can be transpiled to JavaScript so that it can be executed in Node.js.
Node.js makes use of the [npm](cite:cites link:web:npm) package manager for distributing and installing third-party packages (over 1.3 million at the time of writing).
Using a `package.json` file, all dependencies of a module can be defined together with their version range, which are resolved from npm at install time.

[Deno](cite:cites link:web:deno) is a relatively new runtime environment for JavaScript that aims to become a modern replacement for Node.js.
It is also based on the V8 engine, but it allows both JavaScript _and_ TypeScript to be executed without prior transpilation.
Furthermore, it allows external modules to be fetched based on URLs that can include version ranges,
<span class="comment" data-author="RV">I would actually argue the opposite of the next statement: Node has a decoupling point, where the code only contains a name, which _some_ package manager then binds to a concrete package and version. Deno binds to a concrete package and version.</span>
instead of being tightly linked to package names <span class="rephrase" data-author="RV">within the npm registry</span>.
<span class="comment" data-author="RV">Not correct, as Node is tied to node_modules, not npm. (Even though npm is now bundled with Node, it was not at the start)</span>

For the remainder of this article, we will assume the usage of the Node.js runtime.
This is because Components.js <del class="comment" data-author="RV">precedes the introduction of Deno</del>,
and Node.js is still predominantly used at the time of writing.
Nevertheless, since Deno's philosophy regarding dereferenceable modules is compatible with the dereferencebility of Components.js configurations,
we will consider support for it in the future.
