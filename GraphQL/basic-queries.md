
# Basic Queries
[Github explorer](https://developer.github.com/v4/explorer/) 

### Basic query

```tsx
//query
 { 
  viewer { 
    name
  }
}
//response 
{
  "data": {
    "viewer": {
      "name": "Mohamed Hamed"
    }
  }
}
```

### Multiple fields

```tsx
//query
{
  viewer {
    name
    avatarUrl
    bio
    id
  }
}
//response 
{
  "data": {
    "viewer": {
      "name": "Mohamed Hamed",
      "avatarUrl": "https://avatars0.githubusercontent.com/u/44178685?v=4",
      "bio": "",
      "id": "MDQ6VXNlcjQ0MTc4Njg1"
    }
  }
}
```

### Passing arguments

```tsx
//query
{
  repositoryOwner(login: "eveporcello") {
    id
    resourcePath
    url
  }
}
//response 
{
  "data": {
    "repositoryOwner": {
      "id": "MDQ6VXNlcjQ0Mjk4NTI=",
      "resourcePath": "/eveporcello",
      "url": "https://github.com/eveporcello"
    }
  }
}
```

### Required arguments

```tsx
//query
{
  repository(name: "graphql", owner:"facebook") {
    id
  }
}
//response 
{
  "data": {
    "repository": {
      "id": "MDEwOlJlcG9zaXRvcnkzODM0MjIyMQ=="
    }
  }
}
```