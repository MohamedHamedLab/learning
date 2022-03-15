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