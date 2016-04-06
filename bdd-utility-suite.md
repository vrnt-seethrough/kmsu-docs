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




##Search utils

The search utils provide methods for performing searches and retrieving metadata about searches which have been performed.

###fetchLastQueryData( callback )

Performs the last executed UI search against the API and returns the expanded data (first node only).

###fetchLastQueryMetadata( callback )

Performs the last executed UI search against the API and returns metadata about the results.

####Results
| Property | Examples | Description |
|-|-|-|
| totalPages | 4 | Number of total pages of results given the current search page size |
| totalItems | 34 | Number of items in total (not just for the current page) |
| page | 0 | Zero-based page number of the current set of results |
