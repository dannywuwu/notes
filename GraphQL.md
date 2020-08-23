Instead of creating multiple endpoints where each endpoint returns a different response (REST), create 1 endpoint which returns a response depending on the request (GraphQL query)

# Schemas

```js
const schema = new GraphQLSchema({
  query: new GraphQLObjectType({
    // create new HelloWorld object
    name: "HelloWorld",
    fields: () => ({
      message: {
        type: GraphQLString,
        resolve: () => "hey there",
      },
    }),
  }),
});
```

- We create schemas which define types with fields
    - Fields are all the properties of the object we can query and return data from
- Also specifies which queries and mutations are available to the client

# Querying

```json
Query
{
  message
}
```

```json
Response
  "data": {
    "message": "hey there"
  }
}
```

- Very similar to JSON syntax - specify keys and GraphQL will return their respective values