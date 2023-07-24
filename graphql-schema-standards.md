# GraphQL Schema Standards, Patterns, & Practices

When planning a GraphQl Schema design, choosing appropriate type names and casing conventions is essential for creating a clear and consistent API. With no industry-wide standard, there are some common practices and recommendations that I tend to follow when setting up new schema and related project assets:

1. **Type Names**: Use descriptive and meaningful names for GraphQL types. Type names should represent the data they hold or the entities they represent. For example, if you have a type to represent a user, name it `User`.
2. **Nest Objects/Types**: When naming nested types the naming can become more complex. In this case it is sometimes important to put a nested objects type name on the parent type or vice versa to signify where it sits within a conceptual structure. For example:
``` json
type User {
  id: ID!
  name: String!
  address1: Address!  // Notice there is a 1 and 2 address, to which the name differentiates since it is the same nested object, but clearly two differnt addresses.
  address2: Address
  account: Account
}

type Address {
  id: ID!
  address: String!
  userId: ID  // This would be the user the address is related to. If empty, the address wouldn't be related to a specific user.
}

type Account {
  id: ID!
  title: String!
  associatedAccount: Account  // Notice this account name is a compound name, making it more complex, to differentiate it clearly from the "account" that a user might have.
}
```
4. **Naming Conventions**: Stick to a consistent naming convention throughout your schema. There are two popular conventions:
    - **PascalCase**: Capitalize the first letter of each word, including the first word. For example: `User`, `ProductCategory`, `OrderDetails`.
    - **camelCase**: Start with a lowercase letter and capitalize the first letter of each subsequent word. For example: `user`, `productCategory`, `orderDetails`.
    Choose the convention that aligns better with your team's preferences and the overall codebase.
5. **Avoid Abbreviations**: Try to avoid abbreviations in type names unless they are widely known and commonly used. Clear and readable type names make it easier for other developers to understand your schema.
6. **Singular vs. Plural**: Use singular names for types representing single entities (e.g., `User`, `Product`, `Category`) and plural names for types representing collections of those entities (e.g., `users`, `products`, `categories`).
7. **Enumeration Types**: For enumeration types (enums), use singular names, and use uppercase letters for the values. For example:
``` json
enum UserRole {
  ADMIN
  CUSTOMER
  GUEST
}
```
6. **Interfaces and Unions**: For interfaces and unions, use descriptive and noun-based names that indicate the common traits of the types they include. For example:
``` json
interface Vehicle {
  id: ID!
  brand: String!
}

type Car implements Vehicle {
  id: ID!
  brand: String!
  model: String!
}

type Bike implements Vehicle {
  id: ID!
  brand: String!
  color: String!
}
```
7. **Field Names**: Follow similar naming conventions for field names within types. Use descriptive and concise names that indicate the data they represent. For example, prefer `firstName` over `fn` or `fName`.
8. **Boolean Fields**: For boolean fields, use names that suggest a yes/no question and use words like `is`, `has`, or `should`. For example: `isActive`, `hasPermission`, `shouldProcess`.

Remember, while these guidelines provide a helpful starting point, the most crucial aspect is to ensure consistency across the entire schema and within your team's development practices. By creating a well-designed and consistently named schema, you make it easier for other developers to understand, maintain, and extend the API efficiently.
