# How to setup ESLint and Prettier in a project in VSCode from zero
(If you cloned a project that uses ESLint and Prettier, then go to **12.** to activate those features in your VSCode.)

## ESLint

1. Install core ESLint library, ESLint TypeScript parser (to allow ESLint to lint TypeScript code) and ESLint TypeScript plugin (which contains some TypeScript-specific ESLint rules).<br>
*npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin*

2. Create .eslintrc file, select options that fit the project.<br>
*npx eslint --init*<br>
Add rules: [ESLint rules](https://eslint.org/docs/rules/), [ESLint Plugin TypeScript rules](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin#supported-rules).

3. Create .eslintignore file, insert file/folder names to be ignored by ESLint.

## Prettier

4. Install Prettier, eslint-config-prettier (to disable linting rules that might interfere with an existing Prettier rule) and eslint-plugin-prettier (to run Prettier analysis as part of ESLint).<br>
*npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier*

5. Create .prettierrc.json, add rules to be applied when formatting: [Prettier Options](https://prettier.io/docs/en/options.html).

## Git hook

6. Add git hook that will format changed files to be commited.<br>
*npm install --save-dev pretty-quick husky*

7. Add pre-commit hook to package.json.<br>
*"husky": {<br>
&nbsp;&nbsp;&nbsp;&nbsp;"hooks": {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"pre-commit": "pretty-quick --staged"<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
},*<br>

## VSCode

8. Install plugin "ESLint".

9. Install plugin "Prettier - Code formatter".

10. In VSCode -> Preferences -> Settings -> activate "Format on save".<br>
Or add in VSCode settings.json:<br>
*"editor.formatOnSave": true*

11. In VSCode -> Preferences -> Settings -> choose "Eslint: Node Path" and add your path to node.<br>
Or add in VSCode settings.json:<br>
*"eslint.nodePath": "C:\\your_path_here\\nodejs"*

12. In VSCode -> open a file to be formatted (any .ts, .tsx, etc. file) -> Ctrl+Shift+P -> type "Format Document With" -> choose Prettier as formatter.<br>
Or add in VSCode settings.json:<br>
*"[typescriptreact]": {<br>
&nbsp;&nbsp;&nbsp;&nbsp;"editor.defaultFormatter": "esbenp.prettier-vscode"<br>
},<br>
"[typescript]": {<br>
&nbsp;&nbsp;&nbsp;&nbsp;"editor.defaultFormatter": "esbenp.prettier-vscode"<br>
},*

## 

## Additional rules for ESLint
| Rule | Comment |
| ---- | ------- |
|"@typescript-eslint/indent": ["warn", 4]|Indentation style is 4 spaces.|
|"@typescript-eslint/semi": ["warn", "always"]|Missing semicolons are marked.|
|"@typescript-eslint/quotes": ["warn", "double"]|Only double quotes are allowed.|
|"@typescript-eslint/no-explicit-any": "error"|Type "any" is not allowed.|
|complexity: ["warn", 4]|Maximum cyclomatic complexity is 4.|

## Additional rules for Prettier
| Rule | Comment |
| ---- | ------- |
|"trailingComma": "es5",|Trailing commas are removed.|
|"tabWidth": 4,|Tab width is 4 spaces.|
| "semi": true,|Missing semicolons are added.|
|"singleQuote": false|Single quotes changed to double quotes.|
|"printWidth": 120|Maximum line length is 120.|
|"bracketSpacing": true|Spaces between brackets in object literals.|
|"jsxBracketSameLine": true|Sole ">" parentheses in a line is not allowed.|
|"arrowParens": "always"|Single arrow function paramters are surrounded by parentheses.|
|"endOfLine": "auto"|Line endings are changed to windows or unix, depending on the system currently running the code.|

## Supported Rules
| Rule | Recommended | Active | Type | Comment |
| ---- | ----------- | ------ | ---- | ------- |
| @typescript-eslint/adjacent-overload-signatures | [x] | [x] | warn | |
| @typescript-eslint/array-type | [] | [] | | |
| @typescript-eslint/await-thenable | [x] | [x] | error | |
| @typescript-eslint/ban-ts-comment | [x] | [x] | error | |
| @typescript-eslint/ban-tslint-comment | [] | [] | | |
| @typescript-eslint/ban-types | [x] | [x] | error | todo: add forbidden types |
| @typescript-eslint/class-literal-property-style |
| @typescript-eslint/consistent-indexed-object-style |
| @typescript-eslint/consistent-type-assertions |
| @typescript-eslint/consistent-type-definitions |
| @typescript-eslint/consistent-type-imports |
| @typescript-eslint/explicit-function-return-type |
| @typescript-eslint/explicit-member-accessibility |
| @typescript-eslint/explicit-module-boundary-types |
| @typescript-eslint/member-delimiter-style |
| @typescript-eslint/member-ordering |
| @typescript-eslint/method-signature-style |
| @typescript-eslint/naming-convention |
| @typescript-eslint/no-base-to-string |
| @typescript-eslint/no-confusing-non-null-assertion |
| @typescript-eslint/no-confusing-void-expression |
| @typescript-eslint/no-dynamic-delete |
| @typescript-eslint/no-empty-interface |
| @typescript-eslint/no-explicit-any |
| @typescript-eslint/no-extra-non-null-assertion |
| @typescript-eslint/no-extraneous-class |
| @typescript-eslint/no-floating-promises |
| @typescript-eslint/no-for-in-array |
| @typescript-eslint/no-implicit-any-catch |
| @typescript-eslint/no-inferrable-types |
| @typescript-eslint/no-invalid-void-type |
| @typescript-eslint/no-misused-new |
| @typescript-eslint/no-misused-promises |
| @typescript-eslint/no-namespace |
| @typescript-eslint/no-non-null-asserted-optional-chain |
| @typescript-eslint/no-non-null-assertion |
| @typescript-eslint/no-parameter-properties |
| @typescript-eslint/no-require-imports |
| @typescript-eslint/no-this-alias |
| @typescript-eslint/no-type-alias |
| @typescript-eslint/no-unnecessary-boolean-literal-compare |
| @typescript-eslint/no-unnecessary-condition |
| @typescript-eslint/no-unnecessary-qualifier |
| @typescript-eslint/no-unnecessary-type-arguments |
| @typescript-eslint/no-unnecessary-type-assertion |
| @typescript-eslint/no-unnecessary-type-constraint |
| @typescript-eslint/no-unsafe-assignment |
| @typescript-eslint/no-unsafe-call |
| @typescript-eslint/no-unsafe-member-access |
| @typescript-eslint/no-unsafe-return |
| @typescript-eslint/no-var-requires |
| @typescript-eslint/non-nullable-type-assertion-style |
| @typescript-eslint/prefer-as-const |
| @typescript-eslint/prefer-enum-initializers |
| @typescript-eslint/prefer-for-of |
| @typescript-eslint/prefer-function-type |
| @typescript-eslint/prefer-includes |
| @typescript-eslint/prefer-literal-enum-member |
| @typescript-eslint/prefer-namespace-keyword |
| @typescript-eslint/prefer-nullish-coalescing |
| @typescript-eslint/prefer-optional-chain |
| @typescript-eslint/prefer-readonly |
| @typescript-eslint/prefer-readonly-parameter-types |
| @typescript-eslint/prefer-reduce-type-parameter |
| @typescript-eslint/prefer-regexp-exec |
| @typescript-eslint/prefer-string-starts-ends-with |
| @typescript-eslint/prefer-ts-expect-error |
| @typescript-eslint/promise-function-async |
| @typescript-eslint/require-array-sort-compare |
| @typescript-eslint/restrict-plus-operands |
| @typescript-eslint/restrict-template-expressions |
| @typescript-eslint/strict-boolean-expressions |
| @typescript-eslint/switch-exhaustiveness-check |
| @typescript-eslint/triple-slash-reference |
| @typescript-eslint/type-annotation-spacing |
| @typescript-eslint/typedef |
| @typescript-eslint/unbound-method |
| @typescript-eslint/unified-signatures |

## Extension Rules
| Rule | Recommended | Active | Type | Comment |
| ---- | ----------- | ------ | ---- | ------- |
| @typescript-eslint/brace-style |
| @typescript-eslint/comma-dangle |
| @typescript-eslint/comma-spacing |
| @typescript-eslint/default-param-last |
| @typescript-eslint/dot-notation |
| @typescript-eslint/func-call-spacing |
| @typescript-eslint/indent |
| @typescript-eslint/init-declarations |
| @typescript-eslint/keyword-spacing |
| @typescript-eslint/lines-between-class-members |
| @typescript-eslint/no-array-constructor |
| @typescript-eslint/no-dupe-class-members |
| @typescript-eslint/no-duplicate-imports |
| @typescript-eslint/no-empty-function |
| @typescript-eslint/no-extra-parens |
| @typescript-eslint/no-extra-semi |
| @typescript-eslint/no-implied-eval |
| @typescript-eslint/no-invalid-this |
| @typescript-eslint/no-loop-func |
| @typescript-eslint/no-loss-of-precision |
| @typescript-eslint/no-magic-numbers |
| @typescript-eslint/no-redeclare |
| @typescript-eslint/no-shadow |
| @typescript-eslint/no-throw-literal |
| @typescript-eslint/no-unused-expressions |
| @typescript-eslint/no-unused-vars |
| @typescript-eslint/no-use-before-define |
| @typescript-eslint/no-useless-constructor |
| @typescript-eslint/quotes |
| @typescript-eslint/require-await |
| @typescript-eslint/return-await |
| @typescript-eslint/semi |
| @typescript-eslint/space-before-function-paren |
| @typescript-eslint/space-infix-ops |
