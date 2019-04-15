.. Jibia Docs documentation master file, created by
   sphinx-quickstart on Tue Apr 10 20:35:52 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
   
Search
====================================   

HTML implementation
=============================

This javascript example shows how to implement jibia's search bar. The search bar should have 'searchbar' as its id like this:

::

	<input type="name" id = "formSearch" class = "zoekbalk" name="Search" placeholder="Zoekbalk van Jibia"></input>
	
	
Adding the following script tag to your html will make autocomplete results appear under this search bar.	

::

	<script src="https://cdn.jsdelivr.net/gh/stijnvalkenburg/Jibia-search/search.js" token="cd2957a67f78a76a50c94666e21891"/>

.. glossary::

    token
	  Your authentication token.
	  	
	

Styling autocomplete results
===============================

To use our default styling of autocomplete results, you can add the following tag to the bottom of your html file:

::

	<link rel ='stylesheet' href = 'https://cdn.jsdelivr.net/gh/stijnvalkenburg/Jibia-search//search.css'/>

You can style the autocomplete results as well. The list of autocomplete results has the class name "search_auto". The products inside this list have "search_element product_element" as their class name.
	  
Manually handling autocomplete
===============================

If you wish to have more control over how the products are being handles, you can write the logic for this yourself.
The autocomplete can be called with the following request:

::

	curl -X GET \
	  'https://api.jibia.nl/api/do_search?query={QUERY}&token={TOKEN}&n={N}' 

.. glossary::

    query
      The query for the autocomplete

    token
	  Your authentication token
  
    n
	  The amount of autocomplete results
	  
This request will return the products matching the query. The json with products is formatted like this:

::
	
	{
		"result": {
			"products": [
				{
					"product": {
						"img_url": "https://jibia-shop.nl/media/test_product1.png",
						"name": "Test Product 1",
						"url": "https://jibia-shop.nl/products/test_product1.html"
					}
				}
			],
			"words": [
				"trefwoord"
			]
		}
	}	
	
.. glossary::

    img_url
      The product thumbnail url

    name
	  The name/title of the product

    url
      The url suffix for the product

    words
	  A set of keywords that fit the query
	  
	  