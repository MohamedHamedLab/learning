# Built In Components

## Routing
- we want to create a simple website with just two pages; the first one will be the **home page**, while the second one will be a simple **contact page**.
- To do that, we will only need to create two new files inside our pages/ folder: `index.js` and `contacts.js`. Both files will need to export a function returning some JSX content; it will be rendered on the server side and sent to the browser as standard HTML.

### navigating
- If we want to move that page to http://localhost:3000/contact-us, we can just rename our `contacts.js` file to `contact-us.js`, and Next.js will automatically rebuild the page using the new route name for us.
 

### create a dynamic route
- if we want to create a posts page, we can create a new `index.js` file inside the **pages/posts/** 
- We then want to create a dynamic route for every blog post,
- we can create a new file inside the `pages/posts/` folder,` pages/posts/` `[slug].js`, where `[slug]` identifies a route variable that can contain any value, depending on what the user types in the browser's address bar. I
- We can also nest multiple dynamic routes inside the pages/ folder; let's say that we want our post page structure to be as follows: `/posts/[date]/ ` **[slug]**. We can just add a new folder called **[date]** inside our pages/ directory and move the slug.js file inside it: We can now visit `http://localhost:3000/posts/2021-01-01/my-first-post `
 ```javascript 
 pages/
  - index.js
  - contact-us.js
  - posts/
      - index.js
      - [date]/
          - [slug].js
 ```

### Using route variables
- When using both the `getServerSideProps` and `getStaticProps` functions, remember that they must return an `object`. Also, if you want to pass any prop from one of those two functions to your page, make sure to pass them inside the returning object's `props` property.
- 
 ```javascript 
 export async function getServerSideProps({ params }) {
  const { name } = params;
  return {
    props: {
      name
    }
  } 
}
function Greet(props) {
  return (
    <h1> Hello, {props.name}! </h1>
  )
}
export default Greet;
 ```

 ### Using route variables inside components
- if we now try to call the following URL, `http://localhost:3000/greet/Mitch?learning_nextjs=true`, we will see `{learning_nextjs: "true", name: "Mitch"}` in query object.

```javascript 
 import { useRouter } from 'next/router';
function Greet() {
  const { query } = useRouter();
  return <h1>Hello {query.name}!</h1>;
}
export default Greet;
 ```

### Client-side navigation
- Once the user clicks that link, Next.js will redirect the browser to the following URL: http://localhost:3000/blog/2020-01-01/happy-new-year?foo=bar.-
  ```javascript 
 <Link
  href={{
    pathname: '/blog/[date]/[slug]'
    query: {
      date: '2020-01-01',
      slug: 'happy-new-year',
      foo: 'bar'
    }
  }}
/>
  Read post
</Link>
 ```

 ### Using the router.push method

 ```javascript 
 import { useEffect } from 'react';
import { useRouter } from 'next/router';
import PrivateComponent from '../components/Private';
import useAuth from '../hooks/auth';
function MyPage() {
  const router = useRouter();
  const { loggedIn } = useAuth();
  useEffect(() => {
    if (!loggedIn) {
      router.push('/login')
    }
  }, [loggedIn]);
  return loggedIn
    ? <PrivateComponent />
    : null;
}
export default MyPage;
```

- we can create more complex page routes by passing an object to the push method

 ```javascript 
 router.push({
  pathname: '/blog/[date]/[slug]',
  query: {
    date: '2021-01-01',
    slug: 'happy-new-year',
    foo: 'bar'
  }
});
```

### Image optimization
- Starting with **Next.js 10**, the framework introduced a new helpful `Image` component and automatic image optimization.
- automatic image optimization works on-demand, as it optimizes, resizes, and renders the image only when the browser has requested it.
- For external image source use image tag
  
 ```jsx 
import Image from 'next/image';
function IndexPage() {
  return (
    <div>
      <div
        style={{ width: 500, height: 200, position: 
         'relative' }}
      >
        <Image
          src='https://images.unsplash.com/photo-
           1605460375648-278bcbd579a6'
          layout='fill'
          objectFit='cover'
          alt='A beautiful English Setter'
        />
      </div>
    </div>
  );
}
export default IndexPage;
 ```

- Next.js makes it very easy by just configuring the `next.config.js` file and using the Image component. 



 - We can crop our image to fit the desired dimensions using the optional layout prop. 
 - It accepts four different values: fixed, intrinsic, responsive, and fill.
1. fixed works just like the img HTML tag. If we change the viewport size, it will keep the same size, meaning that it won't provide a responsive image for smaller (or bigger) screens.
2. responsive works in the opposite way to fixed; as we resize our viewport, it will serve differently optimized images for our screen size.
3. intrinsic is halfway between fixed and responsive; it will serve different image sizes as we resize down our viewport, but it will leave the largest image untouched on bigger screens.
4. fill will stretch the image according to its parent element's width and height; however, we can't use fill alongside the width and height props. You can use fill or width and height).

### Running automatic image optimization on external services
- By default, automatic image optimization runs on the same server as Next.js.
- If you're deploying your web app to Vercel, you don't actually need to set up any loader in your next.config.js, file as Vercel will take care of optimizing and serving the image files for you.


**Otherwise, you can use the following external services**:
- **Akamai**: https://www.akamai.com
- **Imgix**: https://www.imgix.com
- **Cloudinary**: https://cloudinary.com


 ```jsx 
module.exports = {
  images: {
    loader: 'akamai',
    domains: ['images.unsplash.com']
  }
};
 ```
### Handling metadata
- Head component allows us to update the `<head>` section of our HTML page from any component, meaning that we can dynamically change, add, or delete any metadata, link, or script at runtime depending on our user's navigation.


```jsx 
import Head from 'next/head';
import Link from 'next/link';
function IndexPage() {
  return (
    <>
      <Head>
        <title> Welcome to my Next.js website </title>
      </Head>
      <div>
        <Link href='/about' passHref>
          <a>About us</a>
        </Link>
      </div>
   </>
  );
}
export default IndexPage;
 ```


 #### Grouping common meta tags
 ```jsx 
 import Head from 'next/head';
function PostMeta(props) {
  return (
    <Head>
      <title> {props.title} </title>
      <meta name="description" content={props.subtitle} />
      {/* open-graph meta */}
      <meta property="og:title" content={props.title} />
      <meta property="og:description" 
       content={props.subtitle} />
      <meta property="og:image" content={props.image} />
      {/* twitter card meta */}
      <meta name="twitter:card" content="summary" />
      <meta name="twitter:title" content={props.title} />
      <meta name="twitter:description" 
       content={props.description} />
      <meta name="twitter:image" content={props.image} />
    </Head>
  );
}
export default PostMeta;
 ```

  ```jsx 
  //create a mock for our posts.
  export default [
  {
    id: 'qWD3Pzce',
    slug: 'dog-of-the-day-the-english-setter',
    title: 'Dog of the day: the English Setter',
    subtitle:      'The English Setter dog breed was named 
     for these dogs\' practice of "setting", or crouching 
     low, when they found birds so hunters could throw 
     their nets over them',
    image: 'https://images.unsplash.com/photo-
     1605460375648-278bcbd579a6'
  },
  {
    id: 'yI6BK404',
    slug: 'about-rottweiler',
    title: 'About Rottweiler',
    subtitle:
      "The Rottweiler is a breed of domestic dog, regarded 
       as medium-to-large or large. The dogs were known in 
       German as Rottweiler Metzgerhund, meaning Rottweil 
       butchers' dogs, because their main use was to herd 
       livestock and pull carts laden with butchered meat 
       to market",
    image: 'https://images.unsplash.com/photo-
     1567752881298-894bb81f9379'
  },
  {
    id: 'VFOyZVyH',
    slug: 'running-free-with-collies',
    title: 'Running free with Collies',
    subtitle:
      'Collies form a distinctive type of herding dogs, 
       including many related landraces and standardized 
       breeds. The type originated in Scotland and Northern 
       England. Collies are medium-sized, fairly lightly-
       built dogs, with pointed snouts. Many types have a 
       distinctive white color over the shoulders',
    image: 'https://images.unsplash.com/photo-
     1517662613602-4b8e02886677'
  }
];
 ```
- Great! Now we only need to create a **[slug]** page to display our posts. The full route will be `/blog/[slug]`, so let's create a new file called `[slug].js` inside pages/blog/ and add the following content:

```jsx 
 import PostHead from '../../components/PostHead';
import posts from '../../data/posts';
export function getServerSideProps({ params }) {
  const { slug } = params;
  const post = posts.find((p) => p.slug === slug);
  return {
    props: {
      post
    }
  };
}
function Post({ post }) {
  return (
    <div>
      <PostHead {...post} />
        <h1>{post.title}</h1>
        <p>{post.subtitle}</p>
    </div>
  );
}
export default Post;
 ```


 ### Customizing _app.js and _document.js pages
 - There are certain cases where you need to take control over page initialization, so that every time we render a page, Next.js will need to run certain operations before sending the resulting HTML to the client. To do that, the framework allows us to create two new files, called _app.js and _document.js, inside our pages/ directory.

 ```jsx
// By default, Next.js ships with the following pages/_app.js file
import Navbar from '../components/Navbar';
function MyApp({ Component, pageProps }) {
  return (
    <>
        <Navbar />
        <Component {...pageProps} />
    </>
  );
}
export default MyApp;
```

### adding theme

```jsx

// Theme Context
import { createContext } from 'react';
const ThemeContext = createContext({
  theme: 'light',
  toggleTheme: () => null
});
export default ThemeContext;

import ThemeContext from '../components/themeContext';
import Navbar from '../components/Navbar';
const themes = {
  dark: {
    background: 'black',
    color: 'white'
  },
  light: {
    background: 'white',
    color: 'black'
  }
};

// App component
function MyApp({ Component, pageProps }) {
  const [theme, setTheme] = useState('light');
  const toggleTheme = () => {
    setTheme(theme === 'dark' ? 'light' : 'dark');
  };
  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      <div
        style={{
          width: '100%',
          minHeight: '100vh',
          ...themes[theme]
        }}
      >
        <Navbar />
        <Component {...pageProps} />
      </div>
    </ThemeContext.Provider>
  );
}
export default MyApp;

// Navbar component
import { useContext } from 'react';
import Link from 'next/link';
import themeContext from '../components/themeContext';
function Navbar() {
  const { toggleTheme, theme } = useContext(themeContext);
  const newThemeName = theme === 'dark' ? 'light' : 'dark';
  return (
    <div
      style={{
        display: 'flex',
        flexDirection: 'row',
        justifyContent: 'space-between',
        marginBottom: 25
      }}
    >
      <div>My Website</div>
      <div>
        <Link href="/">Home </Link>
        <Link href="/about">About </Link>
        <Link href="/contacts">Contacts </Link>
        <button onClick={toggleTheme}>
          Set {newThemeName} theme
        </button>
      </div>
    </div>
  );
}
export default Navbar;
```

### The _document.js page
- if  will need a change of approach for both `<html>` and `<body>` tags, create a new file called _document.js inside our pages/ directory, just like we do for our _app.js file:

```jsx
import Document,{
    Html,
    Head,
    Main,
    NextScript
  } from 'next/document';
class MyDocument extends Document {
  static async getInitialProps(ctx) {
    const initialProps =
      await Document.getInitialProps(ctx);
    return { ...initialProps };
  }
  render() {
    return (
      <Html>
        <Head />
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}
export default MyDocument;
```
- **Html**: The `<html>` tag for our **`Next.js`** application. We can pass any standard `HTML` property (such as lang) to it as a prop.
- **Head**: We can use this component for all the tags common to all the application pages. This is not the Head component we've seen in the previous chapter. They behave similarly, but we should use it only for code that is common to all the website pages.
- **Main**: This will be the place where **Next.js** renders our page components. The browser won't initialize every component outside `<Main>`, so if we need to share common components between our pages, we should place them inside the _app.js file. 
- **NextScript**: If you've tried to inspect an HTML page generated by Next.js, you may have noticed that it adds some custom JavaScript scripts to your markup. Inside those scripts, we can find all the code required to run client-side logic, React hydration, and so on.