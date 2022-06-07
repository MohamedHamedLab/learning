# Consuming GraphQL APIs
- install apollo client
```
yarn add @apollo/client graphql isomorphic-unfetch

```
- We will need now to create an Apollo client for our **Next.js** application. We will do that by creating a new file inside `lib/apollo/index.js`

```jsx
import { useMemo } from 'react';
import {
  ApolloClient,
  HttpLink,
  InMemoryCache
} from '@apollo/client';
let uri = 'https://rwnjssignbook.herokuapp.com/v1/graphql';
let apolloClient;
function createApolloClient() {
  return new ApolloClient({
    ssrMode: typeof window === 'undefined',
    link: new HttpLink({ uri }),
    cache: new InMemoryCache(),
  });
} 
```
- As you can assume, by setting `ssrMode: typeof window === "undefined"`, we will use the same Apollo instance for both client and server
- **ApolloClient** uses the browser **fetch** API to make HTTP requests, so we'll need to import a polyfill to make it work on the server side; in that case, we'll be using **isomorphic-unfetch**.
- Inside the same `lib/apollo/index.js` file, let's add a new function to initialize the Apollo client

```jsx
export function initApollo(initialState = null) {
  const client = apolloClient || createApolloClient();
  if (initialState) {
    client.cache.restore({
      ...client.extract(),
      ...initialState
    });
  }
  if (typeof window === "undefined") {
    return client;
  }
  if (!apolloClient) {
    apolloClient = client;
  }
  return client;
}
```
-  If we pass that parameter to the `initApollo` function, it will be merged with the **local cache** to restore a full representation of the state once we move to another page.
-  To achieve that, we will use the React useMemo hook to speed up the process
```jsx
  export function useApollo(initialState) {
  return useMemo(
    () => initApollo(initialState),
    [initialState]
  );
}
```
  - then in `_app.js`

 ```jsx
import { ApolloProvider } from "@apollo/client";
import { useApollo } from "../lib/apollo";
export default function App({ Component, pageProps }) {
  const apolloClient =
    useApollo(pageProps.initialApolloState);
  return (
    <ApolloProvider client={apolloClient}>
      <Component {...pageProps} />
    </ApolloProvider>
  );
}
```

#### Queries
- organize our queries inside a new folder called `lib/apollo/queries/`
- then create the first file **getLatestSigns.js**

```jsx
import { gql } from "@apollo/client";
const GET_LATEST_SIGNS = gql`
  query GetLatestSigns($limit: Int! = 10, $skip: Int! = 0){
    sign(
      offset: $skip,
      limit: $limit,
      order_by: { created_at: desc }
    ) {
      uuid
      created_at
      content
      nickname
      country
    }
  }
`;
export default GET_LATEST_SIGNS;
```
- We can now import this query inside our `pages/index.js` file and try to make our first `GraphQL` request using `Apollo` and `Next.js`

```jsx
import Head from "next/head";
import { ApolloProvider } from "@apollo/client";
import { useApollo } from "../lib/apollo";
export default function App({ Component, pageProps }) {
  const apolloClient =
    useApollo(pageProps.initialApolloState || {});
return (
  <ApolloProvider client={apolloClient}>
    <Head>
      <link href="https://unpkg.com/tailwindcss@^2/dist/        tailwind.min.css"
       rel="stylesheet"
      />
    </Head>
    <Component {...pageProps} />
  </ApolloProvider>
 );
}
```
- let's move back to our home page page for a moment. 
 ```jsx
import { useQuery } from "@apollo/client";
import GET_LATEST_SIGNS from
  '../lib/apollo/queries/getLatestSigns'
function HomePage() {
  const { loading, data } = useQuery(GET_LATEST_SIGNS, {
    fetchPolicy: 'no-cache',
  });
  return <div></div>
}
export default HomePage
```
