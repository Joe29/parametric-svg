<p align="right">
 <img alt="MIT License" src="https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square">
 <img alt="No implementations yet" src="https://img.shields.io/badge/implementations-0-blue.svg?style=flat-square">
</p>

<h1 align="center">
  <img alt="parametric.svg" src="https://raw.githubusercontent.com/tomekwi/parametric.svg/master/assets/logo.png" />
</h1>

 

**A specification for full-fledged parametric SVG graphics.**  
**A simple XML namespace – fully compatible with SVG 2.0.**

   
 



1. Goals
--------


##### ✓ Fully compatible with SVG specs.

You can view parametric.svg graphics directly in the browser or a simple SVG viewer. You can edit or even author them in Inkscape, Adobe Illustrator or any other favourite program of yours.

How is that? Parametric.svg is a regular XML namespace. We don't reinvent the wheel – instead, we extend the impressive capabilities of SVG, which are already built in.


##### ✓ Language-agnostic.

Tailor-cut to web technologies, but easy to implement in any programming language.


##### ✓ Ready for the future.

There already is [a specification for dynamic parameters in SVG 2.0][svg-params] out there. It is a great idea – but it's not implemented in most web browsers yet.

Parametric.svg is fully compatible with the native specification – and brings even more to you. We not only support dynamic parameters and dynamic geometry, but also dynamic relationships between them.

When the implementation comes to web browsers, your parametric.svg drawings will profit from all the goodness of native SVG Parameters – like the ability to set your parameters through the URL's query string.

[svg-params]: http://www.w3.org/TR/SVGParamPrimer/ "SVG Parameters 1.0"


##### ✓ Full-fledged.

Parametric.svg is designed as a complete set of tools to describe relationships between parameters and elements. For the web it could become what Grasshopper is for CAD.




2. Abstract
-----------

The purpose of this document is to outline and specify an XML namespace extending the capabilities of Scalable Vector Graphics. The described namespace provides a complete set of tools to parametrise the position, geometry and number of elements in the graphic, in a declarative way.

The parametrisation should not only provide direct access to these properties, but also allow the author to declare logical and arithmetic relationships between parameters and elements.




3. Specification
----------------

…




4. Implementations
------------------

A [JavaScript implementation][on-npm] is currently being worked on.

[on-npm]: https://www.npmjs.com/package/parametric.svg




5. License
----------

[MIT][license] © [Tomek Wiszniewski][].

[license]: ./License.md
[Tomek Wiszniewski]: https://github.com/tomekwi