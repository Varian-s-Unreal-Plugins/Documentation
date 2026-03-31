---
publish: true
---
# Link Bundle

`LinkBundle`'s is a simple data-only object meant to store an array of `InputLink`'s to quickly grant a set of `InputMappingContext`'s, `InputAction`'s and `InputLink`'s.

![[Pasted image 20260331195537.png]]

* This is a data-only class with no functions. Hence why this is not a data asset and just a object class.
* Only 1 copy of each `LinkBundle` can be active at a time per `InputNexus` component.
* Default `LinkBundle`'s will have their links added to the start of the `InputLink`'s array and everything defined in the component and `LinkBundle`'s added during runtime will have their `InputLink`'s added to the end of the array. It's designed this way because default `LinkBundle`'s are expected to be used as the base data, then everything added through the `InputLinks` array should be treated as the links added on top of them.
  * Remember, the `InputLink`'s  at the [end of the array are activated first](https://varian.gitbook.io/varian-docs/input-nexus/input-link). We use a reverse for-loop rather than a standard for-loop.

# See Also
- [[Input Link]] - The host of gameplay code.
- [[Nexus Component]] - The component where bundles can be granted through.