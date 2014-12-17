FORMAT: 0a

# Fake Catalog API
Fake API is an API that doesn't exist except in document form. It basically mimics what we do now, not what the Catalog API should eventually look like.

## Authentication
Why would you try to authenticate to an API that doesn't exist? I guess we need a secret password? How about "whoa_bundy"?

## Colors
All API responses are sent in black text on a white background. Programs will not care about this distinction, but manual tests against the API and API calls made by hand may.

## Other General API Details
There are other things you might want to know about this API at the service level and this is where they'd go.

# Artwork

This section describes the artwork resource interface.

## Post [/products/{product_id}/]
A post is a singular piece of art, independent of product context (such as image dimension constraints, etc.).

+ Parameters
    + product_id (string, `1`) ... The id of a product.

+ Model (application/json)

    ```js
    {
        "data": {
            "id": "1", // This is a string even though it appears as an integer
            "artist": {
                ...
            },
            "created_at" : "2012-07-16T17:25:47z",
            "name": "the price of gas",
            "promoted": 582,
            "wishlisted": 1029,
            "description": "The price of gas keeps on rising, but ...",
            "comments": [ // DEPRECATED, use Comments resource
                {"commenter": "1",
                 "commented_at": "2014-12-16T13:08:15z",
                 "comment": "I like this piece of art",
                },
                ...
            ],
            "available_as": [ // List of product type IDs
                1, // Prints
                2, // Framed Prints
                8, // T-Shirts (Men's)
                9, // T-Shirts (Women's)
                17, // Clocks
            ],
            "disabled_colors": [ // List of disabled color IDs
                0, // Black - disable black-on-black
            ],
        },
        "meta": {
            "code": 200,
        }
    }
    ```

### Retrieve a Post [GET]
Returns a specific post.

+ Response 200

    [Post][]

### Update a Post [POST]
Update a post. Updates from the artist that owns the post can modify the description, available products, and disabled colors. Updates from an authorized app may increment the promoted and wish-listed counters, add additional comments.

+ Request

    [Post][]

+ Response 200

    [Post][]

### Delete a Post [POST]
Delete a post. Can only be done by the owning user.

+ Response 204
