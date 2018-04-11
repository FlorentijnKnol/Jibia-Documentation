.. Jibia Docs documentation master file, created by
   sphinx-quickstart on Tue Apr 10 20:35:52 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
   
Examples
====================================   

Simple Javascript/XHR-example
=============================
This javascript example shows how to interact with a Jibia user and our API. In this example Jibia recommendations are only used
when the current visitor is connected to Jibia. The examples that follow go into using or services even when the user is not
using the Jibia extension. Because we use HMAC authentication we need logic for making our hashes. In this example we use 
https://github.com/Caligatio/jsSHA. The package is available through NPM. Install it with the following command:
::

	npm install jssha

This example uses XMLHttpRequest for the API request. In the examples after this one we will show the logic using Fetch.

::

	window.onload = addevent;
	function addevent () {
		window.onmessage = function(event){
		recom(event.data);
		};
	}
	recom = (ident) => {
		var ts = Date.now();
		var shaObj = new jsSHA("SHA-1", "TEXT");
		shaObj.setHMACKey(API_SECRET, "TEXT");
		shaObj.update(API_KEY+ts);
		var hmac = shaObj.getHMAC("HEX");
		var req = new XMLHttpRequest();
		req.open('POST', decodeURIComponent('http://146.185.174.192:80/api/recommend'), true);
		var params = {"identifier": ident, "n" : NUMBER_OF_ITEMS, "k": NUMBER_OF_CLUSTERS, 
			"product_id" : ID_OF_CURRENT_PRODUCT, "language": LANGUAGE, "key":
			API_KEY, "nonce":ts};
		req.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
		req.setRequestHeader('sign', hmac);
		req.send(JSON.stringify(params));
		req.onreadystatechange = function () {
			var ans = JSON.parse(req.responseText)['result']
			document.getElementById('test').innerHTML = ans[0]['title'];
			document.getElementById('img').src = ans[0]['img'];
		}
	}

	
.. glossary::
	
	ident:
		This is the user identifier passed to your web page from the user's extension. It's used to identify the user internally.
		
	NUMBER_OF_ITEMS:
		The amount of recommendation-items you wish to display
		
	NUMBER_OF_CLUSTERS:
		The amount of the users "interest-clusters" being used for the recommendation. A higher number will result in more general
		recommendations, while a lower number will result in the recommendations being more specific to the user's biggest interests.
		
	ID_OF_CURRENT_PRODUCT:
		The identifier that represents the product the user is currently viewing. This should correspons to the identifiers in 
		the uploaded product-csv. If you haven't yet uploaded this csv yet, you can do this at http://jibia.nl/business/dashboard.
		
	LANGUAGE:
		The language of your website. Currently only Dutch and English are supported. We will start supporting more languages in the
		near future.