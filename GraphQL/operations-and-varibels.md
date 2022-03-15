# Operations and Varibels

### Operation names

```tsx
//query
query facebookOrgMembers{
  organization(login:"facebook"){
    id
    name
    membersWithRole(first:2){
      edges{
        node{
          name
        }
      }
    }
  }
}
//response 
{
  "data": {
    "organization": {
      "id": "MDEyOk9yZ2FuaXphdGlvbjY5NjMx",
      "name": "Facebook",
      "membersWithRole": {
        "edges": [
          {
            "node": {
              "name": "Andrew Loe"
            }
          },
          {
            "node": {
              "name": "David Reiss"
            }
          }
        ]
      }
    }
  }
}
```

### Variable definitions

```tsx
//query
// single
query facebookOrgMembers($login: String!){
  organization(login:$login){
    id
    name
    membersWithRole(first:2){
      edges{
        node{
          name
        }
      }
    }
  }
}
//multiple
query facebookOrgMembers($login: String!, $n: Int!){
  organization(login:$login){
    id
    name
    membersWithRole(first:$n){
      edges{
        node{
          name
        }
      }
    }
  }
}
```

### Mutation

```tsx
//query
// single
mutation NewComment($input: AddCommentInput!) {
  addComment(input: $input) {
    clientMutationId
    subject {
      id
    }
  }
}
// parameters
{
  "input": {
    "clientMutationId": "324225",
    "subjectId": "MHJJHVH6465464",
    "body": "Test add comment"
  }
}
```

### Reaction Mutation

```tsx
//query
// single
mutation NewRaction($input: AddReactionInput!) {
  addReaction(input: $input) {
    reaction{
      content
    }
  }
}

// parameters
{
  "input": {
    "clientMutationId": "324225",
    "subjectId": "MHJJHVH6465464",
    "content": "THUMBS_DOWN"
  }
}
```