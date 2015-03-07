<p align="right">
  <a href="./License.md"><img alt="MIT License" src="https://img.shields.io/badge/license-MIT-9eab05.svg?style=flat-square"></a> <a href="#5-implementations"><img alt="No implementations yet" src="https://img.shields.io/badge/implementations-0-9eab05.svg?style=flat-square"></a>
</p>

<h1 align="center">
  <img alt="parametric.svg" src="https://rawgit.com/parametric-svg/spec/master/assets/logo.svg" />
</h1>

 

**A specification for full-fledged parametric graphics. In pure SVG.**

**A simple XML namespace – fully compatible with SVG 1.1 and SVG 2.0.**

   
 



1. Goals
--------

<small align="right">This section is informative.</small>


##### ✓ Fully compatible with SVG specs.

_parametric.svg_ graphics can be viewed directly in the browser or in a simple SVG viewer. They can be edited and authored in your favorite program – be it Inkscape, Adobe Illustrator, VIM or any other.

How is that? _parametric.svg_ is a regular XML namespace. We don't reinvent the wheel – instead, we extend the impressive capabilities of SVG, which are already built in.


##### ✓ Language-agnostic.

Tailor-cut for the web, but easy to implement in any programming language.


##### ✓ Ready for the future.

There already is [a specification for dynamic parameters][svg-params] in the upcoming SVG 2.0. _parametric.svg_ is fully compatible with it – profiting from all its goodness, and bringing even more than that. We not only support dynamic parameters – but also logical and arithmetic relationships between them and geometry.

SVG 2.0 isn't yet fully standardized and implemented. But _parametric.svg_ is built upon existing, stable technologies – ready to be used today.

[svg-params]: http://www.w3.org/TR/SVGParamPrimer/ "SVG Parameters 1.0"


##### ✓ Full-fledged.

_parametric.svg_ is a complete set of tools to describe relationships between parameters and elements. For the web it could become what Grasshopper is for CAD.




2. Abstract
-----------

<small align="right">This section is informative.</small>


The purpose of this document is to outline and specify an XML namespace extending the capabilities of Scalable Vector Graphics. The described namespace provides a complete set of tools to parametrize the position, geometry and number of elements in the graphic, in a declarative way.

The parametrization should not only provide direct access to these properties, but also allow the author to declare logical and arithmetic relationships between parameters and elements.




3. Usage
--------

<small align="right">This section is normative.</small>


_parametric.svg_ is a regular XML namespace. In order to be used on an element, the namespace must be declared on the element or any of its ancestors by the following URI: `https://parametric-svg.github.io/v0.x`.

For example, the following declaration will allow using the namespace in the scope of the whole SVG document:

```xml
<svg version="1.1"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:parametric="https://parametric-svg.github.io/v0.x"
  >
  ...
</svg>
```

Once the reference is specified, the namespace can be used on all elements within the scope, like in the following example:

```xml
  <defs>
    <parametric:ref param="factor" default="7" />
  </defs>

  <circle cx="100" cy="100" r="50"
    parametric:r="10 * factor"
    />
```




4. Specification
----------------

<small align="right">This section is normative.</small>


### 4.1 Attributes

Any attribute valid for a given SVG element in the SVG namespace (no prefix) has its counterpart in the [parametric namespace][]. For example – since the attribute `fill` is valid for a `<circle>` element – the attribute `parametric:fill` is also valid for it.

A reference of valid attributes in SVG 1.1 can be found [here][svg-attributes].

[svg-attributes]: http://www.w3.org/TR/SVG/propidx.html


##### Attribute value

The value of a [parametric attribute][parametric] should be a valid [expression][].


##### Evaluation of parametric attributes

The [expression][] declared in the [parametric][] attribute should be evaluated upon loading the SVG document, and upon any change in parameter values. The resulting value should be cast to a string and replace the value of the [counterpart attribute][]. If the [counterpart attribute][] doesn't exist, it should be created.

If an [error][] is thrown during evaluation of the [expression][], the value of the [counterpart attribute][] should be left unchanged. If no [counterpart attribute][] was present at the time of evaluation, it shouldn't be created. The rendering of the SVG document should proceed normally, but the [error][] message may be logged.

If evaluation of the [expression][] results in [null][], the [counterpart attribute][] should be removed.

The order of evaluating [parametric attributes][parametric] is not defined.




### 4.2 Elements

##### `<parametric:ref>`

The only element defined by this specification is `<parametric:ref>`. It's designed as a polyfill for the [`<ref>`][ref] element defined in a working draft of SVG 2.0. It accepts two attributes:

- `param` – the name of a [parameter][];
- `default` – (a valid [literal][]) the default value of the [parameter][] referenced by `param`.

[ref]: http://www.w3.org/TR/2009/WD-SVGParam-20090430/#ref-element
[parametric-ref]: #parametric-ref




### 4.3 Definitions


##### counterpart attribute

The counterpart attribute of a [parametric attribute][parametric] is an attribute of the same `localName` in the SVG namespace. For example, in the SVG element `<circle fill="red" parametric:fill="green" />` the counterpart attribute of `parametric:fill` is the attribute `fill`.

[counterpart attribute]: #counterpart-attribute


##### error

> This definition needs work.

[error]: #error


##### expression

A valid ECMAScript 6 expression consisting only of the [literals][literal], [operators][operator] and [parameter references][parameter reference] allowed by this specification.

When an expression is invalid, an [error][] should be thrown upon its evaluation.

If evaluating part of an expression or a whole expression type conversion, any value should be cast to a `String`. The result of casting should keep in line with the specification of ECMAScript 6.

[expression]: #expression


##### literal

A valid ECMAScript 6 global object, constructed through the literal form – without invoking a constructor function – for example `"abc"` in contrast to the invalid `new String("abc")`. Only the following object types are supported:

- `Number`
- `Boolean`
- `String`
- `null`

An informative reference of global objects and their literal forms can be found on [MDN][mdn-literals].

[mdn-literals]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects
[literal]: #literal


##### null

A value which is valid, but explicitly empty – in contrast to an [error][].

[null]: #null


##### operator

A valid ECMAScript 6 operator. Only the following operators are supported:

- Arithmetic operators:
    - Addition operator (`+`)
    - Substraction operator (`-`)
    - Division operator (`/`)
    - Multiplication operator (`*`)
    - Remainder operator (`%`)
- Unary operators:
    - Unary plus operator (`+`)
    - Unary minus operator (`-`)
- Relational operators:
    - Less than operator (`<`)
    - Greater than operator (`>`)
    - Less than or equal operator (`<=`)
    - Greater than or equal operator (`>=`)
- Equality operators:
    - Identity operator (`===`)
    - Nonidentity operator (`!==`)
- Binary logical operators:
    - Logical AND (`&&`)
    - Logical OR (`||`)
- Other:
    - String concatenation operator (`+`)
    - Conditional (ternary) operator (`condition ? ifTrue : ifFalse`)

An informative reference of operators in ECMAScript can be found on [MDN][mdn-operators].

[mdn-operators]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators
[operator]: #operator


##### parameter reference

A parameter reference is an equivalent of an ECMAScript variable identifier – both in syntax and in meaning. It represents the value of a parameter of the same name. If no parameter is passed, it falls back to the default value delared in the [`<ref>`][ref] or [`<parametric:ref>`][parametric-ref] element.

If the passed value or default value is invalid, or none of them is found, an [error][] should be thrown.

For example, in the declaration `<circle parametric:r="10 * factor" />`, `factor` is a parameter reference. If the parameter `factor` is assigned a value of `5`, the expression `10 * factor` will evalute to `50`.

[parameter reference]: #parameter-reference


##### parametric

An attribute or element in the [parametric namespace][] is referred to as a parametric attribute or element.

[parametric]: #parametric


##### parametric namespace

The parametric namespace is the XML namespace identified by the URI `http://github.com/parametric-svg/parametric.svg/tree/0.1`.

[parametric namespace]: #parametric-namespace






5. Implementations
------------------

<small align="right">This section is informative.</small>


A [JavaScript implementation][on-npm] is currently being worked on.

[on-npm]: https://www.npmjs.com/package/parametric.svg




5. License
----------

<small align="right">This section is informative.</small>


[MIT][license] © [Tomek Wiszniewski][].

[license]: ./License.md
[Tomek Wiszniewski]: https://github.com/tomekwi
