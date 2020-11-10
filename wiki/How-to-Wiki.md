# How to Wiki

This wiki page is about creating pages like this one in a way that they appear in the correct position in the navigation, that you can admire on the right.

Wiki pages can be written in various markup languages, but we use *GitHub Flavored Markdown*. Linking to other pages can either be done with absolute Hyperlinks (i.e. [https://github.com/IT-REX-Platform/Wiki/wiki/Glossary](https://github.com/IT-REX-Platform/Wiki/wiki/Glossary)) or with relative links (i.e. [./Glossary](./Glossary)). The latter is preferred.

The position in the navigation tree is determined by the name of the markdown file. The file name is specified by the following EBNF:

``` ebnf
FileName = {Category}, STRING, ".md";
Category = STRING, "+-";
```

White spaces are not allowed and "+-" separates categories. The name that is displayed in the navigation is parsed from the last part of the fime name. "-" are exchanged by white spaces.

**Important note**: The GitHub Action that creates the navigation and pushes the changes to the real wiki repository (GitHub uses another repository to display the wiki pages) is only triggered when something changes in the /wiki directory and only if the changes are pushed to the so called ["main"](https://www.zdnet.com/article/github-to-replace-master-with-main-starting-next-month/) branch.
