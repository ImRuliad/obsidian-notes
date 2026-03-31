*Linters are tools that can automatically check the style of your code and make improving suggestions.*

Here are some well-known linting tools:
- [JSLint](https://www.jslint.com/) – one of the first linters.
- [JSHint](https://jshint.com/) – more settings than JSLint.
- [ESLint](https://eslint.org/) – probably the newest one.

Most linters are integrated with many popular editors: just enable the plugin in the editor and configure the style.

For instance, for ESLint you should do the following:
1. Install [Node.js](https://nodejs.org/).
2. Install ESLint with the command `npm install -g eslint` (npm is a JavaScript package installer).
3. Create a config file named `.eslintrc` in the root of your JavaScript project (in the folder that contains all your files).
4. Install/enable the plugin for your editor that integrates with ESLint. The majority of editors have one.

Here’s an example of an `.eslintrc` file:
```js
{
  "extends":  "eslint:recommended",
  "env":  {
    "browser":  true,
    "node":  true,
    "es6":  true
  },
  "rules":  {
    "no-console":  0,
    "indent":  2
  }
}
```
Here the directive `"extends"` denotes that the configuration is based on the “eslint:recommended” set of settings. After that, we specify our own.
It is also possible to download style rule sets from the web and extend them instead. See [https://eslint.org/docs/user-guide/getting-started](https://eslint.org/docs/user-guide/getting-started) for more details about installation.

Also certain IDEs have built-in linting, which is convenient but not as customizable as ESLint.