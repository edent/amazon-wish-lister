# Amazon Wish Lister

This is a little API to retrieve Amazon Wish List data. There is no official API, as Amazon shut it down a couple years ago. The only way around that... screen scraping!

## Installation

The two files `wishlist.php` and `phpquery.php` will need to be placed on a webserver running [PHP](https://php.net).

If you do not have a webserver, you can use the [free servers at 000WebHost](https://www.000webhost.com/921806.html).

## Basic Usage

A normal Amazon wishlist URL looks like this - https://www.amazon.co.uk/gp/registry/wishlist/13GFCFR2B2IX4/

(That's my personal wishlist - feel free to buy me something nice!)

To get an RSS feed, you'll need to know two things.

1. The Wishlist ID.
2. Which country's Amazon store you're using.

The Wishlist ID is the jumble of letters and number after `/wishlist/` -  in this example, it is `13GFCFR2B2IX4`.

The country is the bit after `www.amazon.` - in this example, it is `co.uk`

In your web browser, visit

`http://YOURSITE/wishlist.php?tld=co.uk&id=13GFCFR2B2IX4&format=rss`

You should now see an RSS feed with all your wishlist items.

## Options

### Amazon Country
`?tld=AMAZON_COUNTRY`
`?tld=co.uk`

Defaults to `com`.

Tested with: `ca`, `com`, `com.br`, `co.jp`, `co.uk`, `es`, `de`, `fr`, `in`, `it`.

The following stores currently do not offer wishlists: `com.au`, `com.mx`, `nl`.

### Amazon ID
`?id=YOUR_AMAZON_ID`
`?id=13GFCFR2B2IX4`

### Reveal (What to get)
`?reveal=unpurchased` (Default)
`?reveal=all`
`?reveal=purchased`

### Sort
`?sort=date` (Default)
`?sort=priority`
`?sort=title`
`?sort=price-low`  (low to high)
`?sort=price-high` (high to low)
`?sort=updated`

### Output Format
`?format=json` Valid JSON (Default).
`?format=xml` Invalid XML (included for compatibility reasons).
`?format=XML` Valid XML.
`?format=array` a PHP array.
`?format=rss` an RSS feed.

## Amazon Associate / Affiliate tag
`?tag=affiliate-tag`  Allows you to earn money using Amazon's Affiliate programme

### Example
`wishlist.php?id=37XI10RRD17X2&reveal=all&sort=priority&format=json`
`wishlist.php?tld=co.uk&id=13GFCFR2B2IX4&tag=shkspr-21`

What it returns
===============

Below is an example if you had http://amzn.com/B0002FTH66 on your wishlist (item #37 on your wishlist).

    [
        {
            "num": 37,
            "name": "Scotch Box Sealing Tape Dispenser H180, 2 in",
            "link": "http://www.amazon.com/Scotch-Sealing-Tape-Dispenser-H180/dp/B0002FTH66/ref=wl_it_dp_v_nS_nC/185-8110132-3235609?ie=UTF8&colid=3DR0P4HP87IIJ&coliid=I19JS64ZHWBA5M",
            "old-price": "$24.09",
            "new-price": "$19.99",
            "date-added": "June 7, 2012",
            "priority": "low",
            "rating": "4.7 out of 5 stars",
            "total-ratings": "63",
            "comment": "I like taping stuff",
            "picture": "http://ecx.images-amazon.com/images/I/41BKbZu836L._SL500_SL135_.jpg",
            "page": 2,
            "AISN": "B0002FTH66",
            "large-ssl-image": "https://images-eu.ssl-images-amazon.com/images/I/41BKbZu836L._SL500_SL1350_.jpg",
            "affiliate-url": "http://www.amazon.com/dp/B0002FTH66/ref=nosim?tag=yourid-21"
        }
    ]


## Further information

Amazon Wish Lister uses [phpQuery](http://code.google.com/p/phpquery/) (server-side CSS3 selector driven DOM API based on jQuery) to scrape Amazon's Wish List page and exports to JSON, XML, RSS, or PHP Array Object.

* Scrapes the following from your Amazon Wish List:
    1. Item name
    2. Item link
    3. Price of item when added to wish list
    4. Current price of item
    5. Date added to wish list
    6. Priority (set by you)
    7. Item rating
    8. Total ratings
    9. Comments on item (set by you)
    10. Picture of item
* Perfect if you want to host display your wish list on your own website.
* Best used if cached, or saved in database.
* Supports multi-page Amazon Wish Lists as well as Amazon Wish List "Ideas"
* Return list as JSON, XML, or just dump PHP Array Object.

You can read more about the project on my blog https://shkspr.mobi/blog/2015/11/an-api-for-amazon-wishlists/
