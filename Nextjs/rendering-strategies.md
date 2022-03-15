# Rendering Strategies 
 
 ## getServerSideProps
1- We start by exporting an async function called getServerSideProps. During the build phase, Next.js will look for every page exporting this function and make them dynamically server-side rendered for each request. 
2- Inside the getServerSideProps function, we return an object containing a property called props.
3- We then refactor the IndexPage function, which now accepts a props parameter containing all the props passed from the getServerSideProps function.

 ```javascript 
 // here to make the user api call
 export async function getServerSideProps() {
  const userRequest =     await fetch('https://example.com/api/user');
  const userData = await userRequest.json();
  return {
    props: {
      user: userData
    }
  };
}
// here you pass user as props
function IndexPage(props) {
  return <div>Welcome, {props.user.name}!</div>;
}
export default IndexPage;
 ```


## Client-side rendering (CSR)

- in `create-react-app (CRA)` we can only find one `div` inside the body tag: `<div id="root"></div>`.
- During the build phase, `create-react-app` will inject the compiled `JavaScript` and `CSS` files into this `HTML` page and use the `root` div as a target container for rendering the whole application.

 ```javascript 
 
 ```

 ## Using dynamic component loading

- want to display a code snippet on a web page using the `Highlight.js` library, making it easy to highlight and make code more readable. We could just create a component called Highlight
- While this piece of code would perfectly run on a client-side React app, it will crash during the rendering or build phase on `Next.js` because Highlight.js needs the document global variable, which does not exist in Node.js, as it's exposed by browsers only.
- You can easily fix this by wrapping all the `hljs` calls in the `useEffect` hook, That way, `Next.js` will render the HTML markup returned by our component,inject the `Highlight.js` script into our page, and, once the component is mounted on the browser, it will call the library functions on the client side.
  
 ```javascript 
 // highlight react component
import { useEffect } from 'react';
import Head from 'next/head';
import hljs from 'highlight.js';
import javascript from 'highlight.js/lib/languages/javascript';

function Highlight({ code }) {

  useEffect(() => {
    hljs.registerLanguage('javascript', javascript);
    hljs.initHighlighting();

  }, []);

  return (
    <>
      <Head>
        <link rel='stylesheet' href='/highlight.css' />
      </Head>
      <pre>
        <code className='js'>{code}</code>
      </pre>
    </>
  );
}
export default Highlight;


// Nextjs dynamic import 
 import dynamic from 'next/dynamic';
const Highlight = dynamic(
  () => import('../components/Highlight'),
  { ssr: false }
);
import styles from '../styles/Home.module.css';
function DynamicPage() {
  return (
    <div className={styles.main}>
      <Highlight
        code={"console.log('Hello, world!')"}
        language='js'
      />
    </div>
  );
}
export default DynamicPage;
 ```


## Using the process.browser variable
- Another way of avoiding the server-side process crashing when using browser-specific APIs is to conditionally execute scripts and components depending on the process.browser global variable. 



 ```javascript 
function IndexPage() {
  const side = process.browser ? 'client' : 'server';
  return <div>You're currently on the {side}-side.</div>;
}
export default IndexPage;
```


 ##  static site generation (SSG)

- With SSG, we will be able to pre-render some specific pages (or even the whole website if necessary) at build time; that means that when we're building our web app, there might be some pages that won't change their content very often, so it makes sense for us to serve them as static assets.
 
- we've built a very complex dashboard that can handle a lot of data… but the REST API request for this data is taking up to a few seconds to succeed. In that case, we are lucky because that data won't change a lot during this time, so we can cache it for up to 10 minutes (600 seconds) using SSG and ISR

-  `getStaticProps` is used at build time by Next.js for getting the data and rendering the page, and it won't be called again until the next build.
-  To avoid the whole website rebuild, Next.js recently introduced an option called revalidate, which can be set inside the returning object of our getStaticProps function.

 ```javascript 
 import fetch from 'isomorphic-unfetch';
import Dashboard from './components/Dashboard';


export async function getStaticProps() {
  const userReq = await fetch('/api/user');
  const userData = await userReq.json();
  const dashboardReq = await fetch('/api/dashboard');
  const dashboardData = await dashboardReq.json();
  return {
    props: {
      user: userData,
      data: dashboardData,
    },
    revalidate: 600 // time in seconds (10 minutes)
  };
}

function IndexPage(props) {
  return (
    <div>
      <Dashboard
        user={props.user}
        data={props.data}
      />
    </div>
  );
}
export default IndexPage;
 ```
