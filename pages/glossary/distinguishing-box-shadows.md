---
title: Distinguishing box-shadows
key: distinguishing-box-shadows
unambiguous: true
objective: true
---

Look at the [computed](https://drafts.csswg.org/css-cascade/#computed-value) values of the `box-shadow` style property.

Two elements have a distinguishing box-shadow if all of the following are true:

- their [computed](https://drafts.csswg.org/css-cascade/#computed-value) values are different; and
- if the difference is just based on the color values, and only one of the elements has the color value specified then that value has to be different from the [computed](https://drafts.csswg.org/css-cascade/#computed-value) `background-color` of the element or the value's [alpha component](https://drafts.csswg.org/css-color/#alpha-channel) has to be different from 0.