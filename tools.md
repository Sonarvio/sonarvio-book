# Tools

For creating the modules of the systems webpack is used as a build tool. It allows to merge different files into one and also provide various loaders for usage in the browser. To integrate PostCSS or the Babel transpiler its only necessary to include them as loaders during the build process.


React for interface building which allows to abstract
the underlying DOM and not rely on the restrictions of
existing components

Along with PostCSS for for automaticly adding prefixes
for the different, stylus got used to ease the nesting.

Since the browser extension could run on different sites
and shouldn't affect global style definitions -
CSS local scopes are used to prevent overriding definitions.