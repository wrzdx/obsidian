## Cookies
![](Pasted%20image%2020260330082859.png)
**Cookie** – a small text file with (server name, server ID number) pair, to recognise a client by a server.

![](Pasted%20image%2020260330083107.png)

- Cookies allow an HTTP server to keep track of users;
- Cookie technology relies on 4 major components:
	1) Set-cookie header in HTTP response;
	2) Cookie header at an HTTP request;
	3) A cookie file on a user side;
	4) Back-end database on a server side

## HTML Web Pages: Background
- Addressable by a unique identifier – a *Unified Resource Locator (URL)* address;
- Corresponds to one base HTML file and a set of referenced objects (images, videos, etc.)
	- *HTML: HyperText Markup Language*
	- Example:
	  ```html
	  <!DOCTYPE html>
	<html>
	<body>
	<h2>Web Page is</h2>
	<p>a base HTML page and ref. objects</p>
	<img src="dir1/img1.jpg" width="104">
	<img src="dir2/img2.jpg" width="256">
	<a href="https://www.OtherPage.org">Link</a>
	</body>
	</html>
	  ```
- Objects – separate files stored on a server side, possibly at different locations
- To download a web page, an HTTP client should download all files related to that web page: a base HTML file and all referenced objects
- 