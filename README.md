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

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| id | string | The user's unique ID |
| email | string | The user's email |
| first_name | string | The user's first name |
| last_name | string | The user's last name |

### Endpoints
| Method | Path | Description|
| --- | --- | --- | 
| GET | /users.json | These are the user records the currently logged in user has access to, including themselves. |

## Families

A family is a group of users that have relationships to one another. Families typically have at least one parent and one child.

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| id | string | The family's unique ID |
| name | string | The user's last name |

### Endpoints
| Method | Path | Description|
| --- | --- | --- | 
| GET | /families.json | These are the family records the currently logged in user has access to. |

## Family Users

A family user represents the role a given user has in a family. 

A user's experience on Till changes based on the role. A user that is in Family A as an **admin** has the ability to do things like send money to kids in the family, transfer money from a link bank account, etc. A user that is in Family A as a child can do things like spend money, create goals, etc.

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| id | string | The family user's unique ID |
| user_id | string | The user associated with this family user |
| family_id | string | The family associated with this family user |
| role | Role | The user's role type (see Role enum below) |

### Endpoints
| Method | Path | Description|
| --- | --- | --- | 
| GET | /family_users.json | These are the family_user records the currently logged in user has access to. |

With all this in mind, here are the available role types in this static JSON API:

### Role Type Enum

| Name | Description |
| --- | --- |
| Admin | Typically a parent, has access to sending money to the children |
| Child | Typical a parent's child, receives money and can spend it |

## Linked Accounts

A linked account represents an admin's connected bank account. On Till, a parent needs to connect their bank account so they can transfer money to their kids.

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| user_id | string | The user this linked account belongs to
| account_type | string | The kind of bank account this is |
| till_account_id | string | A unique identifier for this account for accounting purposes |
| available_balance | number | The amount of money available in the account |
| pending_balance | number | The amount of money that will be available once all pending transfers clear |

### Endpoints
| Method | Path | Description|
| --- | --- | --- | 
| GET | /linked_accounts.json | These are the linked_account records the currently logged in user has access to. |

## Linked Account Transfers

A linked account transfers represent the money an admin moves from their linked account into Till. These transfers take time, so they have a status that represents whether they have been fully processed or not.

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| linked_account_id | string | The linked account this transfer belongs to
| amount | number | The amount of money transferred |
| status | Linked Account Transfer Status | A unique identifier for this account for accounting purposes |
| created_at | string | The timestamp the transfer was created at |

### Endpoints
| Method | Path | Description|
| --- | --- | --- | 
| GET | /linked_account_transfers.json | These are the linked_account records the currently logged in user has access to. |

### Linked Account Transfer Status Enum

| Name | Description |
| --- | --- |
| pending | The transfer is in progress but has not posted yet |
| processed | The transfer has posted and the money is able to be used |
| cancelled | The transfer has been cancelled and the money will not be made available |

## Spend Balances

A spend balance represents a child's checking account on Till. This is the account that has a debit card connected to it so a kid can swipe to make purchases. Only kids have spend balances.

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| linked_account_id | string | The linked account this transfer belongs to
| amount | number | The amount of money transferred |
| status | Linked Account Transfer Status | A unique identifier for this account for accounting purposes |

### Endpoints
| Method | Path | Description|
| --- | --- | --- | 
| GET | /linked_accounts.json | These are the linked_account records the currently logged in user has access to. |