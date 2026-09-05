# Headers
Headers carry information for:

* Request and Response Body
* Request Authorization
* Response Caching
* Response Cookies

You will have to set the request headers when you are sending the request for testing an API and you will have to set the assertion against the response headers to ensure that right 
headers are being returned.

The headers that you will encounter the most during API testing are the following, you may need to set values for these or set assertions against these headers to ensure that they convey 
the right information and everything works fine in the API:

* Authorization: Carries credentials containing the authentication information of the client for the resource being requested.
* WWW-Authenticate: This is sent by the server if it needs a form of authentication before it can respond with the actual resource being requested. Often sent along with a response
code of 401, which means ‘unauthorized’.
* Accept-Charset: This is a header which is set with the request and tells the server about which character sets are acceptable by the client.
* Content-Type: Indicates the media type (text/html or text/JSON) of the response sent to the client by the server, this will help the client in processing the response body correctly.
* Cache-Control: This is the cache policy defined by the server for this response, a cached response can be stored by the client and re-used till the time defined by the Cache-Control header.
