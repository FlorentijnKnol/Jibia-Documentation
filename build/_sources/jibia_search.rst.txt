.. Jibia Docs documentation master file, created by
   sphinx-quickstart on Tue Apr 10 20:35:52 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
   
Search
====================================   

Simple HTML Example
=============================
This javascript example shows how to implement jibia's search bar. The search bar should have 'searchbar' as its id like this:

::

	<input type="name" id = "searchbar" class = "zoekbalk" name="Search" placeholder="Zoekbalk van Jibia"></input>
	
To show the autocomplete results you need an empty div under this input field.

::

    <div id="data"></div>

This div will be filled with the search results. To finalize the implementation add the following script tag to
the bottom of your html document. Insert your own jibia search token in the token attribute:

::

	<script src="js/jibia_search.js" token="YOUR TOKEN HERE"/>

The only thing left to do now is downloading jibia_search.js and adding this file to your js folder. Once this is done the
search bar should be up and running. 

Besides the token parameter, several other parameters can be set in the script tag above. These are detailed below.
		
.. glossary::

    styled
      This value can be set to true or false.  If this is set to true the search results will use predefined style. The parameter defaults to true.

    result_classname
      This parameter can be set to define the class name for autocomplete suggestions. This parameter defaults to "search_result".
	  

Example of manual autocomplete handling
=============================

If you wish to have more control over what happens under the hood, instead you can write the logic for this yourself.
To do this you first have to load your product feed into Jibia. You can do that with the following request:

::

	curl -X POST \
	  https://api.jibia.nl/api/initialize_search \
	  -H 'Content-Type: application/json' \
	  -d '{"feed_url": FEED_URL}'
	
.. glossary::

    feed_url
      The URL to your product feed.
	  
This request returns a token you can use for the search. Save this token somewhere. It might take several minutes before your feed is fully initialized.

The autocomplete can be called with the following request:

::

	curl -X GET \
	  'https://api.jibia.nl/api/do_search?query={QUERY}&token={TOKEN}&n={N}' 

.. glossary::

    query
      The query for the autocomplete.

    token
	  The token from the response of your call to initialize_search
	  
	n
	  The amount of autocomplete results
	  
This request will return a list of products.
	 