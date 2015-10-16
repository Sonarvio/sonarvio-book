# Tools

For creating the modules of the systems webpack is used as a build tool. It allows to merge different files into one and also provide various loaders for usage in the browser. To integrate PostCSS for automatically adding prefixes or the Babel transpiler to use ES2015 syntax, its only necessary to add them as loaders during the build process.

The interface is mostly defined through React components, which provides an abstracting to the underlying DOM. Regarding the APIs for creating extensions for the different browsers, it provide the advantage of an unified environment which can be shared. Since browser extension run on different sites and shouldn't affect global defined styles, CSS local scopes are used to prevent overriding such definitions.