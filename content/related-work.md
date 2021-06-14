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

A specific technique to achieve IoC is [_Dependency Injection_ (DI)](cite:cites DependencyInjection).
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
then configuring via code may be better suited,
as this can become too complex to define in declarative configuration files.

**Forms of Injection**

In practise, three main forms of DI exist through which dependencies can be injected into a an object:

Constructor injection
: Dependency objects are passed via a class constructor.

Setter injection
: Dependencies are passed to an object by invoking setter methods.

Interface injection
: The interface of dependencies expose a method that –when invoked– injects this dependency into an object that is passed to it. Such passed objects will typically a setter method for this.

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
Such descriptions are however interpretive in that any given tool is subject to having multiple descriptions by different users.
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
In general, both ontologies (or suites) view software from a <q>network of communicating concepts</q> perspective.
This allows for exhaustive descriptions of complex software systems, but is not suited for describing class instances or aspects of modular programming (e.g., package dependencies).

### Dependency Injection Frameworks
{:#related-work-di-frameworks}

existing frameworks, and compare with Components.js (See https://linkedsoftwaredependencies.org/articles/reproducibility/#related-work)
{:.todo}
