# Till Financial Static JSON API

For this project, we'll be building a simple web app using React and this static JSON API. With these building blocks we hope to accomplish the following:
- Initialization of a React app
- Fetching of static JSON from this API
- A couple simple user flows

To start, call `GET https://tillfinancial.github.io/dummy-data/users.json`. This will return the `user_id` of the "logged in" user. Real secure I know...

Here are the other resources found in the API:

### Users

Users are the unique customers of our app.

#### GET users
Full path: GET https://tillfinancial.github.io/dummy-data/users.json
Description: These are the user records the currently logged in user has access to, including themselves.

### Families

A family is a group of users that have relationships to one another. Families typically have at least one parent and one child.

#### GET families
Full path: GET https://tillfinancial.github.io/dummy-data/families.json
Description: These are the family records the currently logged in user has access to.

### Family Users

A family user represents the role a given user has in a family. A user's experience on Till changes based on the role:

| Name | Description |
| --- | --- |
| Admin | Typically a parent, has access to sending money to the children |
| Child | Typical a parent's child, receives money and can spend it |

#### GET family_users
Full path: GET https://tillfinancial.github.io/dummy-data/family_users.json
Description: These are the family_user records the currently logged in user has access to.