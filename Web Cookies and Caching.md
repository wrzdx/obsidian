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

## HTML Web Pages
### Background
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
- Objects can be loaded over the same (that is persistent) or independent (that is non-persistent) HTTP sessions

### Page Download
#### Non-Persistent HTTP
![](Pasted%20image%2020260330084053.png)

![|500](Pasted%20image%2020260330084148.png)

#### Persistent HTTP
![|500](Pasted%20image%2020260330084338.png)

#### Round Trip Time (Performance Metric)
- **RTT** (definition): **round trip time** for a small packet to travel from client to server and back
- HTTP response time: 
	- One RTT to initiate TCP connection 
	- One RTT for HTTP request and first few bytes of HTTP response to return 
	- File transmission time 
	- Non-persistent HTTP response time = 2RTT+ file transmission time

#### Comparison
| Criteria                      | Non-Persistent                                                | Persistent                                               |
| ----------------------------- | ------------------------------------------------------------- | -------------------------------------------------------- |
| Download time per page object | 2 RTTs                                                        | 1 RTT                                                    |
| Connection State              | Closed immediately after server response                      | Remains opened until explicit client request for closure |
| Workload distribution         | Maximized on a client, minimized on a server                  | Minimized on a client, maximized on a server             |
| Limitation overcome           | Parallel connections for webpage objects download by browsers | Connection timeout                                       |

### Web cache (or proxy Server)
Goal: satisfy client request without involving origin server
![|500](Pasted%20image%2020260330091710.png)
- User sets her browser: Web accesses via cache 
- Browser sends all HTTP requests to cache 
- If object in cache: then cache returns object 
- else cache requests object from origin server, then returns object to client
