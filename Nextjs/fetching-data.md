# Data fetching
- Data can come from several resources: databases, search engines, external APIs, filesystems, and many other sources.

## Fetching data on the server side
-  Next.js allows us to fetch data on the server side by using its built-in getStaticProps and getServerSideProps functions
-  Node.js doesn't support JavaScript fetch APIs like browsers do

```
// to fetch data use axios library 
yarn add axios
```

```jsx
import { useEffect } from 'react';
import Link from 'next/link';
import axios from 'axios';
export async function getServerSideProps() {
  const usersReq =
    await axios.get('https://api.rwnjs.com/04/users')
  return {
    props: {
      users: usersReq.data
    }
  }
}
function HomePage({ users }) {
  return (
    <ul>
      {
        users.map((user) =>
          <li key={user.id}>
            <Link
              href={`/users/${user.username}`}
              passHref
            >
              <a> {user.username} </a>
            </Link>
          </li>
        )
      }
    </ul>
  )
}
export default HomePage;
```

- We can solve that problem by creating a new file, `pages/users/[username].js`, and calling another REST API to get the single user data.
- To get the single user data, we can call the following URL, `https://api.rwnjs.com/04/users/[username]`, where **[username]** is a route variable representing the user we want to get the data of.
- Let's move to the `pages/users/[username].js`

```jsx
import Link from 'next/link';
import axios from 'axios';
export async function getServerSideProps(ctx) {
  const { username } = ctx.query;
  const userReq =
    await axios.get(
      `https://api.rwnjs.com/04/users/${username}`
    );
  return {
    props: {
      user: userReq.data
    }
  };
}
```
- Now, inside the same file, let's add a UserPage function, which will be the page template for our` /users/[username]` route


```jsx
import { useEffect, useState } from 'react';
import Link from 'next/link';

function UserData({ user }) {
  return (
    <div style={{ display: 'flex' }}>
      <img src={user.profile_picture} alt={user.username} width={150} height={150} />
      <div>
        <div>
          <b>Username:</b> {user.username}
        </div>
        <div>
          <b>Full name:</b> {user.first_name} {user.last_name}
        </div>
        <div>
          <b>Email:</b> {user.email}
        </div>
        <div>
          <b>Company:</b> {user.company}
        </div>
        <div>
          <b>Job title:</b> {user.job_title}
        </div>
      </div>
    </div>
  );
}

export async function getServerSideProps({ query }) {
  const { username } = query;

  return {
    props: {
      username,
    },
  };
}

function UserPage({ username }) {
  const [loading, setLoading] = useState(true);
  const [data, setData] = useState(null);

  useEffect(async () => {
    const req = await fetch(`/api/singleUser?username=${username}`);
    const data = await req.json();

    setLoading(false);
    setData(data);
  }, []);

  return (
    <div>
      <div>
        <Link href="/" passHref>
          Back to home
        </Link>
      </div>
      <hr />
      {loading && <div>Loading user data...</div>}
      {data && <UserData user={data} />}
    </div>
  );
}

export default UserPage;
```

### Consuming REST APIs on the client side
- While the server-side data fetching phase in Next.js only occurs when declared inside its built-in getServerSideProps and getStaticProps functions, if we make a fetch request inside a given component, it will be executed on the client side by default.

```jsx
Next.js project and edit the pages/index.js file as follows:

import { useEffect, useState } from 'react';
import Link from 'next/link';
function List({users}) {
  return (
    <ul>
      {
        users.map((user) =>
          <li key={user.id}>
            <Link
              href={`/users/${user.username}`}
              passHref
            >
              <a> {user.username} </a>
            </Link>
          </li>
        )
      }
    </ul>
  )
}
function Users() {
  const [loading, setLoading] = useState(true);
  const [data, setData] = useState(null);
  useEffect(async () => {
    const req =
      await fetch('https://api.rwnjs.com/04/users');
    const users = await req.json();
    setLoading(false);
    setData(users);
  }, []);
  return (
    <div>
      {loading &&<div>Loading users...</div>}
      {data &&<List users={data} />}
    </div>
  )
}
export default Users;
```

#### implement the single user page
- create a new file, `pages/users/[username].js`
```jsx
  import { useEffect, useState } from 'react'
import Link from 'next/link';
export async function getServerSideProps({ query }) {
  const { username } = query;
  return {
    props: {
      username,
      authorization: process.env.API_TOKEN
    }
  }
}
```
- create the component for `pages/users/[username].js`
```jsx
function UserData({ user }) {
  return (
    <div style={{ display: 'flex' }}>
      <img
        src={user.profile_picture}
        alt={user.username}
        width={150}
        height={150}
      />
      <div>
        <div>
          <b>Username:</b> {user.username}
        </div>
        <div>
          <b>Full name:</b>
            {user.first_name} {user.last_name}
        </div>
        <div>
          <b>Email:</b> {user.email}
        </div>
        <div>
          <b>Company:</b> {user.company}
        </div>
        <div>
          <b>Job title:</b> {user.job_title}
        </div>
      </div>
    </div>
  )
}
```
> now there are two problems
1. The first one is related to CORS.
2. The second problem relates to exposing the authorization token to the client.

> to fix these issue Let's create a new folder inside pages/ called api/ and a new file, pages/api/singleUser.js:

```jsx
import axios from 'axios';
export default async function handler(req, res) {
  const username = req.query.username;
  const API_ENDPOINT = process.env.API_ENDPOINT;
  const API_TOKEN = process.env.API_TOKEN;
  const userReq = await axios.get(
    `${API_ENDPOINT}/04/users/${username}`,
    { headers: { authorization: API_TOKEN } }
  );
  res
    .status(200)
    .json(userReq.data);
}

```
-  every file inside the **pages/api/** directory will be considered by **Next.js** as an API route.
- Now we can refactor our UserPage component by changing the API endpoint to the newly created one

```jsx
function UserPage({ username }) {
  const [loading, setLoading] = useState(true);
  const [data, setData] = useState(null);
  useEffect(async () => {
    const req = await fetch(
      `/api/singleUser?username=${username}`,
    );
    const data = await req.json();
    setLoading(false);
    setData(data);
  }, []);
  return (
    <div>
      <div>
        <Link href="/" passHref>
          Back to home
        </Link>
      </div>
      <hr />
      {loading && <div>Loading user data...</div>}
      {data && <UserData user={data} />}
    </div>
  );
}
```