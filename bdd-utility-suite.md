#BDD utility suite

##Article view utils

The article view utils are available in the scenario context as <code>this.articleView</code>

###skipTo( section, callback )

Skip to one of the fragments of the currently viewed article. This will result in a new fragment selector in the current URL.

| Argument | Examples | Description |
|--|--|--|
| section | Private / public / tag / tags / file | Text contained in one of the "Skip To:" links |

Example:

```
this.Given(/^I am viewing the private information section of a content item with title "([^"]*)"$/, function ( title, callback) {

        async.series( [

            done => this.search.performSearch( title, 999, done ),
            done => this.searchResults.selectResult( title, done ),
            done => this.articleView.skipTo( "private", done )

        ], callback );

    } );
```
