# [capsid][]-module

This repository describes a capsid-module. (3rd party module for [capsid][])

- A capsid module should specify capsid dependency as a **peer dependency**.
- A capsid module should have `capsidmodule` keyword in `keywords` field of its package.json.
- A capsid module should expose **install function**.
- The install function should have the following signature

```js
install(capsid, options)
```

Where `capsid` is the capsid module and `options` are the object of arbitrary shape.

- The install function may define a component (or components) using the given `capsid.def` method.
- If the install function defines any component, then the names of them should be configurable through `options`. (It can have default names for components.)
- A capsid module shouldn't require('capsid') directly in its source code. (Use the injected capsid object)
- A capsid module should document the available options and their default values.


A typical module structure looks like the below:

```js
exports.install = (capsid, options) => {

  const name = options.name || 'my-capsid-component'

  /**
   * MyComponent is responsible for ...
   */
  class MyComponent {
    __init__ () {
      // ... initializations ...
    }

    @capsid.on.click
    onClick () {
      // ... handling click event ...
    }

    @capsid.on('mouseover', { at: '.tooltip' })
    someReaction () {
      // ... handling mouseover event at .tooltip elements.
    }
  }

  capsid.def(name, MyComponent)
}
```

# Usage of capsid-module

The consumer of a capsid-module should call `capsid.install` method:

```js
const capsid = require('capsid')

capsid.install(require('3rd-party-capsid-module'), options)
```

The above should install `3rd-party-capsid-module` with the give `options`.

# Example of capsid-module

- [capsid-popper][]
  - capsid module for [popper.js][]

[capsid]: https://github.com/capsidjs/capsid
[capsid-popper]: https://github.com/capsidjs/capsid-popper
[popper.js]: https://popper.js.org
