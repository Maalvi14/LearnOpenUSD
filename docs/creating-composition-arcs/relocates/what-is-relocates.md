# Relocates

## What is Relocates?

Suppose one {term}`prim <Prim>` defines a child (for example a prop under `/world/somewhere`), and another prim has a {term}`reference <Reference>` to that subtree. In the composed {term}`stage <Stage>`, referenced children appear under the referencing prim’s {term}`namespace <Namespace>`. That happens even when those children were not authored directly on the referencing prim in your {term}`layer <Layer>`. They appear there only as an effect of {term}`composition <Composition>`.

If that composed child should appear under a different parent, it cannot be moved like locally owned prims without editing the shared source {term}`asset <Asset>`, which would affect every consumer of that asset. {term}`Relocates <Relocate>` record a rule in your layer’s {term}`metadata <Metadata>`. They map the source {term}`path <Path>` where the prim would appear without the relocate to the target path where you want it in this {term}`layer stack <Layer Stack>`. The layer that defines the original hierarchy stays unchanged.

Only prim paths participate. {term}`Attributes <Attribute>` and {term}`relationships <Relationship>` are not relocated.

You author relocates as a dictionary in layer metadata, from source path to target path:

```usda
#usda 1.0
(
    relocates = {
        </Source/Prim/Path> : </Target/Prim/Path>
    }
)
```

## When and Why Do You Use Them?

Relocates let you rename or reparent prims that come from {term}`composition arcs <Composition Arcs>`, such as references, without destructively editing the original source layer.

This is useful when:

- The source prim lives in a referenced asset you do not want to modify.
- You need a cleaner hierarchy for downstream scene organization or pipeline conventions.
- You want local namespace control while preserving source asset reuse.

## Example: Reparenting Referenced Content

In this example, `house` is defined under `/world/somewhere` in content owned by another team. That layer is consumed as delivered and not edited here. The local scene adds `city` with a reference to `somewhere`, so the composed {term}`stage <Stage>` exposes `house` at `/world/city/house` without authoring a second definition under `city`. A sibling prim `town` exists in the local hierarchy but has no authored `house` child yet. The workflow adds relocates so the same composed prim resolves at `/world/town/house`. Prim names use lowercase spelling.

![](../../images/composition-arcs/relocates-example-01.png)

A reference grafts the subtree from `somewhere` onto `city`, so `house` appears under `city` in the composed namespace while its defining specs still live on the other team’s side of the reference. That split between authored location and composed location is what relocates can reshape locally.

![](../../images/composition-arcs/relocates-example-03.png)

The local layer’s metadata carries `relocates` from `/world/city/house` to `/world/town/house`. The same USDA defines `world`, `somewhere` with `house`, `city` with the reference, and `town` as the empty parent that will receive the composed child through the mapping.

![](../../images/composition-arcs/relocates-example-04.png)

Once the relocate applies, work that targets `house` should use `/world/town/house`. {term}`Opinions <Opinions>` authored in this {term}`layer stack <Layer Stack>` belong at that target path. The source path is not valid for new local edits.
