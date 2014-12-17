#CSS/SCSS Style Guide

The following document outlines the Lemonly way of writing well-organized, idiomatic, and consistent CSS/SCSS.

##Table of Contents
1. [General principles](#general-principles)
2. [Whitespace](#whitespace)
3. [Comments](#comments)
4. [Selectors](#selectors)
5. [Units](#units)
6. [Format](#format)


<a name="general-principles"></a>
##1. General Principles
* Don't prematurely optimize your code; keep it readable and understandable
* The goal is to get to the point where all Lemonly CSS looks like it was written by a single person
* Hold yourself and others accountable to the style guide
* Install and use an .editorconfig plugin. All Lemonly projects should use the .editorconfig file from the Project Boilerplate.

<a name="whitespace"></a>
##2. Whitespace
* Spaces should always be used for indentation, not tabs. Spaces are the only way to ensure consistency across all development environments.
* Four (4) spaces should be used for an indentation level

<a name="comments"></a>
##3. Comments
Including comments in your code is extremely important. Take time to communicate what each .scss file is for, any hacks you're using, and any unusual things you're doing.
* Describe each .scss file. This is especially important if you add a new file outside the boilerplate norms.
* Keep line-length to a sensible maximum (80 chars is good)
* For inline comments, use the SCSS double-slash method: "// Comment here". This will be removed by Sass at compile-time.

```css
/*
 * Comment block at the beginning of a .scss file explaining it's purpose.
 *
 * This type of comment should appear at the top of every .scss file in the
 * project.
 *
 * If the content is too long for an 80 character line, it should wrap at
 * about 80 characters and continue on the next line.
 *
 */

.selector {
    // This is a comment describing something I'm doing on the next line
    background: red;
}
```

<a name="selectors"></a>
##4. Selectors
* Class names should use hyphens to separate words
* ID names should be camelCasedWithLeadingLowerCase
* Lemonly uses a loose BEM CSS method of naming classes (e.g. `class="block-name--element_modifier"`)
* Classes are preferred over IDs in selectors
* Don't modify class names with type (e.g. `header.main`)
* Nested selectors should never be more than two selectors deep
    * If nested classes are used, consider creating another class

```css
.parent-selector {
    &>li {
        color: #ccc;
    }
    a {
        color: #0000ff;
    }
}

.child-selector {
    color: #ff0000;
}
```

<a name="units"></a>
##5. Units
* Relative units should always be used.
* rem values are preferred over ems, unless sizes relative to parent are necessary.
* Avoid units on zero-values where possible (e.g. `margin: 0`)
* Leading zeros on property values should be removed
* Sass division should be used when any rem/em values other than /4 are needed (e.g. `font-size: (7rem/8)`)

```css
.selector {
    // Evaluates to 1.3125rem
    margin-bottom: (21rem/16);
    padding: .25rem;
    // Evaluates to .875em
    font-size: (7em/8);
}
```

<a name="format"></a>
##6. Format
* Use one selector per line when in multi-selector rulesets
* The selector should have a single space between it and {
* Include one declaration per line in a declaration block
    * Treat nested Sass selectors as a declaration, so no extra line break before nested selector
* Each declaration should have one level of indentation
* Each declaration should have a single space after the :
* Use lowercase and shorthand hex values (e.g. `#fff` instead of `#FFFFFF` or `white`)
* Prefer single-quotes (e.g. `content: ''`)
* Wrap attribute values in single-quotes in selectors (e.g. `input[type='text']`)
* Include a space after commas in comma-separated property or function values (e.g. `@include border-radius(1em, 2em, 3em, 4em)`)
* Include a semi-colon at the end of every declaration of a declaration block, including the last.
* Place the closing brace of a ruleset in the same column as the first character of the ruleset.
* Separate each ruleset by a blank line.

```css
.selector1,
.selector2,
.selector3[type='text'] {
    display: block;
    background: #fff;
    font-family: helvetica, sans-serif;
    &>li {
        color: #ccc;
    }
}

.selector-a,
.selector-b {
    margin: 0;
    padding: 1em;
}
```

####Declaration Order
Declarations should be in a consistent order. Related properties should be clusetered together, and mixins should go in the order they would if it were CSS.

1. Extend
2. Positioning
    * Position declarations should be in the same order as other shorthands (top, right, bottom, left)
3. Display & Box Model
    * Width should be declared before height
    * Declarations should move from outside to inside of the box (height/width -> margin -> border -> padding)
4. Background & font rules
    * Background first, if any
    * Font rules in alphabetical order
5. Other

For nested selectors, the order they should be placed in is:
1. Pseudo-selectors
2. Additional selectors on original element (e.g.  `&.new-class`)
3. Pseudo-elements
4. Child elements

```css
.selector {
    // Extend
    @extend .other-selector;

    // Positioning
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 2;

    // Display & Box Model
    display: block;
    width: 100%;
    height: 20rem;
    margin: .5rem;
    border: .25rem solid #000;
    @include border-radius(2em, 1em, 3em, 2em);
    padding: .5rem;
    overflow: hidden;

    // Background & Font Rules
    background: #333 url(bg-image.jpg) no-repeat 50% 50%;
    background-size: contain;
    font-family: helvetica, arial, sans-serif;
    font-size: 1.5rem;
    font-style: italic;
    text-align; right;
    text-transform: uppercase;

    // If there are other declarations, they'd go here

    // Nested Selectors
    &:nth-child(2) {
        background: #ccc;
    }
    &.red {
        background: #cc0000;
    }
    &:after {
        content: 'Content';
        color: #fff;
    }
    .child {
        background-color: #fff;
    }
    &>img {
        position: relative;
    }
}
```

####Exceptions
Large blocks of single declarations should be declared on a single line for each selector. A space should be included after the opening brace and before the closing brace.

```css
.selector1 { background: #000; }
.selector2 { background: #333; }
.selector3 { background: #666; }
.selector4 { background: #999; }
```

Long, comma-separated property values (e.g. gradients or box-shadows) should be arranged one-per-line.

```css
.selector {
    background:
        url(bg-image-1.jpg) no-repeat left top,
        url(bg-image-2.jpg) no-repeat center top,
        url(bg-image-3.jpg) repeat 50% 50%;
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
}
```
Thanks to [Nicolas Gallagher for inspiration](https://github.com/necolas/idiomatic-css/).
