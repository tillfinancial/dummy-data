# Till Financial Static JSON API

For this project, we'll be building a simple web app using React and this static JSON API. With these building blocks we hope to accomplish the following:
- Initialization of a React app
- Fetching of static JSON from this API
- A couple simple user flows

## Fundamentals

The API base URL is: `https://tillfinancial.github.io/dummy-data` so for any path below, make sure you have this base url added as a prefix before making the network call.

To start, call `GET /auth.json`. This will return the `user_id` of the "logged in" user. Real secure I know...

Here are the other resources found in the API:

## Users

Users are the unique customers of our app.

#### GET users
| Method | Path | Description|
| --- | --- | --- | 
| GET | /users.json | These are the user records the currently logged in user has access to, including themselves. |

## Families

A family is a group of users that have relationships to one another. Families typically have at least one parent and one child.

#### GET families
| Method | Path | Description|
| --- | --- | --- | 
| GET | /families.json | These are the family records the currently logged in user has access to. |

## Family Users

A family user represents the role a given user has in a family. 

A user's experience on Till changes based on the role. A user that is in Family A as an **admin** has the ability to do things like send money to kids in the family, transfer money from a link bank account, etc. A user that is in Family A as a child can do things like spend money, create goals, etc.

### GET family_users
| Method | Path | Description|
| --- | --- | --- | 
| GET | /family_users.json | These are the family_user records the currently logged in user has access to. |

With all this in mind, here are the available role types in this static JSON API:

### Role Type Enum

| Name | Description |
| --- | --- |
| Admin | Typically a parent, has access to sending money to the children |
| Child | Typical a parent's child, receives money and can spend it |

#### Attributes

| Name | Type | Description |
| --- | --- | --- |
| user_id | string | The user this family user belongs to |
| family_id | string | The family this user is in |
| role | string | The role type. Is one of the role type enum defined above|

## Linked Accounts

A linked account represents an admin's connected bank account. On Till, a parent needs to connect their bank account so they can transfer money to their kids.

### GET linked_accounts
Full path: GET https://tillfinancial.github.io/dummy-data/linked_accounts.json
Description: These are the linked_account records the currently logged in user has access to.

#### Attributes

| Name | Type | Description |
| --- | --- | --- |
| user_id | string | The user this linked account belongs to
| account_type | string | The kind of bank account this is |
| till_account_id | string | A unique identifier for this account for accounting purposes |
| available_balance | number | The amount of money available in the account |
