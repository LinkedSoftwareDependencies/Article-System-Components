## Abstract
<!-- Context      -->
A common practise within object-oriented software,
is the use of _composition_ to represent relationships between objects.
_Dependency Injection (DI)_ is a popular technique to manage such compositions,
which loosely couples objects via minimal interfaces,
and wires these objects together at runtime based on declarative configuration files.

<div class="comment" data-author="miel">
Are there actually DI frameworks with global semantics? If not, you can make this statement more concrete by stating that we propose global semantics for reason X and implement this using Linked Data.
</div>

Configurations for existing DI frameworks typically only have local semantics,
which limits their usage in other contexts.
<!-- Need         -->
In some cases, such configurations are required outside of their local scope,
such as for the reproducibility of experiments, static program analysis, and semantic workflows.
As such, there is a need for globally interoperable, addressable, and discoverable configurations,
which can be achieved by leveraging the power of Linked Data.
<!-- Task         -->
To resolve this need, we introduce _Components.js_,
a semantic DI framework for TypeScript and JavaScript applications
that gives global semantics to its Linked Data-based configuration files.
<!-- Object       -->
In this article, we report on the Components.js framework
by explaining its architecture and configuration,
and we discuss its impact by mentioning where and how it is being used in other applications.
<!-- Findings     -->
We show that Components.js is a stable framework that has seen significant uptake during the last couple of years.
<!-- Conclusion   -->
We recommend it to be used within software projects that require
high flexibility,
configuration without code changes,
sharing configurations with others,
or using these configurations in other contexts such as experimentation or static program analysis.
<!-- Perspectives -->
The ever-increasing complexity of the world will depend on highly flexible software to manage it,
for which frameworks such as Components.js will be crucial foundations.
