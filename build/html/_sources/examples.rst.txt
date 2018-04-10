.. Jibia Docs documentation master file, created by
   sphinx-quickstart on Tue Apr 10 20:35:52 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
   
Examples
====================================   

Javascript example
=====================
Here's an example in javascript of how to implement our API into your service:
::

	window.onload = addevent;
	function addevent () {
		window.onmessage = function(event){
		recom(event.data);
		};
	}
	recom = (ident) => {
		var req = new XMLHttpRequest();
		req.open('POST', decodeURIComponent('http://146.185.174.192:80/api/recommend'), true);
		var params = {"identifier": ident, "n" : NUMBER_OF_ITEMS, "product_id" : ID_OF_CURRENT_PRODUCT, "language": LANGUAGE};
		req.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
		req.send(JSON.stringify(params));
		req.onreadystatechange = function () {
			var ans = JSON.parse(req.responseText)['result']
			document.getElementById('test').innerHTML = ans[0]['title'];
			document.getElementById('img').src = ans[0]['img'];
		}
	}

