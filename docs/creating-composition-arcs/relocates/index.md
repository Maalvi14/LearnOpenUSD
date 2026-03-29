# Relocates

Now, let's explore {term}`relocates <Relocate>`, a {term}`composition arc <Composition Arcs>` used to non-destructively rename or reparent {term}`prims <Prim>` introduced through {term}`composition <Composition>`. Relocates are especially useful when prims come from {term}`references <Reference>` or other arcs and cannot be edited directly at their source.

In this module, we will:

- Understand what relocates are and where they fit in USD composition.
- Learn how relocates are authored in {term}`layer <Layer>` {term}`metadata <Metadata>`.
- See how relocates affect {term}`namespace <Namespace>` validity and local {term}`opinions <Opinions>`.
- Review common constraints and troubleshooting patterns.

Here is an outline for this lesson:

:::{toctree}
:maxdepth: 1
What is Relocates? <what-is-relocates>
Exercise: Working with Relocates <working-with-relocates>
Relocates FAQ <relocates-faq>
:::