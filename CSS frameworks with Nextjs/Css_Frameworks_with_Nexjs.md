
Learn how to use Modern css Frameworks like Tailwind css and Chakra ui with Nextjs 

![image](https://github.com/Codingforhackers/eincode_blog/blob/main/CSS%20frameworks%20with%20Nextjs/Eincode.png?raw=true)


## Introduction

There are cases where we may want to use pre-built UI libraries to take advantage
of their components, themes, and built-in features so that we don't have to build them
from scratch and to take advantage of a vast community that can help us when any
problem occurs.

In this post, we will discover some modern UI libraries and learn how to integrate
them properly in any Next.js application. We will look at the following in detail:

   - What UI libraries are and why we might need them
   - How to integrate TailwindCSS
   - How to integrate Chakra UI

By the end of this article, you will be able to integrate any UI library by following the tips
and principles that we'll see in the following sections.

## Introduction to UI Frameworks

Frameworks and utilities are not essential. We could build any user interface
(despite its complexity) from scratch using vanilla JavaScript, HTML, and CSS. Still,
we would often find ourselves using the same patterns, accessibility rules, optimizations,
and utility functions on every user interface we build. So here comes the concept of
a UI library.
The idea is to abstract our most common use cases, reuse most of the code on different
user interfaces, improve our productivity, and use well-known, tested, and themeable
UI components.
With **"themeable"**, we refer to those libraries and components that allow us to customize
the color scheme, spacing, and the whole design language of a given framework.

## TailwindCSS with Next.js

**TailwindCSS** is a utility-first CSS framework that allows you to build any user interface
using pre-made CSS classes that map CSS rules in a straightforward way.

Its main strengths are the following:

  - *Framework agnostic*: You can use TailwindCSS in React, Vue, Angular, and even in plain HTML and JavaScript. It's just a set of CSS rules.
  - *Themeable*: Just like Chakra UI, you can customize all the TailwindCSS variables to
make them match your design tokens.
  - *Dark and light theme support*: You can easily enable or disable the dark theme by modifying a specific CSS class from the *<html>* element.
  - *Mobile-ready*: You can use specific CSS classes' prefixes to apply certain rules to
mobile, desktop, or tablet screens only.


Let's create a new project and install all the required dependencies:

`npx create-next-app nextjs-with-tailwindcss`

TailwindCSS only requires three devDependencies , so let's enter the newly created
project and install them:

`yarn add -D autoprefixer postcss tailwindcss`

Now that we have all the dependencies installed, we need to set up the basic TailwindCSS
configuration files. We can do that by using the *tailwindcss init* command:

`npx tailwindcss init -p`

This will create two different files:

 - tailwind.config.js : This file will help us configure the TailwindCSS theme,
unused CSS purge, dark mode, plugins, and more.
 - postcss.config.js : TailwindCSS uses PostCSS under the hood and ships
with a pre-configured postcss.config.js that we can always edit as we prefer.

First of all, we want to configure TailwindCSS to remove unused CSS from the final build.
We can do that by opening the *tailwind.config.js* file and editing it as follows:

```js

module.exports = {
   purge: ['./pages/**/*.{js,jsx}',
   './components/**/*.{js,jsx}'],
   theme: {
   extend: {},
   },variants: {
   extend: {},
   },
   plugins: [],
};

```
As you can see, we're telling TailwindCSS to check every file ending with .js or .jsx
inside both *pages/* and *components/* directories and remove all the CSS classes that
are not used inside of any of those files.

We now only need to include the default tailwind.css CSS file on every single page of
our application, and we're ready to start. We can do that by importing **'tailwindcss/
tailwind.css'** inside our **pages/_app.js** file:


```js
import 'tailwindcss/tailwind.css';
function MyApp({ Component, pageProps }) {
  return (
    <div className="bg-gray-800 text-gray-100">
      <Component {...pageProps} />
    </div>
  )
}

export default MyApp

```

![tailwind](https://github.com/Codingforhackers/eincode_blog/blob/main/CSS%20frameworks%20with%20Nextjs/tailwind.png)

Another way is that we just need to add the tailwind directives to our CSS.
Inside our golbal css file **styles/global.css**, we need to add the tailwind directive.

```js
@tailwind base; 
@tailwind components; 
@tailwind utilities;

````

>Make sure your nextjs global css file is imported in *_app.js* custom file.



## Chakra UI with Nextjs

**Chakra UI** is an open source component library used for building modular, accessible,
and good-looking user interfaces.

Its main strengths are the following:

  - *Accessibility*: Chakra UI allows us to use pre-built components (such as buttons, modals, inputs, and many more) created by the Chakra UI team with extra attention to accessibility.

  - *Themeable*: The library ships with a default theme, where (for instance) buttons have a particular default background color, border radius, padding, and so on. We can always customize the default theme using Chakra UI built-in functions for editing every style of the library components.

  - *Light and dark mode*: They're both supported out of the box and can rely on the user's system settings. If users set their computer to use dark mode by default, Chakra UI will load the dark theme as soon as it loads. 

  - *TypeScript support*: Chakra UI is written in TypeScript and provides first-class types for a beautiful developer experience.

To see how to integrate Chakra UI into a Next.js application,we wil start by creating a new Next.js project:

`npx create-next-app nextjs-with-chakra-ui`

We now need to install Chakra UI and its dependencies:

`yarn add @chakra-ui/react @emotion/react@^11 @emotion/styled@^11 framer-motion@^4 @chakra-ui/icons`

We're now ready to integrate Chakra UI with Next.js. To do that, let's open the *pages/_
app.js* file and wrap the default **<Component />** component in the Chakra provider:

```js
import { ChakraProvider } from '@chakra-ui/react';
function MyApp({ Component, pageProps }) {
   return (

      <ChakraProvider>
        <Component {...pageProps} />
      </ChakraProvider>
   );
}
export default MyApp;

```
We can add some Chakra UI components :

```js
import { Wrap, WrapItem, Avatar, AvatarBadge, AvatarGroup } from '@chakra-ui/react';

export default function Home() {
   return (
   <Wrap padding="10">
	  <WrapItem>
	    <Avatar name='Dan Abrahmov' src='https://bit.ly/dan-abramov' />
	  </WrapItem>
	  <WrapItem>
	    <Avatar name='Kola Tioluwani' src='https://bit.ly/tioluwani-kolawole' />
	  </WrapItem>
	  <WrapItem>
	    <Avatar name='Kent Dodds' src='https://bit.ly/kent-c-dodds' />
	  </WrapItem>
	  <WrapItem>
	    <Avatar name='Ryan Florence' src='https://bit.ly/ryan-florence' />
	  </WrapItem>
	  <WrapItem>
	    <Avatar name='Prosper Otemuyiwa' src='https://bit.ly/prosper-baba' />
	  </WrapItem>
	  <WrapItem>
	    <Avatar name='Christian Nwamba' src='https://bit.ly/code-beast' />
	  </WrapItem>
	  <WrapItem>
	    <Avatar name='Segun Adebayo' src='https://bit.ly/sage-adebayo' />
	  </WrapItem>
	</Wrap>
   );
}

```
Opening the page in a web browser, we will see the following result:

![chakra](https://github.com/Codingforhackers/eincode_blog/blob/main/CSS%20frameworks%20with%20Nextjs/chakraexample.png)
