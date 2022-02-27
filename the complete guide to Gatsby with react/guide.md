## introduction 

**what is gatsby**

Gatsby is a free, open source static site generator for  React. Static site
generators are software applications that create static pages from a template or component . 

**so what is diffrence between Gatsby and Wordpress ?** 


traditional database-driven CMS, such as WordPress,  content is managed and stored in a database , mixes it with a
template file, and generates an HTML page as its response *(time consuming)* .

**gatsby**

gatsby generate pages during the build process , its brings data to its GraphQL layer , weher it can be queried in pages and templates .
The requested data is stored in JSON and it accessed by the built pages (composed of HTML ,JS and CSS files) .
a user can deploy these generated pages to a server . when its recive a request the server response with the predetermined static , rendred HTML **(static pages are generated at the build time so they eleminate time that database can take from us )** . 


>>A static site can contain dynamic and exciting experiences! It is a common
misconception that "static" means the site is stationary. This could not be
further from the truth. The word "static" only refers to the manner in which
files are retrieved by a client. 


**Sourcing content**

the best part of gatsby is that you can get data from CMS , real time database (firebase as an example) or a cusntom API ,  and you can merge them all togather into a unfied data layer   by **gatsby plugins** .

**ok Now Gastbyjs vs Nextjs what is diffrence ?**

Back then, the key diffrence between Gatsby and Next was server side rendreing .
Next application like Gastby can be hosted staticlly , but it can be server render pages waher gatsby could not .

*Hum first what is server side rendreing ?* 

Ok, instead of deploying a static build like gatsby , a server is deployed to handle request . When a page is requested ,the server builds that page and caches it befor sending it to the user . But start from version 4 gatsby can have all its page prebuilt staticlly or hybrid build (mix of static and server-side rendered). 

**lets setup a gastby project** 

ok to start using gastby , we need to enusre that we have some prerequsite .

*nodejs*

start from version 4 gastby support nodejs versions that are greather then `14.15.0`
so check the nodejs version on your machine by 

`node -v`

![node-v](https://github.com/Codingforhackers/eincode_blog/blob/main/the%20complete%20guide%20to%20Gatsby%20with%20react/nodev.jpg)

so in my case its `14.19.0` 

in your case if you receive an error, you can download Node.js by navigating to the Node.js website `https://nodejs.org` Node.js comes bundled with npm, a package repository, package manager,
and command-line tool that we will be using to install Gatsby .

**gatsby command line interface (CLI)**

is a tool built by the core Gatsby team , it allows you to perform standard functions, such as creating new Gatsby projects, setting up
local development servers, and building your production site .

To install the CLI globally, *npm install* it with the global flag:

`npm i -g gatsby-cli`

**Directory and package setup**

let's start  creating files and folder that we need to start our project , as well ass necessary dependencies . 

first create a folder name what ever you need , and open tat folder in your terminal , initialize a new packge in this folder by running : 

`npm init -y`

package now initialized, lets start installing react and gatsby : 

`npm i gatsby react react-dom`

now if you open the project folder you should notice that contains three new items , *package.json* , *package-lock.json* and *node-module* folder .
let's open *package.json* file you should see something like this : 

```js
{
 "name": "gatsby-site",
 "version": "1.0.0",
 "description": "",
 "main": "index.js",
 "scripts": {
 "test": "echo \"Error: no test specified\" && exit 1"
 },
 "keywords": [],
 "author": "",
 "license": "ISC",
"dependencies": {
    "gatsby": "^4.8.1",
    "react": "^17.0.2",
    "react-dom": "^17.0.2"
  }
}
```



as you see that this file now contains reference to the dependencies we have just installed *(gatsby, react)* . 

**Development scripts**

let's start modifying *package.json* by adding some useful scripts that will speed up our development process : 

```js
{
 "scripts": {
   "build": "gatsby build",
   "develop": "gatsby develop",
   "start": "npm run develop",
   "serve": "gatsby serve",
   "clean": "gatsby clean"
 },
  "dependencies": {
    "gatsby": "^4.8.1",
    "gatsby-cli": "^4.8.1",
    "react": "^17.0.2",
    "react-dom": "^17.0.2"
  }
}

 ```
 
 
 
let's understand these scripts : 

  - build: run the gatsby cli build command . This creates a compiled ,production-ready build of your site (ready to be deployed) .  
  - develo  : runs the gatsby cli develop command 
  - start : the *start* script redirect to *develop* script .
  - serve : run the gatsby cli *serve* command to serve up a gastby *build* folder . (useful way to review a production build) .
  - clean : the clean script use the gatsby cli *clean* command . this deletes the local gatsby cache and any buidl data . and it will be rebuilt with next *develop* or *build* command .
    

**Gatsby files and folder**

Like any other framework , gastby require certain fles to work .
theres some files that gastby expects to find them .
Create a *gatsby-config.js* file in root Directory and add :

```js
module.exports = {
 plugins: [],
};

```


as the name is the *gatsby-config.js* file ,  contains the core configuration for gatsby . 

Create *gatsby-browser.js* and *gatsby-node.js* files in your root Directory .

The **gatsby-browser** file contains any code we would like to run on client's browser . 
The **gatsby-node** file contains code that we would like to run  during the process of building our site . 

Finally , create a *src* folder . this folder will contain the majority of your development work , like in a react app . pages that we create and components we define all will be contained within this folder .


## Create your first Page

Now its fine we just setup all what we need to get started . 

Navigate to *src* folder as  you know that src folder will contains our pages , so we gonna create a new folder called *pages* . pay attention that any *JS* files we create within The *pages* folder will be treated as route by Gatsby (thats applies also to subfolders inside the *pages* folder ) . 

for example : 

   - **src/pages/index.js** will map to **yourname.com** (home page of your website) .
   - **src/pages/blog/first-post.js** will map to **yourname.com/blog/first-post** .


*Let's create the index page* 

Create an *index.js* file in your pages folder , and file it with the following code : 

```js
import React from "react"
const Index = () => {
return (
<div>
  <h1>My Landing Page</h1>
        <p>This is my landing page.</p>
</div>
)
}
export default Index
```





This is just a simple Reactjs component .



Conratulation, we just create our home page let's see this in our browser .
open your terminal and run the command :

`npm run start`

 if you remamber this *start* command will run the *gatsby develop* command , this will take few second to run . 
 you can now open a browser and navigate to `http://localhost:8000/`, you should see something like this : 


![landingpage](https://github.com/Codingforhackers/eincode_blog/blob/main/the%20complete%20guide%20to%20Gatsby%20with%20react/landingpage.png.png)

This is the rendred version of our *index.js* page component .

**link component**

let's create another page for example *contact.js* will contain this following code :


```js
import React from "react"
const Index = () => {
return (
<div>
  <h1>My contact Page</h1>
<p>This is my contact page.</p>
</div>
)
}
export default Index
```

we need to show this on our home page ( *index.js*) as link , in HTML we use <a/> tag whenever you are linking to a page that is internal . 
The *<LINK />* in gatsby works just like an *<a/>* tag , the only diffrence is that link enables prefetching . 
(prefetching is the fact of reloading a ressource before it is required ).

Our *index.js* file should look like this : 


```js
import React from "react"
import {Link} from "gatsby"
const Index = () => {
return (
<div>
  <h1>My Landing Page</h1>
<p>This is my landing page.</p>
<Link to="/contact">take me to conatct</Link>
</div>
)
}
export default Index
```



As you can see the link component has a **to** this called a prop . Need to be passed to the page you want to navigate to , in our example we want to navigate to the contact page so we add **to="/contact"**

Now let's open our home page and see the result .

![link](https://github.com/Codingforhackers/eincode_blog/blob/main/the%20complete%20guide%20to%20Gatsby%20with%20react/link.png)

