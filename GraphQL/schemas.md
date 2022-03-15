
# Schemas
```tsx
query Schema

{
  __schema {
    queryType {
      name
      description
      fields {
        name
        description
        isDeprecated
        deprecationReason
      }
    }
  }
}

// response 
{
  "data": {
    "__schema": {
      "queryType": {
        "name": "Query",
        "description": "The query root of GitHub's GraphQL interface.",
        "fields": [
          {
            "name": "codeOfConduct",
            "description": "Look up a code of conduct by its key",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "codesOfConduct",
            "description": "Look up a code of conduct by its key",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "enterprise",
            "description": "Look up an enterprise by URL slug.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "enterpriseAdministratorInvitation",
            "description": "Look up a pending enterprise administrator invitation by invitee, enterprise and role.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "enterpriseAdministratorInvitationByToken",
            "description": "Look up a pending enterprise administrator invitation by invitation token.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "license",
            "description": "Look up an open source license by its key",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "licenses",
            "description": "Return a list of known open source licenses",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "marketplaceCategories",
            "description": "Get alphabetically sorted list of Marketplace categories",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "marketplaceCategory",
            "description": "Look up a Marketplace category by its slug.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "marketplaceListing",
            "description": "Look up a single Marketplace listing",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "marketplaceListings",
            "description": "Look up Marketplace listings",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "meta",
            "description": "Return information about the GitHub instance",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "node",
            "description": "Fetches an object given its ID.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "nodes",
            "description": "Lookup nodes by a list of IDs.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "organization",
            "description": "Lookup a organization by login.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "rateLimit",
            "description": "The client's rate limit information.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "relay",
            "description": "Hack to workaround https://github.com/facebook/relay/issues/112 re-exposing the root query object",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "repository",
            "description": "Lookup a given repository by the owner and repository name.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "repositoryOwner",
            "description": "Lookup a repository owner (ie. either a User or an Organization) by login.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "resource",
            "description": "Lookup resource by a URL.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "search",
            "description": "Perform a search across resources.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "securityAdvisories",
            "description": "GitHub Security Advisories",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "securityAdvisory",
            "description": "Fetch a Security Advisory by its GHSA ID",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "securityVulnerabilities",
            "description": "Software Vulnerabilities documented by GitHub Security Advisories",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "topic",
            "description": "Look up a topic by name.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "user",
            "description": "Lookup a user by login.",
            "isDeprecated": false,
            "deprecationReason": null
          },
          {
            "name": "viewer",
            "description": "The currently authenticated user.",
            "isDeprecated": false,
            "deprecationReason": null
          }
        ]
      }
    }
  }
}
``` 