
### Introduction 

AJAX stands for Asynchronous JavaScript and XML.

It is often used as a term to say:

- Get (or send) some data to the server
- Wait for the server to send something back
- Update the page without refreshing it

### XML 

XML stands for Extensible markup language. It was a standard we used to pass information between browsers and servers in the past.

But we rarely use XML now. We use another format called JSON.

### XMLHttpRequest

**XMLHttpRequest** (XHR for short) is a method we used to send and retrieve data. It’s the technology that made Ajax possible.

If you want to get data back from a server, you need to send something to the server first.

We call this data you send to the server a request. We call the stuff the server sends back a response. The action *(sending a request and getting a response)* is called a fetch.

To send a request, we need to create an XMLHttpRequest object first.

`
  const request = new XMLHttpRequest()
`

We want to know when a response comes back from the server. To do so, we listen for the load event.

```js
request.addEventListener('load', e => {
  // do something
})
```

Next, we want to construct the request. This is how it looks like:

```js
request.open(method, link)
```

**method** is the type of request you want to send.  let’s set method to **get**.

**link** is the place you want to request information from. The requested information is also called a resource. If we want to get a list of posts, we can use https://jsonplaceholder.typicode.com/posts (if you open link in your browsers you w'll see posts with id , title and body  ). 

So lets get just the first post by add 1 to url 

```js
request.open('get', 'https://jsonplaceholder.typicode.com/posts/1')
```


Finally, we need to send the request out .



```js
request.send()
````

Here’s the entire **XMLHttpRequest** we created together.

`const request = new XMLHttpRequest()
request.addEventListener('load', e => { /* do something */ })
request.open('get', 'https://jsonplaceholder.typicode.com/posts/1')
request.send()
`
*server must accept request*

Servers can choose to accept or reject your request. If the server does not accept your request, you’ll get an error that says ***“No ‘Access-Control-Allow-Origin’*** header is present on the requested resource”.

Lets do an example try to fetch google.com

```js
request.open('get', 'https://google.com')
```

![cors](https://github.com/Codingforhackers/eincode_blogs/blob/main/How%20Ajax%20Works/images/Noaccess.png)

you cannot fetch `https://google.com`  Google reject our request 

**The callback**

We’re interested in the event target (the **XMLHttpRequest** itself). If you console log the target, you’ll see the response.

```js
request.addEventListener('load', e => {
  console.log(e.target)
})
```

![Response](https://github.com/Codingforhackers/eincode_blogs/blob/main/How%20Ajax%20Works/images/response.jpg) 

The **response** property contains the data you requested from the server. This data is often called the **body** or the **payload**.

If you pay attention to response, you will notice that the response looks like a string. This string is a JSON string (JSON stands for JavaScript Object Notation).

**So why JSON ?**

We use JSON as the main format to pass information between browsers and servers today.
A JSON Object looks like a JavaScript object. The major difference between JSON and JavaScript is.

- JSON can only contain strings
- JSON property and value pairs are always wrapped with double quotes

here is an example of a JSON object : 

`{
  "firstName": "eincode",
  "lastName": "Academy",
  "occupation": "developer",
  "age": "2"
}`


 **Data Types**

 JSON is just one of many types of data we can transfer with **XHR**

 data taypes that are supported by XHR : 
  - ArrayBuffer (array of bytes )
  - Document
  - JSON
  - Text 

Don’t worry about different data types . When you work with APIs, you’ll usually work with JSON and Text only.

**Rate limits Error**

>Each APi has a number of request you can make ,if you send more you'll get an 403 error (forbidden) . 

>Number of request is definde by API creators they help prevent the API from crashing due too many request .

