# WP-REST-API-Nuggets
Just a few useful (useless?) things.

## Adding Pages
Just a simple script to create pages on the fly. It assumes you have an array of titles.
```
(function($) {
    let pages = [
        'Some Page',
        'Hey Another Page!!!',
        'Whaaat???',
    ];

    function addPages(pageArray){
        // Create a page with the WordPress REST API

        // You don't have to set these here. I just wanted all my pages published from the outset
        // There's also all the other parameters, if you want to be all like that...
        // https://developer.wordpress.org/rest-api/reference/pages/#create-a-page
        let data = {};
        data.status = 'publish';
        data.type = 'page'; // or 'post' if you'd like.
        
        pageArray.forEach(page => {
            data.title = page;
            data.content = `I am the ${page} content`; // You don't have to set this here, I just wanted some content.
            $.ajax({
                method: "POST",
                url: restapi_details.rest_url + 'wp/v2/pages',
                data: data,
                beforeSend: function ( xhr ) {
                    xhr.setRequestHeader( 'X-WP-Nonce', restapi_details.nonce );
                },
                success : function( response ) {
            
                    // Save the page ID in case you need it for something
            
                    var myNewPageID = response.id;
            
                }
            });
            
        });
        
    }
    // I fired this on page load,  but you might want to do some testing *first* ;) 🤠
    // addPages(pages);

})(jQuery);
```