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
query {
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

###  Arguments

```js
book: {
    type: BookType,
    description: "A single book",
    args: {
    id: { type: GraphQLInt },
    },
    resolve: (parent, args) => books.find((book) => book.id === args.id),
},
```

```json
query {
  book(id: 1)
}
```

- We can pass in arguments into queries

# Mutations

```js
addBook: {
    type: BookType,
    description: "Add a book",
    args: {
    name: { type: GraphQLNonNull(GraphQLString) },
    authorId: { type: GraphQLNonNull(GraphQLInt) },
    },
    resolve: (parent, args) => {
    const book = {
        id: books.length + 1,
        name: args.name,
        authorId: args.authorId,
    };
    books.push(book);
    return book;
    },
},
```

- Very similar to creating a new query response
- Updates data in the current instance