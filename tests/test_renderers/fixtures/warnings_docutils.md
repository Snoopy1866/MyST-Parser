Duplicate Reference definitions:
.
[a]: b
[a]: c
.
<string>:2: (WARNING/2) Duplicate reference definition: A [myst.duplicate_def]
.

Unhandled URI:
.
[a](b)
.
<string>:1: (WARNING/2) Unhandled link URI (prepend with '#' or 'myst:any#'?): 'b' [myst.link_uri]
.

Missing local reference:
.
[a](#b)
.
<string>:1: (WARNING/2) ref name does not match any known target: 'b' [myst.ref_missing]
.

Unsupported myst link
.
[a](myst:link)
.
<string>:1: (WARNING/2) docutils only parsing does not support 'myst:' links: 'myst:link' [myst.xref_unsupported]
.

Unknown role:
.
abc

{xyz}`a`
.
<string>:3: (ERROR/3) Unknown interpreted text role "xyz".
.

Unknown directive:
.

```{xyz}
```
.
<string>:2: (ERROR/3) Unknown directive type "xyz".
.

Bad Front Matter:
.
---
a: {
---
.
<string>:1: (WARNING/2) Malformed YAML [myst.topmatter]
.

Unknown Front Matter myst key:
.
---
myst:
  unknown: true
---
.
<string>:1: (WARNING/2) Unknown field: unknown [myst.topmatter]
.

Invalid Front Matter myst key:
.
---
myst:
  title_to_header: 1
  url_schemes: [1]
  substitutions:
    key: []
---
.
<string>:1: (WARNING/2) 'title_to_header' must be of type <class 'bool'> (got 1 that is a <class 'int'>). [myst.topmatter]
<string>:1: (WARNING/2) 'url_schemes[0]' must be of type <class 'str'> (got 1 that is a <class 'int'>). [myst.topmatter]
<string>:1: (WARNING/2) 'substitutions['key']' must be of type (<class 'str'>, <class 'int'>, <class 'float'>) (got [] that is a <class 'list'>). [myst.topmatter]
.

Bad HTML Meta
.
---
myst:
  html_meta:
    name noequals: value

---
.
<string>:: (ERROR/3) Error parsing meta tag attribute "name noequals": no '=' in noequals.
.

Directive parsing error:
.

```{class}
```
.
<string>:2: (ERROR/3) Directive 'class': 1 argument(s) required, 0 supplied
.

Directive run error:
.

```{date}
x
```
.
<string>:2: (ERROR/3) Invalid context: the "date" directive can only be used within a substitution definition.
.

Do not start headings at H1:
.
## title 1
.
<string>:1: (WARNING/2) Document headings start at H2, not H1 [myst.header]
.

Non-consecutive headings:
.
# title 1
### title 3
.
<string>:2: (WARNING/2) Non-consecutive header level increase; H1 to H3 [myst.header]
.

multiple footnote definitions
.
[^a]

[^a]: definition 1
[^a]: definition 2
.
<string>:: (WARNING/2) Multiple footnote definitions found for label: 'a' [myst.footnote]
.

Warnings in eval-rst
.
some external

lines

```{eval-rst}
some internal

lines

.. unknown:: some text

:unknown:`a`
```
.
<string>:10: (ERROR/3) Unknown directive type "unknown".

.. unknown:: some text

<string>:12: (ERROR/3) Unknown interpreted text role "unknown".
.

bad-option-value
.
```{note}
:class: [1]
```
.
<string>:1: (ERROR/3) Directive 'note': option "class" value not string (enclose with ""): [1]

:class: [1]

.

header nested in admonition
.
```{note}
# Header
```
.
<string>:2: (WARNING/2) Disallowed nested header found, converting to rubric [myst.nested_header]
.

nested parse warning
.
Paragraph

```{note}
:class: abc
:name: xyz

{unknown}`a`
```
.
<string>:7: (ERROR/3) Unknown interpreted text role "unknown".
.