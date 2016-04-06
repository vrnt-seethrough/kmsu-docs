#BDD utility suite

##Article view utils

The article view utils are available in the scenario context as <code>this.articleView</code>

###skipTo( section, callback )

Skip to one of the fragments of the currently viewed article. This will result in a new fragment selector in the current URL.

| Argument | Examples | Description |
|--|--|--|
| section | Private / public / tag / tags / file | Text contained in one of the "Skip To:" links |

