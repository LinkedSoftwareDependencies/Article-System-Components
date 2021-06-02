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

See https://linkedsoftwaredependencies.org/articles/reproducibility/#related-work
{:.todo}

### Dependency Injection Frameworks
{:#related-work-di-frameworks}

existing frameworks, and compare with Components.js (See https://linkedsoftwaredependencies.org/articles/reproducibility/#related-work)
{:.todo}
