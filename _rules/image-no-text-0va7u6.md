---
id: 0va7u6
name: HTML graphics contain no text
rule_type: atomic
description: |
  This rule checks that images of text are not used
accessibility_requirements:
  wcag20:1.4.5: # Images of Text (AA)
    forConformance: true
    failed: not satisfied
    passed: further testing needed
    inapplicable: further testing needed
  wcag20:1.4.9: # Images of Text (No Exception) (AA)
    forConformance: true
    failed: not satisfied
    passed: further testing needed
    inapplicable: further testing needed
input_aspects:
  - DOM Tree
  - CSS Styling
  - Language
acknowledgments:
  authors:
    - Carlos Duarte
  images:
    - Letter posted from Dulverton (Somerset, England) to Bristol (England) in 1894. Released into the public domain by Adrian Pingstone.
    - Times Square image released into the public domain by (WT-shared) Ypsilonatshared at wts wikivoyage.
---

## Applicability

This rule applies to any [visible][] [embedded image][].

## Expectation

For each test target, at least one of the following is true:

- the image resource contains text and it is [essential][] that the text is rendered with that specific presentation; or
- the image resource does not contain text expressing anything in a [human language][]; or
- the image resource contains text and the text is not a significant part of the visual content in the image; or
- the test target is [purely decorative][].

## Assumptions

- The text in the image resource is visible and not hidden by other resources rendered on the web page. If the text is not visible, even though parts of the image are, this rule may fail while [SC 1.4.5 Images of Text][sc1.4.5] and [SC 1.4.9 Images of Text (No Exception)][sc1.4.9] might by satisfied.
- The page does not provide a mechanism to change the rendered text in the image resource. Otherwise, the rule might fail while [SC 1.4.5 Images of Text][sc1.4.5] and [SC 1.4.9 Images of Text (No Exception)][sc1.4.9] might by satisfied.
- The specific presentation of the text rendered in the image resource can be achieved through formatted text. Otherwise, the rule might fail while [SC 1.4.5 Images of Text][sc1.4.5] and [SC 1.4.9 Images of Text (No Exception)][sc1.4.9] might by satisfied.

## Accessibility Support

_No accessibility support issues known._

## Background

This rule is designed specifically for [SC 1.4.5 Images of Text][sc1.4.5] which includes exceptions to the images it applies to. [SC 1.4.9 Images of Text (No Exception)][sc1.4.9] does not consider any exceptions. Therefore, some images that are inapplicable for this rule can be applicable to [SC 1.4.9 Images of Text (No Exception)][sc1.4.9].

- [Understanding Success Criterion 1.4.5: Images of Text][sc1.4.5]
- [Understanding Success Criterion 1.4.9: Images of Text (No Exception)][sc1.4.9]

## Test Cases

### Passed

#### Passed Example 1

This `img` element references an image resource that does not contain text.

```html
<img src="/test-assets/shared/fireworks.jpg" alt="fireworks going off behind the Eiffel tower at night" />
```

#### Passed Example 2

This `input` element references an image resource that does not contain text.

```html
<input type="image" src="test-assets/shared/file.svg" alt="New file" />
```

#### Passed Example 3

This `svg` element displays an image resource that does not contain text.

```html
<svg width="2in" height="3in" xmlns="http://www.w3.org/2000/svg">
	<image x="20" y="20" width="200px" height="100px" href="/test-assets/shared/fireworks.jpg">
		<title>Fireworks in Paris</title>
	</image>
</svg>
```

#### Passed Example 4

This `object` element references an image resource where text is not the most significant content.

```html
<object data="/test-assets/0va7u6/times_square.jpg"></object>
```

#### Passed Example 5

This `img` element references an image resource that contains text but where the presentation of the text is essential to convey the information.

```html
<p>The following image illustrates the use of cursive writing in the late nineteenth century.</p>

<canvas id="canvas"> Your browser does not support the HTML5 canvas element. </canvas>

<script>
	var img = new Image()
	img.src = '/test-assets/0va7u6/letter.jpg'
	img.onload = function () {
		fill_canvas(img)
	}
	function fill_canvas(img) {
		var canvas = document.getElementById('canvas')
		var ctx = canvas.getContext('2d')
		canvas.width = img.width
		canvas.height = img.height
		ctx.drawImage(img, 0, 0)
	}
</script>
```

#### Passed Example 6

This `div` element has a background image with a logo with text. Logotypes are considered an essential exception.

```html
<div
	style="
    width: 100px;
    height: 100px;
    background-image: url(test-assets/shared/w3c-logo.png);
    background-repeat: no-repeat;
  "
></div>
```

#### Passed Example 7

This `img` element is [purely decorative][].

```html
<img src="/test-assets/0va7u6/welcome.png" alt="" />
<p>Welcome to our website</p>
```

### Failed

#### Failed Example 1

This `img` element references an image resource that contains text and the way the text is presented is not relevant.

```html
<img
	src="/test-assets/0va7u6/textimage.jpg"
	alt="The Accessibility Conformance Testing (ACT) Rules Format 1.0 defines a format for writing accessibility test rules."
/>
```

#### Failed Example 2

This `input` element in the [Image Button][] references an image resource that contains text and the way the text is presented is not relevant.

```html
<input type="image" src="/test-assets/0va7u6/button.jpg" alt="Press me" />
```

#### Failed Example 3

This `div` element has a `background-image` property that references an image resource that contains text and the way the text is presented is not relevant.

```html
<div style="background-image: url(/test-assets/0va7u6/textimage.jpg); width: 500px; height: 200px;" />
```

### Inapplicable

#### Inapplicable Example 1

This `object` element is not [visible][].

```html
<object date="/test-assets/0va7u6/textimage.jpg" style="display: none"></object>
```

#### Inapplicable Example 2

This `svg` element does not have `image` element descendants.

```html
<svg xmlns="http://www.w3.org/2000/svg">
	<text x="20" y="35">My</text>
	<text x="45" y="35">cat</text>
	<text x="55" y="55">is</text>
	<text x="70" y="55">Grumpy!</text>
</svg>
```

[embedded image]: #embedded-image 'Definition of Embedded Image'
[essential]: https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html#dfn-essential 'WCAG 2.1, Definition of essential'
[human language]: https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html#dfn-human-language 'WCAG 2.1, Definition of human language'
[image button]: https://html.spec.whatwg.org/multipage/input.html#image-button-state-(type=image)
[purely decorative]: https://www.w3.org/TR/WCAG21/#dfn-pure-decoration 'WCAG 2.1, Purely decorative'
[sc1.4.5]: https://www.w3.org/WAI/WCAG21/Understanding/images-of-text
[sc1.4.9]: https://www.w3.org/WAI/WCAG21/Understanding/images-of-text-no-exception
[visible]: #visible 'Definition of visible'