# How to setup ESLint and Prettier in a project in VSCode from zero
ATTENTION: If you cloned a project that uses ESLint and Prettier, then go to **8.** to activate those features in your VSCode.

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

5. Create .prettierrc.json, add rules to be applied when formatting: [Prettier options](https://prettier.io/docs/en/options.html).

## Git hook

6. Add git hook that will format changed files to be commited.<br>
*npm install --save-dev pretty-quick husky*

7. Add pre-commit hook to package.json.<br>
```json
    "husky": {
        "hooks": {
            "pre-commit": "pretty-quick --staged"
        }
    },
```

## VSCode

8. In VSCode -> extensions marketplace -> install plugin "ESLint" (dbaeumer.vscode-eslint).

9. In VSCode -> extensions marketplace -> install plugin "Prettier - Code formatter" (esbenp.prettier-vscode).

10. In VSCode -> Preferences -> Settings -> activate "Format on save".<br>
Or add in VSCode settings.json:
```json
  "editor.formatOnSave": true,
```

11. In VSCode -> Preferences -> Settings -> choose "Eslint: Node Path" and add your path to node.<br>
Or add in VSCode settings.json:
```json
  "eslint.nodePath": "C:\\your_path_here\\nodejs",
```

12. In VSCode -> open a file to be formatted (any .ts, .tsx, etc. file) -> Ctrl+Shift+P -> type "Format Document With" -> choose Prettier as formatter.<br>
Or add in VSCode settings.json:
```json
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
```

## Addendum

**Additional rules for ESLint:**
| Rule | Comment |
| ---- | ------- |
|"@typescript-eslint/indent": ["warn", 4]|Indentation style is 4 spaces.|
|"@typescript-eslint/semi": ["warn", "always"]|Missing semicolons are marked.|
|"@typescript-eslint/quotes": ["warn", "double"]|Only double quotes are allowed.|
|"@typescript-eslint/no-explicit-any": "error"|Type "any" is not allowed.|
|complexity: ["warn", 4]|Maximum cyclomatic complexity is 4.|

**Additional rules for Prettier:**
| Rule | Comment |
| ---- | ------- |
|"trailingComma": "es5",|Trailing commas are removed.|
|"tabWidth": 4,|Tab width is 4 spaces.|
| "semi": true,|Missing semicolons are added.|
|"singleQuote": false|Single quotes changed to double quotes.|
|"printWidth": 120|Maximum line length is 120.|
|"bracketSpacing": true|Spaces between brackets in object literals.|
|"jsxBracketSameLine": true|A sole ">" parentheses in a line is not allowed.|
|"arrowParens": "always"|Single arrow function parameters are surrounded by parentheses.|
|"endOfLine": "auto"|Line endings are changed to windows or unix, depending on the system currently running the code.|
