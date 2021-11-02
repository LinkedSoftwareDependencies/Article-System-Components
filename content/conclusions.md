## Conclusions
{:#conclusions}

After more than four years of development, Components.js has become a stable Dependency Injection framework for TypeScript and JavaScript projects,
and has seen a significant uptake by popular tools that make use of it as core technology.
It has been shown to be useful for enabling the primary tasks of a DI framework,
but thanks to its semantic configuration files,
it also brings with it the power of Linked Data and the Semantic Web for enabling globally interoperable and discoverable configurations.
Using the Linked Software Dependencies service, components and configurations become dereferenceable and citable,
which allows software configurations to be shared easily with others,
which is for example beneficial for improving the reproducibility of software experiments.

The previous section has shown that Components.js provides significant value in real-world applications.
On the one hand, tools such as Solid Community Server and Comunica allow developers and researchers to rewire these applications based on their specific needs.
On the other hand, applications by companies such as Digita depend on this flexibility for making logic changes via configuration files,
as they want to enable their clients to make changes by only modifying the configuration files,
since their clients are sometimes non-technical people that have limited programming knowledge.

We can recommend Components.js for TypeScript/JavaScript projects that have at least a subset of the following characteristics:

* Architectures that require **high modularity and flexibility**;
* Need to modify wiring of components **without changing code**;
* Need for ability to **share wiring configurations** with others;
* Managing and including **configurations across different projects**;
* Using **configurations in other contexts**.

As with all DI frameworks, Components.js comes with the downside that for large applications,
configurations can become complex and logic flow may be harder to follow.
In order to mitigate these risks, we recommend a structured management of configuration files,
which may involve splitting up configuration files based on your architecture's primary subsystems,
which is the approach followed by large projects such as Solid Community Server and Comunica.

In future work, we do not foresee the need for any major changes or additions within the Components.js framework itself,
aside from keeping up with new language features from JavaScript and TypeScript.
However, all large projects that make use of Components.js have identified the need for better tooling to create and manage configuration files.
For example, the Comunica project is developing a [graphical user interface](cite:cites link:docs:comunicapackager)
to visually customize the wiring of the engine, which can then be exported into a reusable configuration file.
Since Components.js configurations make use of the Linked Data principles,
it is possible to create a generic user interface to create such configuration files for any project that makes use of Components.js.
Furthermore, since components and configuration files are largely programming language-independent,
it is possible to create equivalent implementations of Components.js for other OO languages such as Java and C#.

In general, Components.js gives us the necessary foundation for building next-level applications that depend on high flexiblity, such as smart agents.
These applications are crucial for environments such as Linked Data and the Semantic Web,
which require and benefit from this level of flexibility.
Therefore, DI frameworks such as Components.js pave the road towards a world with more flexible applications.
