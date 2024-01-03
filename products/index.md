---
icon: note
tags: [guide]
---

# Products



=== [!badge Hyper AI Computing Service](hac.md)

===


=== [!badge Platform Cloud Service](platformcloudservice.md)


===


=== [!badge AI Model Hub](Aimodelhub.md)


===



=== [!badge Moreh API](morehapi.md)



===


=== [!badge HAC Web Console](webconsole.md)



===




||| Demo
[!badge Platform Cloud Service](platformcloudservice.md)
||| Source
```md
[!badge Badge]
```
|||

---

## Variant

```md
[!badge variant="primary" text="Primary"]
```



---
icon: rows
tags: [component]
---

A Panel is created by surrounding a block of content with `===` and including a `title` for the Panel.

```
=== My Panel
This is a Panel. Expanded by default.
===
```


The `title` must be separated from the opening `===` by one space. The pattern `=== My Panel` will work as expected, and `===My Panel` will not.

Multiple Panels can be [stacked](#stacking) by repeating Panel component configurations.

```

===

!!!
Currently, Panel components cannot be nested within each other, only stacked. We're hoping to support nesting Panels in a future release. [Let us know](https://github.com/retypeapp/retype/issues) if you require the functionality.

All other components can be nested within any Panel component.
!!!

---

job roles and titles always against this segments