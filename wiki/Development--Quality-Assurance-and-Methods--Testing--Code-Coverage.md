# How to activate code coverage tool to visually display method/statement/decision coverage

1. In VSCode install extension "Coverage Gutters" (ryanluker.vscode-coverage-gutters).

2. In VSCode add to your settings.json:<br>
```json
    "coverage-gutters.showLineCoverage": true
```

3. Create coverage report.<br>
*npm run test*

4. In VSCode click on "Watch" left on the bottom blue bar to display code coverage.



