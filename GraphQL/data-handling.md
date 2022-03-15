# Data Handling

### Aliases

```tsx
//query
graphqlProject:repository(name:"graphql", owner:"facebook"){
    id
    description
    homepageUrl
  }
    reactProject:repository(name:"react", owner:"facebook"){
    id
    description
    homepageUrl
  }
}
//response 
{
  "data": {
    "graphqlProject": {
      "id": "MDEwOlJlcG9zaXRvcnkzODM0MjIyMQ==",
      "description": "GraphQL is a query language and execution engine tied to any backend service.",
      "homepageUrl": "https://graphql.org/"
    },
    "reactProject": {
      "id": "MDEwOlJlcG9zaXRvcnkxMDI3MDI1MA==",
      "description": "A declarative, efficient, and flexible JavaScript library for building user interfaces.",
      "homepageUrl": "https://reactjs.org"
    }
  }
}
```

### Fragments

```tsx
//query
{
  graphqlProject:repository(name:"graphql", owner:"facebook"){
    ...repoFields
  }
    reactProject:repository(name:"react", owner:"facebook"){
    ...repoFields
  }
}

fragment repoFields on Repository{
      id
    description
    homepageUrl
}
//response 
{
  "data": {
    "graphqlProject": {
      "id": "MDEwOlJlcG9zaXRvcnkzODM0MjIyMQ==",
      "description": "GraphQL is a query language and execution engine tied to any backend service.",
      "homepageUrl": "https://graphql.org/"
    },
    "reactProject": {
      "id": "MDEwOlJlcG9zaXRvcnkxMDI3MDI1MA==",
      "description": "A declarative, efficient, and flexible JavaScript library for building user interfaces.",
      "homepageUrl": "https://reactjs.org"
    }
  }
}
```

### Nested

```tsx
//query
{
  viewer {
    id
    name
    repositories(last:5) {
      edges {
        node {
          id
        }
      }
    }
  }
}

//response 
{
  "data": {
    "viewer": {
      "id": "MDQ6VXNlcjQ0MTc4Njg1",
      "name": "Mohamed Hamed",
      "repositories": {
        "edges": [
          {
            "node": {
              "id": "MDEwOlJlcG9zaXRvcnkxNjYxMTEyNzI="
            }
          },
          {
            "node": {
              "id": "MDEwOlJlcG9zaXRvcnkxNjc0NTY5ODQ="
            }
          },
          {
            "node": {
              "id": "MDEwOlJlcG9zaXRvcnkxOTY4NzU4NjI="
            }
          },
          {
            "node": {
              "id": "MDEwOlJlcG9zaXRvcnkxOTY4ODQzMzM="
            }
          },
          {
            "node": {
              "id": "MDEwOlJlcG9zaXRvcnkyMDExNDkzMDQ="
            }
          }
        ]
      }
    }
  }
}
```

### Multi nested fields

```tsx
//query
{
  repository(owner: "github", name: "opensource.guide") {
    id
    name
    watchers(first: 50) {
      edges {
        node {
          id
          name
        }
      }
    }
    pullRequests(last:4){
      edges{
        node{
          id
        }
      }
    }
  }
}
//response 
{
  "data": {
    "repository": {
      "id": "MDEwOlJlcG9zaXRvcnk2MTIwNDgxOA==",
      "name": "opensource.guide",
      "watchers": {
        "edges": [
          {
            "node": {
              "id": "MDQ6VXNlcjQ4ODc=",
              "name": "Ryan Waldron"
            }
          },
          {
            "node": {
              "id": "MDQ6VXNlcjEwODcy",
              "name": "TAKAGI Masahiro"
            }
          },
        ....
        ]
      },
      "pullRequests": {
        "edges": [
          {
            "node": {
              "id": "MDExOlB1bGxSZXF1ZXN0MzM3MjI3NTM2"
            }
          },
          {
            "node": {
              "id": "MDExOlB1bGxSZXF1ZXN0MzM3MjM3ODky"
            }
          },
          ....
        ]
      }
    }
  }
}
```

### Pagination

```tsx
//query
{
  repository(owner: "facebook", name: "graphql") {
    id
    name
    issues(last: 5, states: CLOSED) {
      edges {
        node {
          id
          number
          title
        }
      }
    }
  }
}
//response 
{
  "data": {
    "repository": {
      "id": "MDEwOlJlcG9zaXRvcnkzODM0MjIyMQ==",
      "name": "graphql-spec",
      "issues": {
        "edges": [
          {
            "node": {
              "id": "MDU6SXNzdWU0ODQ3NDAzODg=",
              "number": 612,
              "title": "Feat: Return raw JSON.  Typeless Fields.  Metadata?"
            }
          },
          .......
        ]
      }
    }
  }
}
```

### Connections

The RepositoryConnection represents the relationship between our one field and another object. A one to many relationship. We have a Repositories field and that's connected to each individual Repository. You can think of it like an array of objects. Now Edges represents a connection to another array of data. And then each Node is an individual Repository.


![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b94b1c4c-94b4-47f9-8018-8cfb6f6f8e88/Screen_Shot_2019-11-11_at_9.34.55_AM.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b94b1c4c-94b4-47f9-8018-8cfb6f6f8e88/Screen_Shot_2019-11-11_at_9.34.55_AM.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220313%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220313T204025Z&X-Amz-Expires=86400&X-Amz-Signature=36a0b8e0f4d62748312cc60a6549a0ca346f115e50d658041eb6a1ad06518ec7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Screen_Shot_2019-11-11_at_9.34.55_AM.png%22&x-id=GetObject)