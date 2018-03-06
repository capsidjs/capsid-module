# [capsid][]-module

This repository describes a capsid-module.

- A capsid module should specify capsid dependency as a **peer dependency**.
- A capsid module should provide **register function(s) of components**.
  - A register function of a component should take the name of the component as a parameter.
  - A register function of a component may have the default value for name parameter.
  - A capsid module shouldn't automatically register the component as a side effect.
  - (The user of the module should be able to choose the name of the component.)
- A register function of a component should take `capsid` module as a parameter.
  - A capsid module shouldn't require('capsid') directly in its source code.

A typical module structure looks like the below:

```js
module.exports = (capsid, name = 'my-module') => {
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

[capsid]: https://github.com/capsidjs/capsid
