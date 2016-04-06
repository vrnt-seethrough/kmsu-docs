#Search utils

The search utils provide methods for performing searches and retrieving metadata about searches which have been performed. This utility object is available within the scenario context as <code>this.search</code>

##fetchLastQueryData( callback )

Performs the last executed UI search against the API and returns the expanded data (first node only).

##fetchLastQueryItems( callback )

Performs the last executed UI search against the API and returns information about the matched results.

So far the included properties are limited to:

| Property | Examples | Description |
|-|-|-|
| synopsis | To change a customer's address: Identify the customer Complete data protection verification. Click on 'Edit Customer' on the customer's entry on the left panel. Select to edit Home or Work address. On the pop-up click on 'Search for Address' Search for the... | The synopsis of a search result |
| title | Changing Customer's Address | The title of the search result |
| docTypes | [ "article" ], [ "knowledgedocument", "faq" ] | The types of the search result |
Example:

```
this.Given(/^each item's synopsis and content\-type icon are also displayed$/, function (callback) {

        var items = this.browser.queryAll( ".search-result" ).map( x => ( {

            synopsis: x.querySelector( ".search-result-synopsis" ).innerHTML,
            title: x.querySelector( ".search-result-header" ).textContent,
            classes: x.getAttribute( "class" )

        } ) );
        this.search.fetchLastQueryItems( ( e, apiItems ) => {

            if ( e ) { callback( e ); } else {

                items.length.should.eql( apiItems.length );
                items.forEach( item => {

                    var apiItem = apiItems.find( x => x.title === item.title );
                    should.exist( apiItem, "Couldn't find an item returned from the API matching the on-screen item with title: " + item.title );
                    apiItem.synopsis.should.eql( apiItem.synopsis );
                    should.exist(

                        apiItem.docTypes.find( t => ~item.classes.indexOf( "search-result-" + t ) ),
                        "Couldn't find a match between the search result type (" + item.classes + ") and the api type (" + apiItem.docTypes + ")"

                    );
                    callback();

                } );

            }

        } );


    } );
```
##fetchLastQueryMetadata( callback )

Performs the last executed UI search against the API and returns metadata about the results.

###Results

| Property | Examples | Description |
|-|-|-|
| totalPages | 4 | Number of total pages of results given the current search page size |
| totalItems | 34 | Number of items in total (not just for the current page) |
| page | 0 | Zero-based page number of the current set of results |
