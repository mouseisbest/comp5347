
# æŠ¼é¢˜
---
## week 1 how web works
- protocol is a set of rules that partners in communication use when they communicate.
- TCP ensures that transmissions arrive, in order, and without error
- request methods: HTTP/1.0(GET, POST, HEAD) & HTTP/1.1(GET, POST, HEAD, PUT, DELETE)
- HTTP Response status code: 1XX, 2XX, 3XX, 4XX, 5Xx
- RTT: time to send a small packet to travel from client to server and back.
- â€“	Response time:  
one RTT to initiate TCP connection  
one RTT for HTTP request and first few bytes of HTTP response to return  
file transmission time  
total = 2RTT+transmit time  
- TTFB: time to first byte: one RTT plus server processing time.
- persistent HTTP: HTTP é•¿è¿žæŽ¥ï¼Œ 1.1é»˜è®¤
- caching in HTTP <span style="color: red">(important)</span>
	``` 
	- goal of caching:
		- Eliminate the need to send requests in many cases
			- reduce the number of network round-trips required for many operations
			- an "expiration" mechanism
		- Eliminate the need to send full responses in many other cases
			- reduce network bandwidth requirements
			- a "calidation" mechanism
	- level of caches: server side, client side (proxy and browser)
	- cache correctness: 
		- It has been checked for equivalence with what the origin server would have returned by revalidating the response with the origin server å‘é€è¯·æ±‚ç»™æºæœåŠ¡å™¨ï¼Œé—®å®ƒå¦‚æžœè¦è¿”å›žï¼Œä¼šè¿”å›žå“ªä¸ªç‰ˆæœ¬çš„å†…å®¹ï¼Œå¹¶ä¸Žæœ¬åœ°å¯¹æ¯”
	- It is "fresh enough". In the default case, this means it meets the least restrictive freshness requirement of the client, origin server, and cache éœ€è¦æœ€æ–°çš„é‚£ä¸ªç‰ˆæœ¬çš„æ•°æ®
	- It is an appropriate 304 (Not Modified), 305 (Proxy Redirect), or error (4xx or 5xx) response message 
	- expiration model è¿‡æœŸæ¨¡åž‹
		- server-specified expiration æœåŠ¡ç«¯æŒ‡å®šè¿‡æœŸæ—¶é—´ï¼šCache-Control: no-cache; Cache-Control: max-age=60
		- heuristic expiration å¯å‘å¼ç¼“å­˜
	- validation model
		- When a cache has a staleé™ˆè…çš„ entry that it would like to use as a response to a clients request, it first has to check with the origin server (or possibly an intermediate cache with a fresh response) to see if its cached entry is still usable å…ˆå‘é€ä¸€ä¸ªå°å¼€é”€çš„è¯·æ±‚è¯¢é—®å½“å‰ç‰ˆæœ¬çš„ç¼“å­˜æ˜¯å¦å¯ç”¨ï¼Œå¯ç”¨åˆ™å¯èŠ‚çœå¼€é”€ï¼Œä¸å¯ç”¨åˆ™å¤šä¸€ä¸ªRTTçš„å¼€é”€
		- No overhead of re-transmitting the whole response when the entry is valid, but incurs overhead in RTT.
		- æ„Ÿè§‰å°±è€ƒå‰é¢çš„ï¼Œä¸»è¦æ˜¯è¿‡æœŸæ¨¡åž‹çš„åŽŸç†
		- last-modified dates:
		- entiry tage cache validators: Entity tags are used for comparing two or more entities from the same requested resource
		- requestor side:
			- if-match
			- if-none-match
			- if-modified-since
	```
---
## week 2 HTML & CSS
- HTML 5
	- syntax: å¯ä»¥åµŒå¥—(nested)ï¼Œä¸å¯ä»¥äº¤å‰(cross)
	- structure: <html><head>...</head><body>...</body></html>
	- quick tour: 
		- link: 
			```<a href="javascript:doSomething()"></a>```
		- list: ä¸¤è€…å¯ä»¥äº’ç›¸åµŒå¥—
			```
			//unordered list
			<ul>
				<li></li>
				<li></li>
			</ul>
			//ordered list
			<ol>
				<li></li>
				<li></li>
			</ol>
			```
	- HTML5 new semantic tags: <span style="color: red">(important)</span>
		- ```<article>, <section>, <header>, <footer>, <aside>```
		- ```<nac>``` navigation
- CSS: cascading style sheets
	- ```selector {declaration, declaration}``` , each declaration: ```property:value```
	- relative vs absolute measurement 
	- inline: <span style="color: red">(important)</span>
		- ```<h1 style="font-family:console; color:red">hello world</h1>```
		- åœ¨htmlä¸­çš„å®žä¾‹ï¼š<h1 style="font-family:console; color:red">hello world</h1>
	- external: <span style="color: red">(important)</span>
		- ```<link href="path/style.css" rel="stylesheet">```
	- browser has a default set of rules, user style sheet can overwrite default css.
	- cascading (principle to resolve conflicting style rules)
		- inheritance ç»§æ‰¿
			- å­æ ‡ç­¾ç»§æ‰¿çˆ¶æ ‡ç­¾çš„å±žæ€§
		- specificity ç‰¹å¼‚æ€§
			- å­å±žæ€§overrideçˆ¶å±žæ€§
		- location å®šä½
			- å¦‚æžœç»§æ‰¿å±žæ€§å’Œç‰¹å¼‚å±žæ€§æ²¡æœ‰æŒ‡å®šä¼˜å…ˆçº§æ—¶ï¼Œå°±è¿‘åŽŸåˆ™ï¼Œè°è¿‘ç”¨è°
	- selector
		- grouped selector
		- class selector
		- id selector
		- pseudo selector
		- contextual selector
	- box model ä¸‡ç‰©çš†ç›’ (every element in web design is a rectangular box)<span style="color: red">(important)</span>
		![box](./img2/box-model.svg)
		- background: ```repeat, no-repeat, repeat-y, repeat-x```
		- margin/padding å‚æ•°ä¸ªæ•°åˆ†åˆ«ä¸º1, 2, 3, 4æ—¶: 
			- 4: ä¾æ¬¡ä¸Šå³ä¸‹å·¦ top-right-bottom-left é¡ºæ—¶é’ˆ
			- 3: ä¾æ¬¡ä¸Šï¼Œå·¦å³ï¼Œä¸‹
			- 2: ä¾æ¬¡ä¸Šä¸‹ï¼Œå·¦å³
			- 1: ä¸Šä¸‹å·¦å³
		- collapsing margin
			- å½“ä¸¤ä¸ªæˆ–æ›´å¤šä¸ªåž‚ç›´è¾¹è·ç›¸é‡æ—¶ï¼Œ å®ƒä»¬å°†å½¢æˆä¸€ä¸ªå¤–è¾¹è·ã€‚è¿™ä¸ªå¤–è¾¹è·çš„é«˜åº¦ç­‰äºŽä¸¤ä¸ªå‘ç”Ÿå åŠ çš„å¤–è¾¹è·çš„é«˜åº¦ä¸­çš„è¾ƒå¤§è€…ã€‚ä½†æ˜¯æ³¨æ„åªæœ‰æ™®é€šæ–‡æ¡£æµä¸­å—æ¡†çš„åž‚ç›´å¤–è¾¹è·æ‰ä¼šå‘ç”Ÿå¤–è¾¹è·å åŠ ã€‚ è¡Œå†…æ¡†ã€ æµ®åŠ¨æ¡†æˆ–ç»å¯¹å®šä½æ¡†ä¹‹é—´çš„å¤–è¾¹è·ä¸ä¼šå åŠ ã€‚ä¸€èˆ¬æ¥è¯´ï¼Œ åž‚ç›´å¤–è¾¹è·å åŠ æœ‰ä¸‰ç§æƒ…å†µï¼š
				- å…ƒç´ è‡ªèº«å åŠ  å½“å…ƒç´ æ²¡æœ‰å†…å®¹ï¼ˆå³ç©ºå…ƒç´ ï¼‰ã€å†…è¾¹è·ã€è¾¹æ¡†æ—¶ï¼Œ å®ƒçš„ä¸Šä¸‹è¾¹è·å°±ç›¸é‡äº†ï¼Œ å³ä¼šäº§ç”Ÿå åŠ ï¼ˆåž‚ç›´æ–¹å‘ï¼‰ã€‚ å½“ä¸ºå…ƒç´ æ·»åŠ å†…å®¹ã€ å†…è¾¹è·ã€ è¾¹æ¡†ä»»ä½•ä¸€é¡¹ï¼Œ å°±ä¼šå–æ¶ˆå åŠ ã€‚
				- ç›¸é‚»å…ƒç´ å åŠ  ç›¸é‚»çš„ä¸¤ä¸ªå…ƒç´ ï¼Œ å¦‚æžœå®ƒä»¬çš„ä¸Šä¸‹è¾¹è·ç›¸é‡ï¼Œå³ä¼šäº§ç”Ÿå åŠ ã€‚
				- åŒ…å«ï¼ˆçˆ¶å­ï¼‰å…ƒç´ å åŠ  åŒ…å«å…ƒç´ çš„å¤–è¾¹è·éš”ç€ çˆ¶å…ƒç´ çš„å†…è¾¹è·å’Œè¾¹æ¡†ï¼Œ å½“è¿™ä¸¤é¡¹éƒ½ä¸å­˜åœ¨çš„æ—¶å€™ï¼Œ çˆ¶å­å…ƒç´ åž‚ç›´å¤–è¾¹è·ç›¸é‚»ï¼Œ äº§ç”Ÿå åŠ ã€‚ æ·»åŠ ä»»ä½•ä¸€é¡¹å³ä¼šå–æ¶ˆå åŠ ã€‚
	- text styling:
		- font-family: ä¾æ¬¡é€‰æ‹©ï¼Œå‰ä¸€é¡¹ä¸å¯ç”¨åˆ™ä½¿ç”¨åŽä¸€é¡¹  
		```p {font-family: Cambria, Georgia, "Times New Roman", serif;}```
		- size: ```em``` å±žæ€§ï¼ŒæŒ‡elementï¼Œrelative sizeï¼ŒæŒ‡ç›¸å¯¹è¯¥å…ƒç´ çš„å¤§å°(40%, 100%, 200%)  
		```rem``` å±žæ€§: 1rem=16px, pxè·Ÿè®¾å¤‡å’Œcssæœ‰å…³
---
## week 3 table/form and js <span style="color: red">(important)</span>
### table
- å®Œæ•´tableä»£ç åŠç¤ºä¾‹
	- ä»£ç 
	```
	<table border="1" cellpadding="10">
		<caption>19th century french paintings</caption>
		<col class="artistName"/>
		<colgroup id="paintingColumns">
			<col />
			<col />
		</colgroup>
		
		<thead>
			<tr>
				<th>Title</th>
				<th>Artist</th>
				<th>Year</th>
			</tr>
		</thead>
		<tfoot>
			<tr>
				<td colspan="2">total number of paintings</td>
				<td>2</td>
			</tr>
		</tfoot>
		<tbody>
			<tr>
				<td>the death of marat</td>
				<td>jacques-louis david</td>
				<td>1793</td>
			</tr>
			<tr>
				<td>burial at ornans</td>
				<td>gustave courbet</td>
				<td>1849</td>
			</tr>
		</tbody>
	</table>
	```
	- ç¤ºä¾‹
	<table border="1" cellpadding="10">
		<caption>19th century french paintings</caption>
		<col class="artistName"/>
		<colgroup id="paintingColumns">
			<col />
			<col />
		</colgroup>
		
		<thead>
			<tr>
				<th>Title</th>
				<th>Artist</th>
				<th>Year</th>
			</tr>
		</thead>
		<tfoot>
			<tr>
				<td colspan="2">total number of paintings</td>
				<td>2</td>
			</tr>
		</tfoot>
		<tbody>
			<tr>
				<td>the death of marat</td>
				<td>jacques-louis david</td>
				<td>1793</td>
			</tr>
			<tr>
				<td>burial at ornans</td>
				<td>gustave courbet</td>
				<td>1849</td>
			</tr>
		</tbody>
	</table>
- pseudo class
	- ```tbody tr: hover{background-color: #9e9e9e; color: black;}```
	- ```tbody tr: nth-child(odd){background-color: white;}```

### form (interact with web server)
- formä»£ç åŠå®žä¾‹ï¼š
	- ä»£ç 
	```
	<form method="get" action="process.php">
		<fieldset>
			<legend>Details</legend>
			<p>
				<label>title:</label>
				<input type="text" name="title" />
			</p>
			<p>
				<label>country:</label>
				<select name="where">
					<option>canada</option>
					<option>finland</option>
					<option>US</option>
				</select>
			</p>
			<input type="submit">
		</fieldset>
	</form>
	```
	- form å®žä¾‹ï¼š
	<form method="get" action="">
		<fieldset>
			<legend>Details</legend>
			<p>
				<label>title:</label>
				<input type="text" name="title" />
			</p>
			<p>
				<label>country:</label>
				<select name="where">
					<option>canada</option>
					<option>finland</option>
					<option>US</option>
				</select>
			</p>
			<input type="submit">
		</fieldset>
	</form>
- form ä¸­çš„å…ƒç´ : button, datalist, fieldset, form, input, label, legend, option, optgroup, select, textarea
- input çš„ç±»åž‹: text, textarea, password, search, email, tel, url, button, number, range, checkbox, radio, color, date, time, datetime, datetime-local
- selectå“ªä¸ªå€¼è¢«å‘é€:   
	```
	<select name="choice">
		<option>second</option>
	</select>
	//?choice=second

	<select name="choice">
		<option value="2">second</option>
	</select>
	//?choice=2
	```
### JavaScript: object based, dynamically type scripting language
#### local 
- three types: 
	- inline: 
		- ```<a href="JavaScript: OpenWindow();">more info</a>```
		- ```<input type="button" onclick="alert('r u ok?');"/>```
	- embedded: 
	```
	<script>
		alert("hello world!");
	</script>
	```
	- external:
	```
	<head>
		<script type="text/javascript" src="greeting.js"></script>
	</head>
	```
- object:
```
var person = {
	firstName: "John",
	lastName: "Doe",
	age: 50,
	fullName: function(){
		return this.firstName + " " + this.lastName;
	}
}
```
- data type: 
	- primitive: boolean, string, number, null, undefined
	- complex: object, array, function
	- array: ```var greetings = ["good morning", "good afternoon"]
	- scope: local & global
	- è¾“å‡º: alert(), console.log(), document.write()ç›´æŽ¥è¾“å‡ºåˆ°html
#### windows and DOM object
- js objects:
	- build-in objects for common processing: string, date, math, etc.
	- can access browser object: window, history, location
	- can access html element as DOM. DOM categories: core, html, style, event
	- DOM nodes: element node, text node, attribute node
	- node properties: 
		- attribute
		- childNode
		- firstNode
		- lastNode
		- nextSibling
		- previousSibling
		- nodeName
		- nodeType
		- nodeValue
		- parentNode
	- node method (accessing node)
		- createAttribute()
		- createElement()
		- creatTextNode()
		- getElementById(id)
		- getElementByTagName(name)
	- modify DOM element
		- removeChild()
		- appendChild()
		- createTextNode()
	- modify element's style:
		- commentTag.style.borderWidth = "3px"
		- commentTag.className = "someClassName"
		
#### event model
- ä¸¤ä¸ªè§¦å‘å™¨è®¾ç½® registering event handler
	1. element.onclick = functionName;  
	å˜ä½“: element.onclick = function(...){...};
	2. element.addEventListener('click', functionName);  
	å˜ä½“: element.addEventListener('click', function(...){...});
- window.onload = function(){//js code here};
- event obj and this
	```
	document.getElementById("loginFrom").onsubmit = function(e){
		var fieldValue = document.getElementById("username").value; //valueä¸éœ€è¦æ‹¬å·
		if(fieldValue == null || fieldValue == ""){
			e.preventDefault(); //eæ˜¯è§¦å‘å™¨ï¼ŒpreventDefaultæ˜¯ç¦æ­¢è¯¥å¯¹è±¡çš„é»˜è®¤æ“ä½œ
			alert("you must enter a username");
		}
	}
	```
---







ä¸­é—´ä»¶ w6 p28

