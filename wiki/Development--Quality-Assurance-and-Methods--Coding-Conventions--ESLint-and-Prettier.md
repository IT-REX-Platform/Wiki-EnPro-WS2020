# How to setup ESLint and Prettier in a project in VSCode from zero
(If you cloned a project that uses ESLint and Prettier, then go to **6.** to activate those features in your VSCode.)

## ESLint

1. Install core ESLint library, ESLint TypeScript parser (to allow ESLint to lint TypeScript code) and ESLint TypeScript plugin (which contains some TypeScript-specific ESLint rules).<br>
*npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin*

2. Create .eslintrc file, select options that fit the project.<br>
*npx eslint --init*

3. Create .eslintignore file, insert file/folder names to be ignored by ESLint.

## Prettier

4. Install Prettier, eslint-config-prettier (to disable linting rules that might interfere with an existing Prettier rule) and eslint-plugin-prettier (to run Prettier analysis as part of ESLint).<br>
*npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier*

5. Create .prettierrc.json, insert rules to be applied when formatting.

## VSCode

6. Install plugin "ESLint".

7. Install plugin "Prettier - Code formatter".

8. In VSCode -> Preferences -> Settings -> activate "Format on save".<br>
Or add in VSCode settings.json: *"editor.formatOnSave": true*

9. In VSCode -> Preferences -> Settings -> choose "Eslint: Node Path" and add your path to node.<br>
Or add in VSCode settings.json: *"eslint.nodePath": "C:\\your_path_here\\nodejs"*

10. In VSCode -> open a file to be formatted (any .ts, .tsx, etc. file) -> Ctrl+Shift+P -> type "Format Document With" -> choose Prettier as formatter.<br>
Or add in VSCode settings.json:<br>
*"[typescriptreact]": {<br>
&nbsp;&nbsp;"editor.defaultFormatter": "esbenp.prettier-vscode"<br>
},<br>
"[typescript]": {<br>
&nbsp;&nbsp;"editor.defaultFormatter": "esbenp.prettier-vscode"<br>
},<br>
"[jsonc]": {<br>
&nbsp;&nbsp;"editor.defaultFormatter": "esbenp.prettier-vscode"<br>
}*


