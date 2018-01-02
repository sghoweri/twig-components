# Twig Components

An experimental repository to use Twig templates in Web Components.

This project provides a base web component that others can extend, and
specifications for what distributed Twig components should look like.

Beyond being useful to users already using something like [Twig.js](https://github.com/twigjs/twig.js)
, using Twig templates opens the door to server side rendering _without_
Javascript. This is critical for progressive enhancement, SEO, and
accessibility. A PHP server side renderer is already in development.

# Installation

`npm install --save-dev twig-components`

# Extending the base component

The base component in `twig-base.js` can be extended minimally by implementing
the `observedAttributes` and `getTemplate` methods:

```js
import TwigBase from 'twig-components/twig-base';

class MyComponent extends TwigBase {

  static get observedAttributes() {
    return ['name'];
  }

  getTemplate() {
    'Hello {{ name }}!';
  }

}

customElements.define('my-component', MyComponent);
```

Then, when `<my-component name="World"></my-component>` is placed on a page,
the template will be compiled and rendered with the current attributes.

# Creating a component library with Webpack

While extending the base component in the above example seems easy, getting it
working in production has a few hard problems:

- Distributing one JS file for multiple components
- Supporting older browsers
- Bundling Web Component polyfills
- Splitting up assets into distinct files (ex: .js, .twig, and .scss)
- Building a templates.json file

To ease some of this pain, a Yeoman generator is available to quickly spin up a
new component library, which has a complex Webpack configuration that does all
of this out of the box. See [generator-twig-components-webpack](https://github.com/mortenson/generator-twig-components-webpack)
for more details.

# Distribution specification

To help keep various distribution and bundling methods consistent, a
specification is maintained in [DISTRIBUTION.md](DISTRIBUTION.md).

# Todo

- [x] Create base custom element
- [x] Import SCSS/Twig from a file during build
- [x] Create a Yeoman generator for new components
- [x] Figure out what production packaging looks like
- [ ] Write unit test coverage for the base class
- [ ] Implment server-side-rendering with PHP Twig (50%)
- [ ] Write a ton of docs
