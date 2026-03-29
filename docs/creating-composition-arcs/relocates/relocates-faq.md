# Relocates Frequently Asked Questions

Let’s take some time to ask common questions about working with {term}`relocates <Relocate>`.

## Can I relocate any prim?

No. Relocates are meant for prims introduced through {term}`composition arcs <Composition Arcs>`. The source path cannot be a root {term}`prim <Prim>`.

## Can relocates target properties?

No. Relocates map {term}`prim <Prim>` paths only, not {term}`properties <Property>` in general. {term}`Attribute <Attribute>` and {term}`relationship <Relationship>` paths are not valid source or target entries.

## Can I keep authoring opinions at the old source path?

No. Once a source path is relocated, it is no longer valid in that {term}`namespace <Namespace>`. Author local {term}`opinions <Opinions>` at the relocate target path instead.

## Can I chain relocates like A -> B and B -> C?

Not in the same {term}`layer stack <Layer Stack>` as separate entries. Collapse them into a single mapping (for example, `A -> C`).

## Can two source paths map to the same target?

No. Conflicting mappings are invalid. Each source and target pairing must resolve to a unique, unambiguous namespace result.

## Does relocates change the source asset file?

No. Relocates are non-destructive. They only affect {term}`composition <Composition>` in the local layer stack where they are authored.

## How does relocates interact with inherits?

A relocated prim still carries inherited {term}`opinions <Opinions>` from its original composed identity, including those contributed by {term}`inherit <Inherit>` arcs. This can be subtle in deeper compositions: the relocated location does not automatically mean inherited data comes from a matching relocated {term}`class <Class>` path.

## How does relocates interact with ancestral arcs?

During prim index construction, relocates ignore most ancestral arcs except {term}`variant sets <Variant Set>`. {term}`Variant <Variant>` opinions on ancestors can still compose at the relocated target.

## Where does relocates sit in strength ordering?

Relocates is stronger than {term}`references <Reference>` and weaker than {term}`variants <Variant>`. This means relocated namespace changes can affect referenced content, while stronger arcs can still contribute stronger opinions at the target location.

## Where should I debug relocates issues first?

Start with these checks:

- Verify `relocates` {term}`metadata <Metadata>` is authored in the expected {term}`layer <Layer>`.
- Confirm both source and target are absolute prim paths.
- Ensure no local opinions remain at the relocation source path.
- Check for namespace conflicts or transitive mappings.
- Inspect composed results in usdview and flattened output.

## When should I use relocates vs editing the asset?

Use relocates when you need local namespace restructuring without changing shared source {term}`assets <Asset>`. Edit the source asset only when the structural change should apply globally to all consumers.
