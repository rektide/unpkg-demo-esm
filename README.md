# unpkg-demo-esm

> A trivial module to see how unpkg exposes bare specifier modules

# Modules in the browser

The source code here just imports another module and does nothing with it. This is meant to represent how the world currently expects to consume a "module".

# unpkg-demo-esm.js

```
import devrep from "devrep"
```

# Bare specifier problem in the browser

However if you try to use this code directly in the browser, you'll see this (or maybe something like it?):

> "Uncaught TypeError: Failed to resolve module specifier "nope". Relative references must start with either "/", "./", or "../"."

# Unpkg

[Based off some conversation](https://mobile.twitter.com/WebReflection/status/959611367648038913) about the usability of modules in the browser, I came to believe the [unpkg cdn](https://unpkg.com/) may be doing some instrumentation to make modules (as we know and author them) viable in the browser.

So I wrote this very simple test to see what if anything it would do to make this dependency work.

Compare the [./unpkg-demo-esm.js](#unpkg-demo-esmjs) file on github with [unpkg output](https://unpkg.com/unpkg-demo-esm@1.0.0/unpkg-demo-esm.js?module):

```
import devrep from "https://unpkg.com/devrep@^1.0.0?module";
```

# Verdict

Unpkg does a bunch of specific rewriting of "modules" such that the browser can actually consume them & locate their dependencies. It remains, IMO, very sad and unfortunate that there is no universal, modular way to begin to directly author modules that the browser can consume, but at least there exists some tooling to work-around modules not being modular in the browser environment.




